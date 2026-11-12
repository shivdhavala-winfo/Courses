# Oracle ZPR — Zero Trust Packet Routing (Explained Simply)

## What is ZPR?

**ZPR** stands for **Zero Trust Packet Routing**. It is a security service in
**Oracle Cloud Infrastructure (OCI)**.

It adds an **extra layer of network protection** on top of the normal firewall rules
(security lists and NSGs) you already use in OCI.

> **Simple definition:**
> ZPR lets you say things like *"only my trusted app servers are allowed to talk to
> my sensitive databases"* — using **labels**, instead of writing IP addresses.

---

## The Problem ZPR Solves

Normally in OCI, network security depends on **network structure**:

- Security Lists apply to a whole subnet.
- NSGs (Network Security Groups) apply to selected VNICs.
- Rules are based on **IP addresses and CIDR ranges**.

This causes problems:

- If the network is redesigned, IP addresses change, and old rules may break or
  silently allow wrong traffic.
- Rules are hard to understand — "why is 10.0.1.7 talking to 10.0.2.3?" is not
  obvious.
- A small misconfiguration can accidentally expose sensitive data.

**ZPR fixes this by separating "security" from "network design."**

---

## A Simple Analogy

Imagine a company building:

- **Old way (Security Lists / NSGs):** Guards check **office room numbers** on
  badges. If rooms get renumbered, the rules become wrong.

- **ZPR way:** Guards check **job titles / departments** on badges —
  *"HR staff can enter only the HR room."* Rooms can move around freely;
  the rule still works.

In ZPR terms:

- **Labels** = security attributes (e.g., `data:sensitive`, `hosts:trusted`)
- **Rules** = ZPR policies (written in a simple language called ZPL)

---

## Key Concepts (Only 3 Things to Know)

| Concept | What it means |
|---|---|
| **Security Attribute** | A label you attach to resources, like `data:sensitive` or `hosts:trusted`. Example: put `data:sensitive` on a database. |
| **Security Attribute Namespace** | A folder/container for organizing your labels (e.g., namespace `apps` can contain `apps:hr-app`, `apps:payroll`). |
| **ZPR Policy** | A rule that says who (which labels) can talk to what (which labels). Written in **ZPL** (Zero Trust Packet Routing Policy Language). |

---

## How It Works (In 3 Steps)

1. **Create security attributes (labels)** — e.g., `hosts:trusted`, `data:sensitive`.
2. **Write a ZPR policy** — e.g., *"trusted hosts can connect to sensitive data."*
3. **Attach the labels to resources** — e.g., put `data:sensitive` on your DB,
   and `hosts:trusted` on your app servers.

That's it. ZPR does the rest.

### Example ZPL Policy

```
in networks:application VCN
allow hosts:trusted endpoints to connect to data:sensitive endpoints
```

**English translation:**
*"Inside the application VCN, only endpoints labeled `hosts:trusted`
are allowed to connect to endpoints labeled `data:sensitive`."*

When someone tries to connect, ZPR checks the labels on the **source** and
**destination** of every network packet and either **allows** or **blocks** it.

---

## Important Things to Remember

- **ZPR is "on top of" existing rules, not a replacement.** For traffic to flow,
  it must:
  1. Have a **route** in the route table, AND
  2. Pass **security list** rules, AND
  3. Pass **NSG** rules, AND
  4. Pass **ZPR policy** rules.

  ✅ All four must allow it. ❌ If any one blocks it, traffic is dropped.

- **Resources without a security attribute are NOT affected.** ZPR only protects
  resources you have labeled. Everything else works as before.

- **Zero Trust means "never trust, always verify."** Every access request is
  checked at the network level, every time — even if the network architecture
  changes later.

- ZPR works **across multiple VCNs** in the same region (a big advantage over
  NSGs, which are limited to one VCN).

- ZPR does **not** control traffic coming from the internet or on-premises
  networks directly — it enforces policy on VCN traffic (via LPGs/DRGs).

---

## How to Enable It

- ZPR is enabled **once per tenancy, in the home region**.
- In OCI Console: **Identity & Security → Zero Trust Packet Routing → Enable ZPR**
- Or via CLI: `oci zpr configuration create --compartment-id <compartment_ocid>`
- Enabling it is free to try, and enabling alone does **not** change any traffic
  behavior until you label resources and write policies.

---

## ZPR vs NSG vs Security List (Quick Comparison)

| Feature | Security List | NSG | ZPR |
|---|---|---|---|
| Applies to | Whole subnet/VCN | Selected VNICs | Any labeled resource |
| Based on | IP addresses | IP addresses | **Labels (security attributes)** |
| Can span multiple VCNs | No | No | **Yes** |
| Needs network redesign to update rules? | Yes | Yes | **No** |

---

## TL;DR

> **Oracle ZPR = label-based ("attribute-based") network firewall for OCI.**
> You tag resources with labels, write simple rules like
> *"this label can talk to that label,"* and ZPR enforces those rules on every
> network packet — regardless of IP addresses or network layout.

**Reference:** [OCI Zero Trust Packet Routing Documentation](https://docs.oracle.com/en-us/iaas/Content/zero-trust-packet-routing/overview.htm)
