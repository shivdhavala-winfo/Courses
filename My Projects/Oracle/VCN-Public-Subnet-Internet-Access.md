# How a Public Subnet Connects to the Internet (OCI VCN Guide)

## Your Setup (Demo VCN)

| Item | Value |
|---|---|
| VCN | Demo VCN |
| Private Subnet | `10.0.0.0/8` |
| Public Subnet | `172.168.0.0/16` |

> ⚠️ **Note before we start:** `172.168.0.0/16` is technically a **public IP range**
> (RFC 1918 private ranges are `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`).
> `172.16.x.x` is private, but `172.168.x.x` is **not**. It will still work inside
> OCI, but best practice is to use **`172.16.0.0/16`** or similar.
> Also, `10.0.0.0/8` is very large (16 million addresses) — for a demo,
> `10.0.0.0/16` is more typical. Just make sure the two CIDRs **never overlap**.

---

## The Short Answer

A subnet is only "public" if **all four** of these exist:

```
1. Internet Gateway (IGW)  → attached to the VCN
2. Route Rule              → 0.0.0.0/0  →  Internet Gateway  (in PUBLIC subnet's route table)
3. Security Rules          → allow inbound (ingress) ports from 0.0.0.0/0 (e.g., 22, 80, 443)
4. Public IP Address       → assigned to the instance (ephemeral or reserved)
```

**Miss any one of these → no internet access.**

---

## How It Works (Picture)

```
   INTERNET
      |
      |  (user: ssh / http://... )
      v
 [ Internet Gateway ]  ← attached to Demo VCN
      |
      |  route table: 0.0.0.0/0 → IGW
      v
 [ PUBLIC SUBNET 172.168.0.0/16 ]   ← instance has PUBLIC IP
      |                                Security List: allow 22/80/443 from 0.0.0.0/0
      |
      |   (optional: NAT for private subnet)
      v
 [ PRIVATE SUBNET 10.0.0.0/8 ]     ← NO public IP, no route to IGW
```

**Key idea:** In OCI, subnets are private by default. A subnet becomes public
**only because its route table points `0.0.0.0/0` to an Internet Gateway**.
The subnet label "public/private" in the console is just a convenience — the
routing is what actually matters.

---

## Step-by-Step: Changes Needed

### Step 1 — Create / Verify the Internet Gateway

Path: **Networking → Virtual Cloud Networks → your VCN → Internet Gateways → Create Internet Gateway**

- Name: `demo-igw`
- State: **Enabled**
- Compartment: same as the VCN

> The IGW is a virtual router at the edge of your VCN. Traffic going to it can
> reach the internet, and traffic from the internet can reach it.

### Step 2 — Add a Route Rule to the PUBLIC subnet's route table

Path: **VCN → Route Tables → (public subnet's route table) → Add Route Rules**

| Field | Value |
|---|---|
| Target Type | **Internet Gateway** |
| Destination CIDR | `0.0.0.0/0` |
| Target | `demo-igw` |
| Route Status | Enabled |

- The **public subnet** (`172.168.0.0/16`) route table gets this rule.
- The **private subnet** (`10.0.0.0/8`) route table should **NOT** have this rule
  (otherwise it's effectively public).

> `0.0.0.0/0` means "all destinations not matched by another rule" = internet.

### Step 3 — Open the Security List / NSG (Ingress Rules)

Path: **VCN → Security Lists → (public subnet's security list) → Add Ingress Rules**

| Direction | Type | Protocol | Source Port | Dest Port | Description |
|---|---|---|---|---|---|
| Ingress | CIDR | TCP | All | **22** | SSH access |
| Ingress | CIDR | TCP | All | **80** | HTTP |
| Ingress | CIDR | TCP | All | **443** | HTTPS |

- Source: `0.0.0.0/0` (anyone) — or restrict to your office IP for better security, e.g., `203.0.113.10/32`.
- **Egress** (outbound): the default rule usually already allows all outbound
  (`0.0.0.0/0`, all protocols). Keep it — the instance needs it to download
  updates and talk to OCI services.

> OCI security lists are **stateful**: when you allow inbound SSH, the reply
> traffic is automatically allowed back — you don't need a separate egress rule
> for the response.


### Step 4 — Assign a Public IP to the Instance

A public subnet does **not** automatically give instances a public IP. You need:

**Option A — Ephemeral public IP (free, dies when instance is terminated)**
- At launch: **Create Instance → Show network options → check
  "Assign public IP address"** (only possible if the subnet has a route to the IGW).

**Option B — Reserved public IP (survives stop/terminate, better for servers)**
- **Networking → IP Management → Reserved Public IPs → Reserve Public IP**
- Then: **Compute → your instance's VNIC → IP Management → Edit → Assign Reserved Public IP**

### Step 5 — (Optional but common) Instance OS Firewall

Even with everything above, the guest OS firewall can block traffic:

```bash
# On the instance (Oracle Linux/CentOS), check and open ports:
sudo firewall-cmd --list-ports
sudo firewall-cmd --permanent --add-port=80/tcp
sudo firewall-cmd --reload
```

### Step 6 — Connect from Outside

```bash
# SSH (Linux/Mac/Git Bash) — key must match the one used at launch
chmod 400 demo-key.pem
ssh -i demo-key.pem opc@<PUBLIC_IP>

# Or via a browser:
http://<PUBLIC_IP>
```

In the OCI console, find the public IP under:
**Compute → Instances → your instance → Instance Details → Public IP address**.

---

## What About the Private Subnet (10.0.0.0/8)?

By design it has **no route to the IGW** → no direct inbound internet access.
That's the point. If you later want to access private instances from outside,
choose one of these:

| Method | Use case |
|---|---|
| **OCI Bastion service** | Temporary, audited SSH into a private instance |
| **VPN / FastConnect** | Site-to-site connection from your office/data center |
| **Load Balancer in public subnet** | Public entry point that forwards to private instances |
| **NAT Gateway (outbound only)** | Lets private instances reach the internet (patches, updates) — does NOT allow inbound |

Example for outbound-only internet from the private subnet:
- Create a **NAT Gateway** (public, route traffic to `0.0.0.0/0`).
- In the **private subnet's route table**: `0.0.0.0/0 → NAT Gateway`.
- Private instances still can't be reached from outside. ✔

---

## Quick Troubleshooting Checklist

If internet access isn't working, check in this order:

1. ✅ IGW exists and is **Enabled**?
2. ✅ Public subnet's route table has `0.0.0.0/0 → IGW`?
3. ✅ Security List has **ingress** rule for the port (22/80/443) from `0.0.0.0/0`?
4. ✅ Instance actually has a **public IP** shown in console?
5. ✅ Instance OS firewall isn't blocking the port?
6. ✅ (If ZPR enabled) instance doesn't have a security attribute blocking traffic?
7. ✅ Your corporate firewall / VPN isn't blocking outbound 22/80/443?

---

## TL;DR — The 4 Changes

```
1. Internet Gateway         → attach to VCN
2. Route rule               → 0.0.0.0/0 → IGW   (in PUBLIC subnet's route table ONLY)
3. Security List ingress    → allow TCP 22/80/443 from 0.0.0.0/0
4. Public IP on instance    → ephemeral or reserved
```

That's it — these four changes let your `172.168.0.0/16` public subnet be reached
from anywhere on the internet. The `10.0.0.0/8` private subnet stays protected
(no IGW route), and you access it later via Bastion/VPN/LB if needed.

**References:**
- [OCI VCN Documentation](https://docs.oracle.com/en-us/iaas/Content/Network/Tasks/managingVCNs.htm)
- [OCI Internet Gateway](https://docs.oracle.com/en-us/iaas/Content/Network/Tasks/managingIGW.htm)