# Microsoft Azure — Complete Engineering Curriculum
## Zero to Senior Azure / DevOps Engineer

> **Covers:** AZ-900 · AZ-104 · AZ-204 · AZ-400 · AZ-305 · AZ-500 · AZ-700 · DP-203 · AI-102
> **Track:** Cloud/DevOps Career Path | Beginner → Senior Engineer
> **Author:** Azure Cloud & DevOps Mastery Program
> **Based on:** Official Microsoft Azure Documentation & Microsoft Well-Architected Framework

---

## How to Use This Document

- Read each lesson in order — concepts build on each other
- Do every hands-on lab — reading alone will not make you job-ready
- Run every CLI command yourself — muscle memory matters
- Attempt every practice question before reading the answer
- Return to earlier sections when later ones reference them

---

## Table of Contents

### PHASE 1 — Foundations (AZ-900)
- [Lesson 1 — Cloud Computing Fundamentals](#lesson-1--cloud-computing-fundamentals)
- [Lesson 2 — Azure Identity and Access Management](#lesson-2--azure-identity-and-access-management)
- [Lesson 3 — Azure Virtual Machines](#lesson-3--azure-virtual-machines)
- [Lesson 4 — Azure Virtual Networks](#lesson-4--azure-virtual-networks)
- [Lesson 5 — Azure Storage](#lesson-5--azure-storage)

### PHASE 2 — Associate Level (AZ-104 / AZ-204)
- [Lesson 6 — Azure Virtual Machines Deep Dive](#lesson-6--azure-virtual-machines-deep-dive)
- [Lesson 7 — Advanced Networking — NSG, ASG, Load Balancer, App Gateway](#lesson-7--advanced-networking)
- [Lesson 8 — Azure App Service](#lesson-8--azure-app-service)
- [Lesson 9 — Azure Functions and Serverless](#lesson-9--azure-functions-and-serverless)
- [Lesson 10 — Azure SQL Database and Cosmos DB](#lesson-10--azure-sql-database-and-cosmos-db)
- [Lesson 11 — Azure Monitor and Log Analytics](#lesson-11--azure-monitor-and-log-analytics)
- [Lesson 12 — Azure DNS and CDN](#lesson-12--azure-dns-and-cdn)
- [Lesson 13 — API Management](#lesson-13--api-management)

### PHASE 3 — DevOps Engineer Level (AZ-400)
- [Lesson 14 — Infrastructure as Code with Terraform](#lesson-14--infrastructure-as-code-with-terraform)
- [Lesson 15 — ARM Templates and Bicep](#lesson-15--arm-templates-and-bicep)
- [Lesson 16 — Azure DevOps Pipelines](#lesson-16--azure-devops-pipelines)
- [Lesson 17 — GitHub Actions with Azure](#lesson-17--github-actions-with-azure)
- [Lesson 18 — Azure Container Registry and Docker](#lesson-18--azure-container-registry-and-docker)
- [Lesson 19 — Azure Kubernetes Service (AKS)](#lesson-19--azure-kubernetes-service)
- [Lesson 20 — Azure Container Apps](#lesson-20--azure-container-apps)
- [Lesson 21 — Azure Key Vault and Secrets Management](#lesson-21--azure-key-vault-and-secrets-management)

### PHASE 4 — Architect Level (AZ-305)
- [Lesson 22 — Designing Highly Available Architectures](#lesson-22--designing-highly-available-architectures)
- [Lesson 23 — Multi-Region Deployment and Disaster Recovery](#lesson-23--multi-region-deployment-and-disaster-recovery)
- [Lesson 24 — Hybrid Cloud with Azure Arc](#lesson-24--hybrid-cloud-with-azure-arc)
- [Lesson 25 — VNet Peering and Azure Private Link](#lesson-25--vnet-peering-and-azure-private-link)
- [Lesson 26 — Cost Optimization Strategies](#lesson-26--cost-optimization-strategies)
- [Lesson 27 — Performance and Scalability Architecture](#lesson-27--performance-and-scalability-architecture)

### PHASE 5 — Expert and Specialty Level (AZ-500 · AZ-700 · DP-203 · AI-102)
- [Lesson 28 — Azure Security Architecture](#lesson-28--azure-security-architecture)
- [Lesson 29 — Advanced Azure Networking](#lesson-29--advanced-azure-networking)
- [Lesson 30 — Azure Data Engineering](#lesson-30--azure-data-engineering)
- [Lesson 31 — Azure AI and Cognitive Services](#lesson-31--azure-ai-and-cognitive-services)
- [Lesson 32 — Production Incident Response and Troubleshooting](#lesson-32--production-incident-response-and-troubleshooting)
- [Lesson 33 — Azure Interview Preparation — Senior Engineer Level](#lesson-33--azure-interview-preparation)

---

---

# PHASE 1 — FOUNDATIONS
## AZ-900: Azure Fundamentals Certification Track

---

## Lesson 1 — Cloud Computing Fundamentals

> **Certification:** AZ-900 Domain 1 — Cloud Concepts (25–30% of exam)
> **Level:** Absolute Beginner

---

### 1.1 What is Cloud Computing?

Before touching Azure, build the right mental model.

**The Analogy:** Imagine you run a restaurant. For electricity, you have two options:

- **Option A — Own Your Generator:** Buy it, maintain it, pay for fuel, hire an electrician, replace it when it breaks. All costs, all risk, all responsibility is yours.
- **Option B — City Power Grid:** Pay only for what you consume. Let someone else build and operate the infrastructure. Scale instantly. No upfront investment.

> **Cloud computing = Option B, but for computing resources** — servers, storage, databases, networking, AI, analytics — all delivered over the internet on demand.

**Microsoft's Definition:**
> Cloud computing is the delivery of computing services over the internet, enabling faster innovation, flexible resources, and economies of scale.

---

### 1.2 The Five Core Characteristics of Cloud Computing

These are defined by NIST (National Institute of Standards and Technology) and tested on AZ-900.

| Characteristic | What It Means | Real Azure Example |
|---|---|---|
| **On-Demand Self-Service** | Provision resources yourself, no human needed from Microsoft | Spin up a VM in 2 minutes via Azure Portal |
| **Broad Network Access** | Available from anywhere on any device via internet | Your Azure-hosted app is reachable from any browser globally |
| **Resource Pooling** | Microsoft serves many customers from shared infrastructure | Your VM runs on shared physical hardware, securely isolated |
| **Rapid Elasticity** | Scale up or down instantly based on demand | Auto-scale web servers during a flash sale traffic spike |
| **Measured Service** | Usage is monitored, metered, and billed accurately | Azure Cost Management shows per-resource billing in real time |

> **Why This Matters for Your Career:** Every architecture decision — whether to scale horizontally, use reserved pricing, or choose serverless — connects back to these five characteristics.

---

### 1.3 Cloud Deployment Models

Three models. Know when and why to use each — this is tested heavily on AZ-900.

#### Public Cloud
- **Definition:** Infrastructure owned and operated by a third-party provider (Azure, AWS, GCP)
- **Who uses it:** Startups, SaaS companies, enterprises migrating to cloud
- **Real Example:** A fintech startup runs their entire app on Azure — zero physical servers
- **Pros:** No capital expenditure, global scale, pay-as-you-go
- **Cons:** Less direct control, data residency concerns in regulated industries

#### Private Cloud
- **Definition:** Cloud infrastructure operated solely for one organisation (on-premises or hosted)
- **Who uses it:** Government, large banks, hospitals — highly regulated industries
- **Real Example:** A major Indian bank runs its own virtualised infrastructure in a Mumbai data centre
- **Pros:** Full control over hardware, data, and security policies
- **Cons:** You bear all infrastructure costs, maintenance, and capacity planning

#### Hybrid Cloud — The Real-World Standard
- **Definition:** Combination of public and private cloud, connected securely via VPN or ExpressRoute
- **Who uses it:** 85%+ of large enterprises — this is the dominant model in production
- **Real Example:** A manufacturing company keeps SAP ERP on-premises (RBI compliance) but runs customer-facing apps and analytics on Azure
- **Why Azure wins here:** Microsoft architected Azure for hybrid from day one — Azure Arc, Azure Stack, ExpressRoute

> **Architect Note:** In your career, you will design hybrid architectures constantly. Pure public-only is for startups. Pure private is expensive and dying. Hybrid is enterprise reality.

---

### 1.4 Cloud Service Models — IaaS, PaaS, SaaS

The model you choose determines how much you manage versus how much Azure manages.

| Model | Full Name | Azure Example | You Manage | Azure Manages |
|---|---|---|---|---|
| **IaaS** | Infrastructure as a Service | Azure Virtual Machines | OS, Runtime, App, Data | Hardware, Hypervisor |
| **PaaS** | Platform as a Service | Azure App Service | App Code, Data | OS, Runtime, Scaling, Patching |
| **SaaS** | Software as a Service | Microsoft 365 | Your Data, User Config | Everything else |

**Practical Scenario — Deploying a Web App:**
- **IaaS approach:** You provision a VM, install Linux/Windows, install Nginx, deploy app, configure firewalls, patch monthly. Full control, full burden.
- **PaaS approach:** You push your code. Azure handles OS, runtime, auto-scaling, load balancing, patching. You own only the code and data.
- **SaaS approach:** You just log in and use it. Zero infrastructure responsibility.

> **Career Insight:** Modern cloud engineers minimise IaaS usage and maximise PaaS wherever possible. 'Lift and shift to VMs' is a starting point, never a final architecture. You will hear this in every AZ-305 scenario.

---

### 1.5 The Shared Responsibility Model

Who is responsible for what? This is tested across AZ-900, AZ-104, and AZ-500.

| Responsibility Area | On-Premises | IaaS | PaaS | SaaS |
|---|---|---|---|---|
| Physical Datacenter | YOU | AZURE | AZURE | AZURE |
| Physical Network | YOU | AZURE | AZURE | AZURE |
| Physical Host | YOU | AZURE | AZURE | AZURE |
| Operating System | YOU | **YOU** | AZURE | AZURE |
| Network Controls | YOU | **YOU** | SHARED | AZURE |
| Application | YOU | **YOU** | **YOU** | AZURE |
| Identity & Access | YOU | **YOU** | **YOU** | **YOU** |
| Data | YOU | **YOU** | **YOU** | **YOU** |

> **The Golden Rule:** No matter what service model — IaaS, PaaS, or SaaS — you ALWAYS own your **data** and **identity management**. Azure never takes responsibility for who you grant access to.

> **Exam Trap:** If a question asks who is responsible for "data" or "identities", the answer is always the customer — regardless of service model.

---

### 1.6 Azure Global Infrastructure

Every architecture decision you make is built on this foundation.

```
AZURE GEOGRAPHY  (e.g., India, Europe, United States)
  └── REGION  (e.g., Central India — Pune)
        └── AVAILABILITY ZONE  (AZ1, AZ2, AZ3)
              └── DATA CENTER  (physical building)
```

#### Geographies
- Defined areas meeting **data residency and compliance boundaries**
- India Geography: Central India (Pune), South India (Chennai), West India (Mumbai)
- Relevant law: India's DPDP Act, RBI data localisation requirements

#### Regions
- A set of data centres deployed within a defined geographic area
- Azure has **60+ regions globally** — more than any other cloud provider
- When you deploy any resource, you choose a region
- **Choice of region affects:** latency, compliance, disaster recovery, cost

#### Availability Zones
- **3+ physically separate data centres** within a single region
- Each zone has independent power, cooling, and networking
- Connected by ultra-low latency fibre (< 2ms between zones)
- **Purpose:** Protect against individual data centre failures

**Production Example:**
> A bank deploys their payment processing app across all 3 AZs in Central India. When AZ1 has a cooling failure, traffic automatically moves to AZ2 and AZ3. Zero downtime. Zero customer impact.

#### Region Pairs
- Every Azure region is paired with another region at least 300 miles away
- Azure never patches both regions in a pair simultaneously
- Some storage services auto-replicate to the paired region

| Region | Paired With |
|---|---|
| Central India (Pune) | South India (Chennai) |
| East US | West US |
| North Europe | West Europe |

> **Exam Alert — Common Trap:**
> - **Availability Zones** = protect from individual data centre failures within a region
> - **Region Pairs** = protect from entire regional disasters
> - **Geographies** = define data residency boundaries for compliance
> These three are regularly confused in exam questions. Know the difference cold.

---

### 1.7 Azure CLI Setup

The Azure CLI is how production engineers interact with Azure. Learn it from day one.

**Install Azure CLI:**

```bash
# macOS
brew update && brew install azure-cli

# Windows (PowerShell as Administrator)
winget install -e --id Microsoft.AzureCLI

# Ubuntu / Debian Linux
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

# Verify installation
az --version
```

**Essential first commands:**

```bash
# Login to Azure (opens browser)
az login

# List all subscriptions
az account list --output table

# Set active subscription
az account set --subscription "Your Subscription Name"

# Verify current account
az account show

# List all Azure regions
az account list-locations --query "[].{Region:name, DisplayName:displayName}" --output table

# List India regions only
az account list-locations \
  --query "[?contains(name, 'india')].{Name:name, DisplayName:displayName}" \
  --output table
```

**The CLI Pattern — memorise this:**
```
az [resource-type] [action] --[parameters]

Examples:
az vm create ...
az storage account create ...
az network vnet create ...
az group create ...
```

---

### 1.8 Hands-On Lab — Explore Azure Infrastructure

**Objective:** Create your first Resource Group and explore Azure's infrastructure via CLI and Portal.
**Duration:** 20 minutes | **Cost:** Free

**Step 1 — Create Azure Free Account**
1. Go to [portal.azure.com](https://portal.azure.com)
2. Sign up for a free account — $200 credit for 30 days + 12 months of free services
3. No charges without explicit upgrade to pay-as-you-go

**Step 2 — Create Your First Resource Group via CLI**

```bash
# Login
az login

# Create a resource group in Central India
az group create \
  --name az-training-rg \
  --location centralindia

# Verify it was created
az group list --output table

# Get details about your resource group
az group show --name az-training-rg
```

**Step 3 — Explore via Portal**
1. Go to portal.azure.com → search "Resource Groups"
2. Click `az-training-rg` → explore the empty dashboard
3. Click "Overview" → note the Region and Subscription ID

> **What is a Resource Group?** Every Azure resource must live inside a Resource Group. It's a logical container for related resources. You can manage, monitor, tag, and delete all resources in a group together. Always organise resources by environment and application: `prod-webapp-rg`, `dev-api-rg`, `staging-db-rg`.

---

### 1.9 AZ-900 Practice Questions — Lesson 1

**Q1.** A company must ensure their data never leaves India due to regulatory requirements. Which Azure feature directly addresses this?

- A) Availability Zones
- B) Azure Geographies
- C) Azure Resource Groups
- D) Region Pairs

<details>
<summary>Answer and Explanation</summary>

**Answer: B — Azure Geographies**

Geographies define data residency and compliance boundaries. Availability Zones are about resilience within a region, not data location. Resource Groups are organisational containers. Region Pairs relate to disaster recovery.

</details>

---

**Q2.** A company runs their HR application on Azure Virtual Machines. Who is responsible for patching the operating system?

- A) Microsoft Azure
- B) The company (customer)
- C) Shared equally between Azure and the company
- D) Azure patches it automatically on a schedule

<details>
<summary>Answer and Explanation</summary>

**Answer: B — The company (customer)**

IaaS means you manage the OS. Azure manages the physical hardware and hypervisor only. This is Shared Responsibility Model — core to AZ-900, AZ-104, and AZ-500.

</details>

---

**Q3.** Which cloud characteristic allows a retail company to add 100 servers during a holiday sale and remove them the next day, paying only for what was used?

- A) Broad network access
- B) On-demand self-service
- C) Rapid elasticity
- D) Resource pooling

<details>
<summary>Answer and Explanation</summary>

**Answer: C — Rapid Elasticity**

Rapid elasticity = scale resources quickly based on demand and pay only for what you use. Classic AZ-900 question.

</details>

---

**Q4 — Scenario.** Contoso Bank has a core banking system that cannot move to public cloud due to RBI regulations. They want to run their customer mobile app backend on Azure and connect it securely to the on-premises system. What deployment model?

- A) Public Cloud
- B) Private Cloud
- C) Hybrid Cloud
- D) Community Cloud

<details>
<summary>Answer and Explanation</summary>

**Answer: C — Hybrid Cloud**

Core banking stays on-premises for regulatory compliance. Customer apps run on Azure. Both connected via ExpressRoute or VPN Gateway. This is the standard architecture for large Indian enterprises.

</details>

---

---

## Lesson 2 — Azure Identity and Access Management

> **Certification:** AZ-900 Domain 2 + AZ-104 Domain 1 + AZ-500 Domain 1
> **Level:** Beginner → Intermediate

---

### 2.1 Why Identity is the New Security Perimeter

In traditional IT, security was a network perimeter — a firewall around a data centre. In cloud, that model breaks down. Users work from anywhere. Apps call other apps. Services talk to services.

> **The modern security perimeter is Identity.** In Azure, controlling *who* and *what* can access *which resources* under *what conditions* is the foundation of everything.

Two systems manage this in Azure:
1. **Microsoft Entra ID** (formerly Azure Active Directory) — manages human and application identities
2. **Azure RBAC** (Role-Based Access Control) — controls what those identities can do

---

### 2.2 Microsoft Entra ID (Azure Active Directory)

**What it is:** Microsoft's cloud-based identity and access management service. Think of it as the login system for everything Microsoft — Azure, Microsoft 365, Teams, your custom apps.

**Key Objects in Entra ID:**

| Object | What It Is | Real Example |
|---|---|---|
| **User** | A human identity in your organisation | john.doe@company.com |
| **Group** | Collection of users — assign permissions to groups, not individuals | Developers-Group, Admins-Group |
| **Service Principal** | Identity for an application or service | Your CI/CD pipeline authenticating to Azure |
| **Managed Identity** | Azure-managed service principal — no credentials to manage | A VM reading secrets from Key Vault |
| **Tenant** | Your organisation's dedicated Entra ID instance | company.onmicrosoft.com |

> **Production Best Practice:** Never assign permissions directly to individual users. Always use groups. When someone joins or leaves a team, you change their group membership — not dozens of individual role assignments.

---

### 2.3 Azure RBAC — Role-Based Access Control

RBAC answers: **Who** can do **what** to **which resources**?

**The Three Components:**

```
WHO (Security Principal)  +  WHAT (Role Definition)  +  WHICH (Scope)  =  Role Assignment
```

**Security Principals (WHO):**
- User, Group, Service Principal, or Managed Identity

**Built-in Roles (WHAT) — Know These for Every Certification:**

| Role | What It Can Do | Typical User |
|---|---|---|
| **Owner** | Full access + manage access | Subscription admin |
| **Contributor** | Create and manage resources, cannot manage access | Senior developer |
| **Reader** | View resources only, no changes | Auditor, junior developer |
| **User Access Administrator** | Manage access only | Security team |

**Scope (WHICH) — Hierarchy:**
```
Management Group
  └── Subscription
        └── Resource Group
              └── Individual Resource
```

Permissions assigned at a higher scope **inherit downward**. A Contributor on a Resource Group is a Contributor on everything inside it.

**Deny Assignments:** Explicitly block access even if a role assignment grants it. Used in Azure Blueprints. Deny always overrides allow.

> **The Principle of Least Privilege:** Always assign the minimum permissions needed. Never give Owner when Contributor works. Never give Contributor when Reader works. This is asked in AZ-104, AZ-305, and AZ-500 scenarios constantly.

---

### 2.4 Multi-Factor Authentication (MFA)

**What it is:** Requiring more than just a password to authenticate. Something you know (password) + something you have (phone/authenticator app).

**Why it matters:** 99.9% of account compromise attacks are stopped by MFA. Microsoft's own data.

**In Azure:** Enabled via Microsoft Entra ID → Security → MFA

**Conditional Access:** More sophisticated than simple MFA. Define policies like:
- "Require MFA when accessing from outside India"
- "Block access from unknown devices"
- "Require compliant device for accessing financial apps"

---

### 2.5 Managed Identities — The Right Way to Authenticate Services

**The Problem:** You have an Azure Function that needs to read from Azure Blob Storage. How does it authenticate? You could hardcode credentials — but that's a massive security risk. You could store them in config — still risky.

**The Solution: Managed Identities.** Azure creates and manages an identity for your service. No credentials to store, rotate, or worry about.

**Two Types:**
- **System-assigned:** Tied to one specific resource. Deleted when the resource is deleted.
- **User-assigned:** Independent identity. Can be assigned to multiple resources.

```bash
# Enable system-assigned managed identity on a VM
az vm identity assign \
  --name myVM \
  --resource-group az-training-rg

# Assign a role to that managed identity
az role assignment create \
  --assignee <principal-id> \
  --role "Storage Blob Data Reader" \
  --scope /subscriptions/<sub-id>/resourceGroups/az-training-rg
```

> **Production Best Practice:** Always use Managed Identities for service-to-service authentication within Azure. Never store credentials in application code, config files, or environment variables.

---

### 2.6 Hands-On Lab — Identity and RBAC

**Objective:** Create a user, create a group, assign RBAC roles
**Duration:** 25 minutes | **Cost:** Free

```bash
# Step 1: Create a new user in Entra ID
az ad user create \
  --display-name "Dev User One" \
  --user-principal-name devuser1@<your-tenant>.onmicrosoft.com \
  --password "TempP@ssword123!" \
  --force-change-password-next-sign-in true

# Step 2: Create a group
az ad group create \
  --display-name "AzureDevTeam" \
  --mail-nickname "AzureDevTeam"

# Step 3: Add the user to the group
az ad group member add \
  --group "AzureDevTeam" \
  --member-id <user-object-id>

# Step 4: Assign Contributor role to the group on your resource group
az role assignment create \
  --assignee <group-object-id> \
  --role "Contributor" \
  --resource-group az-training-rg

# Step 5: List role assignments on your resource group
az role assignment list \
  --resource-group az-training-rg \
  --output table
```

---

### 2.7 Practice Questions — Lesson 2

**Q1.** A developer needs to read resources in a resource group but must not be able to create, modify, or delete anything. Which built-in RBAC role should be assigned?

- A) Owner
- B) Contributor
- C) Reader
- D) User Access Administrator

<details>
<summary>Answer</summary>

**Answer: C — Reader**. Read-only access. Contributor would allow changes. Owner allows everything including managing access.

</details>

---

**Q2.** An Azure Function needs to read secrets from Azure Key Vault. What is the most secure authentication method?

- A) Store the Key Vault access key in the Function's application settings
- B) Hardcode the credentials in the Function's source code
- C) Use a System-Assigned Managed Identity and grant it Key Vault access
- D) Create a service principal with a client secret and store it in a config file

<details>
<summary>Answer</summary>

**Answer: C — System-Assigned Managed Identity**. No credentials to manage, rotate, or accidentally expose. Azure handles the identity lifecycle automatically.

</details>

---

---

## Lesson 3 — Azure Virtual Machines

> **Certification:** AZ-900 + AZ-104 Domain 2
> **Level:** Beginner → Intermediate

---

### 3.1 What is a Virtual Machine?

A Virtual Machine is an emulation of a physical computer. Azure runs your VM on physical hardware in their data centres, but you get your own isolated environment with your own OS, CPU, RAM, and storage.

**When to use VMs:**
- Migrating existing on-premises workloads ("lift and shift")
- Running legacy applications that need specific OS versions
- Workloads requiring full OS control
- When PaaS options don't fit (rare, but exists)

**When NOT to use VMs:**
- When Azure App Service, Functions, or containers can do the job — they're cheaper and lower maintenance

---

### 3.2 VM Size Families — Know These

Azure has dozens of VM sizes organised into families. Each family is optimised for different workloads.

| Family | Use Case | Example Sizes |
|---|---|---|
| **B-series** | Burstable, dev/test, low cost | B1s, B2s |
| **D-series** | General purpose, balanced CPU/RAM | D2s_v5, D4s_v5 |
| **E-series** | Memory optimised, databases | E4s_v5, E8s_v5 |
| **F-series** | Compute optimised, batch processing | F4s_v2, F8s_v2 |
| **N-series** | GPU, machine learning, rendering | NC6, ND40rs_v2 |
| **M-series** | Very large memory, SAP HANA | M128s |

**Naming Convention:** `Standard_D4s_v5`
- `Standard` = pricing tier
- `D` = series family
- `4` = number of vCPUs
- `s` = supports Premium SSD
- `v5` = version 5

---

### 3.3 VM Storage — Managed Disks

Every VM has at least one disk. Azure Managed Disks are the modern standard — Azure handles the underlying storage account for you.

| Disk Type | Performance | Use Case | Cost |
|---|---|---|---|
| **Ultra Disk** | Up to 160,000 IOPS | SQL Server, SAP HANA | Highest |
| **Premium SSD v2** | Up to 80,000 IOPS | Production databases | High |
| **Premium SSD** | Up to 20,000 IOPS | Production workloads | Medium-High |
| **Standard SSD** | Up to 6,000 IOPS | Dev/Test, light production | Medium |
| **Standard HDD** | Up to 2,000 IOPS | Backups, infrequent access | Lowest |

> **Production Rule:** Always use Premium SSD or above for production workloads. Standard HDD for backups and archival only.

---

### 3.4 VM Availability Options

| Option | Protection Against | SLA |
|---|---|---|
| **Single VM (Premium SSD)** | Hardware failures | 99.9% |
| **Availability Set** | Rack-level failures within one DC | 99.95% |
| **Availability Zone** | Full data centre failures | 99.99% |
| **VM Scale Sets** | Traffic spikes + failures | 99.99% |

> **Production Rule:** Never deploy a single production VM without availability configuration. Minimum: Availability Zone deployment.

---

### 3.5 Hands-On Lab — Deploy Your First VM

**Duration:** 30 minutes | **Cost:** ~$0.01 on free account

```bash
# Step 1: Create a resource group for this lab
az group create \
  --name vm-lab-rg \
  --location centralindia

# Step 2: Create a Linux VM (Ubuntu, smallest/cheapest size)
az vm create \
  --resource-group vm-lab-rg \
  --name my-first-vm \
  --image Ubuntu2204 \
  --size Standard_B1s \
  --admin-username azureuser \
  --generate-ssh-keys \
  --public-ip-sku Standard

# Step 3: Open port 22 for SSH access
az vm open-port \
  --resource-group vm-lab-rg \
  --name my-first-vm \
  --port 22

# Step 4: Get the public IP address
az vm show \
  --resource-group vm-lab-rg \
  --name my-first-vm \
  --show-details \
  --query publicIps \
  --output tsv

# Step 5: SSH into the VM
ssh azureuser@<public-ip>

# Step 6: Inside the VM — explore
uname -a
df -h
free -m
exit

# Step 7: Stop the VM (saves cost — stopped VM = no compute charge)
az vm stop \
  --resource-group vm-lab-rg \
  --name my-first-vm

# Step 8: Clean up when done
az group delete --name vm-lab-rg --yes --no-wait
```

---

### 3.6 Practice Questions — Lesson 3

**Q1.** A company wants to deploy a production web server on Azure VM with the highest availability. Which availability option provides a 99.99% SLA?

- A) Single VM with Premium SSD
- B) Availability Set with 2 VMs
- C) Availability Zone deployment
- D) Standard VM with no redundancy

<details>
<summary>Answer</summary>

**Answer: C — Availability Zone**. Zones provide 99.99% SLA, protecting from entire data centre failures. Availability Sets only protect from rack-level failures within one data centre (99.95%).

</details>

---

---

## Lesson 4 — Azure Virtual Networks

> **Certification:** AZ-900 + AZ-104 Domain 3 + AZ-700
> **Level:** Beginner → Intermediate

---

### 4.1 Why Networking is Fundamental

Every resource in Azure — VMs, databases, App Services — needs to communicate. Azure Virtual Networks (VNets) are how you control that communication: who can talk to whom, over which path, with what security controls.

> **The real-world analogy:** A VNet is your office building's private internal network. Just like your office network has an internal IP range (192.168.x.x), your VNet has its own IP range. Internal resources talk to each other privately. Access from outside goes through controlled entry points.

---

### 4.2 VNet Core Concepts

**Virtual Network (VNet):**
- An isolated, private network in Azure
- You define the IP address space (e.g., 10.0.0.0/16)
- Scoped to one region
- Resources inside a VNet can communicate privately

**Subnets:**
- Subdivisions within a VNet
- Allow you to segment and control traffic
- Each subnet has its own IP range within the VNet space
- Resources (VMs, App Services, etc.) are deployed into subnets

**Example VNet Architecture:**
```
VNet: 10.0.0.0/16 (65,536 addresses)
  ├── Subnet: web-tier     10.0.1.0/24  (web servers)
  ├── Subnet: app-tier     10.0.2.0/24  (application servers)
  ├── Subnet: data-tier    10.0.3.0/24  (databases — no internet access)
  └── Subnet: mgmt         10.0.4.0/24  (management/bastion)
```

> **Architecture Principle:** Always separate tiers into different subnets. This lets you apply different security rules to web servers, app servers, and databases independently.

---

### 4.3 Network Security Groups (NSGs)

NSGs are virtual firewalls. They contain rules that allow or deny inbound and outbound traffic.

**NSG Rules contain:**
- Priority (lower number = higher priority, processed first)
- Source (IP, range, or service tag)
- Destination (IP, range, or service tag)
- Protocol (TCP, UDP, Any)
- Port or port range
- Action (Allow or Deny)

**Default rules (cannot be deleted, can be overridden):**
- Allow VNet inbound traffic
- Allow Azure Load Balancer inbound
- Deny all other inbound (DenyAllInbound — priority 65500)
- Allow VNet outbound
- Allow internet outbound
- Deny all other outbound (DenyAllOutbound — priority 65500)

**NSGs can be attached to:**
- Subnets (apply to all resources in the subnet)
- Individual Network Interfaces (apply to specific VMs)

> **Best Practice:** Attach NSGs to subnets, not individual NICs. Easier to manage at scale. Apply NIC-level NSGs only when a specific VM needs different rules from the subnet.

---

### 4.4 Hands-On Lab — Create a VNet with Subnets and NSG

**Duration:** 30 minutes

```bash
# Step 1: Create resource group
az group create \
  --name vnet-lab-rg \
  --location centralindia

# Step 2: Create VNet with address space
az network vnet create \
  --resource-group vnet-lab-rg \
  --name my-vnet \
  --address-prefix 10.0.0.0/16 \
  --location centralindia

# Step 3: Create subnets
az network vnet subnet create \
  --resource-group vnet-lab-rg \
  --vnet-name my-vnet \
  --name web-subnet \
  --address-prefix 10.0.1.0/24

az network vnet subnet create \
  --resource-group vnet-lab-rg \
  --vnet-name my-vnet \
  --name data-subnet \
  --address-prefix 10.0.2.0/24

# Step 4: Create an NSG
az network nsg create \
  --resource-group vnet-lab-rg \
  --name web-nsg

# Step 5: Add rule — allow HTTP traffic on port 80
az network nsg rule create \
  --resource-group vnet-lab-rg \
  --nsg-name web-nsg \
  --name Allow-HTTP \
  --priority 100 \
  --protocol Tcp \
  --destination-port-range 80 \
  --access Allow \
  --direction Inbound

# Step 6: Add rule — allow HTTPS on port 443
az network nsg rule create \
  --resource-group vnet-lab-rg \
  --nsg-name web-nsg \
  --name Allow-HTTPS \
  --priority 110 \
  --protocol Tcp \
  --destination-port-range 443 \
  --access Allow \
  --direction Inbound

# Step 7: Associate NSG with web subnet
az network vnet subnet update \
  --resource-group vnet-lab-rg \
  --vnet-name my-vnet \
  --name web-subnet \
  --network-security-group web-nsg

# Step 8: Verify configuration
az network vnet show \
  --resource-group vnet-lab-rg \
  --name my-vnet \
  --output table

# Clean up
az group delete --name vnet-lab-rg --yes --no-wait
```

---

### 4.5 Practice Questions — Lesson 4

**Q1.** A company wants to prevent all internet traffic from reaching their database subnet while allowing the application subnet to communicate with it. What is the most appropriate approach?

- A) Deploy a separate VNet for the database
- B) Apply an NSG to the database subnet that denies inbound traffic from the internet
- C) Use Azure Firewall on the database VM
- D) Move the database to a different region

<details>
<summary>Answer</summary>

**Answer: B.** Apply an NSG to the database subnet with rules that deny inbound from the internet but allow inbound from the app subnet. This is standard three-tier architecture in Azure.

</details>

---

---

## Lesson 5 — Azure Storage

> **Certification:** AZ-900 + AZ-104 Domain 4
> **Level:** Beginner → Intermediate

---

### 5.1 Azure Storage Overview

Azure Storage is a massively scalable, durable cloud storage service. It is the foundation for storing virtually any type of data in Azure — files, blobs, tables, queues, and disks.

**One storage account can contain multiple storage services:**
```
Storage Account
  ├── Blob Storage      (unstructured data, files, images, backups)
  ├── File Storage      (managed file shares, SMB protocol)
  ├── Queue Storage     (message queuing between services)
  └── Table Storage     (NoSQL key-value store — largely replaced by Cosmos DB)
```

---

### 5.2 Blob Storage — Deep Dive

Blob = Binary Large Object. Blob storage stores any type of unstructured data: images, videos, documents, backups, log files, application data.

**Three Blob Types:**
- **Block Blob:** Most common. Files, images, videos. Optimised for sequential read/write.
- **Append Blob:** Optimised for append operations only. Perfect for log files.
- **Page Blob:** Optimised for random read/write. Used internally for Azure VM disks.

**Access Tiers (for Block Blobs) — Critical for Cost Optimisation:**

| Tier | Access Pattern | Storage Cost | Access Cost | Retrieval Time |
|---|---|---|---|---|
| **Hot** | Frequently accessed data | Highest | Lowest | Immediate |
| **Cool** | Infrequently accessed (once/month) | Lower | Higher | Immediate |
| **Cold** | Rarely accessed (once/quarter) | Lower still | Higher still | Immediate |
| **Archive** | Rarely accessed (compliance, backup) | Lowest | Highest | 1–15 hours |

> **Cost Optimisation Rule:** Use Lifecycle Management policies to automatically move blobs between tiers. Move to Cool after 30 days, Archive after 90 days. This alone can reduce storage costs by 70–80%.

---

### 5.3 Storage Redundancy Options

| Option | What It Does | Copies | Use Case |
|---|---|---|---|
| **LRS** | 3 copies in one data centre | 3 | Dev/test, data that can be recreated |
| **ZRS** | 3 copies across 3 AZs in one region | 3 | Production — protects from DC failure |
| **GRS** | LRS + async copy to paired region | 6 | Production — protects from regional failure |
| **GZRS** | ZRS + async copy to paired region | 6 | Most critical production data |
| **RA-GRS** | GRS + read access to secondary | 6 | Need to read from secondary during outage |

> **Architect Guideline:** For production data, minimum ZRS. For business-critical data, GZRS. RA-GRS when you need read access to the secondary region (e.g., for reporting).

---

### 5.4 Hands-On Lab — Azure Storage

**Duration:** 30 minutes

```bash
# Step 1: Create a storage account (name must be globally unique, lowercase, 3-24 chars)
az storage account create \
  --name mystore$(date +%s) \
  --resource-group az-training-rg \
  --location centralindia \
  --sku Standard_ZRS \
  --kind StorageV2 \
  --access-tier Hot

# Step 2: Get the storage account key
az storage account keys list \
  --resource-group az-training-rg \
  --account-name <your-storage-name> \
  --output table

# Step 3: Create a blob container
az storage container create \
  --name mycontainer \
  --account-name <your-storage-name> \
  --auth-mode login

# Step 4: Upload a file
echo "Hello Azure Storage!" > test.txt
az storage blob upload \
  --account-name <your-storage-name> \
  --container-name mycontainer \
  --name test.txt \
  --file test.txt \
  --auth-mode login

# Step 5: List blobs in container
az storage blob list \
  --account-name <your-storage-name> \
  --container-name mycontainer \
  --auth-mode login \
  --output table

# Step 6: Download the blob
az storage blob download \
  --account-name <your-storage-name> \
  --container-name mycontainer \
  --name test.txt \
  --file downloaded.txt \
  --auth-mode login

cat downloaded.txt

# Step 7: Set lifecycle management policy (move to Cool after 30 days)
cat > lifecycle.json << 'POLICY'
{
  "rules": [
    {
      "name": "move-to-cool",
      "type": "Lifecycle",
      "definition": {
        "actions": {
          "baseBlob": {
            "tierToCool": { "daysAfterModificationGreaterThan": 30 },
            "tierToArchive": { "daysAfterModificationGreaterThan": 90 }
          }
        },
        "filters": {
          "blobTypes": ["blockBlob"]
        }
      }
    }
  ]
}
POLICY

az storage account management-policy create \
  --account-name <your-storage-name> \
  --resource-group az-training-rg \
  --policy @lifecycle.json
```

---

### 5.5 Practice Questions — Lesson 5

**Q1.** A company needs to store large amounts of log data that must be retained for 7 years for compliance but is almost never accessed. Which storage tier is most cost-effective?

- A) Hot
- B) Cool
- C) Cold
- D) Archive

<details>
<summary>Answer</summary>

**Answer: D — Archive**. Rarely accessed compliance data belongs in Archive tier — the lowest storage cost, highest retrieval cost, with retrieval times up to 15 hours. Perfect for compliance archives.

</details>

---

**Q2.** A company needs their production storage to survive the failure of an entire Azure data centre. Which redundancy option provides this at minimum cost?

- A) LRS (Locally Redundant Storage)
- B) ZRS (Zone-Redundant Storage)
- C) GRS (Geo-Redundant Storage)
- D) RA-GRS

<details>
<summary>Answer</summary>

**Answer: B — ZRS**. Zone-Redundant Storage copies data across 3 availability zones, surviving a full data centre failure. LRS only protects within one DC. GRS and RA-GRS offer more protection but at higher cost than what is "minimum" for DC-failure protection.

</details>


---

---

# PHASE 2 — ASSOCIATE LEVEL
## AZ-104: Azure Administrator + AZ-204: Azure Developer

---

## Lesson 6 — Azure Virtual Machines Deep Dive

> **Certification:** AZ-104 Domain 2
> **Level:** Intermediate

---

### 6.1 VM Scale Sets — Auto-Scaling Production Workloads

A VM Scale Set is a group of identical, load-balanced VMs that automatically increase or decrease in number based on demand or a schedule.

**Why Scale Sets exist:**
- You cannot manually add VMs fast enough during a sudden traffic spike
- Over-provisioning VMs wastes money during off-peak hours
- Scale Sets solve both problems automatically

**Scaling Policies:**

| Policy | Trigger | Use Case |
|---|---|---|
| **Manual** | You decide when to scale | Predictable batch jobs |
| **Custom Autoscale** | CPU %, memory %, custom metrics | Most production web workloads |
| **Predictive Autoscale** | ML-based prediction of traffic | E-commerce, media streaming |
| **Schedule-based** | Time of day/week | Known peak hours (9am-5pm weekdays) |

**Scale Set Architecture:**
```
Internet Traffic
     │
     ▼
Load Balancer (distributes traffic)
     │
     ▼
Scale Set (2–100 identical VMs)
  ├── VM Instance 1
  ├── VM Instance 2
  └── VM Instance N (auto-created/destroyed)
```

---

### 6.2 Azure Bastion — Secure VM Access Without Public IP

**The Problem:** If you expose port 22 (SSH) or 3389 (RDP) to the internet, attackers will find it and brute-force it within hours.

**The Solution: Azure Bastion** — a managed service that provides secure SSH/RDP access to VMs through the Azure Portal over HTTPS (port 443), without exposing any public IP on your VMs.

```
Your Browser (HTTPS/443)  →  Azure Bastion  →  VM (private IP only)
```

**Benefits:**
- VMs have no public IP address at all
- No need to manage jump servers
- Session recorded for auditing (Premium tier)
- Fully managed by Microsoft — no patches, no maintenance

> **Production Requirement:** In enterprise environments, Azure Bastion or a VPN is mandatory. Direct SSH/RDP to public IPs is never acceptable in production. This comes up in AZ-104 and AZ-500 exams.

---

### 6.3 VM Backup and Disaster Recovery

**Azure Backup:**
- Agent-based or agentless VM backup
- Stored in Recovery Services Vault
- Supports application-consistent snapshots
- Retention policies: daily, weekly, monthly, yearly

```bash
# Create a Recovery Services Vault
az backup vault create \
  --resource-group az-training-rg \
  --name my-backup-vault \
  --location centralindia

# Enable backup on a VM
az backup protection enable-for-vm \
  --resource-group az-training-rg \
  --vault-name my-backup-vault \
  --vm my-first-vm \
  --policy-name DefaultPolicy

# Trigger an on-demand backup
az backup protection backup-now \
  --resource-group az-training-rg \
  --vault-name my-backup-vault \
  --container-name my-first-vm \
  --item-name my-first-vm \
  --backup-management-type AzureIaasVM
```

**Azure Site Recovery (ASR):**
- Full VM replication to a secondary region
- RPO (Recovery Point Objective): as low as 30 seconds
- RTO (Recovery Time Objective): typically under 30 minutes
- Used for mission-critical workloads requiring regional DR

---

### 6.4 VM Extensions and Custom Script Extension

VM Extensions are small programs that configure and automate tasks on Azure VMs after deployment.

**Common Extensions:**
- **Custom Script Extension:** Run a shell script on the VM after creation
- **Azure Monitor Agent:** Install monitoring agent
- **Azure AD Login:** Login to Linux VMs with Entra ID credentials
- **Disk Encryption:** Enable Azure Disk Encryption (ADE)

```bash
# Install Nginx on a Linux VM using Custom Script Extension
az vm extension set \
  --resource-group vm-lab-rg \
  --vm-name my-first-vm \
  --name customScript \
  --publisher Microsoft.Azure.Extensions \
  --settings '{"commandToExecute": "apt-get update && apt-get install -y nginx"}'
```

---

### 6.5 Practice Questions — Lesson 6

**Q1 — Scenario.** A retail website experiences traffic spikes every Friday evening. The team wants VMs to automatically scale from 2 to 10 instances at 6pm on Fridays and scale back to 2 at midnight. Which scaling approach is best?

- A) Manual scaling with alerts
- B) CPU-based autoscaling
- C) Schedule-based autoscaling
- D) Predictive autoscaling

<details>
<summary>Answer</summary>

**Answer: C — Schedule-based autoscaling**. The traffic pattern is predictable (every Friday 6pm). Schedule-based scaling reacts proactively before the traffic hits, rather than reactively after CPU spikes.

</details>

---

---

## Lesson 7 — Advanced Networking

> **Certification:** AZ-104 Domain 3 + AZ-700
> **Level:** Intermediate

---

### 7.1 Application Security Groups (ASGs)

NSGs work with IP addresses. But in a dynamic cloud environment, IP addresses change when VMs scale. **Application Security Groups** let you group VMs by function (web servers, app servers, databases) and write NSG rules using those groups instead of IPs.

**Without ASGs (IP-based rules):**
```
Allow 10.0.1.4, 10.0.1.5, 10.0.1.6 → 10.0.2.4, 10.0.2.5  on port 8080
# Problem: Every time a VM is added or removed, you update all rules
```

**With ASGs (function-based rules):**
```
Allow WebServers-ASG → AppServers-ASG on port 8080
# VMs join/leave the group; rules never change
```

```bash
# Create Application Security Groups
az network asg create --name WebServers-ASG --resource-group vnet-lab-rg --location centralindia
az network asg create --name AppServers-ASG --resource-group vnet-lab-rg --location centralindia

# Create NSG rule using ASGs
az network nsg rule create \
  --resource-group vnet-lab-rg \
  --nsg-name web-nsg \
  --name Allow-Web-To-App \
  --priority 200 \
  --protocol Tcp \
  --destination-port-range 8080 \
  --source-asgs WebServers-ASG \
  --destination-asgs AppServers-ASG \
  --access Allow
```

---

### 7.2 Azure Load Balancer vs Application Gateway

Two load balancing services — understanding the difference is critical for AZ-104 and AZ-305.

| Feature | Azure Load Balancer | Application Gateway |
|---|---|---|
| **OSI Layer** | Layer 4 (TCP/UDP) | Layer 7 (HTTP/HTTPS) |
| **Routing** | IP + Port based | URL path, hostname, headers |
| **SSL Termination** | No | Yes |
| **WAF** | No | Yes (WAF SKU) |
| **Use Case** | Non-HTTP traffic, any TCP/UDP | Web apps, HTTP/HTTPS |
| **Health Probes** | TCP/HTTP | HTTP/HTTPS |

**When to use which:**
- **Load Balancer:** SQL Server, Redis, any non-HTTP, internal services
- **Application Gateway:** Public-facing web apps, microservices with path-based routing, SSL termination

**Application Gateway URL routing example:**
```
https://myapp.com/api/*    →  API servers backend pool
https://myapp.com/images/* →  Static content servers
https://myapp.com/*        →  General web servers
```

---

### 7.3 Azure DNS

Azure DNS hosts your DNS zones and records using Azure infrastructure.

**Key Concepts:**
- **DNS Zone:** Container for DNS records for a domain (e.g., `company.com`)
- **A Record:** Maps name to IPv4 address
- **CNAME:** Maps name to another name (alias)
- **MX:** Mail exchange record
- **TXT:** Text records (domain verification, SPF)
- **Private DNS Zones:** DNS resolution within a VNet (no public exposure)

```bash
# Create a public DNS zone
az network dns zone create \
  --resource-group az-training-rg \
  --name mycompany.example.com

# Create an A record
az network dns record-set a add-record \
  --resource-group az-training-rg \
  --zone-name mycompany.example.com \
  --record-set-name www \
  --ipv4-address 10.0.1.4

# Create a private DNS zone for VNet resolution
az network private-dns zone create \
  --resource-group az-training-rg \
  --name internal.company.local

# Link private zone to VNet
az network private-dns link vnet create \
  --resource-group az-training-rg \
  --zone-name internal.company.local \
  --name myVNetLink \
  --virtual-network my-vnet \
  --registration-enabled true
```

---

### 7.4 Practice Questions — Lesson 7

**Q1.** A company has a web application and wants to route traffic to different backend pools based on the URL path. `/api` requests go to API servers and `/web` requests go to web servers. Which Azure service should they use?

- A) Azure Load Balancer
- B) Azure Traffic Manager
- C) Application Gateway
- D) Azure Front Door

<details>
<summary>Answer</summary>

**Answer: C — Application Gateway**. URL path-based routing is a Layer 7 feature. Azure Load Balancer operates at Layer 4 and cannot inspect URLs. Application Gateway supports path-based routing natively.

</details>

---

---

## Lesson 8 — Azure App Service

> **Certification:** AZ-204 Domain 1 + AZ-104
> **Level:** Intermediate

---

### 8.1 What is Azure App Service?

App Service is a fully managed PaaS platform for hosting web applications, REST APIs, and mobile backends. You bring your code — Azure handles everything else: OS patching, scaling, load balancing, SSL certificates, and uptime SLAs.

**Supported Runtimes:**
- .NET, .NET Framework
- Node.js
- Python
- Java (SE, Tomcat, JBoss)
- Ruby
- PHP
- Custom containers (Docker)

**The Value Proposition:**
- No VM management
- Auto-scaling built in
- Deployment slots for zero-downtime deployments
- Built-in authentication (Easy Auth)
- Continuous deployment from GitHub, Azure DevOps, Bitbucket

---

### 8.2 App Service Plans — Choosing the Right Tier

Every App Service runs within an App Service Plan, which defines the underlying compute.

| Tier | Use Case | Features | Scaling |
|---|---|---|---|
| **Free (F1)** | Learning only | 60 min/day compute | None |
| **Shared (D1)** | Dev/test | Shared VMs | None |
| **Basic (B1-B3)** | Dev/test, low traffic | Dedicated VMs | Manual only |
| **Standard (S1-S3)** | Production | Auto-scale, staging slots | Up to 10 instances |
| **Premium (P1v3-P3v3)** | High performance production | VNet integration, more RAM | Up to 30 instances |
| **Isolated (I1-I3)** | Regulated, high security | Dedicated VNet, private | Up to 100 instances |

> **Architect Rule:** Standard or above for production. Premium when you need VNet Integration (connecting to private resources). Isolated for PCI-DSS, HIPAA, or other compliance requirements.

---

### 8.3 Deployment Slots — Zero-Downtime Deployments

Deployment slots are live environments within a single App Service. The most common pattern is `staging` and `production`.

**The Blue-Green Deployment Pattern:**
```
Step 1: Deploy new version to STAGING slot
Step 2: Run smoke tests on staging URL
Step 3: Swap staging → production (near-instant, zero downtime)
Step 4: If issues arise, swap back (previous version still in staging)
```

> **Why this matters:** This is the standard zero-downtime deployment pattern used in enterprise Azure. The old version becomes the new staging — instant rollback if something goes wrong.

```bash
# Create an App Service Plan
az appservice plan create \
  --name my-app-plan \
  --resource-group az-training-rg \
  --location centralindia \
  --sku S1 \
  --is-linux

# Create a Web App
az webapp create \
  --resource-group az-training-rg \
  --plan my-app-plan \
  --name my-webapp-$(date +%s) \
  --runtime "NODE:18-lts"

# Create a staging slot
az webapp deployment slot create \
  --name <your-webapp-name> \
  --resource-group az-training-rg \
  --slot staging

# Deploy to staging (example: from local zip)
az webapp deployment source config-zip \
  --resource-group az-training-rg \
  --name <your-webapp-name> \
  --slot staging \
  --src app.zip

# Swap staging to production
az webapp deployment slot swap \
  --resource-group az-training-rg \
  --name <your-webapp-name> \
  --slot staging \
  --target-slot production
```

---

### 8.4 App Service — Key Configuration

**Application Settings (Environment Variables):**
```bash
# Set environment variables for the app
az webapp config appsettings set \
  --resource-group az-training-rg \
  --name <your-webapp-name> \
  --settings \
    DB_CONNECTION_STRING="Server=mydb..." \
    API_KEY="@Microsoft.KeyVault(SecretUri=...)" \
    NODE_ENV="production"
```

> **Security Note:** Never store secrets directly in application settings. Use the `@Microsoft.KeyVault(SecretUri=...)` reference syntax to pull secrets from Key Vault at runtime. The app itself never sees the secret value in plain text.

**VNet Integration:**
Connect App Service to a private VNet to reach private resources (databases, APIs) without exposing them to the internet.

```bash
az webapp vnet-integration add \
  --resource-group az-training-rg \
  --name <your-webapp-name> \
  --vnet my-vnet \
  --subnet app-subnet
```

---

### 8.5 Practice Questions — Lesson 8

**Q1 — Scenario.** A team wants to deploy a new version of their web application with zero downtime and the ability to instantly roll back if issues are found. Which App Service feature enables this?

- A) App Service scaling
- B) Deployment slots with swap
- C) Custom domains
- D) Application Insights

<details>
<summary>Answer</summary>

**Answer: B — Deployment slots with swap**. Deploy to staging, test, swap to production. Rollback = swap back. Zero downtime because the swap is near-instant at the load balancer level.

</details>

---

---

## Lesson 9 — Azure Functions and Serverless

> **Certification:** AZ-204 Domain 2
> **Level:** Intermediate

---

### 9.1 What is Serverless?

**Serverless does not mean no servers.** It means you don't think about, manage, or pay for servers directly. Azure provisions and manages all infrastructure. You pay per execution, not per hour.

**Azure Functions:** Event-driven, serverless compute. You write a function. Azure runs it when triggered.

**When to use Azure Functions:**
- Processing events (blob uploaded, queue message received)
- HTTP APIs with variable/unpredictable traffic
- Scheduled tasks (cron jobs)
- Integrating services in lightweight pipelines
- Real-time data processing

**When NOT to use Azure Functions:**
- Long-running processes (> 10 minutes) — use Azure Container Apps or AKS
- Stateful workflows — use Azure Durable Functions or Logic Apps
- High-compute ML workloads

---

### 9.2 Function Triggers and Bindings

**Triggers** define what causes a Function to run.
**Bindings** are declarative connections to input/output services — no SDK code needed.

| Trigger | When It Fires |
|---|---|
| **HTTP** | On HTTP request (REST API) |
| **Timer** | On a cron schedule |
| **Blob** | When a file is created/modified in storage |
| **Queue** | When a message arrives in a Storage Queue |
| **Service Bus** | When a message arrives in Service Bus |
| **Event Hub** | On streaming events |
| **Cosmos DB** | When documents change (change feed) |

**Function with HTTP trigger and Blob output binding (Python):**
```python
import azure.functions as func
import logging

app = func.FunctionApp(http_auth_level=func.AuthLevel.ANONYMOUS)

@app.route(route="process")
@app.blob_output(arg_name="outputBlob",
                 path="output-container/{rand-guid}.txt",
                 connection="AzureWebJobsStorage")
def process_request(req: func.HttpRequest, outputBlob: func.Out[str]) -> func.HttpResponse:
    data = req.get_json()
    result = f"Processed: {data}"
    outputBlob.set(result)
    return func.HttpResponse(f"Done: {result}", status_code=200)
```

---

### 9.3 Hosting Plans

| Plan | Cold Start | Scaling | Max Duration | Best For |
|---|---|---|---|---|
| **Consumption** | Yes | Automatic, 0→∞ | 10 minutes | Infrequent, unpredictable workloads |
| **Premium** | No (pre-warmed) | Automatic | Unlimited | Production, VNet integration |
| **Dedicated (App Service)** | No | Manual/auto | Unlimited | Predictable workloads, reuse existing plan |

> **Architecture Note:** Use Premium Plan for production functions that need: no cold start, VNet integration, or runtime longer than 10 minutes.

---

### 9.4 Durable Functions — Stateful Serverless

Standard Functions are stateless. **Durable Functions** add orchestration and state management.

**Patterns:**
- **Function Chaining:** Function A → B → C in sequence
- **Fan-out/Fan-in:** Call multiple functions in parallel, aggregate results
- **Async HTTP API:** Long-running operation with polling endpoint
- **Human Interaction:** Wait for approval/input before continuing

```python
# Durable function orchestrator example
import azure.durable_functions as df

def orchestrator_function(context: df.DurableOrchestrationContext):
    # Run three activities in sequence
    result1 = yield context.call_activity('ProcessOrder', 'order-001')
    result2 = yield context.call_activity('ChargePayment', result1)
    result3 = yield context.call_activity('SendConfirmation', result2)
    return result3

main = df.Orchestrator.create(orchestrator_function)
```

---

### 9.5 Practice Questions — Lesson 9

**Q1.** An application needs to process uploaded images automatically whenever a new image is saved to Azure Blob Storage. The workload is unpredictable — sometimes 10 uploads per day, sometimes 10,000. Which is the most cost-effective and appropriate solution?

- A) A VM that polls storage every minute
- B) An Azure Function with a Blob trigger on Consumption plan
- C) An App Service Web Job on Premium plan
- D) An Azure Logic App with manual trigger

<details>
<summary>Answer</summary>

**Answer: B**. Blob trigger fires the function automatically when a blob is created. Consumption plan scales to zero when idle (no cost) and scales to thousands of concurrent executions when needed. Perfect for unpredictable, event-driven workloads.

</details>

---

---

## Lesson 10 — Azure SQL Database and Cosmos DB

> **Certification:** AZ-204 Domain 3 + DP-203
> **Level:** Intermediate

---

### 10.1 Azure SQL Database

A fully managed PaaS relational database based on SQL Server. Microsoft handles patching, backups, high availability, and scaling.

**Deployment Options:**

| Option | Description | Best For |
|---|---|---|
| **Single Database** | One database, dedicated resources | Single application |
| **Elastic Pool** | Multiple databases share resources | Multiple apps with variable usage |
| **Managed Instance** | Near-100% SQL Server compatibility | Migration from on-premises SQL Server |
| **Hyperscale** | Auto-scaling storage, fast scale-out reads | Very large databases (up to 100TB) |

**Service Tiers:**

| Tier | Model | Use Case |
|---|---|---|
| **General Purpose** | vCore-based, remote storage | Most production workloads |
| **Business Critical** | vCore-based, local SSD, in-memory | High I/O, low latency requirements |
| **Hyperscale** | Distributed architecture | 4TB+ databases |

```bash
# Create Azure SQL Server
az sql server create \
  --name mysqlserver-$(date +%s) \
  --resource-group az-training-rg \
  --location centralindia \
  --admin-user sqladmin \
  --admin-password "StrongP@ssword123!"

# Create a database
az sql db create \
  --resource-group az-training-rg \
  --server <your-server-name> \
  --name myappdb \
  --service-objective S1 \
  --backup-storage-redundancy Zone

# Configure firewall (allow Azure services)
az sql server firewall-rule create \
  --resource-group az-training-rg \
  --server <your-server-name> \
  --name AllowAzureServices \
  --start-ip-address 0.0.0.0 \
  --end-ip-address 0.0.0.0
```

---

### 10.2 Azure Cosmos DB

A globally distributed, multi-model NoSQL database. Designed for applications that need:
- Single-digit millisecond response times globally
- Automatic and instant scalability
- Multiple consistency models
- Global distribution with multi-region writes

**APIs Supported:**
- **NoSQL (Core SQL):** JSON documents, SQL-like query syntax — native Cosmos DB
- **MongoDB:** Wire-protocol compatible with MongoDB
- **Cassandra:** Compatible with Apache Cassandra
- **Gremlin:** Graph database API
- **Table:** Azure Table Storage compatible

**Consistency Levels (from strongest to weakest):**

| Level | Guarantee | Latency | Use Case |
|---|---|---|---|
| **Strong** | Always reads latest write | Higher | Financial transactions |
| **Bounded Staleness** | Reads within defined lag | Medium | Leaderboards, social feeds |
| **Session** | Consistent within a session | Low | User-specific data (default) |
| **Consistent Prefix** | Reads never see out-of-order writes | Low | Event sourcing |
| **Eventual** | All replicas converge eventually | Lowest | Likes, view counts |

> **Exam Note:** The default consistency level for Cosmos DB is **Session**. Strong consistency is the only one that guarantees latest write globally. Know these for AZ-204 and DP-203.

---

### 10.3 Practice Questions — Lesson 10

**Q1.** A mobile app stores user profiles that are read frequently from multiple global regions. Low latency is critical, and strong consistency is not required. Which Cosmos DB consistency level is most appropriate?

- A) Strong
- B) Bounded Staleness
- C) Session
- D) Eventual

<details>
<summary>Answer</summary>

**Answer: C — Session** (or D depending on strictness). Session gives consistent reads for the user's own session. Eventual would work for view counts but not user profile data where stale reads could confuse users. Session is the right balance for user data.

</details>

---

---

## Lesson 11 — Azure Monitor and Log Analytics

> **Certification:** AZ-104 Domain 5 + AZ-400
> **Level:** Intermediate

---

### 11.1 Azure Monitor Architecture

Azure Monitor is the umbrella service for all monitoring in Azure. Understanding its architecture is essential for AZ-104, AZ-204, and AZ-400.

```
All Azure Resources
        │
        ▼
   AZURE MONITOR
   ┌─────────────────────────────────────────────────────┐
   │                                                     │
   │  Metrics (numbers over time)  Logs (structured text)│
   │         │                           │               │
   │         ▼                           ▼               │
   │   Metrics Explorer          Log Analytics Workspace │
   │         │                           │               │
   │         └─────────┬─────────────────┘               │
   │                   ▼                                 │
   │               Alerts                               │
   │               Dashboards                           │
   │               Workbooks                            │
   └─────────────────────────────────────────────────────┘
```

**Metrics:** Numerical data over time (CPU %, memory, requests/sec). Stored for 93 days. Fast and lightweight.

**Logs:** Structured events and telemetry. Stored in Log Analytics Workspace. Queried with KQL (Kusto Query Language). Retained up to 2 years by default.

---

### 11.2 Log Analytics and KQL

Log Analytics Workspace is the central store for all log data in Azure. You query it with **KQL (Kusto Query Language)**.

**Essential KQL Queries — Learn These:**

```kql
// Find all Azure VM heartbeats from the last hour
Heartbeat
| where TimeGenerated > ago(1h)
| summarize count() by Computer

// Top 10 errors from App Service logs
AppServiceHTTPLogs
| where TimeGenerated > ago(24h)
| where ScStatus >= 500
| summarize ErrorCount = count() by CsUriStem
| top 10 by ErrorCount

// Azure Activity Log — who deleted what
AzureActivity
| where OperationNameValue contains "delete"
| where ActivityStatusValue == "Success"
| project TimeGenerated, Caller, OperationNameValue, ResourceGroup
| order by TimeGenerated desc

// VM CPU usage over time
Perf
| where ObjectName == "Processor"
| where CounterName == "% Processor Time"
| where TimeGenerated > ago(1h)
| summarize AvgCPU = avg(CounterValue) by Computer, bin(TimeGenerated, 5m)
| render timechart

// Failed logins in the last 24 hours
SecurityEvent
| where EventID == 4625
| where TimeGenerated > ago(24h)
| summarize FailedLogins = count() by Account, Computer
| order by FailedLogins desc
```

---

### 11.3 Alerts

Alerts notify you (or trigger automated actions) when conditions are met.

**Alert Types:**
- **Metric Alert:** CPU > 90% for 5 minutes
- **Log Alert:** Error count > 10 in the last hour (KQL-based)
- **Activity Log Alert:** Resource deleted, policy violated
- **Smart Detection:** Application Insights auto-detects anomalies

**Action Groups:** Define what happens when an alert fires.
- Email, SMS, push notification
- Call a webhook
- Run an Azure Function
- Create an ITSM ticket (PagerDuty, ServiceNow)
- Trigger Logic App

```bash
# Create an action group
az monitor action-group create \
  --resource-group az-training-rg \
  --name CriticalAlerts \
  --short-name CritAlerts \
  --email-receivers \
    name=OpsTeam address=ops@company.com

# Create a metric alert (VM CPU > 90%)
az monitor metrics alert create \
  --name HighCPUAlert \
  --resource-group az-training-rg \
  --scopes /subscriptions/<sub-id>/resourceGroups/vm-lab-rg/providers/Microsoft.Compute/virtualMachines/my-first-vm \
  --condition "avg Percentage CPU > 90" \
  --window-size 5m \
  --evaluation-frequency 1m \
  --action /subscriptions/<sub-id>/resourceGroups/az-training-rg/providers/microsoft.insights/actionGroups/CriticalAlerts
```

---

### 11.4 Application Insights

Application Insights is APM (Application Performance Monitoring) for your applications. Unlike Azure Monitor which monitors infrastructure, Application Insights monitors your application code.

**What it tracks automatically:**
- HTTP request rates and response times
- Dependency calls (database, external APIs)
- Exceptions and stack traces
- Page views and user sessions (client-side)
- Custom events and metrics you define

```bash
# Create Application Insights
az monitor app-insights component create \
  --app my-app-insights \
  --location centralindia \
  --resource-group az-training-rg \
  --application-type web

# Get the Instrumentation Key
az monitor app-insights component show \
  --app my-app-insights \
  --resource-group az-training-rg \
  --query instrumentationKey
```

**Application Map:** Visual diagram of all components and dependencies of your app, with health indicators. Use this to immediately identify which component is causing a problem.

---

### 11.5 Practice Questions — Lesson 11

**Q1.** A DevOps team wants to be automatically notified via SMS when a VM's CPU usage exceeds 95% for more than 5 minutes. Which combination of Azure Monitor components should they configure?

- A) Log Analytics Workspace + KQL query
- B) Metric Alert + Action Group with SMS receiver
- C) Application Insights + Smart Detection
- D) Azure Advisor + Notification

<details>
<summary>Answer</summary>

**Answer: B**. CPU % is a metric (numerical, time-series). Create a Metric Alert with threshold of 95%, window of 5 minutes. Add an Action Group with an SMS receiver. This is the standard pattern.

</details>

---

---

## Lesson 12 — Azure DNS and CDN

> **Certification:** AZ-104 + AZ-700
> **Level:** Intermediate

---

### 12.1 Azure CDN — Content Delivery Network

A CDN caches your content at edge locations close to your users, reducing latency and offloading traffic from your origin server.

**How CDN works:**
```
User in Chennai requests image.jpg
        │
        ▼
CDN Edge Server (nearest — Chennai POP)
   ├── Image in cache? → Serve immediately (< 10ms)
   └── Not cached? → Fetch from origin, cache, serve (< 100ms)
```

**Azure CDN Providers:**

| Provider | Best For |
|---|---|
| **Azure CDN from Microsoft** | Standard use cases, tight Azure integration |
| **Azure Front Door** | Global web apps, API acceleration, WAF |

**Azure Front Door** is the modern recommendation — it combines CDN, global load balancing, WAF, and SSL offloading in one service.

```bash
# Create Azure Front Door profile
az afd profile create \
  --resource-group az-training-rg \
  --profile-name my-front-door \
  --sku Standard_AzureFrontDoor

# Add an origin (your App Service)
az afd origin-group create \
  --resource-group az-training-rg \
  --profile-name my-front-door \
  --origin-group-name myOriginGroup

az afd origin create \
  --resource-group az-training-rg \
  --profile-name my-front-door \
  --origin-group-name myOriginGroup \
  --origin-name myAppServiceOrigin \
  --host-name <your-webapp>.azurewebsites.net \
  --origin-host-header <your-webapp>.azurewebsites.net \
  --http-port 80 \
  --https-port 443
```

---

---

## Lesson 13 — API Management

> **Certification:** AZ-204 Domain 4
> **Level:** Intermediate

---

### 13.1 What is Azure API Management?

API Management (APIM) is a gateway that sits in front of your backend APIs and provides:
- **Security:** Authentication, authorisation, rate limiting
- **Transformation:** Modify requests/responses without changing backend
- **Analytics:** Track usage, latency, errors
- **Developer Portal:** Auto-generated documentation for API consumers
- **Versioning:** Manage multiple API versions simultaneously

**Architecture:**
```
API Consumers (mobile, web, third-party)
              │
              ▼
    API Management Gateway
    ├── Authentication (OAuth, API Key, JWT)
    ├── Rate limiting (100 req/min per user)
    ├── Request transformation
    ├── Caching
    └── Logging → Azure Monitor
              │
              ▼
    Backend APIs (App Service, Functions, AKS)
```

---

### 13.2 APIM Policies — The Core Feature

Policies are XML-based transformations applied to requests and responses. They are APIM's most powerful feature.

**Common Policies:**

```xml
<policies>
  <inbound>
    <!-- Validate JWT token -->
    <validate-jwt header-name="Authorization" failed-validation-httpcode="401">
      <openid-config url="https://login.microsoftonline.com/{tenant}/v2.0/.well-known/openid-configuration"/>
    </validate-jwt>

    <!-- Rate limit: 100 calls per minute per subscription key -->
    <rate-limit-by-key calls="100" renewal-period="60"
                       counter-key="@(context.Subscription.Id)" />

    <!-- Transform request — add header to backend -->
    <set-header name="X-Internal-Request" exists-action="override">
      <value>true</value>
    </set-header>
  </inbound>

  <backend>
    <forward-request />
  </backend>

  <outbound>
    <!-- Remove sensitive headers from response -->
    <set-header name="X-Powered-By" exists-action="delete" />
  </outbound>
</policies>
```

---

### 13.3 Practice Questions — Lesson 13

**Q1 — Scenario.** A company exposes a public REST API used by 50 third-party partners. They need to rate-limit each partner to 500 calls per hour, authenticate via API keys, and track per-partner usage. Which Azure service is designed for this?

- A) Azure Load Balancer
- B) Azure Application Gateway
- C) Azure API Management
- D) Azure Front Door

<details>
<summary>Answer</summary>

**Answer: C — Azure API Management**. APIM is purpose-built for API gateway scenarios — authentication, rate limiting per subscriber, usage analytics, and developer portal. Load Balancer and App Gateway don't handle per-subscriber rate limiting or developer portals.

</details>


---

---

# PHASE 3 — DEVOPS ENGINEER LEVEL
## AZ-400: Azure DevOps Engineer Expert

---

## Lesson 14 — Infrastructure as Code with Terraform

> **Certification:** AZ-400 + Real-world DevOps requirement
> **Level:** DevOps Engineer

---

### 14.1 Why Infrastructure as Code?

**The Problem with Manual Infrastructure:**
- "It works on my machine" — configuration drift between environments
- No history of what changed when and why
- Impossible to reliably recreate environments
- Manual processes are slow and error-prone
- No peer review for infrastructure changes

**Infrastructure as Code (IaC) solves all of this:**
- Infrastructure defined in code files → version controlled in Git
- Same code deploys identical dev, staging, and production environments
- Every change is reviewed via pull request
- Environments can be destroyed and recreated in minutes
- Disaster recovery becomes: `terraform apply`

**Two IaC tools in Azure:**
- **Terraform:** Multi-cloud, most widely used in industry, HCL syntax
- **Bicep/ARM:** Azure-native, Microsoft-supported, tighter Azure integration

> **Career Advice:** Terraform is the industry standard. If you can only learn one, learn Terraform. But know Bicep too — it comes up in AZ-400 exams and some companies prefer it for Azure-only environments.

---

### 14.2 Terraform Fundamentals

**Core Concepts:**

| Concept | Description |
|---|---|
| **Provider** | Plugin that talks to a cloud API (azurerm for Azure) |
| **Resource** | A real infrastructure component to create |
| **Variable** | Input to make configurations reusable |
| **Output** | Values to export after apply |
| **State** | Terraform's record of what it has created |
| **Module** | Reusable group of resources |

**Terraform Workflow:**
```bash
terraform init      # Download providers and modules
terraform plan      # Preview changes (read-only, safe to run anytime)
terraform apply     # Create/update infrastructure
terraform destroy   # Remove all infrastructure
```

---

### 14.3 Terraform with Azure — Complete Example

**Install Terraform:**
```bash
# macOS
brew tap hashicorp/tap && brew install hashicorp/tap/terraform

# Ubuntu
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform

# Verify
terraform -v
```

**Complete Terraform Project — Web App Infrastructure:**

```
project/
├── main.tf           # Main resource definitions
├── variables.tf      # Input variables
├── outputs.tf        # Output values
├── terraform.tfvars  # Variable values (don't commit secrets)
└── backend.tf        # Remote state configuration
```

**main.tf:**
```hcl
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.0"
    }
  }
}

provider "azurerm" {
  features {}
}

# Resource Group
resource "azurerm_resource_group" "main" {
  name     = "${var.project_name}-${var.environment}-rg"
  location = var.location

  tags = {
    Environment = var.environment
    Project     = var.project_name
    ManagedBy   = "Terraform"
  }
}

# Virtual Network
resource "azurerm_virtual_network" "main" {
  name                = "${var.project_name}-vnet"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  address_space       = ["10.0.0.0/16"]

  tags = azurerm_resource_group.main.tags
}

# Web Subnet
resource "azurerm_subnet" "web" {
  name                 = "web-subnet"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = ["10.0.1.0/24"]
}

# App Service Plan
resource "azurerm_service_plan" "main" {
  name                = "${var.project_name}-plan"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  os_type             = "Linux"
  sku_name            = var.app_service_sku

  tags = azurerm_resource_group.main.tags
}

# Web App
resource "azurerm_linux_web_app" "main" {
  name                = "${var.project_name}-${var.environment}-webapp"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  service_plan_id     = azurerm_service_plan.main.id

  site_config {
    application_stack {
      node_version = "18-lts"
    }
    always_on = var.environment == "production" ? true : false
  }

  app_settings = {
    "ENVIRONMENT"         = var.environment
    "APPLICATIONINSIGHTS_CONNECTION_STRING" = azurerm_application_insights.main.connection_string
  }

  tags = azurerm_resource_group.main.tags
}

# Application Insights
resource "azurerm_application_insights" "main" {
  name                = "${var.project_name}-insights"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name
  application_type    = "web"

  tags = azurerm_resource_group.main.tags
}

# Storage Account
resource "azurerm_storage_account" "main" {
  name                     = "${replace(var.project_name, "-", "")}${var.environment}stor"
  resource_group_name      = azurerm_resource_group.main.name
  location                 = azurerm_resource_group.main.location
  account_tier             = "Standard"
  account_replication_type = var.environment == "production" ? "ZRS" : "LRS"

  tags = azurerm_resource_group.main.tags
}
```

**variables.tf:**
```hcl
variable "project_name" {
  description = "Name of the project — used in all resource names"
  type        = string
}

variable "environment" {
  description = "Deployment environment: dev, staging, production"
  type        = string
  validation {
    condition     = contains(["dev", "staging", "production"], var.environment)
    error_message = "Environment must be dev, staging, or production."
  }
}

variable "location" {
  description = "Azure region for all resources"
  type        = string
  default     = "centralindia"
}

variable "app_service_sku" {
  description = "App Service Plan SKU"
  type        = string
  default     = "B1"
}
```

**outputs.tf:**
```hcl
output "resource_group_name" {
  value = azurerm_resource_group.main.name
}

output "web_app_url" {
  value = "https://${azurerm_linux_web_app.main.default_hostname}"
}

output "storage_account_name" {
  value = azurerm_storage_account.main.name
}
```

**terraform.tfvars (dev environment):**
```hcl
project_name    = "myapp"
environment     = "dev"
location        = "centralindia"
app_service_sku = "B1"
```

---

### 14.4 Remote State — Critical for Teams

By default, Terraform state is a local file (`terraform.tfstate`). This breaks when multiple people or CI/CD pipelines run Terraform. Store state remotely in Azure Blob Storage.

**backend.tf:**
```hcl
terraform {
  backend "azurerm" {
    resource_group_name  = "terraform-state-rg"
    storage_account_name = "tfstatemycompany"
    container_name       = "tfstate"
    key                  = "myapp/production/terraform.tfstate"
  }
}
```

```bash
# Create the state storage (one time, before init)
az group create --name terraform-state-rg --location centralindia
az storage account create \
  --name tfstatemycompany \
  --resource-group terraform-state-rg \
  --location centralindia \
  --sku Standard_ZRS

az storage container create \
  --name tfstate \
  --account-name tfstatemycompany

# Now init and apply
terraform init
terraform plan -var-file="terraform.tfvars"
terraform apply -var-file="terraform.tfvars"
```

---

### 14.5 Hands-On Lab — Deploy Azure Infrastructure with Terraform

```bash
# Step 1: Clone or create the project structure
mkdir terraform-azure-lab && cd terraform-azure-lab

# Step 2: Create main.tf, variables.tf, outputs.tf as shown above

# Step 3: Login to Azure
az login

# Step 4: Initialise Terraform
terraform init

# Step 5: Preview what will be created
terraform plan -var="project_name=training" -var="environment=dev"

# Step 6: Apply (type 'yes' to confirm)
terraform apply -var="project_name=training" -var="environment=dev"

# Step 7: Verify in Azure
az webapp list --resource-group training-dev-rg --output table

# Step 8: Destroy when done (saves cost)
terraform destroy -var="project_name=training" -var="environment=dev"
```

---

---

## Lesson 15 — ARM Templates and Bicep

> **Certification:** AZ-104 + AZ-400
> **Level:** DevOps Engineer

---

### 15.1 ARM Templates

Azure Resource Manager (ARM) templates are JSON files that define Azure infrastructure declaratively. They are Azure-native IaC.

**ARM Template Structure:**
```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "webAppName": {
      "type": "string",
      "minLength": 3,
      "metadata": { "description": "Name of the web app" }
    }
  },
  "variables": {
    "appServicePlanName": "[concat(parameters('webAppName'), '-plan')]"
  },
  "resources": [
    {
      "type": "Microsoft.Web/serverfarms",
      "apiVersion": "2022-03-01",
      "name": "[variables('appServicePlanName')]",
      "location": "[resourceGroup().location]",
      "sku": { "name": "S1", "tier": "Standard" },
      "kind": "linux",
      "properties": { "reserved": true }
    },
    {
      "type": "Microsoft.Web/sites",
      "apiVersion": "2022-03-01",
      "name": "[parameters('webAppName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('appServicePlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('appServicePlanName'))]"
      }
    }
  ],
  "outputs": {
    "webAppUrl": {
      "type": "string",
      "value": "[concat('https://', reference(parameters('webAppName')).defaultHostName)]"
    }
  }
}
```

---

### 15.2 Bicep — The Modern ARM Alternative

Bicep is a domain-specific language (DSL) that compiles to ARM templates. It's simpler, more readable, and has better IDE support. Microsoft recommends Bicep over raw ARM templates for new projects.

**The same App Service in Bicep:**
```bicep
param webAppName string
param location string = resourceGroup().location

var appServicePlanName = '${webAppName}-plan'

resource appServicePlan 'Microsoft.Web/serverfarms@2022-03-01' = {
  name: appServicePlanName
  location: location
  sku: {
    name: 'S1'
    tier: 'Standard'
  }
  kind: 'linux'
  properties: {
    reserved: true
  }
}

resource webApp 'Microsoft.Web/sites@2022-03-01' = {
  name: webAppName
  location: location
  properties: {
    serverFarmId: appServicePlan.id
  }
}

output webAppUrl string = 'https://${webApp.properties.defaultHostName}'
```

**Deploy Bicep:**
```bash
# Deploy Bicep template to a resource group
az deployment group create \
  --resource-group az-training-rg \
  --template-file main.bicep \
  --parameters webAppName=my-bicep-webapp

# View deployment output
az deployment group show \
  --resource-group az-training-rg \
  --name main \
  --query properties.outputs
```

---

---

## Lesson 16 — Azure DevOps Pipelines

> **Certification:** AZ-400 Core Domain
> **Level:** DevOps Engineer

---

### 16.1 Azure DevOps Overview

Azure DevOps is Microsoft's end-to-end DevOps platform. It contains five services:

| Service | Purpose |
|---|---|
| **Azure Repos** | Git source control |
| **Azure Pipelines** | CI/CD automation |
| **Azure Boards** | Agile project management (Scrum/Kanban) |
| **Azure Test Plans** | Test management |
| **Azure Artifacts** | Package management (npm, NuGet, Maven) |

> **In practice:** Most companies use Azure Pipelines with GitHub Repos, or all five services together. Azure Pipelines is the most-used and most examined component.

---

### 16.2 Pipeline Fundamentals — YAML Pipelines

Modern Azure Pipelines are defined in YAML files stored in your repo. This means your pipeline is code — version controlled, reviewed, auditable.

**Key Concepts:**

| Concept | Description |
|---|---|
| **Trigger** | What starts the pipeline (push, PR, schedule) |
| **Stage** | Major phase (Build, Test, Deploy-Dev, Deploy-Prod) |
| **Job** | Unit of work within a stage, runs on one agent |
| **Step** | Individual task within a job |
| **Agent** | The machine that runs the job |
| **Artifact** | Output of a build, passed between stages |
| **Environment** | Named deployment target with approvals/checks |

---

### 16.3 Complete CI/CD Pipeline Example

**azure-pipelines.yml — Node.js App to Azure App Service:**

```yaml
trigger:
  branches:
    include:
      - main
      - develop

variables:
  azureSubscription: 'MyAzureServiceConnection'
  webAppName: 'my-production-webapp'
  nodeVersion: '18.x'
  buildConfiguration: 'Release'

stages:
  # ─── STAGE 1: BUILD AND TEST ──────────────────────────────────────
  - stage: Build
    displayName: 'Build and Test'
    jobs:
      - job: BuildJob
        displayName: 'Build Application'
        pool:
          vmImage: 'ubuntu-latest'

        steps:
          - task: NodeTool@0
            displayName: 'Use Node.js $(nodeVersion)'
            inputs:
              versionSpec: $(nodeVersion)

          - script: |
              npm ci
              npm run lint
            displayName: 'Install dependencies and lint'

          - script: |
              npm test -- --coverage --reporters=jest-junit
            displayName: 'Run unit tests'

          - task: PublishTestResults@2
            displayName: 'Publish test results'
            inputs:
              testResultsFormat: 'JUnit'
              testResultsFiles: '**/junit.xml'

          - task: PublishCodeCoverageResults@1
            displayName: 'Publish code coverage'
            inputs:
              codeCoverageTool: 'Cobertura'
              summaryFileLocation: '**/coverage/cobertura-coverage.xml'

          - script: npm run build
            displayName: 'Build application'

          - task: ArchiveFiles@2
            displayName: 'Archive build output'
            inputs:
              rootFolderOrFile: '$(System.DefaultWorkingDirectory)/dist'
              includeRootFolder: false
              archiveFile: '$(Build.ArtifactStagingDirectory)/app.zip'

          - task: PublishBuildArtifacts@1
            displayName: 'Publish artifact'
            inputs:
              PathtoPublish: '$(Build.ArtifactStagingDirectory)'
              ArtifactName: 'drop'

  # ─── STAGE 2: DEPLOY TO DEV ───────────────────────────────────────
  - stage: DeployDev
    displayName: 'Deploy to Development'
    dependsOn: Build
    condition: succeeded()
    variables:
      environmentName: 'dev'
      slotName: 'dev-slot'
    jobs:
      - deployment: DeployToDev
        displayName: 'Deploy to Dev Environment'
        pool:
          vmImage: 'ubuntu-latest'
        environment: 'Development'
        strategy:
          runOnce:
            deploy:
              steps:
                - task: AzureWebApp@1
                  displayName: 'Deploy to Dev App Service'
                  inputs:
                    azureSubscription: $(azureSubscription)
                    appType: 'webAppLinux'
                    appName: $(webAppName)
                    deployToSlotOrASE: true
                    resourceGroupName: 'myapp-dev-rg'
                    slotName: $(slotName)
                    package: '$(Pipeline.Workspace)/drop/app.zip'
                    runtimeStack: 'NODE|18-lts'

  # ─── STAGE 3: DEPLOY TO PRODUCTION ───────────────────────────────
  - stage: DeployProduction
    displayName: 'Deploy to Production'
    dependsOn: DeployDev
    condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/main'))
    jobs:
      - deployment: DeployToProduction
        displayName: 'Deploy to Production'
        pool:
          vmImage: 'ubuntu-latest'
        environment: 'Production'   # This environment has approval gates configured
        strategy:
          runOnce:
            deploy:
              steps:
                - task: AzureWebApp@1
                  displayName: 'Deploy to Staging Slot'
                  inputs:
                    azureSubscription: $(azureSubscription)
                    appType: 'webAppLinux'
                    appName: $(webAppName)
                    deployToSlotOrASE: true
                    resourceGroupName: 'myapp-prod-rg'
                    slotName: 'staging'
                    package: '$(Pipeline.Workspace)/drop/app.zip'

                - task: AzureAppServiceManage@0
                  displayName: 'Swap staging to production'
                  inputs:
                    azureSubscription: $(azureSubscription)
                    Action: 'Swap Slots'
                    WebAppName: $(webAppName)
                    ResourceGroupName: 'myapp-prod-rg'
                    SourceSlot: 'staging'
```

---

### 16.4 Service Connections — Connecting Pipelines to Azure

Pipelines need permission to deploy to Azure. **Service Connections** handle this.

**Create a Service Connection:**
1. Azure DevOps → Project Settings → Service Connections → New
2. Choose "Azure Resource Manager"
3. Choose "Workload Identity Federation" (recommended — no secret management)
4. Select your subscription and resource group
5. Name it (this is your `azureSubscription` variable value)

> **Production Note:** Use Workload Identity Federation (OIDC) instead of Service Principal with client secret. OIDC requires no credentials to rotate — Azure handles the trust relationship automatically.

---

### 16.5 Pipeline Gates and Approvals

Add manual approval gates before deploying to production:

1. Azure DevOps → Environments → Production → Approvals and Checks
2. Add "Approvals" → add approvers (e.g., Lead Engineer, QA Lead)
3. Pipeline will pause before Production stage and wait for approval

**Other gates available:**
- Required number of successful builds
- Work item query (all blocking bugs resolved)
- REST API call (external service health check)
- Business hours gate (only deploy during working hours)

---

---

## Lesson 17 — GitHub Actions with Azure

> **Certification:** AZ-400
> **Level:** DevOps Engineer

---

### 17.1 GitHub Actions for Azure

GitHub Actions is GitHub's CI/CD system. If your code is in GitHub, GitHub Actions is a natural choice for pipelines.

**Key Differences from Azure DevOps Pipelines:**

| Aspect | GitHub Actions | Azure DevOps Pipelines |
|---|---|---|
| **Location** | Code repo (GitHub) | Separate DevOps service |
| **Syntax** | YAML (similar) | YAML (similar) |
| **Marketplace** | GitHub Marketplace | Azure DevOps Marketplace |
| **Authentication** | OIDC to Azure | Service Connections |
| **Best For** | Open source, GitHub-first teams | Enterprise, Microsoft shops |

---

### 17.2 GitHub Actions Workflow — Deploy to Azure

**.github/workflows/deploy.yml:**
```yaml
name: Build and Deploy to Azure

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

env:
  AZURE_WEBAPP_NAME: my-production-webapp
  AZURE_RESOURCE_GROUP: myapp-prod-rg
  NODE_VERSION: '18.x'

jobs:
  build-and-test:
    name: Build and Test
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Use Node.js ${{ env.NODE_VERSION }}
        uses: actions/setup-node@v4
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Run tests
        run: npm test

      - name: Build
        run: npm run build

      - name: Upload artifact
        uses: actions/upload-artifact@v4
        with:
          name: app-build
          path: dist/

  deploy:
    name: Deploy to Azure
    runs-on: ubuntu-latest
    needs: build-and-test
    if: github.ref == 'refs/heads/main'
    environment: production

    permissions:
      id-token: write   # Required for OIDC
      contents: read

    steps:
      - name: Download artifact
        uses: actions/download-artifact@v4
        with:
          name: app-build
          path: dist/

      - name: Azure Login (OIDC — no secrets!)
        uses: azure/login@v2
        with:
          client-id: ${{ secrets.AZURE_CLIENT_ID }}
          tenant-id: ${{ secrets.AZURE_TENANT_ID }}
          subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}

      - name: Deploy to Azure Web App
        uses: azure/webapps-deploy@v3
        with:
          app-name: ${{ env.AZURE_WEBAPP_NAME }}
          slot-name: staging
          package: dist/

      - name: Swap staging to production
        run: |
          az webapp deployment slot swap \
            --name ${{ env.AZURE_WEBAPP_NAME }} \
            --resource-group ${{ env.AZURE_RESOURCE_GROUP }} \
            --slot staging \
            --target-slot production
```

**Set up OIDC authentication (no secrets needed):**
```bash
# Create app registration for GitHub Actions
az ad app create --display-name "github-actions-myapp"

# Get the app ID
APP_ID=$(az ad app list --display-name "github-actions-myapp" --query "[0].appId" -o tsv)

# Create service principal
az ad sp create --id $APP_ID

# Add federated credential for GitHub OIDC
az ad app federated-credential create \
  --id $APP_ID \
  --parameters '{
    "name": "github-main",
    "issuer": "https://token.actions.githubusercontent.com",
    "subject": "repo:your-org/your-repo:ref:refs/heads/main",
    "audiences": ["api://AzureADTokenExchange"]
  }'

# Assign Contributor role to service principal
SP_OBJECT_ID=$(az ad sp show --id $APP_ID --query id -o tsv)
az role assignment create \
  --assignee-object-id $SP_OBJECT_ID \
  --role Contributor \
  --scope /subscriptions/<your-sub-id>/resourceGroups/myapp-prod-rg
```

---

---

## Lesson 18 — Azure Container Registry and Docker

> **Certification:** AZ-204 + AZ-400
> **Level:** DevOps Engineer

---

### 18.1 Docker Fundamentals (Quick Review)

```dockerfile
# Example Dockerfile for a Node.js API
FROM node:18-alpine

WORKDIR /app

# Copy package files first (layer caching optimisation)
COPY package*.json ./
RUN npm ci --only=production

# Copy application code
COPY . .

# Run as non-root user (security best practice)
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001
USER nodejs

EXPOSE 3000

CMD ["node", "server.js"]
```

```bash
# Build and tag the image
docker build -t myapp:v1.0 .

# Run locally
docker run -p 3000:3000 myapp:v1.0

# Test
curl http://localhost:3000/health
```

---

### 18.2 Azure Container Registry (ACR)

ACR is a private Docker registry in Azure. Store your container images securely, close to your deployments.

**Why use ACR instead of Docker Hub:**
- Private — your images are not public
- Geographically close to Azure deployments (faster pulls)
- Integrated with Entra ID and RBAC
- Geo-replication available for global deployments
- Image scanning (Azure Defender for Containers)

```bash
# Create a Container Registry
az acr create \
  --resource-group az-training-rg \
  --name mycompanyacr \
  --sku Standard \
  --location centralindia

# Login to ACR
az acr login --name mycompanyacr

# Build and push using ACR Tasks (builds in the cloud, no local Docker needed)
az acr build \
  --registry mycompanyacr \
  --image myapp:v1.0 \
  --file Dockerfile \
  .

# List images in the registry
az acr repository list --name mycompanyacr --output table

# List tags for an image
az acr repository show-tags \
  --name mycompanyacr \
  --repository myapp \
  --output table
```

---

---

## Lesson 19 — Azure Kubernetes Service (AKS)

> **Certification:** AZ-204 + AZ-400 + real-world senior requirement
> **Level:** Senior DevOps Engineer

---

### 19.1 Why Kubernetes?

**The Container Orchestration Problem:**
- You have 20 microservices, each in a Docker container
- You need to deploy 100 instances across multiple VMs
- When one crashes, it must restart automatically
- When traffic spikes, you need more instances
- How do services find and talk to each other?
- How do you roll out updates without downtime?

**Kubernetes solves all of this.** It's the de facto standard for container orchestration.

**AKS = Azure Kubernetes Service:** Microsoft manages the control plane (master nodes). You manage the worker nodes (or use managed node pools). This removes the complexity of setting up and maintaining Kubernetes itself.

---

### 19.2 Kubernetes Core Concepts

| Concept | Description |
|---|---|
| **Pod** | Smallest unit. One or more containers. Shares network/storage. |
| **Deployment** | Manages a set of identical Pods. Handles rolling updates and rollbacks. |
| **Service** | Stable network endpoint to access Pods (Pods have changing IPs). |
| **Ingress** | HTTP/HTTPS routing from outside the cluster to Services. |
| **ConfigMap** | Non-secret configuration data injected into Pods. |
| **Secret** | Sensitive configuration (passwords, keys) injected into Pods. |
| **Namespace** | Virtual cluster within a cluster. Isolate teams or environments. |
| **Node Pool** | Group of identical VMs (nodes) in the cluster. |
| **HPA** | Horizontal Pod Autoscaler. Scale Pod count based on CPU/custom metrics. |

---

### 19.3 Create an AKS Cluster

```bash
# Step 1: Create resource group
az group create --name aks-lab-rg --location centralindia

# Step 2: Create AKS cluster
az aks create \
  --resource-group aks-lab-rg \
  --name my-aks-cluster \
  --node-count 2 \
  --node-vm-size Standard_B2s \
  --enable-managed-identity \
  --network-plugin azure \
  --generate-ssh-keys

# Step 3: Connect kubectl to the cluster
az aks get-credentials \
  --resource-group aks-lab-rg \
  --name my-aks-cluster

# Verify connection
kubectl get nodes
```

---

### 19.4 Deploy an Application to AKS

**deployment.yaml:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  namespace: default
  labels:
    app: myapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0       # Zero-downtime rolling update
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: myapp
          image: mycompanyacr.azurecr.io/myapp:v1.0
          ports:
            - containerPort: 3000
          resources:
            requests:
              memory: "128Mi"
              cpu: "100m"
            limits:
              memory: "256Mi"
              cpu: "500m"
          readinessProbe:
            httpGet:
              path: /health
              port: 3000
            initialDelaySeconds: 10
            periodSeconds: 5
          env:
            - name: DB_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: myapp-secrets
                  key: db-password
---
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
  type: ClusterIP
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myapp-ingress
  annotations:
    kubernetes.io/ingress.class: azure/application-gateway
spec:
  rules:
    - host: myapp.company.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: myapp-service
                port:
                  number: 80
```

```bash
# Deploy the application
kubectl apply -f deployment.yaml

# Watch the rollout
kubectl rollout status deployment/myapp

# List pods
kubectl get pods -o wide

# Check logs of a pod
kubectl logs -f deployment/myapp

# Scale manually
kubectl scale deployment myapp --replicas=5

# Rollback if something goes wrong
kubectl rollout undo deployment/myapp

# Clean up
az group delete --name aks-lab-rg --yes --no-wait
```

---

### 19.5 Horizontal Pod Autoscaler

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: myapp-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: myapp
  minReplicas: 2
  maxReplicas: 20
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70
```

```bash
kubectl apply -f hpa.yaml
kubectl get hpa
```

---

---

## Lesson 20 — Azure Container Apps

> **Certification:** AZ-204
> **Level:** DevOps Engineer

---

### 20.1 Container Apps vs AKS

**Azure Container Apps** is a managed serverless container service. AKS gives you full Kubernetes control — Container Apps abstracts Kubernetes away.

| Feature | Container Apps | AKS |
|---|---|---|
| Kubernetes knowledge needed | No | Yes |
| Scale to zero | Yes | Not by default |
| Control plane management | None (Microsoft) | Partial (Microsoft manages control plane) |
| Custom Kubernetes resources | No | Yes |
| Best for | Microservices, event-driven, APIs | Complex workloads needing full K8s |

**Use Container Apps when:**
- You want containers without Kubernetes complexity
- Your app needs to scale to zero (cost saving)
- Event-driven scaling (KEDA rules built-in)

**Use AKS when:**
- You need full Kubernetes capabilities
- You have existing Kubernetes workloads
- Your team has Kubernetes expertise

```bash
# Create Container Apps environment
az containerapp env create \
  --name my-containerapp-env \
  --resource-group az-training-rg \
  --location centralindia

# Deploy a container app
az containerapp create \
  --name myapi \
  --resource-group az-training-rg \
  --environment my-containerapp-env \
  --image mcr.microsoft.com/azuredocs/containerapps-helloworld:latest \
  --target-port 80 \
  --ingress external \
  --min-replicas 0 \
  --max-replicas 10 \
  --cpu 0.5 \
  --memory 1.0Gi

# Get the URL
az containerapp show \
  --name myapi \
  --resource-group az-training-rg \
  --query properties.configuration.ingress.fqdn \
  --output tsv
```

---

---

## Lesson 21 — Azure Key Vault and Secrets Management

> **Certification:** AZ-204 + AZ-500 + AZ-400
> **Level:** DevOps Engineer

---

### 21.1 What is Azure Key Vault?

Key Vault is Azure's managed secrets, keys, and certificates service. It solves the #1 security problem in cloud: where do you store passwords, connection strings, and API keys?

**What Key Vault stores:**
- **Secrets:** Passwords, connection strings, API keys, any text secret
- **Keys:** Cryptographic keys for encryption (RSA, EC) — HSM-backed available
- **Certificates:** SSL/TLS certificates with automatic renewal

**Why Key Vault:**
- Centralised secret management — no secrets in code or config files
- Access controlled via RBAC or Key Vault access policies
- Full audit log of who accessed which secret and when
- Automatic certificate renewal
- Software or HSM-backed key protection

---

### 21.2 Key Vault Setup and Usage

```bash
# Create a Key Vault
az keyvault create \
  --name mycompany-kv-$(date +%s) \
  --resource-group az-training-rg \
  --location centralindia \
  --sku standard \
  --enable-rbac-authorization true   # Use RBAC, not legacy access policies

# Add a secret
az keyvault secret set \
  --vault-name <your-kv-name> \
  --name DatabaseConnectionString \
  --value "Server=mydbserver;Database=mydb;User=admin;Password=secret123;"

# Retrieve a secret
az keyvault secret show \
  --vault-name <your-kv-name> \
  --name DatabaseConnectionString \
  --query value \
  --output tsv

# Grant an App Service access to Key Vault
# (using system-assigned managed identity)

# 1. Get the app's principal ID
PRINCIPAL_ID=$(az webapp identity show \
  --name <your-webapp-name> \
  --resource-group az-training-rg \
  --query principalId \
  --output tsv)

# 2. Grant Key Vault Secrets User role
az role assignment create \
  --assignee $PRINCIPAL_ID \
  --role "Key Vault Secrets User" \
  --scope /subscriptions/<sub-id>/resourceGroups/az-training-rg/providers/Microsoft.KeyVault/vaults/<your-kv-name>
```

**Reference Key Vault secrets in App Service:**
```bash
# In App Service application settings, reference KV secret
az webapp config appsettings set \
  --resource-group az-training-rg \
  --name <your-webapp-name> \
  --settings \
  "DB_CONNECTION=@Microsoft.KeyVault(VaultName=<your-kv-name>;SecretName=DatabaseConnectionString)"
```

> **The pattern:** App has Managed Identity → Identity has "Key Vault Secrets User" role → App references secret via `@Microsoft.KeyVault(...)` → Azure resolves it at runtime. No credentials in code, no credentials in config. This is the gold standard for secrets management in Azure.

---

### 21.3 Key Vault in Pipelines

```yaml
# Azure DevOps pipeline — read Key Vault secrets
- task: AzureKeyVault@2
  displayName: 'Read secrets from Key Vault'
  inputs:
    azureSubscription: 'MyAzureServiceConnection'
    KeyVaultName: 'mycompany-kv'
    SecretsFilter: 'DatabasePassword,ApiKey,StorageConnectionString'
    RunAsPreJob: true

# Now use the secrets as pipeline variables
- script: |
    echo "Deploying with database connection..."
    # $(DatabasePassword) is now available as a masked variable
  displayName: 'Use secret in pipeline step'
```


---

---

# PHASE 4 — ARCHITECT LEVEL
## AZ-305: Azure Solutions Architect Expert

---

## Lesson 22 — Designing Highly Available Architectures

> **Certification:** AZ-305 Core Domain
> **Level:** Senior Architect

---

### 22.1 The Reliability Pillars

The **Microsoft Well-Architected Framework (WAF)** defines five pillars:
1. **Reliability** — Recovers from failures, meets availability targets
2. **Security** — Protects against threats
3. **Cost Optimisation** — Eliminates waste, maximises value
4. **Operational Excellence** — Runs and monitors effectively
5. **Performance Efficiency** — Scales efficiently to meet demand

For high availability, **Reliability** is the foundation.

---

### 22.2 SLA Composition — The Maths of Reliability

**The Composite SLA Rule:** When services run in sequence (A depends on B depends on C), you multiply the SLAs.

**Example — Three-tier app:**
```
App Service SLA:    99.95%
SQL Database SLA:   99.99%
Storage SLA:        99.9%

Composite SLA = 0.9995 × 0.9999 × 0.999 = 99.84%
```

That means ~13 hours of potential downtime per year.

**To improve composite SLA — use redundancy:**
```
Two App Services (different AZs):
1 - (1 - 0.9995) × (1 - 0.9995) = 99.9999975%

Combined with SQL and Storage: ~99.99%
```

> **Architect Rule:** Always calculate composite SLA when designing a solution. Understand the weakest link. Add redundancy at the components that reduce the composite SLA the most.

---

### 22.3 High Availability Architecture Patterns

**Pattern 1 — Three-Tier Web App (Standard Production):**
```
                    ┌──────────────────┐
Internet Traffic    │  Azure Front Door │  (Global load balancing + WAF + CDN)
                    └────────┬─────────┘
                             │
                    ┌────────▼─────────┐
                    │  App Service     │  (Zone-redundant, auto-scale)
                    │  Premium P2v3    │
                    └────────┬─────────┘
                             │
               ┌─────────────▼──────────────┐
               │  Private VNet              │
               │  ┌──────────┐              │
               │  │ App Layer│  (AKS or     │
               │  │ Services │   Containers)│
               │  └────┬─────┘              │
               │       │                    │
               │  ┌────▼─────────────────┐  │
               │  │  Azure SQL Database  │  │
               │  │  Business Critical   │  │
               │  │  (Zone redundant)    │  │
               │  └──────────────────────┘  │
               └────────────────────────────┘
```

**Pattern 2 — Availability Zone Spread:**
```
Region: Central India
  ├── Zone 1: 2 VMs + Primary DB
  ├── Zone 2: 2 VMs + Secondary DB (sync replica)
  └── Zone 3: 2 VMs + Read replica
  
Load Balancer distributes across all zones.
If any zone fails: remaining 4 VMs handle all traffic.
SLA: 99.99%
```

---

### 22.4 Health Probes and Circuit Breakers

**Health Probes:** Load balancers continuously check if backends are healthy. Failed backends are automatically removed from rotation.

```bash
# Configure health probe on Application Gateway
az network application-gateway probe create \
  --resource-group az-training-rg \
  --gateway-name myAppGateway \
  --name healthcheck \
  --protocol Http \
  --host-name-from-http-settings true \
  --path /health \
  --interval 30 \
  --threshold 3 \
  --timeout 30
```

**Azure Health Check (App Service):**
```bash
# Enable health check — automatically removes unhealthy instances
az webapp config set \
  --resource-group az-training-rg \
  --name <your-webapp-name> \
  --generic-configurations '{"healthCheckPath": "/health"}'
```

---

---

## Lesson 23 — Multi-Region Deployment and Disaster Recovery

> **Certification:** AZ-305
> **Level:** Senior Architect

---

### 23.1 RTO and RPO — The DR Language

Before designing DR, define your targets:

| Term | Definition | Example |
|---|---|---|
| **RPO** | Recovery Point Objective — maximum data loss acceptable | "We can lose at most 5 minutes of data" |
| **RTO** | Recovery Time Objective — maximum downtime acceptable | "We must be back online within 30 minutes" |

**The lower RPO/RTO, the higher the cost.** Design to the actual business requirement, not to theoretical perfection.

| RPO | RTO | Strategy | Typical Cost |
|---|---|---|---|
| Hours | Hours | Backup and restore | Low |
| Minutes | < 1 hour | Warm standby | Medium |
| Seconds | < 15 min | Hot standby (active-passive) | High |
| Zero | Zero | Active-active multi-region | Very High |

---

### 23.2 Azure Traffic Manager vs Azure Front Door

Both provide global routing. Know the difference.

| Feature | Traffic Manager | Azure Front Door |
|---|---|---|
| **Protocol** | DNS-based (Layer 7 DNS) | HTTP/HTTPS (Layer 7) |
| **Routing** | DNS-level | Actual HTTP routing with caching |
| **SSL Termination** | No | Yes |
| **WAF** | No | Yes |
| **Caching/CDN** | No | Yes |
| **Best For** | Non-HTTP, global DNS routing | Web apps needing CDN + WAF + routing |

**Traffic Manager Routing Methods:**
- **Priority:** Primary region active, secondary on failover
- **Weighted:** Split traffic 80/20 between regions (testing)
- **Performance:** Route to lowest-latency region for each user
- **Geographic:** Route based on user's country/continent

---

### 23.3 Active-Active Multi-Region Architecture

```
Users in India                    Users in Europe
      │                                  │
      ▼                                  ▼
Azure Front Door (Performance Routing — sends each user to nearest region)
      │                                  │
      ▼                                  ▼
Central India Region           West Europe Region
├── App Service (P2v3)         ├── App Service (P2v3)
├── Redis Cache                ├── Redis Cache
└── Cosmos DB (Write Region)   └── Cosmos DB (Write Region)
           │                              │
           └──────── Cosmos DB ───────────┘
                   Multi-region sync
                   (both regions write)
```

> **Key Insight:** Cosmos DB with multi-region writes is the enabler of true active-active. SQL Database with geo-replication only supports active-passive (one write region). For active-active at global scale, Cosmos DB is the right choice.

---

### 23.4 Azure Site Recovery Configuration

```bash
# Create Recovery Services Vault in secondary region
az backup vault create \
  --resource-group dr-rg \
  --name site-recovery-vault \
  --location southindia   # Paired region for Central India

# ASR is configured through the Portal or PowerShell
# The key configurations are:
# 1. Source Region: Central India
# 2. Target Region: South India
# 3. Cache Storage Account: Central India (temporary during replication)
# 4. Target Resource Group: dr-rg
# 5. Target VNet: dr-vnet (mirroring production VNet)
# 6. Replication policy: RPO 30 seconds, app-consistent snapshot every hour
```

---

---

## Lesson 24 — Hybrid Cloud with Azure Arc

> **Certification:** AZ-305 + AZ-104
> **Level:** Senior Architect

---

### 24.1 What is Azure Arc?

Azure Arc extends Azure management to resources outside Azure — your on-premises servers, other clouds (AWS, GCP), and edge locations.

**What you can Arc-enable:**
- On-premises Windows and Linux servers
- Kubernetes clusters (anywhere — on-prem, AWS, GCP)
- SQL Server instances on-premises
- VMware vSphere VMs
- Azure Stack HCI

**What you get once Arc-enabled:**
- Manage everything through Azure Portal
- Apply Azure Policy to on-premises servers
- Use Azure Monitor and Log Analytics
- Deploy Azure services (App Service, Functions, Data) to on-premises clusters
- Azure Defender protection for on-premises workloads

---

### 24.2 Arc Architecture

```
On-premises Data Centre
├── Arc Agent (installed on each server)
│     └── Connects outbound to Azure over HTTPS 443
│
└── Connected to Azure →

Azure Portal
├── Shows on-premises servers alongside Azure VMs
├── Azure Policy applied to Arc servers
├── Azure Monitor collecting metrics/logs
└── Azure Defender protecting all resources
```

```bash
# Generate onboarding script for a Linux server
az connectedmachine connect \
  --resource-group hybrid-rg \
  --name my-onprem-server \
  --location centralindia \
  --subscription <sub-id>

# The above generates a script to run on the on-premises server
# Once connected, the server appears in Azure Portal

# List all Arc-connected machines
az connectedmachine list --resource-group hybrid-rg --output table

# Assign a policy to Arc machines
az policy assignment create \
  --name "Audit-OS-Updates" \
  --policy "/providers/Microsoft.Authorization/policyDefinitions/<policy-id>" \
  --scope /subscriptions/<sub-id>/resourceGroups/hybrid-rg
```

---

---

## Lesson 25 — VNet Peering and Azure Private Link

> **Certification:** AZ-305 + AZ-700
> **Level:** Senior Architect

---

### 25.1 VNet Peering

VNet Peering connects two VNets so resources in each can communicate as if they were on the same network. Traffic stays on Microsoft's backbone — never traverses the internet.

**Types:**
- **Regional Peering:** Both VNets in the same region
- **Global Peering:** VNets in different regions

**Key Properties:**
- Non-transitive by default (A peers B, B peers C — A cannot reach C through B)
- Low latency, high bandwidth
- No encryption overhead (traffic on Microsoft backbone)
- Can peer across subscriptions

```bash
# Create two VNets
az network vnet create \
  --name vnet-hub \
  --resource-group peering-rg \
  --location centralindia \
  --address-prefix 10.0.0.0/16

az network vnet create \
  --name vnet-spoke \
  --resource-group peering-rg \
  --location centralindia \
  --address-prefix 10.1.0.0/16

# Get VNet IDs
HUB_ID=$(az network vnet show --name vnet-hub --resource-group peering-rg --query id -o tsv)
SPOKE_ID=$(az network vnet show --name vnet-spoke --resource-group peering-rg --query id -o tsv)

# Create peering from hub to spoke
az network vnet peering create \
  --name hub-to-spoke \
  --resource-group peering-rg \
  --vnet-name vnet-hub \
  --remote-vnet $SPOKE_ID \
  --allow-vnet-access true

# Create peering from spoke to hub (must be bidirectional)
az network vnet peering create \
  --name spoke-to-hub \
  --resource-group peering-rg \
  --vnet-name vnet-spoke \
  --remote-vnet $HUB_ID \
  --allow-vnet-access true
```

---

### 25.2 Hub-and-Spoke Network Topology

The most common enterprise Azure network architecture.

```
           ┌─────────────────────────────────┐
           │         HUB VNet                │
           │  ├── Azure Firewall             │
           │  ├── VPN Gateway / ExpressRoute │
           │  ├── Azure Bastion             │
           │  └── DNS Servers               │
           └────┬──────────────────┬────────┘
                │    Peering       │
        ┌───────▼──────┐   ┌───────▼──────┐
        │  Spoke 1     │   │  Spoke 2     │
        │  (App team)  │   │  (Data team) │
        │  10.1.0.0/16 │   │  10.2.0.0/16 │
        └──────────────┘   └──────────────┘
```

**Why Hub-and-Spoke:**
- Centralised security (Firewall, Bastion, VPN in hub)
- Shared services in hub (DNS, monitoring)
- Spoke teams manage their own VNets independently
- Enforced traffic inspection via hub firewall
- Scales to hundreds of spoke VNets

---

### 25.3 Azure Private Link

Private Link enables you to access Azure PaaS services (Storage, SQL, Cosmos DB) via a **private IP in your VNet** instead of over the public internet.

```
Without Private Link:
Your VM (10.0.1.4) → Internet → storage.blob.core.windows.net (public IP)

With Private Link:
Your VM (10.0.1.4) → Private endpoint (10.0.1.100) → Azure Storage (private, same VNet)
```

**Use Cases:**
- Database servers accessible only from within VNet
- Key Vault accessible only from App Service's VNet
- Storage accounts with no public access

```bash
# Create a private endpoint for Azure SQL
az network private-endpoint create \
  --name sql-private-endpoint \
  --resource-group az-training-rg \
  --vnet-name my-vnet \
  --subnet data-subnet \
  --private-connection-resource-id /subscriptions/<sub-id>/resourceGroups/az-training-rg/providers/Microsoft.Sql/servers/<sql-server-name> \
  --group-ids sqlServer \
  --connection-name sql-private-connection

# Disable public access on the SQL server
az sql server update \
  --name <sql-server-name> \
  --resource-group az-training-rg \
  --enable-public-network false
```

---

---

## Lesson 26 — Cost Optimisation Strategies

> **Certification:** AZ-305 + Well-Architected Framework
> **Level:** Architect

---

### 26.1 Azure Pricing Models

| Model | Description | Best For |
|---|---|---|
| **Pay-as-you-go** | Per-second/hour billing, no commitment | Dev/test, unpredictable workloads |
| **Reserved Instances** | 1 or 3 year commitment, up to 72% savings | Stable production workloads |
| **Spot VMs** | Unused capacity, up to 90% savings, can be evicted | Batch processing, fault-tolerant workloads |
| **Azure Hybrid Benefit** | Reuse existing Windows/SQL Server licenses | Companies migrating from on-premises |
| **Dev/Test Pricing** | Discounted rates for non-production | Development and test environments |

---

### 26.2 Cost Optimisation by Service

**Virtual Machines:**
- Right-size: Use Azure Advisor recommendations — it identifies over-provisioned VMs
- Stop/deallocate non-production VMs overnight and weekends (saves ~60%)
- Use Reserved Instances for VMs running > 8 months/year
- Use B-series burstable VMs for workloads with variable CPU (web servers, CI agents)
- Spot VMs for batch jobs, rendering, CI/CD agents

**Storage:**
- Implement Lifecycle Management (auto-tier to Cool and Archive)
- Delete unattached managed disks (orphaned after VM deletion)
- Use the right redundancy tier (LRS for dev, ZRS for production, GRS only when required)

**Networking:**
- Egress costs money — data leaving Azure is charged
- Keep services in the same region to avoid inter-region egress
- Use CDN/Front Door to serve content from edge (reduces egress from origin)

```bash
# Azure Advisor: get cost recommendations
az advisor recommendation list \
  --category Cost \
  --output table

# Find unattached managed disks (easy cost saving)
az disk list \
  --query "[?diskState=='Unattached'].{Name:name, Size:diskSizeGb, RG:resourceGroup}" \
  --output table

# Find stopped (not deallocated) VMs (still charged for compute)
az vm list \
  --show-details \
  --query "[?powerState=='VM stopped'].{Name:name, State:powerState, RG:resourceGroup}" \
  --output table
```

---

### 26.3 Azure Cost Management

```bash
# View current month spend by resource group
az consumption usage list \
  --billing-period-name <period> \
  --query "[].{Service:consumedService, Cost:pretaxCost, Resource:instanceName}" \
  --output table

# Set a budget alert (notify when spend reaches 80% of £1000/month)
az consumption budget create \
  --budget-name MonthlyBudget \
  --amount 1000 \
  --time-grain Monthly \
  --category Cost \
  --notification-threshold 80 \
  --contact-emails ops@company.com
```

---

---

## Lesson 27 — Performance and Scalability Architecture

> **Certification:** AZ-305 + Well-Architected Framework
> **Level:** Architect

---

### 27.1 Caching Strategies

**Azure Cache for Redis** is the primary caching solution in Azure.

**Where to cache:**
- Session state (user login sessions)
- Database query results (expensive, frequently read)
- API responses (external API calls)
- Computed results (dashboards, reports)

**Cache-Aside Pattern (most common):**
```python
def get_user(user_id):
    # 1. Check cache first
    cached = redis_client.get(f"user:{user_id}")
    if cached:
        return json.loads(cached)

    # 2. Cache miss — fetch from database
    user = db.query("SELECT * FROM users WHERE id = ?", user_id)

    # 3. Store in cache with 1 hour TTL
    redis_client.setex(f"user:{user_id}", 3600, json.dumps(user))

    return user
```

```bash
# Create Azure Cache for Redis
az redis create \
  --name mycompany-redis \
  --resource-group az-training-rg \
  --location centralindia \
  --sku Standard \
  --vm-size c1
```

---

### 27.2 Asynchronous Architecture — Message Queues

**The Problem with Synchronous Architecture:**
```
User uploads video → App immediately calls video processor → 
Processor takes 5 minutes → User's HTTP request times out
```

**The Async Solution:**
```
User uploads video → App puts message in queue → Returns 202 Accepted
                                                         │
                               Worker service picks up message
                               Processes video (5 minutes)
                               Updates database when done
                               User polls or gets notification
```

**Azure Queue Services:**

| Service | Use Case | Message Size | Retention |
|---|---|---|---|
| **Storage Queue** | Simple, lightweight queuing | 64KB | 7 days max |
| **Service Bus Queue** | Enterprise messaging, ordering, sessions | 256KB-1MB | 14 days |
| **Service Bus Topic** | Pub/sub, multiple subscribers | 256KB-1MB | 14 days |
| **Event Grid** | Event-driven, reactive architecture | 1MB | 24 hours |
| **Event Hub** | High-throughput streaming, IoT, analytics | 1MB | 7-90 days |

---

---

# PHASE 5 — EXPERT AND SPECIALTY LEVEL
## AZ-500 · AZ-700 · DP-203 · AI-102

---

## Lesson 28 — Azure Security Architecture

> **Certification:** AZ-500: Azure Security Engineer
> **Level:** Security Expert

---

### 28.1 Defence in Depth

Azure security is implemented in layers. No single layer is sufficient — every layer adds protection.

```
Layer 1: Physical security     (Microsoft's responsibility — data centre access)
Layer 2: Identity & Access     (Entra ID, MFA, Conditional Access, PIM)
Layer 3: Perimeter             (DDoS Protection, Azure Firewall, WAF)
Layer 4: Network               (VNet, NSG, Private Link, no public exposure)
Layer 5: Compute               (VM patches, Defender for Cloud, Bastion)
Layer 6: Application           (Key Vault, secure coding, input validation)
Layer 7: Data                  (Encryption at rest, in transit, Key Vault)
```

---

### 28.2 Microsoft Defender for Cloud

Defender for Cloud is the unified security management platform. It gives you:
- **Secure Score:** Overall security health rating (0–100%)
- **Recommendations:** Specific actions to improve security
- **Alerts:** Active threat detection
- **Compliance:** Dashboard against standards (ISO 27001, SOC 2, PCI-DSS)

```bash
# Enable Defender for Cloud on subscription
az security pricing create \
  --name VirtualMachines \
  --tier Standard

az security pricing create \
  --name SqlServers \
  --tier Standard

az security pricing create \
  --name StorageAccounts \
  --tier Standard

# Get your Secure Score
az security secure-score list --output table

# Get security recommendations
az security assessment list \
  --query "[?status.code=='Unhealthy'].{Name:displayName, Severity:metadata.severity}" \
  --output table
```

---

### 28.3 Azure Policy and Governance

**Azure Policy** enforces organisational standards and assesses compliance. It runs continuously and evaluates resources as they are created or changed.

**Policy Effects:**
| Effect | What Happens |
|---|---|
| **Deny** | Block resource creation if it violates policy |
| **Audit** | Allow creation, but log a non-compliance warning |
| **Append** | Automatically add required fields to resources |
| **Modify** | Automatically change properties during creation |
| **DeployIfNotExists** | Deploy required companion resource if missing |

**Common Policy Examples:**
```bash
# Deny creating resources outside allowed regions
az policy assignment create \
  --name "Allow-India-Regions-Only" \
  --policy "/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4f" \
  --params '{"listOfAllowedLocations": {"value": ["centralindia", "southindia", "westindia"]}}'

# Require tags on all resources
az policy assignment create \
  --name "Require-Environment-Tag" \
  --policy "/providers/Microsoft.Authorization/policyDefinitions/96670d01-0a4d-4649-9c89-2d3abc0a5025"

# Audit SQL Servers without Azure AD authentication
az policy assignment create \
  --name "Audit-SQL-AAD-Admin" \
  --policy "/providers/Microsoft.Authorization/policyDefinitions/1f314764-cb73-4fc9-b863-8eca98ac36e9"
```

---

### 28.4 Privileged Identity Management (PIM)

PIM provides **just-in-time (JIT) privileged access** to Azure resources. Instead of permanently having Owner or Global Administrator role, users request elevated access when needed, for a limited time, with approval and full audit.

**PIM Workflow:**
```
Engineer needs to modify production config
        │
        ▼
Requests Owner role via PIM (states reason, duration: 2 hours)
        │
        ▼
Manager/Lead approves the request
        │
        ▼
Engineer has Owner role for 2 hours only
        │
        ▼
Role automatically removed after 2 hours
All actions logged with justification
```

> **Production Standard:** In any mature Azure environment, no human permanently holds Global Administrator, Owner, or User Access Administrator roles. All elevated access is via PIM with approval and time limits. This is required for SOC 2, ISO 27001, and most enterprise compliance frameworks.

---

### 28.5 Encryption Deep Dive

**Encryption at Rest — Server-Side Encryption (SSE):**
- All Azure storage (disks, blobs, databases) encrypted at rest by default
- Microsoft-managed keys: Enabled automatically, no action needed
- Customer-managed keys (CMK): You control the encryption key in Key Vault

**Azure Disk Encryption (ADE):**
- OS and data disks encrypted using BitLocker (Windows) or dm-crypt (Linux)
- Keys managed in Key Vault
- Required for compliance in most regulated industries

```bash
# Enable disk encryption on VM
az vm encryption enable \
  --resource-group vm-lab-rg \
  --name my-first-vm \
  --disk-encryption-keyvault <keyvault-name>

# Check encryption status
az vm encryption show \
  --resource-group vm-lab-rg \
  --name my-first-vm
```

**Encryption in Transit:**
- All Azure services enforce TLS 1.2+ for data in transit
- Enforce HTTPS-only on App Service:
```bash
az webapp update \
  --resource-group az-training-rg \
  --name <your-webapp-name> \
  --https-only true
```

---

---

## Lesson 29 — Advanced Azure Networking

> **Certification:** AZ-700: Azure Network Engineer
> **Level:** Network Expert

---

### 29.1 Azure Firewall

Azure Firewall is a managed, cloud-native firewall. Unlike NSGs (which are stateless packet filters), Azure Firewall is a full stateful firewall with application-level filtering.

**Azure Firewall vs NSG:**

| Feature | NSG | Azure Firewall |
|---|---|---|
| **Type** | Stateless L4 filter | Stateful L4/L7 firewall |
| **Scope** | Subnet or NIC | Hub VNet (all traffic) |
| **FQDN filtering** | No | Yes (e.g., allow *.microsoft.com) |
| **Threat intelligence** | No | Yes (blocks known malicious IPs) |
| **Logs** | Limited | Full logging to Log Analytics |
| **Use case** | Basic subnet security | Central egress control |

```bash
# Deploy Azure Firewall in hub VNet
az network firewall create \
  --name hub-firewall \
  --resource-group hub-rg \
  --location centralindia \
  --sku-tier Premium   # Premium has TLS inspection and IDPS

# Create a firewall policy
az network firewall policy create \
  --name firewall-policy \
  --resource-group hub-rg \
  --location centralindia

# Add application rule — allow outbound HTTPS to Microsoft
az network firewall policy rule-collection-group create \
  --name DefaultRuleGroup \
  --policy-name firewall-policy \
  --resource-group hub-rg \
  --priority 100

az network firewall policy rule-collection-group collection add-filter-collection \
  --name AllowMicrosoft \
  --policy-name firewall-policy \
  --resource-group hub-rg \
  --rule-collection-group-name DefaultRuleGroup \
  --priority 100 \
  --action Allow \
  --rule-name AllowAzureServices \
  --rule-type ApplicationRule \
  --source-addresses "*" \
  --protocols Http=80 Https=443 \
  --target-fqdns "*.microsoft.com" "*.azure.com" "*.windows.net"
```

---

### 29.2 ExpressRoute — Dedicated Private Connectivity

ExpressRoute provides a dedicated private connection from your on-premises network to Azure, bypassing the public internet entirely.

**VPN Gateway vs ExpressRoute:**

| Feature | VPN Gateway | ExpressRoute |
|---|---|---|
| **Connection** | Over public internet (encrypted) | Dedicated private circuit |
| **Bandwidth** | Up to 10 Gbps | Up to 100 Gbps |
| **Latency** | Variable (internet path) | Consistent (private network) |
| **SLA** | 99.95% | 99.95% |
| **Cost** | Low | High (circuit charges) |
| **Use case** | SMB, backup connectivity | Enterprise, latency-sensitive, regulated |

> **When to recommend ExpressRoute:** Banks, regulated industries, latency-sensitive workloads (real-time trading, video processing). The RBI in India often requires ExpressRoute-equivalent connectivity for cloud workloads.

---

---

## Lesson 30 — Azure Data Engineering

> **Certification:** DP-203: Azure Data Engineer
> **Level:** Data Expert

---

### 30.1 The Modern Data Platform on Azure

```
DATA SOURCES                INGEST               STORE          PROCESS        SERVE
──────────────────────────────────────────────────────────────────────────────────────
Databases     ──┐
APIs          ──┤
Files         ──┤──► Event Hub  ──────────────┐
IoT Devices   ──┤    (streaming)               │──► Azure     ──► Databricks  ──► Power BI
Log Files     ──┘                              │    Data                         Synapse
                    Data Factory ─────────────►│    Lake      ──► Synapse     ──► Reports
                    (batch)                    │    Gen2          Analytics
                    Azure ADF  ────────────────┘
                    Pipelines
```

---

### 30.2 Core Data Services

**Azure Data Factory (ADF):**
- ETL/ELT orchestration service
- 90+ connectors (SQL Server, Oracle, Salesforce, SAP, etc.)
- No-code pipeline builder + code support
- Schedule, trigger, monitor pipelines

**Azure Data Lake Storage Gen2:**
- Blob storage + hierarchical namespace (folder structure)
- Designed for analytics workloads (Spark, Hadoop compatible)
- Separate compute and storage (scale independently)

**Azure Synapse Analytics:**
- Unified analytics platform combining data warehouse + data lake + Spark
- Synapse SQL (serverless + dedicated pools)
- Synapse Spark (PySpark, Scala)
- Integration with Power BI

**Azure Databricks:**
- Managed Apache Spark platform
- Best for complex data engineering + ML pipelines
- Collaborative notebooks
- Delta Lake for reliable data lake management

---

### 30.3 Simple ADF Pipeline

```bash
# Create Data Factory
az datafactory factory create \
  --resource-group az-training-rg \
  --factory-name mycompany-adf \
  --location centralindia

# Create linked service to Azure Blob Storage
az datafactory linked-service create \
  --resource-group az-training-rg \
  --factory-name mycompany-adf \
  --linked-service-name BlobStorageLS \
  --properties '{
    "type": "AzureBlobStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"
    }
  }'
```

---

---

## Lesson 31 — Azure AI and Cognitive Services

> **Certification:** AI-102: Azure AI Engineer
> **Level:** AI Expert

---

### 31.1 Azure AI Services Overview

Azure AI Services (formerly Cognitive Services) are pre-built AI models exposed as REST APIs. You don't need ML expertise — call the API, get intelligent results.

**Categories:**

| Category | Services | Use Cases |
|---|---|---|
| **Vision** | Computer Vision, Face, Custom Vision | Image classification, OCR, object detection |
| **Speech** | Speech-to-Text, Text-to-Speech, Translation | Call centres, accessibility, real-time translation |
| **Language** | Text Analytics, Translator, LUIS | Sentiment analysis, entity extraction, chatbots |
| **Decision** | Personaliser, Anomaly Detector, Content Moderator | Recommendations, fraud detection |
| **OpenAI** | GPT-4, DALL-E, Whisper | Generative AI, code generation, image generation |

---

### 31.2 Azure OpenAI Service

Azure's enterprise deployment of OpenAI models — same GPT-4, same DALL-E, but with:
- Data privacy (your data is not used to train models)
- SLA and enterprise support
- VNet integration
- Content filtering and responsible AI guardrails

```python
from openai import AzureOpenAI

client = AzureOpenAI(
    api_key="<your-api-key>",
    api_version="2024-02-01",
    azure_endpoint="https://<your-resource>.openai.azure.com/"
)

response = client.chat.completions.create(
    model="gpt-4",  # Your deployment name
    messages=[
        {"role": "system", "content": "You are a helpful Azure support engineer."},
        {"role": "user", "content": "How do I set up VNet peering?"}
    ],
    max_tokens=500
)

print(response.choices[0].message.content)
```

---

---

## Lesson 32 — Production Incident Response and Troubleshooting

> **Level:** Senior Engineer / Principal Engineer

---

### 32.1 The Incident Response Process

Every senior Azure engineer must know this process cold.

```
DETECTION → TRIAGE → CONTAINMENT → INVESTIGATION → RESOLUTION → POST-MORTEM
```

**Step 1 — Detection:**
- Azure Monitor alert fires, or user reports, or automated health check fails
- First action: **Check Azure Service Health** — is this an Azure platform issue?

```bash
# Check Azure service health for your region
az rest \
  --method get \
  --url "https://management.azure.com/subscriptions/<sub-id>/providers/Microsoft.ResourceHealth/availabilityStatuses?api-version=2015-01-01"
```

**Step 2 — Triage (first 5 minutes):**
- Is this affecting customers right now?
- What is the blast radius?
- Who else needs to know? (Escalation)

**Step 3 — Containment:**
- Can you route traffic away from the failing component?
- Can you roll back the last deployment?
- Can you scale up to handle degraded performance?

```bash
# Rollback App Service deployment
az webapp deployment slot swap \
  --resource-group prod-rg \
  --name myapp \
  --slot staging \
  --target-slot production

# Or via Azure DevOps — trigger previous successful pipeline run

# Scale up App Service plan immediately
az appservice plan update \
  --name myapp-plan \
  --resource-group prod-rg \
  --sku P3v3

# Force restart all instances
az webapp restart --name myapp --resource-group prod-rg
```

---

### 32.2 Common Troubleshooting Scenarios

**Scenario 1 — App Service returning 500 errors:**
```bash
# 1. Check App Service logs
az webapp log download \
  --name myapp \
  --resource-group prod-rg \
  --log-file logs.zip

# 2. Stream logs live
az webapp log tail \
  --name myapp \
  --resource-group prod-rg

# 3. Check Application Insights for exceptions
# Portal: Application Insights → Failures → Exceptions → Timeline

# 4. Check recent deployments
az webapp deployment list-publishing-credentials \
  --name myapp \
  --resource-group prod-rg
```

**Scenario 2 — VM is unreachable:**
```bash
# 1. Check VM power state
az vm show --name myvm --resource-group prod-rg --show-details --query powerState

# 2. Check NSG rules — is port 22/3389 actually allowed?
az network nsg rule list --nsg-name myvm-nsg --resource-group prod-rg --output table

# 3. Check if there's a boot error
az vm boot-diagnostics get-boot-log --name myvm --resource-group prod-rg

# 4. Use Run Command to execute commands without network access
az vm run-command invoke \
  --name myvm \
  --resource-group prod-rg \
  --command-id RunShellScript \
  --scripts "systemctl status nginx && df -h && free -m"
```

**Scenario 3 — Database connection timeouts:**
```bash
# 1. Check SQL Database metrics (DTU/vCore utilisation)
az monitor metrics list \
  --resource /subscriptions/<sub>/resourceGroups/<rg>/providers/Microsoft.Sql/servers/<server>/databases/<db> \
  --metric "dtu_consumption_percent" \
  --interval PT5M

# 2. Check connection limit
az sql db show \
  --name mydb \
  --server myserver \
  --resource-group prod-rg \
  --query "maxSizeBytes,currentServiceObjectiveName"

# 3. Check firewall rules — is app's IP allowed?
az sql server firewall-rule list \
  --server myserver \
  --resource-group prod-rg \
  --output table
```

---

### 32.3 KQL for Incident Investigation

```kql
// Find all 5xx errors in the last hour, by endpoint
AppServiceHTTPLogs
| where TimeGenerated > ago(1h)
| where ScStatus >= 500
| summarize Count = count() by CsUriStem, ScStatus
| order by Count desc

// Find the exact moment something broke
requests
| where timestamp > ago(2h)
| summarize FailureRate = countif(success == false) / count() * 100 by bin(timestamp, 1m)
| render timechart

// Find which deployment caused the issue
AzureActivity
| where TimeGenerated > ago(4h)
| where OperationNameValue contains "deployments"
| where ActivityStatusValue == "Success"
| project TimeGenerated, Caller, ResourceGroup, Properties
| order by TimeGenerated desc

// Application exceptions with stack traces
exceptions
| where timestamp > ago(1h)
| project timestamp, type, outerMessage, innermostMessage, customDimensions
| order by timestamp desc
| take 20
```

---

---

## Lesson 33 — Azure Interview Preparation

> **Level:** Senior Engineer / Lead Engineer

---

### 33.1 Common Senior Azure Interview Questions

**Architecture Questions:**

**Q: "Design a highly available web application for 1 million users in India. Walk me through your architecture."**

> Model Answer:
> "I'd use Azure Front Door for global entry — it gives us CDN, WAF, and health-based routing in one service. Behind Front Door, I'd deploy Azure App Service on Premium P2v3 tier across all three availability zones in Central India. Auto-scaling from 3 to 30 instances based on CPU and request queue depth. The application tier connects to Azure Cache for Redis for session state and hot data. Database is Azure SQL Database Business Critical tier, zone-redundant, with a read replica for reporting queries. All sensitive configuration in Azure Key Vault, accessed via Managed Identity — no credentials in code. Azure Monitor and Application Insights for full observability. Storage on ZRS-redundant Azure Blob via Private Endpoint — no public internet access to the storage account. Everything deployed via Terraform and Azure DevOps pipelines with staging slots and mandatory PR approval for production changes."

---

**Q: "How do you handle secrets management in a production Azure environment?"**

> Model Answer:
> "All secrets — database passwords, API keys, connection strings — live in Azure Key Vault. Applications authenticate using Managed Identity (system-assigned for single-resource scenarios, user-assigned when multiple resources share an identity). The Managed Identity is granted the Key Vault Secrets User RBAC role with scope limited to the specific vault. In App Service, we use the @Microsoft.KeyVault() reference syntax in application settings so secrets are resolved at runtime and never appear in deployment artifacts, logs, or environment variables in plain text. In CI/CD pipelines, we use the AzureKeyVault task in Azure DevOps to inject secrets as masked pipeline variables. Key Vault has diagnostic logging enabled, and we alert on any unexpected secret access patterns. We rotate secrets quarterly via Azure Key Vault's rotation feature, with zero application downtime using dual-version secrets."

---

**Q: "A VM in production suddenly becomes unresponsive. Walk me through your troubleshooting steps."**

> Model Answer:
> "First, check Azure Service Health to rule out platform-level issues. Next, check the VM power state via CLI — `az vm show --show-details`. If it's running, check NSG rules to confirm the required ports are allowed from expected sources. Use the Boot Diagnostics screenshot in the Portal to see if the VM is hanging at boot. If the VM is reachable but the application is down, use Run Command to execute diagnostics without needing network access — check service status, disk space, memory. If there was a recent deployment, I'd roll back immediately and confirm if that resolves it. Check Application Insights and Log Analytics for errors in the 30 minutes preceding the incident. If it's a disk full issue, Run Command can clear logs or temp files. If memory pressure, I'd resize the VM to a larger SKU temporarily. Throughout this, I'm keeping a running timeline in our incident channel and looping in relevant team members based on what I find."

---

### 33.2 Scenario-Based Questions

**Q: "Your company needs to comply with India's DPDP Act — all customer data must stay in India. How do you ensure this architecturally?"**

Key points to cover:
- Deploy all data services in India regions only (Central India, South India, West India)
- Use Azure Policy to deny creation of data services outside India geographies
- Azure Storage with no geo-replication (LRS or ZRS — both stay in the same region/zone, not paired regions outside India)
- Cosmos DB: India-only replication regions
- Document the data residency architecture for auditors
- Azure Blueprints to package the policy set for consistent enforcement

---

**Q: "How would you migrate a monolithic .NET application from on-premises to Azure with minimal downtime?"**

A strong migration approach:
1. **Assess** with Azure Migrate — understand dependencies, size VMs correctly
2. **Lift and shift first** — replicate VMs to Azure with Azure Site Recovery (zero-downtime migration)
3. **Test in Azure** — run both environments in parallel
4. **DNS cutover** — change DNS to point at Azure (TTL already reduced to 60 seconds)
5. **Modernise over time** — progressively move to App Service, SQL Managed Instance, microservices
6. **Never try to modernise and migrate simultaneously** — do it in phases

---

### 33.3 Azure CLI Cheat Sheet — Commands You Must Know

```bash
# ─── RESOURCE MANAGEMENT ────────────────────────────────────
az group create --name <rg> --location centralindia
az group delete --name <rg> --yes
az resource list --resource-group <rg> --output table
az resource move --destination-group <target-rg> --ids <resource-id>

# ─── VIRTUAL MACHINES ───────────────────────────────────────
az vm create --resource-group <rg> --name <vm> --image Ubuntu2204 --size Standard_B2s --generate-ssh-keys
az vm start/stop/restart/deallocate --resource-group <rg> --name <vm>
az vm list --show-details --output table
az vm resize --resource-group <rg> --name <vm> --size Standard_D4s_v5
az vm run-command invoke --resource-group <rg> --name <vm> --command-id RunShellScript --scripts "..."

# ─── NETWORKING ─────────────────────────────────────────────
az network vnet create --resource-group <rg> --name <vnet> --address-prefix 10.0.0.0/16
az network vnet subnet create --resource-group <rg> --vnet-name <vnet> --name <subnet> --address-prefix 10.0.1.0/24
az network nsg create --resource-group <rg> --name <nsg>
az network nsg rule create --resource-group <rg> --nsg-name <nsg> --name <rule> --priority 100 --destination-port-range 443 --access Allow

# ─── IDENTITY AND ACCESS ─────────────────────────────────────
az ad user create --display-name <name> --user-principal-name <upn> --password <pwd>
az ad group create --display-name <name> --mail-nickname <nick>
az role assignment create --assignee <id> --role "Contributor" --resource-group <rg>
az role assignment list --resource-group <rg> --output table

# ─── APP SERVICE ─────────────────────────────────────────────
az webapp create --resource-group <rg> --plan <plan> --name <name> --runtime "NODE:18-lts"
az webapp deployment slot create --name <app> --resource-group <rg> --slot staging
az webapp deployment slot swap --name <app> --resource-group <rg> --slot staging
az webapp log tail --name <app> --resource-group <rg>
az webapp restart --name <app> --resource-group <rg>

# ─── AKS ────────────────────────────────────────────────────
az aks create --resource-group <rg> --name <cluster> --node-count 3 --enable-managed-identity
az aks get-credentials --resource-group <rg> --name <cluster>
az aks scale --resource-group <rg> --name <cluster> --node-count 5
az aks upgrade --resource-group <rg> --name <cluster> --kubernetes-version 1.29

# ─── MONITORING ──────────────────────────────────────────────
az monitor metrics alert create --name <alert> --resource-group <rg> --scopes <resource-id> --condition "avg Percentage CPU > 90"
az monitor log-analytics workspace create --resource-group <rg> --workspace-name <name>
az webapp log download --name <app> --resource-group <rg> --log-file logs.zip

# ─── SECURITY ────────────────────────────────────────────────
az keyvault create --name <kv> --resource-group <rg> --location centralindia --enable-rbac-authorization true
az keyvault secret set --vault-name <kv> --name <secret-name> --value <value>
az keyvault secret show --vault-name <kv> --name <secret-name> --query value

# ─── COST ────────────────────────────────────────────────────
az advisor recommendation list --category Cost --output table
az disk list --query "[?diskState=='Unattached'].{Name:name, RG:resourceGroup}" --output table
```

---

### 33.4 Azure Certification Roadmap

**Recommended study order for a cloud/DevOps career:**

```
Month 1–2:   AZ-900 (Azure Fundamentals)
             ↓ Easy entry point. Gets you thinking in Azure.

Month 3–5:   AZ-104 (Azure Administrator)
             ↓ Core platform skills. VMs, networking, storage, identity.

Month 5–7:   AZ-204 (Azure Developer)  OR  AZ-400 (DevOps Engineer)
             ↓ Choose based on your role (developer vs DevOps).

Month 8–10:  AZ-305 (Solutions Architect Expert)
             ↓ Requires AZ-104 as prerequisite. Senior-level.

Month 11–12: AZ-500 (Security Engineer)  +  AZ-700 (Network Engineer)
             ↓ Specialty certifications that differentiate you.

Year 2:      DP-203 (Data Engineer)  +  AI-102 (AI Engineer)
             ↓ Expand your platform breadth.
```

---

## Official Microsoft Learning Resources

| Resource | URL |
|---|---|
| Azure Documentation | https://learn.microsoft.com/azure/ |
| Azure Architecture Center | https://learn.microsoft.com/azure/architecture/ |
| Azure Certifications | https://learn.microsoft.com/certifications/ |
| Microsoft Learn Paths | https://learn.microsoft.com/training/ |
| Azure CLI Reference | https://learn.microsoft.com/cli/azure/ |
| AKS Documentation | https://learn.microsoft.com/azure/aks/ |
| Azure DevOps Documentation | https://learn.microsoft.com/azure/devops/ |
| Terraform Azure Provider | https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs |
| Well-Architected Framework | https://learn.microsoft.com/azure/well-architected/ |
| Azure Free Account | https://azure.microsoft.com/free/ |
| Azure Architecture Diagrams | https://learn.microsoft.com/azure/architecture/browse/ |

---

## Final Note

This curriculum is your foundation. The path from here to Senior Azure or Azure DevOps Engineer is:

1. **Work through every lab** — reading alone is passive. Doing is learning.
2. **Build a real project** — deploy a multi-tier application using Terraform, AKS, Key Vault, and Azure DevOps pipelines. Put it on GitHub.
3. **Get AZ-900 first** — then AZ-104. Certifications prove your knowledge to employers.
4. **Contribute at work or on GitHub** — write Terraform modules, create reusable pipelines, document architectures.
5. **Join the community** — Microsoft Tech Community, Azure Weekly newsletter, Azure subreddit.

Every senior engineer was once a beginner. The difference is consistent practice over time.

---

*Built on: Microsoft Azure Official Documentation | Microsoft Well-Architected Framework | Azure Architecture Center*
