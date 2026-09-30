# Azure Databricks: Free 8-Week Learning Plan

> **Time needed:** about 1–1.5 hours a day · **Cost:** free · **Level:** beginner to certification-ready
>
> **How it works:** Microsoft Learn covers the Azure-specific parts, YouTube gives you video walkthroughs, and Databricks Free Edition is where you practice.

---

## Table of Contents
- [Step 0: Set up](#step-0-set-up-day-1)
- [Week-by-Week Plan](#week-by-week-plan)
- [All Video Links](#all-video-links)
- [All Microsoft Learn Links](#all-microsoft-learn-links)
- [Tips](#tips-to-keep-it-smooth)
- [Progress Tracker](#progress-tracker)

---

## Step 0: Set up (Day 1)

| What | Link |
|---|---|
| Free practice workspace (no credit card) | [Databricks Free Edition](https://www.databricks.com/learn/free-edition) |
| Free Edition setup guide | [MS Learn: Sign up for Free Edition](https://learn.microsoft.com/en-us/azure/databricks/getting-started/free-edition) |
| Free official training (Databricks Academy) | [Get free Databricks training](https://learn.microsoft.com/en-us/azure/databricks/getting-started/free-training) |
| Official getting-started tutorials | [Get started tutorials on Azure Databricks](https://learn.microsoft.com/en-us/azure/databricks/getting-started/) |
| Optional: real Azure workspace | [Azure free account](https://azure.microsoft.com/free) (delete resources when you're done so you aren't charged) |

---

## Week-by-Week Plan

### Week 1: Basics
**Goal:** understand what Databricks is and find your way around a workspace.
- 📺 [Databricks Tutorial – Zero to Hero (Azure Databricks Masterclass)](https://www.youtube.com/watch?v=7pee6_Sq3VY), about 4 hours. Watch the first 1.5 hours this week.
- 📘 [Explore Azure Databricks (MS Learn module)](https://learn.microsoft.com/en-us/training/modules/explore-azure-databricks/)
- 🛠 **Practice:** create a notebook, attach compute, and run basic Python and SQL cells.

### Week 2: Workspace, compute and Unity Catalog
- 📺 Finish [Databricks Tutorial – Zero to Hero](https://www.youtube.com/watch?v=7pee6_Sq3VY).
- 📘 [Set up and Configure an Azure Databricks Environment](https://learn.microsoft.com/en-us/training/paths/azure-databricks-data-engineer-set-up-configure-environment/)
- 🛠 **Practice:** create a catalog, a schema and a table, and upload a CSV file.

### Weeks 3–4: Spark with PySpark and SQL
**Goal:** read, transform and write data with DataFrames.
- 📺 **Choose one playlist** and follow it all the way through:
  - [Azure Databricks For Beginners](https://www.youtube.com/playlist?list=PLpnBHtRj5A6Fa7a1fo1xL--0Ro5ZwDh-z)
  - [Azure Databricks Tutorials for Beginners](https://www.youtube.com/playlist?list=PLrG_BXEk3kXznRvTJXwmazGCvTSxdCMsN)
  - [Databricks and PySpark | Full Course](https://www.youtube.com/playlist?list=PLxy0DxWEupiNjGSv1hzRFBXgSzV-bZu94)
- 🛠 **Practice:** select, filter, groupBy, joins, window functions and UDFs, using the built-in `samples` datasets.

### Week 5: Delta Lake and the Medallion architecture
- 📺 [Delta Lake Databricks FULL Course – Zero to Pro in 4 Hours](https://www.youtube.com/watch?v=rBiOQ_68DFk)
- 📘 [Implement a Data Analytics Solution with Azure Databricks](https://learn.microsoft.com/en-us/training/paths/data-engineer-azure-databricks/)
- 🛠 **Practice:** build Bronze → Silver → Gold tables. Try MERGE, time travel, OPTIMIZE and schema evolution.

### Week 6: Ingestion and transformation with Unity Catalog
- 📺 [Databricks Full Course (With Unity Catalog)](https://www.youtube.com/watch?v=P5pEeR3xQpI), about 4 hours.
- 📘 [Prepare and Process Data with Azure Databricks](https://learn.microsoft.com/en-us/training/paths/azure-databricks-data-engineer-prepare-process-data/)
- 🛠 **Practice:** Auto Loader, COPY INTO, and adding data quality checks.

### Week 7: Pipelines, jobs and deployment
- 📘 [Deploy and Maintain Data Pipelines and Workloads With Azure Databricks](https://learn.microsoft.com/en-us/training/paths/azure-databricks-data-engineer-deploy-maintain-data-pipelines-workloads/)
- 📺 Go back to the pipelines and jobs videos in the playlist you picked in Weeks 3–4.
- 🛠 **Practice:** create a Lakeflow Job that runs your notebooks in order on a schedule, and connect a Git repo.

### Week 8: Capstone project and certification prep
- 🛠 **Project:** take a public dataset (for example NYC Taxi from `samples`, or a Kaggle CSV) through ingest → Bronze/Silver/Gold → a scheduled job → a SQL dashboard. Push it to GitHub.
- 📺 Certification prep videos:
  - [Databricks Data Engineer Associate Ultimate Course (playlist)](https://www.youtube.com/playlist?list=PLx5_UkGNs24cASxCHqgSqoyt_3Y8DpFF-)
  - [Databricks Certification Preparation (playlist)](https://www.youtube.com/playlist?list=PL7S7dD8r4QdXTKFvVNnGRFWrJ82HnBWnp)
  - [freeCodeCamp: 7.5-hour Databricks Data Engineer Associate course](https://www.freecodecamp.org/news/prepare-for-the-databricks-data-engineer-associate-certification-exam-and-pass/) (the article links to the full YouTube video)
  - [Interview Series: Databricks | Spark | PySpark | Delta Lake](https://www.youtube.com/playlist?list=PLgPb8HXOGtsT2uUaujhsFBNENhXVbI0ro)
- 🎯 Certification options:
  - [Microsoft Certified: Azure Databricks Data Engineer Associate](https://learn.microsoft.com/en-us/credentials/certifications/implementing-data-engineering-solutions-using-azure-databricks/) (course outline: [DP-750](https://learn.microsoft.com/en-us/training/courses/dp-750t00))
  - Databricks Certified Data Engineer Associate. Prepare with Databricks Academy's free courses.
  - Studying for either is free, but the exams themselves cost money.

### Optional after that: Machine learning
- 📘 [Build machine learning solutions using Azure Databricks](https://learn.microsoft.com/en-us/training/paths/build-operate-machine-learning-solutions-azure-databricks/)

---

## All Video Links

### Full-length single videos
| # | Video | Topic | Length |
|---|---|---|---|
| 1 | [Databricks Tutorial – Zero to Hero (Azure Databricks Masterclass)](https://www.youtube.com/watch?v=7pee6_Sq3VY) | Fundamentals to advanced | ~4 hrs |
| 2 | [Databricks Full Course (With Unity Catalog)](https://www.youtube.com/watch?v=P5pEeR3xQpI) | Unity Catalog and end-to-end | ~4 hrs |
| 3 | [Delta Lake Databricks FULL Course – Zero to Pro (2026)](https://www.youtube.com/watch?v=rBiOQ_68DFk) | Delta Lake with PySpark | ~4 hrs |
| 4 | [Delta Lake Databricks – Zero to Pro (2025)](https://www.youtube.com/watch?v=O18afGTGoIU) | Delta Lake with PySpark | ~4 hrs |
| 5 | [Delta Lake Masterclass – Azure Databricks, Zero to Expert](https://www.youtube.com/watch?v=8IjCyvyAPpM) | Delta Lake deep dive with labs | ~6 hrs |

### Playlists: Azure Databricks
| # | Playlist |
|---|---|
| 6 | [Azure Databricks For Beginners](https://www.youtube.com/playlist?list=PLpnBHtRj5A6Fa7a1fo1xL--0Ro5ZwDh-z) |
| 7 | [Azure Databricks Tutorials for Beginners](https://www.youtube.com/playlist?list=PLrG_BXEk3kXznRvTJXwmazGCvTSxdCMsN) |
| 8 | [Azure Databricks Tutorial](https://www.youtube.com/playlist?list=PLNRxk1s77zfgubs75vVMzHhPIhWqRo79C) |
| 9 | [Azure Databricks](https://www.youtube.com/playlist?list=PL7_h0bRfL52rUU6chVIygk7eEiB3Htj-C) |
| 10 | [Azure Databricks (full series)](https://www.youtube.com/playlist?list=PLBYFzjTfo5XeE7NR5RuTvRHdOzwSkGwqW) |
| 11 | [Azure Databricks (additional playlist)](https://www.youtube.com/playlist?list=PLqFcsvtmzkhCeBm1jORQgF1CovrdlrtbU) |

### Playlists: PySpark and Delta Lake
| # | Playlist |
|---|---|
| 12 | [Databricks and PySpark | Full Course](https://www.youtube.com/playlist?list=PLxy0DxWEupiNjGSv1hzRFBXgSzV-bZu94) |
| 13 | [Databricks Playlist – PySpark](https://www.youtube.com/playlist?list=PLZv9tikE8WQj6DV5X5yDQKbMirf0wxZGD) |
| 14 | [Delta Lake Deep Dive – Complete Playlist](https://www.youtube.com/playlist?list=PLlHuhl-cAAnG61oDEzySZzcTMQO1eurUj) |

### Playlists: Certification and interviews
| # | Playlist |
|---|---|
| 15 | [Databricks Data Engineer Associate Ultimate Course](https://www.youtube.com/playlist?list=PLx5_UkGNs24cASxCHqgSqoyt_3Y8DpFF-) |
| 16 | [Databricks Certification Preparation](https://www.youtube.com/playlist?list=PL7S7dD8r4QdXTKFvVNnGRFWrJ82HnBWnp) |
| 17 | [Interview Series: Databricks, Spark, PySpark, Delta Lake](https://www.youtube.com/playlist?list=PLgPb8HXOGtsT2uUaujhsFBNENhXVbI0ro) |
| 18 | [freeCodeCamp 7.5-hour Data Engineer Associate course (article with the video)](https://www.freecodecamp.org/news/prepare-for-the-databricks-data-engineer-associate-certification-exam-and-pass/) |

---

## All Microsoft Learn Links
| Learning path / module | Link |
|---|---|
| Explore Azure Databricks | [Module](https://learn.microsoft.com/en-us/training/modules/explore-azure-databricks/) |
| Set up and Configure an Azure Databricks Environment | [Path](https://learn.microsoft.com/en-us/training/paths/azure-databricks-data-engineer-set-up-configure-environment/) |
| Prepare and Process Data with Azure Databricks | [Path](https://learn.microsoft.com/en-us/training/paths/azure-databricks-data-engineer-prepare-process-data/) |
| Implement a Data Analytics Solution with Azure Databricks | [Path](https://learn.microsoft.com/en-us/training/paths/data-engineer-azure-databricks/) |
| Deploy and Maintain Data Pipelines and Workloads | [Path](https://learn.microsoft.com/en-us/training/paths/azure-databricks-data-engineer-deploy-maintain-data-pipelines-workloads/) |
| Build Machine Learning Solutions using Azure Databricks | [Path](https://learn.microsoft.com/en-us/training/paths/build-operate-machine-learning-solutions-azure-databricks/) |
| DP-750 Course Outline | [Course](https://learn.microsoft.com/en-us/training/courses/dp-750t00) |
| Azure Databricks Data Engineer Associate Certification | [Certification](https://learn.microsoft.com/en-us/credentials/certifications/implementing-data-engineering-solutions-using-azure-databricks/) |

---

## Tips to keep it smooth
1. **Prerequisites:** basic SQL and Python make everything easier. If either is weak, spend a few days on it first.
2. **Practice every day:** type the code yourself instead of only watching.
3. **Stick with one playlist:** switching between channels repeats material.
4. **Watch for older UI:** some videos show older screens or the old Community Edition. Free Edition has replaced Community Edition, and the concepts still apply.
5. **Keep notes:** add them to this repo as you go.

---

## Progress Tracker
- [ ] Step 0: Free Edition account created
- [ ] Week 1: Basics
- [ ] Week 2: Workspace, compute and Unity Catalog
- [ ] Week 3: PySpark DataFrames
- [ ] Week 4: Spark SQL and transformations
- [ ] Week 5: Delta Lake and Medallion architecture
- [ ] Week 6: Ingestion (Auto Loader, COPY INTO)
- [ ] Week 7: Jobs, pipelines and Git
- [ ] Week 8: Capstone project on GitHub
- [ ] Certification exam booked
