<div align="center">

# 🗄️ IBM Z Xplore — PDS1: Files for Miles

### *Mastering Partitioned Data Sets on IBM Z Mainframe*

[![IBM Z Xplore](https://img.shields.io/badge/IBM%20Z%20Xplore-Advanced%20Challenge-0062FF?style=for-the-badge&logo=ibm&logoColor=white)](https://ibmzxplore.influitive.com/)
[![z/OS](https://img.shields.io/badge/z%2FOS-Mainframe-critical?style=for-the-badge&logo=ibm&logoColor=white)](https://www.ibm.com/products/zos)
[![VS Code](https://img.shields.io/badge/VS%20Code-Zowe%20Explorer-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white)](https://marketplace.visualstudio.com/items?itemName=Zowe.vscode-extension-for-zowe)
[![Status](https://img.shields.io/badge/Challenge-Completed%20✓-success?style=for-the-badge)](https://github.com)
[![Level](https://img.shields.io/badge/Level-Advanced-orange?style=for-the-badge)](https://github.com)

---

> **"On IBM Z, every byte matters — and I know exactly where each one lives."**

</div>

---

## 🧭 What Is This?

This repository documents my completion of **PDS1 — Files for Miles**, an advanced hands-on challenge from [IBM Z Xplore](https://ibmzxplore.influitive.com/). The challenge lives on a **real IBM Z mainframe system** accessed through Visual Studio Code and covers the fundamentals of one of the most critical data structures in enterprise computing: **Partitioned Data Sets (PDS)**.

If you've never heard of a mainframe — that's the engine quietly running your bank transactions, airline bookings, and government records, processing **over 30 billion transactions every day**. This challenge proves I can navigate that world confidently.

---

## 🤔 Why Should You Care? (Non-Technical Version)

Think of it this way:

> 🗂️ **Your PC** stores files in folders on your hard drive.
> 🏦 **IBM Z Mainframe** stores files in *Data Sets* — a smarter, faster, and far more secure version — designed to never lose data, even under the heaviest workloads on the planet.

This challenge taught me how to navigate, organize, copy, and process those enterprise-grade data files — skills that are rare, in high demand, and critical in banking, insurance, healthcare, and government IT.

---

## 🏗️ Technical Architecture

### What Is a Partitioned Dataset (PDS)?

A **Partitioned Dataset** is like a folder that contains multiple files (called **Members**). But unlike a regular computer folder, a PDS:

- Has a built-in **directory** (index) tracking every member
- Stores data in fixed **record formats**
- Lives on a named **volume** (storage device)
- Is identified by a **High Level Qualifier (HLQ)** — your unique namespace on the mainframe

```
ZXP.PUBLIC.INPUT          ← This is the PDS (like a folder)
    ├── PDSPART1           ← This is a Member (like a file)
    ├── PDSPART2
    └── PDS1CCAT
```

### z/OS Dataset Type Comparison

| Dataset Type | Best Used For | Access Style | Analogy |
|---|---|---|---|
| **PDS** (Partitioned) | Source code, JCL, config | Random by member | 📁 Folder with files |
| **PS** (Sequential) | Logs, batch output | Top-to-bottom | 📜 Scroll / tape |
| **VSAM** | Databases, indexes | Keyed / random | 🗃️ Filing cabinet |
| **GDG** (Generation) | Version history | Generational | 🗓️ Dated archives |
| **PDSE** (Extended) | Modern source libs | Random + larger | 📂 Upgraded folder |

---

## 🗺️ System Architecture Diagram

```mermaid
graph TD
    A[👤 Developer - VS Code] -->|Zowe Explorer Plugin| B[🌐 z/OS Connection Profile]
    B --> C[🖥️ IBM Z Mainframe]
    C --> D[📦 DATA SET View]
    D --> E[🔍 HLQ Filter: Zxxxxx]
    D --> F[🔍 HLQ Filter: ZXP.PUBLIC.*]
    E --> G[📁 SOURCE PDS]
    E --> H[📁 JCL PDS]
    F --> I[📁 ZXP.PUBLIC.INPUT]
    F --> J[📁 ZXP.PUBLIC.JCL]
    G --> K[📄 PDSPART1]
    G --> L[📄 PDSPART2]
    G --> M[📄 RECIPE]
    H --> N[📄 PDS1CCAT]
    J --> O[📄 CHKAPDS1]
```

---

## ⚙️ End-to-End Workflow

```mermaid
flowchart LR
    A([🚀 Start]) --> B[Set HLQ Filter\nto Zxxxxx]
    B --> C[Mark SOURCE\nas Favorite ⭐]
    C --> D[Switch HLQ\nto ZXP.PUBLIC.*]
    D --> E[Inspect Dataset\nAttributes & Volume]
    E --> F[Copy PDSPART1\n& PDSPART2\nto SOURCE]
    F --> G[Copy PDS1CCAT\nto JCL]
    G --> H[Submit Job\nPDS1CCAT]
    H --> I{Job\nSuccessful?}
    I -->|CC 0000 ✅| J[Rename PDS1OUT\nto RECIPE]
    I -->|Error ❌| K[Check SYSOUT\nLogs]
    K --> H
    J --> L[Submit CHKAPDS1\nValidation Job]
    L --> M([🏆 Challenge Complete])
```

---

## 📋 Step-by-Step Walkthrough

### Step 1 — Set the Filter (HLQ) 🔍

The **High Level Qualifier** is like your username namespace on the mainframe. Setting a filter in VS Code tells it: *"Only show me datasets that belong to me."*

**What I did:** Clicked the magnifying glass icon in the DATA SETS panel → entered my Z-userid `Zxxxxx` → only my datasets appeared.

![Set HLQ Filter](images/step1_set_hlq_filter.png)

> 💡 **Why it matters:** On a real mainframe, there are thousands of datasets. The HLQ filter is your first layer of data access control — you only see what you're authorized to see.

---

### Step 2 — Mark Favorites ⭐

The VS Code Zowe Explorer lets you **star** frequently used datasets so they always appear at the top of your view.

**What I did:** Hovered over the `SOURCE` dataset → clicked the ⭐ star icon → it now appears pinned at the top.

![Favorites](images/step2_favorites.png)

> 💡 **Why it matters:** In production mainframe work, you may have hundreds of datasets. Favorites are your productivity shortcut — like bookmarking the most critical system files.

---

### Step 3 — Switch HLQ & Locate Datasets 🗂️

Next, I switched my HLQ filter to `ZXP.PUBLIC.*` to browse pre-built public datasets provided by IBM Z Xplore.

**What I did:** Updated the filter → right-clicked a dataset to inspect its attributes → found the dataset on storage **volume `VPWRKD`**.

![Switch HLQ and Locate](images/step3_switch_hlq_locate.png)

> 💡 **Why it matters:** On IBM Z, data lives on physical **volumes** (storage disks). Knowing which volume a dataset is on is essential for capacity planning, backup, and disaster recovery — skills that enterprise architects need daily.

---

### Step 4 — Copy & Paste Members 📋

This step mirrors what developers do constantly in mainframe teams: **copying source code members** from a shared library into your personal workspace.

**What I did:**
- Right-clicked `ZXP.PUBLIC.INPUT(PDSPART1)` → **Copy**
- Right-clicked my `SOURCE` dataset → **Paste** → kept the name `PDSPART1`
- Repeated for `PDSPART2`
- Copied `PDS1CCAT` from `ZXP.PUBLIC.JCL` into my `JCL` dataset

![Copy and Paste](images/step4_copy_paste.png)

> 💡 **Why it matters:** This is exactly how real mainframe teams manage source code — developers pull from shared libraries (like a Git repository equivalent) into their personal datasets to test and modify.

---

### Step 5 — Run That Job! ⚡

A **JCL Job** (Job Control Language) is a script that tells the mainframe's operating system what to do — similar to a shell script or a CI/CD pipeline job.

**What I did:** Right-clicked `PDS1CCAT` in my JCL dataset → selected **"Submit Job"** → waited for the job to execute → a new member `PDS1OUT` appeared in my `SOURCE` dataset.

![Run the Job](images/step5_run_job.png)

> 💡 **Why it matters:** JCL job submission is the heartbeat of mainframe operations. Every bank statement, payroll run, and insurance claim is processed by a JCL job. Running one successfully proves I understand the core execution model of IBM Z.

---

### Step 6 — Rename the Output 🏷️

The final step was renaming the job's output member from `PDS1OUT` to `RECIPE`, then running a validation job to confirm completion.

**What I did:** Right-clicked `PDS1OUT` → **Rename** → `RECIPE` → submitted the `CHKAPDS1` validation job → received **CC 0000** (Condition Code 0 = perfect success).

> 🎉 The `RECIPE` member contained instructions for making **vegetarian tacos** — a fun way IBM Z Xplore confirms you've successfully processed a data member!

---

## 🔐 Security Features & Concepts

This challenge, while introductory, demonstrates real enterprise-grade security concepts baked into z/OS:

| Security Feature | How It Works | Why It Matters |
|---|---|---|
| **HLQ Namespacing** | Each user has a unique HLQ (e.g., `Zxxxxx`) | Prevents accidental access to other users' data |
| **RACF Integration** | z/OS uses Resource Access Control Facility | Controls who can read, write, or delete any dataset |
| **Volume Isolation** | Data lives on named volumes (e.g., `VPWRKD`) | Physical separation of data sets |
| **Job Authorization** | Only authorized users can submit JCL jobs | Prevents unauthorized batch execution |
| **Condition Codes** | Jobs return codes (CC 0000 = success) | Auditable job execution trail |
| **Zowe Secure Connection** | VS Code connects via encrypted profile | TLS-secured mainframe communication |

---

## 🛠️ Tech Stack

| Component | Technology | Purpose |
|---|---|---|
| **IDE** | Visual Studio Code | Development environment |
| **Extension** | Zowe Explorer (IBM) | Mainframe connectivity |
| **Operating System** | IBM z/OS | Mainframe OS |
| **Data Structure** | Partitioned Dataset (PDS) | File organization on z/OS |
| **Job Language** | JCL (Job Control Language) | Batch job execution |
| **Connection Protocol** | z/OSMF / Zowe API | Secure REST-based mainframe access |
| **Storage** | Named Volumes (VPWRKD) | Physical data storage on IBM Z |
| **Validation** | Batch Job (CHKAPDS1) | Automated challenge verification |

---

## 📊 Challenge at a Glance

![Challenge Steps Time](images/challenge_steps_bar.png)

![z/OS Dataset Types](images/dataset_types_pie.png)

![IBM Z vs PC](images/mainframe_vs_pc.png)

---

## 🔁 JCL Job Lifecycle

```mermaid
sequenceDiagram
    participant D as 👤 Developer (VS Code)
    participant Z as 🖥️ z/OS Mainframe
    participant J as ⚙️ Job Entry Subsystem (JES)
    participant S as 💾 Storage (VPWRKD)

    D->>Z: Submit PDS1CCAT JCL Job
    Z->>J: Queue Job for Execution
    J->>S: Read PDSPART1 + PDSPART2 from SOURCE
    S-->>J: Return member data
    J->>J: Concatenate members
    J->>S: Write output → SOURCE(PDS1OUT)
    J-->>Z: Return CC 0000 (Success)
    Z-->>D: Job Complete Notification
    D->>Z: Rename PDS1OUT → RECIPE
    D->>Z: Submit CHKAPDS1 (Validation)
    Z-->>D: ✅ Challenge Validated!
```

---

## 📐 Dataset Structure Deep Dive

```mermaid
graph LR
    subgraph MY["👤 My Workspace (Zxxxxx.*)"]
        S[📁 SOURCE PDS]
        J[📁 JCL PDS]
        S --> S1[📄 PDSPART1]
        S --> S2[📄 PDSPART2]
        S --> S3[📄 RECIPE ⭐]
        J --> J1[📄 PDS1CCAT]
    end

    subgraph PUB["🌐 Public Datasets (ZXP.PUBLIC.*)"]
        PI[📁 ZXP.PUBLIC.INPUT]
        PJ[📁 ZXP.PUBLIC.JCL]
        PI --> PI1[📄 PDSPART1]
        PI --> PI2[📄 PDSPART2]
        PJ --> PJ1[📄 PDS1CCAT]
        PJ --> PJ2[📄 CHKAPDS1]
    end

    PI1 -->|Copy| S1
    PI2 -->|Copy| S2
    PJ1 -->|Copy| J1
    J1 -->|Submit Job| S3
```

---

## 🧠 What I Learned (And Why You Should Hire Me)

After completing this challenge, I can confidently say:

- ✅ I understand how **IBM Z organizes enterprise data** at a structural level
- ✅ I can **navigate, copy, and manage PDS members** using modern tooling (VS Code + Zowe)
- ✅ I can **submit and monitor JCL batch jobs** — the lifeblood of mainframe workloads
- ✅ I understand **volume-based storage architecture** and dataset attributes
- ✅ I know how **security namespacing (HLQ + RACF)** protects mainframe data
- ✅ I bridge the gap between **modern developer tooling** and **legacy mainframe systems**

> 🌐 **The mainframe is not legacy — it's the invisible backbone of the global economy.**
> I'm one of the rare engineers who can work on both sides of that bridge.

---

## 🔗 Resources

- [IBM Z Xplore Learning Platform](https://ibmzxplore.influitive.com/)
- [Zowe Explorer for VS Code](https://marketplace.visualstudio.com/items?itemName=Zowe.vscode-extension-for-zowe)
- [IBM z/OS Dataset Documentation](https://www.ibm.com/docs/en/zos)
- [JCL Reference Guide](https://www.ibm.com/docs/en/zos/latest?topic=language-job-control)
- [IBM Z Skills Network](https://www.ibm.com/training/z)

---

<div align="center">

**Built with 🖤 on a real IBM Z Mainframe**

*IBM Z Xplore — PDS1 Challenge | Advanced Level | Completed ✅*

[![LinkedIn](https://img.shields.io/badge/Connect%20on-LinkedIn-0077B5?style=for-the-badge&logo=linkedin)](https://linkedin.com/in/anandsundar96)
[![GitHub](https://img.shields.io/badge/More%20Projects-GitHub-181717?style=for-the-badge&logo=github)](https://github.com/anandsundar)

</div>
