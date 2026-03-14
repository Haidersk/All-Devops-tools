# Terraform Mastery — Complete Engineering Curriculum
## Zero to Senior DevOps / IaC Engineer

> **Covers:** IaC Fundamentals · HCL Syntax · Providers · State Management · Modules · Multi-Cloud · CI/CD · Security · Expert Internals
> **Track:** DevOps Career Path | Beginner → Senior Engineer
> **Based on:** Official HashiCorp Terraform Documentation — https://developer.hashicorp.com/terraform/docs

---

## How to Use This Document

- Work through every lesson in order — each one builds on the last
- Run every CLI command and lab yourself — reading is passive, doing is learning
- Attempt every practice question before reading the answer
- Return to earlier sections when later lessons reference them
- The labs use Azure as the primary cloud — swap provider config for AWS/GCP as needed

---

## Table of Contents

### PHASE 1 — Foundations (Beginner)
- [Lesson 1 — Infrastructure as Code and Terraform Architecture](#lesson-1--infrastructure-as-code-and-terraform-architecture)
- [Lesson 2 — HCL Syntax and Terraform Configuration](#lesson-2--hcl-syntax-and-terraform-configuration)
- [Lesson 3 — Providers and Resources](#lesson-3--providers-and-resources)
- [Lesson 4 — Terraform State](#lesson-4--terraform-state)
- [Lesson 5 — Variables and Outputs](#lesson-5--variables-and-outputs)

### PHASE 2 — Intermediate
- [Lesson 6 — Terraform Modules](#lesson-6--terraform-modules)
- [Lesson 7 — Data Sources and Dependencies](#lesson-7--data-sources-and-dependencies)
- [Lesson 8 — Remote State and State Locking](#lesson-8--remote-state-and-state-locking)
- [Lesson 9 — Terraform Functions and Expressions](#lesson-9--terraform-functions-and-expressions)
- [Lesson 10 — Workspaces and Environment Management](#lesson-10--workspaces-and-environment-management)
- [Lesson 11 — Lifecycle Rules and Meta-Arguments](#lesson-11--lifecycle-rules-and-meta-arguments)

### PHASE 3 — DevOps Level
- [Lesson 12 — Terraform with Azure (Deep Dive)](#lesson-12--terraform-with-azure-deep-dive)
- [Lesson 13 — Terraform with AWS](#lesson-13--terraform-with-aws)
- [Lesson 14 — Terraform with GCP](#lesson-14--terraform-with-gcp)
- [Lesson 15 — Terraform in CI/CD Pipelines](#lesson-15--terraform-in-cicd-pipelines)
- [Lesson 16 — Terraform Secrets Management](#lesson-16--terraform-secrets-management)
- [Lesson 17 — Terraform Drift Detection and Remediation](#lesson-17--terraform-drift-detection-and-remediation)

### PHASE 4 — Advanced Architecture
- [Lesson 18 — Designing Reusable Module Libraries](#lesson-18--designing-reusable-module-libraries)
- [Lesson 19 — Multi-Environment Infrastructure](#lesson-19--multi-environment-infrastructure)
- [Lesson 20 — Multi-Region Deployments](#lesson-20--multi-region-deployments)
- [Lesson 21 — Infrastructure Cost Optimisation](#lesson-21--infrastructure-cost-optimisation)
- [Lesson 22 — Infrastructure Dependency Graphs and Change Management](#lesson-22--infrastructure-dependency-graphs-and-change-management)

### PHASE 5 — Expert Level
- [Lesson 23 — Terraform Internals](#lesson-23--terraform-internals)
- [Lesson 24 — State Debugging and Corruption Recovery](#lesson-24--state-debugging-and-corruption-recovery)
- [Lesson 25 — Large-Scale Infrastructure Management](#lesson-25--large-scale-infrastructure-management)
- [Lesson 26 — Terraform Security Hardening](#lesson-26--terraform-security-hardening)
- [Lesson 27 — DevOps Interview Preparation — Terraform Edition](#lesson-27--devops-interview-preparation--terraform-edition)

---

---

# PHASE 1 — FOUNDATIONS
## Terraform Beginner Level

---

## Lesson 1 — Infrastructure as Code and Terraform Architecture

> **Level:** Absolute Beginner
> **Goal:** Understand what IaC is, why Terraform exists, and install it

---

### 1.1 What is Infrastructure as Code?

Before Terraform, provisioning infrastructure looked like this:

**The Manual Way (ClickOps):**
1. Log into cloud console
2. Click through menus to create a VM
3. Configure networking manually
4. Set up security groups by hand
5. Add a database — more clicking
6. Document what you did (maybe)
7. Do this again for dev, staging, and production
8. Do this again when disaster strikes and you need to rebuild

**Problems with manual infrastructure:**
- **Not reproducible:** Nobody can prove the staging environment matches production
- **Not auditable:** No history of who changed what and when
- **Not scalable:** 5 engineers clicking through consoles for 50 services breaks down quickly
- **Error-prone:** Humans make mistakes under pressure
- **Undocumented:** The infrastructure lives in one engineer's head — until they leave

> **Infrastructure as Code (IaC)** solves this by describing your infrastructure in code files. The code is the documentation. The code is version-controlled in Git. The code is reviewed in pull requests. The code can be applied repeatedly to produce identical results.

**The IaC way:**
```hcl
resource "azurerm_linux_virtual_machine" "web" {
  name                = "web-server"
  resource_group_name = azurerm_resource_group.main.name
  location            = "centralindia"
  size                = "Standard_B2s"
  # ... complete configuration
}
```

This file is:
- Committed to Git — full change history
- Reviewed in pull requests — peer review before any production change
- Applied to dev, staging, and production identically — no drift
- Recoverable — disaster recovery means `terraform apply`

---

### 1.2 Why Terraform? The Alternatives

| Tool | Supported Clouds | Language | Maintained by |
|---|---|---|---|
| **Terraform** | AWS, Azure, GCP, 3000+ providers | HCL (HashiCorp Config Language) | HashiCorp / OpenTofu |
| **CloudFormation** | AWS only | YAML / JSON | AWS |
| **ARM Templates / Bicep** | Azure only | JSON / Bicep DSL | Microsoft |
| **Deployment Manager** | GCP only | YAML / Python / Jinja2 | Google |
| **Pulumi** | Multi-cloud | Python, TypeScript, Go, C# | Pulumi |
| **Ansible** | Any (via SSH/API) | YAML | Red Hat |

**Why Terraform wins in most teams:**
- **Multi-cloud:** One tool, one workflow regardless of cloud provider
- **Declarative:** You describe the desired state — Terraform figures out how to get there
- **Idempotent:** Run it 10 times — same result every time
- **Massive ecosystem:** 3,000+ providers (AWS, Azure, GCP, Kubernetes, GitHub, Datadog, PagerDuty...)
- **Industry standard:** Most DevOps job descriptions list Terraform as required
- **State management:** Tracks exactly what infrastructure it manages
- **Plan before apply:** Preview changes before making them — like `git diff` for infrastructure

---

### 1.3 Terraform Architecture — How It Works

```
You write HCL code (.tf files)
           │
           ▼
    terraform init
    Downloads providers and modules
           │
           ▼
    terraform plan
    Compares desired state (your code)
    against current state (state file)
    Shows what will be created/changed/destroyed
           │
           ▼
    terraform apply
    Calls cloud APIs to make changes
    Updates state file with new reality
           │
           ▼
    terraform destroy
    Removes all managed infrastructure
    Cleans state file
```

**Core Components:**

| Component | What It Is | Where It Lives |
|---|---|---|
| **Configuration files** | Your `.tf` files describing desired infrastructure | Your project directory / Git repo |
| **Provider** | Plugin that talks to a cloud API (Azure, AWS, GCP) | Downloaded to `.terraform/` on `init` |
| **State file** | Terraform's record of real infrastructure it manages | `terraform.tfstate` locally or remote backend |
| **Plan** | Preview of changes before applying | Generated in memory, optionally saved as `.tfplan` |
| **Backend** | Where state is stored (local or remote S3/Azure/GCS) | Configured in `backend` block |
| **Registry** | Public library of providers and modules | registry.terraform.io |

**The Execution Flow in Detail:**
```
Your .tf files (desired state)
         │
         ▼
terraform plan:
  Read .tf files  →  Parse desired state
  Read state file →  Parse known current state
  Call cloud APIs →  Refresh actual current state
  Diff: desired vs actual → Show plan
         │
         ▼
terraform apply:
  Execute the plan
  Call provider APIs (az, aws, gcloud under the hood)
  Each resource created/updated/deleted
  State file updated after each successful operation
```

---

### 1.4 Installing Terraform

**macOS:**
```bash
# Option 1: Homebrew (recommended)
brew tap hashicorp/tap
brew install hashicorp/tap/terraform

# Option 2: tfenv (manage multiple Terraform versions)
brew install tfenv
tfenv install 1.6.0
tfenv use 1.6.0
```

**Ubuntu / Debian Linux:**
```bash
# Add HashiCorp GPG key and repository
wget -O- https://apt.releases.hashicorp.com/gpg | \
  sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
  https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
  sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update && sudo apt install terraform
```

**Windows (PowerShell as Administrator):**
```powershell
# Option 1: winget
winget install HashiCorp.Terraform

# Option 2: Chocolatey
choco install terraform

# Option 3: Download binary from https://developer.hashicorp.com/terraform/downloads
# Extract terraform.exe, add directory to PATH
```

**Verify installation:**
```bash
terraform version
# Should output: Terraform v1.x.x on <your OS>

terraform -help
terraform -help plan
```

**IDE Setup (highly recommended):**
```
VS Code → Install extension: "HashiCorp Terraform"
  - Syntax highlighting
  - Auto-completion
  - Inline documentation
  - Format on save
  - Error detection

Add to VS Code settings.json:
{
  "[terraform]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "hashicorp.terraform"
  }
}
```

---

### 1.5 The Terraform Workflow — Core Commands

```bash
# Initialise a project (download providers, set up backend)
terraform init

# Format code (auto-fix indentation and style)
terraform fmt
terraform fmt -recursive    # Format all .tf files in subdirectories

# Validate syntax and configuration
terraform validate

# Preview changes (reads state, compares to code, shows diff)
terraform plan
terraform plan -out=tfplan  # Save plan to file (use in CI/CD)

# Apply changes
terraform apply
terraform apply tfplan       # Apply a saved plan (exactly what was previewed)
terraform apply -auto-approve  # Skip confirmation prompt (CI/CD only)

# Destroy all managed infrastructure
terraform destroy
terraform destroy -auto-approve

# Show current state
terraform show
terraform show -json | jq   # JSON format for scripting

# List resources in state
terraform state list

# Show details of one resource in state
terraform state show azurerm_resource_group.main

# Output values
terraform output
terraform output web_app_url

# Graph infrastructure dependencies
terraform graph | dot -Tsvg > graph.svg
```

---

### 1.6 Hands-On Lab 1 — Your First Terraform Configuration

**Objective:** Install Terraform, write your first config, understand the init/plan/apply/destroy cycle.

**Prerequisites:** Azure free account + Azure CLI installed and logged in (`az login`)

```bash
# Create project directory
mkdir terraform-lab-1 && cd terraform-lab-1

# Create your first Terraform configuration
cat > main.tf << 'EOF'
# Tell Terraform which providers we need and their versions
terraform {
  required_version = ">= 1.5.0"
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.80"
    }
  }
}

# Configure the Azure provider
provider "azurerm" {
  features {}
}

# Create a Resource Group
resource "azurerm_resource_group" "main" {
  name     = "terraform-lab-rg"
  location = "centralindia"

  tags = {
    Environment = "learning"
    ManagedBy   = "Terraform"
    CreatedBy   = "your-name"
  }
}
EOF
```

**Step 1 — Initialise:**
```bash
terraform init
# Watch: Terraform downloads the azurerm provider (~50MB)
# Creates: .terraform/ directory with provider binaries
# Creates: .terraform.lock.hcl (locks provider versions — commit this to Git)
```

**Step 2 — Format and Validate:**
```bash
terraform fmt        # Formats main.tf
terraform validate   # Checks syntax — should say "Success!"
```

**Step 3 — Plan:**
```bash
terraform plan
# Read the output carefully:
# + resource "azurerm_resource_group" "main"  ← + means CREATE
#   name     = "terraform-lab-rg"
#   location = "centralindia"
#   tags     = {...}
# Plan: 1 to add, 0 to change, 0 to destroy.
```

**Step 4 — Apply:**
```bash
terraform apply
# Type 'yes' to confirm
# Watch: Terraform calls Azure API, creates resource group
# "Apply complete! Resources: 1 added, 0 changed, 0 destroyed."

# Verify in Azure CLI
az group show --name terraform-lab-rg --output table
```

**Step 5 — Understand the State File:**
```bash
# Look at what Terraform created
cat terraform.tfstate
# This JSON file is Terraform's memory of what it created
# NEVER edit this manually

# Show state summary
terraform show
terraform state list
```

**Step 6 — Make a Change:**
```bash
# Add a tag to the resource group in main.tf
# Change tags block to:
# tags = {
#   Environment = "learning"
#   ManagedBy   = "Terraform"
#   CreatedBy   = "your-name"
#   UpdatedAt   = "2024-01-15"   ← ADD THIS LINE
# }

terraform plan
# Read output: ~ means MODIFY (in-place update)
# ~ resource "azurerm_resource_group" "main"
#   ~ tags = {
#       + "UpdatedAt" = "2024-01-15"
#     }

terraform apply -auto-approve
```

**Step 7 — Destroy:**
```bash
terraform destroy
# Type 'yes'
# "Destroy complete! Resources: 1 destroyed."

# Verify resource group is gone
az group list --query "[?name=='terraform-lab-rg']" --output table
```

---

### 1.7 Practice Questions — Lesson 1

**Q1.** What is the purpose of the `terraform plan` command?

- A) It creates infrastructure in the cloud
- B) It shows a preview of what will be created, changed, or destroyed without making any changes
- C) It downloads the required providers
- D) It validates the syntax of your Terraform files

<details>
<summary>Answer and Explanation</summary>

**Answer: B.** `terraform plan` is a read-only operation — it reads your code, reads the state file, optionally refreshes against the actual cloud, and produces a diff. No infrastructure is created or changed. This is why you should always run `plan` before `apply`, especially in production.

</details>

---

**Q2.** What does the `terraform.tfstate` file contain, and why should it never be manually edited?

<details>
<summary>Answer</summary>

The state file contains Terraform's complete record of all infrastructure it manages — resource IDs, attributes, dependencies, and metadata. It's the source of truth that lets `terraform plan` know what already exists. Manual edits can corrupt the state, causing Terraform to lose track of resources (which could lead to duplicate resource creation or deletion of live infrastructure). Always use `terraform state` commands for any manipulation.

</details>

---

**Q3 — Scenario.** Your colleague ran `terraform apply` manually from their laptop and now the state file on their machine doesn't match what other team members have. How does this cause problems and how do you prevent it?

<details>
<summary>Answer</summary>

This is the "state divergence" problem. Different state files mean different team members have different views of infrastructure. One person's `terraform plan` shows changes another person's doesn't. Applying from divergent state can create duplicate resources or delete ones another person just created.

Prevention: Use remote state (Lesson 8) — store `terraform.tfstate` in a shared backend (Azure Blob, S3, Terraform Cloud) with state locking enabled. Only one operation runs at a time, and everyone reads from the same truth.

</details>

---

---

## Lesson 2 — HCL Syntax and Terraform Configuration

> **Level:** Beginner
> **Goal:** Master HCL — the language of Terraform

---

### 2.1 HCL — HashiCorp Configuration Language

HCL is designed to be human-readable and writable. It is not a general programming language — it is a declarative configuration language. You describe *what* you want, not *how* to create it.

**HCL File Types:**

| Extension | Purpose |
|---|---|
| `.tf` | Main configuration files |
| `.tfvars` | Variable value files |
| `.tfvars.json` | Variable values in JSON format |
| `.terraform.lock.hcl` | Provider version lock file (auto-generated) |
| `terraform.tfstate` | State file (auto-generated) |

---

### 2.2 HCL Syntax — Complete Reference

**Block Types:**
```hcl
# Block syntax
block_type "label_one" "label_two" {
  argument_name = value
}

# The four core block types you use daily:
terraform { }           # Global Terraform settings
provider "azurerm" { }  # Provider configuration
resource "type" "name" { }  # Infrastructure resource
variable "name" { }     # Input variable declaration
output "name" { }       # Output value declaration
data "type" "name" { }  # Data source (read existing infra)
locals { }              # Local computed values
module "name" { }       # Module call
```

**Value Types:**
```hcl
# String
name = "my-resource"
name = "prefix-${var.environment}-suffix"  # String interpolation

# Number
count   = 3
timeout = 30

# Boolean
enabled     = true
public_ip   = false

# List (array)
locations = ["centralindia", "southindia", "westindia"]

# Map (key-value pairs)
tags = {
  Environment = "production"
  Team        = "platform"
  CostCenter  = "engineering"
}

# Set (like list but unordered, unique values)
availability_zones = toset(["1", "2", "3"])

# Object (structured type)
disk = {
  type = "Premium_LRS"
  size = 128
}

# Null (explicitly no value)
custom_dns = null
```

**Comments:**
```hcl
# Single line comment

// Also single line comment

/*
  Multi-line
  comment block
*/
```

---

### 2.3 String Interpolation and Expressions

```hcl
# Basic interpolation
resource "azurerm_resource_group" "main" {
  name     = "${var.project_name}-${var.environment}-rg"
  location = var.location
}

# Conditional expression (ternary)
size = var.environment == "production" ? "Standard_D4s_v5" : "Standard_B2s"

# For expressions — transform lists and maps
upper_names = [for name in var.names : upper(name)]

# Filter with if
prod_tags = {for k, v in var.all_tags : k => v if v != ""}

# Splat expression — get a list of attribute values
all_vm_ids = azurerm_linux_virtual_machine.web[*].id
```

---

### 2.4 File and Project Structure

**Single environment (small project):**
```
project/
├── main.tf           # Primary resources
├── variables.tf      # Variable declarations
├── outputs.tf        # Output declarations
├── locals.tf         # Local values
├── providers.tf      # Provider configuration
├── terraform.tfvars  # Variable values (don't commit if it contains secrets)
└── .terraform.lock.hcl  # Provider lock file (commit this)
```

**Why multiple files?** Terraform reads ALL `.tf` files in a directory as one configuration. Splitting into files is purely for human organisation. Terraform doesn't care which file a resource is in.

---

### 2.5 A Real Project — Structured Configuration

**providers.tf:**
```hcl
terraform {
  required_version = ">= 1.5.0"
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.80"
    }
    random = {
      source  = "hashicorp/random"
      version = "~> 3.5"
    }
  }
}

provider "azurerm" {
  features {
    key_vault {
      purge_soft_delete_on_destroy    = false
      recover_soft_deleted_key_vaults = true
    }
    resource_group {
      prevent_deletion_if_contains_resources = true
    }
  }
}
```

**variables.tf:**
```hcl
variable "project_name" {
  description = "Name of the project — used in all resource names"
  type        = string

  validation {
    condition     = can(regex("^[a-z0-9-]{3,20}$", var.project_name))
    error_message = "project_name must be 3-20 chars, lowercase letters, numbers, and hyphens only."
  }
}

variable "environment" {
  description = "Deployment environment"
  type        = string

  validation {
    condition     = contains(["dev", "staging", "production"], var.environment)
    error_message = "environment must be dev, staging, or production."
  }
}

variable "location" {
  description = "Azure region for all resources"
  type        = string
  default     = "centralindia"
}

variable "tags" {
  description = "Tags applied to all resources"
  type        = map(string)
  default     = {}
}
```

**locals.tf:**
```hcl
locals {
  # Standard naming prefix for all resources
  name_prefix = "${var.project_name}-${var.environment}"

  # Merged tags — combine default tags with user-provided tags
  common_tags = merge(
    {
      Project     = var.project_name
      Environment = var.environment
      ManagedBy   = "Terraform"
      LastUpdated = timestamp()
    },
    var.tags
  )
}
```

**main.tf:**
```hcl
resource "azurerm_resource_group" "main" {
  name     = "${local.name_prefix}-rg"
  location = var.location
  tags     = local.common_tags
}
```

**outputs.tf:**
```hcl
output "resource_group_name" {
  description = "Name of the created resource group"
  value       = azurerm_resource_group.main.name
}

output "resource_group_id" {
  description = "ID of the created resource group"
  value       = azurerm_resource_group.main.id
}
```

**terraform.tfvars:**
```hcl
project_name = "myapp"
environment  = "dev"
location     = "centralindia"

tags = {
  Team       = "platform-engineering"
  CostCenter = "tech-001"
}
```

---

---

## Lesson 3 — Providers and Resources

> **Level:** Beginner → Intermediate
> **Goal:** Deeply understand providers and how resources work

---

### 3.1 Providers — The Bridge to Cloud APIs

A Terraform provider is a plugin that knows how to talk to a specific API. The Azure provider (`azurerm`) knows how to call Azure Resource Manager APIs. The AWS provider knows the AWS APIs. Providers translate your HCL into API calls.

**Provider configuration:**
```hcl
# Minimal Azure provider
provider "azurerm" {
  features {}   # Required block (can be empty)
}

# Azure provider with specific subscription
provider "azurerm" {
  subscription_id = "00000000-0000-0000-0000-000000000000"
  tenant_id       = "00000000-0000-0000-0000-000000000000"
  features {}
}

# Multiple providers — different environments
provider "azurerm" {
  alias           = "production"
  subscription_id = var.prod_subscription_id
  features {}
}

provider "azurerm" {
  alias           = "development"
  subscription_id = var.dev_subscription_id
  features {}
}

# Reference aliased provider
resource "azurerm_resource_group" "prod" {
  provider = azurerm.production
  name     = "prod-rg"
  location = "centralindia"
}
```

**Provider version constraints:**
```hcl
required_providers {
  azurerm = {
    source  = "hashicorp/azurerm"
    version = "~> 3.80"    # >= 3.80.0, < 4.0.0  (most common — allow patch+minor)
  }
  aws = {
    source  = "hashicorp/aws"
    version = ">= 5.0, < 6.0"  # Range constraint
  }
  random = {
    source  = "hashicorp/random"
    version = "= 3.5.1"    # Exact version (very strict)
  }
}
```

**Version constraint operators:**

| Operator | Meaning | Example |
|---|---|---|
| `=` | Exact version | `= 3.5.1` |
| `!=` | Not this version | `!= 3.5.0` |
| `>`, `>=` | Greater than | `>= 3.80` |
| `<`, `<=` | Less than | `< 4.0.0` |
| `~>` | Allows rightmost version component to increment | `~> 3.80` = `>= 3.80, < 4.0` |

---

### 3.2 Resources — The Core of Terraform

Every cloud resource you create is a `resource` block. The syntax is:

```hcl
resource "<provider>_<resource_type>" "<local_name>" {
  argument = value
}
```

**Naming convention:**
- `<provider>_<resource_type>` — from the provider documentation (e.g., `azurerm_virtual_network`, `aws_instance`, `google_compute_instance`)
- `<local_name>` — your name for it within Terraform (used to reference it elsewhere)

**Referencing resource attributes:**
```hcl
resource "azurerm_resource_group" "main" {
  name     = "myapp-rg"
  location = "centralindia"
}

resource "azurerm_virtual_network" "main" {
  name                = "myapp-vnet"
  resource_group_name = azurerm_resource_group.main.name      # Reference!
  location            = azurerm_resource_group.main.location  # Reference!
  address_space       = ["10.0.0.0/16"]
}
# When you reference azurerm_resource_group.main.name,
# Terraform automatically knows the VNet DEPENDS ON the resource group
# It will create the resource group FIRST, then the VNet
```

---

### 3.3 Meta-Arguments — Special Resource Arguments

These work on every resource type regardless of provider:

```hcl
resource "azurerm_subnet" "web" {
  count = 3    # Create 3 identical subnets
  name  = "web-subnet-${count.index}"
  # count.index = 0, 1, 2 for each instance
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = ["10.0.${count.index + 1}.0/24"]
}

# Reference: azurerm_subnet.web[0], azurerm_subnet.web[1], azurerm_subnet.web[2]
```

```hcl
# for_each — create resources from a map or set
variable "subnets" {
  default = {
    web  = "10.0.1.0/24"
    app  = "10.0.2.0/24"
    data = "10.0.3.0/24"
  }
}

resource "azurerm_subnet" "main" {
  for_each = var.subnets

  name                 = each.key      # "web", "app", "data"
  address_prefixes     = [each.value]  # CIDR range
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
}

# Reference: azurerm_subnet.main["web"], azurerm_subnet.main["app"]
```

```hcl
# depends_on — explicit dependency when implicit isn't enough
resource "azurerm_role_assignment" "main" {
  depends_on = [azurerm_kubernetes_cluster.main]  # Wait for AKS before assigning role
  # ...
}
```

---

### 3.4 Hands-On Lab 3 — Real Azure Infrastructure

```bash
mkdir terraform-lab-3 && cd terraform-lab-3
```

**providers.tf:**
```hcl
terraform {
  required_version = ">= 1.5.0"
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.80"
    }
  }
}

provider "azurerm" {
  features {}
}
```

**variables.tf:**
```hcl
variable "project_name" {
  type    = string
  default = "tflab"
}

variable "environment" {
  type    = string
  default = "dev"
}

variable "location" {
  type    = string
  default = "centralindia"
}
```

**main.tf:**
```hcl
locals {
  prefix = "${var.project_name}-${var.environment}"
  tags = {
    Project     = var.project_name
    Environment = var.environment
    ManagedBy   = "Terraform"
  }
}

resource "azurerm_resource_group" "main" {
  name     = "${local.prefix}-rg"
  location = var.location
  tags     = local.tags
}

resource "azurerm_virtual_network" "main" {
  name                = "${local.prefix}-vnet"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  address_space       = ["10.0.0.0/16"]
  tags                = local.tags
}

resource "azurerm_subnet" "web" {
  name                 = "web-subnet"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = ["10.0.1.0/24"]
}

resource "azurerm_subnet" "data" {
  name                 = "data-subnet"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = ["10.0.2.0/24"]
}

resource "azurerm_network_security_group" "web" {
  name                = "${local.prefix}-web-nsg"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  tags                = local.tags

  security_rule {
    name                       = "Allow-HTTP"
    priority                   = 100
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "80"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }

  security_rule {
    name                       = "Allow-HTTPS"
    priority                   = 110
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "443"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }
}

resource "azurerm_subnet_network_security_group_association" "web" {
  subnet_id                 = azurerm_subnet.web.id
  network_security_group_id = azurerm_network_security_group.web.id
}
```

**outputs.tf:**
```hcl
output "resource_group_name" {
  value = azurerm_resource_group.main.name
}

output "vnet_id" {
  value = azurerm_virtual_network.main.id
}

output "web_subnet_id" {
  value = azurerm_subnet.web.id
}
```

```bash
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply -auto-approve

# Verify in Azure
az network vnet list --resource-group tflab-dev-rg --output table
az network nsg list --resource-group tflab-dev-rg --output table

# Check dependency graph
terraform graph > graph.dot
# Paste content at https://dreampuf.github.io/GraphvizOnline/ to visualise

# Clean up
terraform destroy -auto-approve
cd .. && rm -rf terraform-lab-3
```

---

---

## Lesson 4 — Terraform State

> **Level:** Beginner → Intermediate
> **Goal:** Deeply understand state — the most critical Terraform concept

---

### 4.1 Why State Exists

**The Problem Terraform State Solves:**

Cloud APIs are not like databases where you can query "give me everything Terraform created." When you run `terraform plan`, Terraform needs to know:
1. What infrastructure currently exists in the cloud
2. What YOU created (vs what exists from other tools or manual actions)
3. The mapping between your HCL resource names and actual cloud resource IDs

The state file solves all three. It maps `azurerm_resource_group.main` → `/subscriptions/xxx/resourceGroups/myapp-rg` along with all attributes of that resource.

---

### 4.2 What the State File Contains

```json
{
  "version": 4,
  "terraform_version": "1.6.0",
  "resources": [
    {
      "mode": "managed",
      "type": "azurerm_resource_group",
      "name": "main",
      "provider": "provider[\"registry.terraform.io/hashicorp/azurerm\"]",
      "instances": [
        {
          "schema_version": 0,
          "attributes": {
            "id": "/subscriptions/xxx/resourceGroups/myapp-dev-rg",
            "location": "centralindia",
            "name": "myapp-dev-rg",
            "tags": {
              "Environment": "dev",
              "ManagedBy": "Terraform"
            }
          }
        }
      ]
    }
  ]
}
```

---

### 4.3 The State Refresh

During `terraform plan`, Terraform can refresh state against the actual cloud:

```bash
# Plan with refresh (default — queries cloud APIs)
terraform plan

# Plan without refresh (faster, uses cached state — risky if manual changes made)
terraform plan -refresh=false

# Refresh state only (update state file to match reality, no changes made)
terraform apply -refresh-only
```

---

### 4.4 Terraform State Commands

```bash
# List all resources in state
terraform state list

# Show details of one resource
terraform state show azurerm_resource_group.main
terraform state show "azurerm_subnet.main[\"web\"]"   # for_each resource

# Move a resource in state (rename or move to module)
terraform state mv azurerm_resource_group.old_name azurerm_resource_group.new_name
terraform state mv azurerm_resource_group.main module.networking.azurerm_resource_group.main

# Remove a resource from state (stop managing it — does NOT delete from cloud)
terraform state rm azurerm_resource_group.main
# Use case: hand off resource to another team's Terraform project

# Import an existing cloud resource into state
terraform import azurerm_resource_group.main /subscriptions/xxx/resourceGroups/myapp-rg
# Use case: bring manually-created resource under Terraform management

# Pull remote state to local file
terraform state pull > current_state.json

# Push local state to remote backend
terraform state push current_state.json   # Use with extreme caution
```

---

### 4.5 The Import Workflow — Adopting Existing Infrastructure

One of the most common real-world tasks: bringing manually-created infrastructure under Terraform management.

```bash
# Step 1: Write the Terraform resource block matching the existing resource
cat >> main.tf << 'EOF'
resource "azurerm_virtual_network" "existing" {
  # Fill in the attributes matching the existing VNet
  name                = "existing-vnet"
  resource_group_name = "existing-rg"
  location            = "centralindia"
  address_space       = ["10.0.0.0/16"]
}
EOF

# Step 2: Import the existing resource into state
terraform import azurerm_virtual_network.existing \
  /subscriptions/<sub-id>/resourceGroups/existing-rg/providers/Microsoft.Network/virtualNetworks/existing-vnet

# Step 3: Run plan to see if your code matches reality
terraform plan
# Goal: "No changes. Your infrastructure matches the configuration."
# If plan shows changes, update your .tf file to match the actual resource attributes

# Step 4: Once plan is clean, you manage this resource with Terraform
```

**Terraform v1.5+ Import Block (declarative import):**
```hcl
# In your .tf file — no CLI import command needed
import {
  to = azurerm_virtual_network.existing
  id = "/subscriptions/<sub-id>/resourceGroups/existing-rg/providers/Microsoft.Network/virtualNetworks/existing-vnet"
}

resource "azurerm_virtual_network" "existing" {
  name                = "existing-vnet"
  resource_group_name = "existing-rg"
  location            = "centralindia"
  address_space       = ["10.0.0.0/16"]
}
```

---

### 4.6 Practice Questions — Lessons 2–4

**Q1.** What happens if two engineers run `terraform apply` at the same time on the same infrastructure with local state?

<details>
<summary>Answer</summary>

Both engineers read the same state, compute their plans, and apply. The second one's state file write overwrites the first's, potentially losing the record of resources the first engineer created. In the worst case, the second apply might try to create resources that were already created (duplicates) or leave the state inconsistent with reality. This is why remote state with locking is non-negotiable in team environments.

</details>

---

**Q2.** Your team manually deleted a resource group in the Azure portal that Terraform was managing. What happens when you run `terraform plan` next?

<details>
<summary>Answer</summary>

During `terraform plan`, Terraform refreshes state by querying Azure. When it tries to fetch the resource group, Azure returns 404. Terraform notes this discrepancy. The plan output shows `+` (create) for the resource group and all resources that were in it — Terraform will recreate them to match the desired state in your code. This is the "drift detection and correction" behaviour.

</details>

---

---

## Lesson 5 — Variables and Outputs

> **Level:** Beginner → Intermediate
> **Goal:** Make configurations reusable and discoverable

---

### 5.1 Input Variables — Complete Reference

Variables make your Terraform code reusable across environments and teams.

```hcl
# variables.tf — variable DECLARATIONS (not values)
variable "vm_size" {
  description = "Azure VM size"  # Always write descriptions — future you will thank you
  type        = string
  default     = "Standard_B2s"   # Used if not provided
}

variable "vm_count" {
  description = "Number of VMs to create"
  type        = number
  default     = 2
}

variable "enable_diagnostics" {
  description = "Enable diagnostic settings"
  type        = bool
  default     = false
}

variable "allowed_ports" {
  description = "List of allowed inbound ports"
  type        = list(number)
  default     = [80, 443]
}

variable "tags" {
  description = "Resource tags"
  type        = map(string)
  default     = {}
}

# Complex object type
variable "database_config" {
  description = "Database configuration"
  type = object({
    sku_name    = string
    storage_mb  = number
    backup_days = number
    geo_backup  = bool
  })
  default = {
    sku_name    = "GP_Standard_D2s_v3"
    storage_mb  = 32768
    backup_days = 7
    geo_backup  = false
  }
}

# Sensitive variable — value masked in logs
variable "db_password" {
  description = "Database administrator password"
  type        = string
  sensitive   = true  # Terraform will never print this in output
}

# Variable with validation
variable "environment" {
  description = "Deployment environment"
  type        = string

  validation {
    condition     = contains(["dev", "staging", "production"], var.environment)
    error_message = "environment must be one of: dev, staging, production"
  }
}
```

---

### 5.2 How to Set Variable Values

**Priority order (highest to lowest):**

```
1. -var flag on CLI
2. -var-file flag on CLI
3. *.auto.tfvars files (auto-loaded)
4. terraform.tfvars file (auto-loaded)
5. Environment variables TF_VAR_<name>
6. Default value in variable declaration
7. Interactive prompt (if no value provided and no default)
```

```bash
# Method 1: CLI flag (highest priority)
terraform apply -var="environment=production" -var="vm_count=5"

# Method 2: var-file flag
terraform apply -var-file="production.tfvars"

# Method 3: Environment variables (great for CI/CD secrets)
export TF_VAR_db_password="mysecretpassword"
export TF_VAR_environment="production"
terraform apply

# Method 4: terraform.tfvars (auto-loaded if present)
# File: terraform.tfvars
# environment = "dev"
# vm_count    = 2

# Method 5: Named tfvars files (for multiple environments)
terraform apply -var-file="environments/production.tfvars"
```

**Environment-specific tfvars files:**
```
project/
├── main.tf
├── variables.tf
├── outputs.tf
└── environments/
    ├── dev.tfvars
    ├── staging.tfvars
    └── production.tfvars
```

**environments/production.tfvars:**
```hcl
environment = "production"
location    = "centralindia"
vm_size     = "Standard_D4s_v5"
vm_count    = 5

database_config = {
  sku_name    = "GP_Standard_D4s_v3"
  storage_mb  = 131072
  backup_days = 35
  geo_backup  = true
}

tags = {
  Team       = "platform"
  CostCenter = "tech-001"
}
```

---

### 5.3 Local Values — Computed Intermediates

Locals are computed once and reused throughout the configuration. They avoid repetition and keep expressions readable.

```hcl
locals {
  # Name prefix used everywhere
  name_prefix = "${var.project_name}-${var.environment}"

  # Conditional logic
  is_production = var.environment == "production"

  # Dynamic compute
  vm_size = local.is_production ? "Standard_D4s_v5" : "Standard_B2s"
  vm_count = local.is_production ? 3 : 1

  # Merged tags
  common_tags = merge(var.tags, {
    Project     = var.project_name
    Environment = var.environment
    ManagedBy   = "Terraform"
    Repository  = "github.com/myorg/infra"
  })

  # Build a list
  all_subnet_ids = concat(
    azurerm_subnet.web[*].id,
    azurerm_subnet.app[*].id
  )
}

# Use locals
resource "azurerm_resource_group" "main" {
  name     = "${local.name_prefix}-rg"
  location = var.location
  tags     = local.common_tags
}
```

---

### 5.4 Outputs — Exposing Values

Outputs expose information about your infrastructure to:
- Humans (printed after `terraform apply`)
- Other Terraform configurations (via remote state)
- CI/CD pipelines (`terraform output -json`)

```hcl
output "resource_group_name" {
  description = "Name of the created resource group"
  value       = azurerm_resource_group.main.name
}

output "web_app_url" {
  description = "Public URL of the web application"
  value       = "https://${azurerm_linux_web_app.main.default_hostname}"
}

output "database_fqdn" {
  description = "Database server fully qualified domain name"
  value       = azurerm_postgresql_flexible_server.main.fqdn
  sensitive   = true  # Will not be printed in plain text
}

output "all_vm_ips" {
  description = "Public IPs of all VM instances"
  value       = azurerm_public_ip.main[*].ip_address
}

output "subnet_ids" {
  description = "Map of subnet names to IDs"
  value = {
    for name, subnet in azurerm_subnet.main :
    name => subnet.id
  }
}
```

```bash
# View all outputs
terraform output

# Get specific output value (for scripting)
terraform output web_app_url

# Get all outputs as JSON (for CI/CD pipelines)
terraform output -json

# Get sensitive output (force reveal)
terraform output -raw database_fqdn
```

---

### 5.5 Hands-On Lab 5 — Parameterised Infrastructure

```bash
mkdir terraform-lab-5 && cd terraform-lab-5
```

Create **variables.tf**, **main.tf**, **outputs.tf**, and **environments/dev.tfvars** as shown in the lessons above, then:

```bash
terraform init

# Deploy dev environment
terraform plan -var-file="environments/dev.tfvars"
terraform apply -var-file="environments/dev.tfvars" -auto-approve

# View outputs
terraform output
terraform output -json

# Change environment to staging
terraform plan -var-file="environments/staging.tfvars"
# Notice different sizes/counts in the plan

# Destroy dev
terraform destroy -var-file="environments/dev.tfvars" -auto-approve
cd .. && rm -rf terraform-lab-5
```

---

---

# PHASE 2 — INTERMEDIATE

---

## Lesson 6 — Terraform Modules

> **Level:** Intermediate
> **Goal:** Build and use reusable modules — the foundation of scalable IaC

---

### 6.1 What is a Terraform Module?

A module is simply a directory containing `.tf` files. Every Terraform configuration you've written so far IS a module — the "root module." Modules become powerful when you call them from other modules, creating reusable infrastructure components.

**Without modules — copy-paste anti-pattern:**
```hcl
# dev/main.tf
resource "azurerm_resource_group" "dev" { name = "myapp-dev-rg" ... }
resource "azurerm_virtual_network" "dev" { ... 40 more lines ... }
resource "azurerm_subnet" "dev_web" { ... }
resource "azurerm_subnet" "dev_app" { ... }

# production/main.tf  ← copy of dev with different values
resource "azurerm_resource_group" "prod" { name = "myapp-prod-rg" ... }
resource "azurerm_virtual_network" "prod" { ... 40 more lines ... }
resource "azurerm_subnet" "prod_web" { ... }
resource "azurerm_subnet" "prod_app" { ... }
```

**With modules — reusable, single source of truth:**
```hcl
# Modules defined once in modules/networking/
# Called multiple times with different inputs:

module "dev_network" {
  source      = "./modules/networking"
  environment = "dev"
  cidr_block  = "10.0.0.0/16"
}

module "prod_network" {
  source      = "./modules/networking"
  environment = "production"
  cidr_block  = "10.1.0.0/16"
}
```

---

### 6.2 Module Structure

```
modules/
└── networking/              ← Module directory
    ├── main.tf              ← Module's resources
    ├── variables.tf         ← Module's inputs
    ├── outputs.tf           ← Module's outputs
    └── README.md            ← Module documentation (important!)
```

**modules/networking/variables.tf:**
```hcl
variable "project_name" {
  description = "Project name used in resource naming"
  type        = string
}

variable "environment" {
  description = "Deployment environment"
  type        = string
}

variable "location" {
  description = "Azure region"
  type        = string
}

variable "vnet_cidr" {
  description = "VNet address space CIDR"
  type        = string
  default     = "10.0.0.0/16"
}

variable "subnet_config" {
  description = "Map of subnet name to CIDR block"
  type        = map(string)
  default = {
    web  = "10.0.1.0/24"
    app  = "10.0.2.0/24"
    data = "10.0.3.0/24"
  }
}

variable "tags" {
  description = "Tags to apply to all resources"
  type        = map(string)
  default     = {}
}
```

**modules/networking/main.tf:**
```hcl
locals {
  prefix = "${var.project_name}-${var.environment}"
}

resource "azurerm_virtual_network" "main" {
  name                = "${local.prefix}-vnet"
  resource_group_name = var.resource_group_name
  location            = var.location
  address_space       = [var.vnet_cidr]
  tags                = var.tags
}

resource "azurerm_subnet" "main" {
  for_each = var.subnet_config

  name                 = "${each.key}-subnet"
  resource_group_name  = var.resource_group_name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = [each.value]
}

resource "azurerm_network_security_group" "web" {
  name                = "${local.prefix}-web-nsg"
  resource_group_name = var.resource_group_name
  location            = var.location
  tags                = var.tags

  security_rule {
    name                       = "Allow-HTTPS"
    priority                   = 100
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "443"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }
}
```

**modules/networking/outputs.tf:**
```hcl
output "vnet_id" {
  description = "ID of the created VNet"
  value       = azurerm_virtual_network.main.id
}

output "vnet_name" {
  description = "Name of the created VNet"
  value       = azurerm_virtual_network.main.name
}

output "subnet_ids" {
  description = "Map of subnet name to subnet ID"
  value       = { for k, v in azurerm_subnet.main : k => v.id }
}
```

---

### 6.3 Calling Modules

```hcl
# root/main.tf
resource "azurerm_resource_group" "main" {
  name     = "${var.project_name}-${var.environment}-rg"
  location = var.location
}

module "networking" {
  source = "./modules/networking"   # Relative path to module

  # Pass values to module's input variables
  project_name        = var.project_name
  environment         = var.environment
  location            = var.location
  resource_group_name = azurerm_resource_group.main.name
  vnet_cidr           = "10.0.0.0/16"

  subnet_config = {
    web  = "10.0.1.0/24"
    app  = "10.0.2.0/24"
    data = "10.0.3.0/24"
  }

  tags = local.common_tags
}

# Use module outputs
resource "azurerm_private_endpoint" "db" {
  subnet_id = module.networking.subnet_ids["data"]   # Use module output!
  # ...
}
```

---

### 6.4 Module Sources

```hcl
# Local path
module "network" {
  source = "./modules/networking"
}

# Terraform Registry (public modules)
module "network" {
  source  = "Azure/network/azurerm"
  version = "5.3.0"
}

# GitHub
module "network" {
  source = "github.com/myorg/terraform-modules//networking"
}

# GitHub with specific tag
module "network" {
  source = "git::https://github.com/myorg/terraform-modules.git//networking?ref=v2.1.0"
}

# Azure DevOps
module "network" {
  source = "git::https://dev.azure.com/myorg/terraform-modules/_git/networking"
}
```

---

### 6.5 Hands-On Lab 6 — Build a Module Library

```
terraform-module-lab/
├── modules/
│   └── networking/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
├── main.tf
├── variables.tf
├── outputs.tf
└── terraform.tfvars
```

Build the module structure from this lesson, deploy it, then call the same module twice with different CIDR ranges:

```hcl
# main.tf — call module twice
module "dev_network" {
  source              = "./modules/networking"
  project_name        = "myapp"
  environment         = "dev"
  location            = var.location
  resource_group_name = azurerm_resource_group.dev.name
  vnet_cidr           = "10.0.0.0/16"
}

module "staging_network" {
  source              = "./modules/networking"
  project_name        = "myapp"
  environment         = "staging"
  location            = var.location
  resource_group_name = azurerm_resource_group.staging.name
  vnet_cidr           = "10.1.0.0/16"
}
```

```bash
terraform init   # Downloads any registry modules
terraform plan
terraform apply -auto-approve
terraform state list   # Notice module resources: module.dev_network.azurerm_virtual_network.main
terraform destroy -auto-approve
```

---

---

## Lesson 7 — Data Sources and Dependencies

> **Level:** Intermediate

---

### 7.1 Data Sources — Read Existing Infrastructure

Data sources let you read information from existing infrastructure that Terraform didn't create (or that another Terraform project manages).

```hcl
# Read an existing resource group
data "azurerm_resource_group" "shared" {
  name = "shared-services-rg"   # Must already exist
}

# Read an existing Key Vault
data "azurerm_key_vault" "main" {
  name                = "company-kv"
  resource_group_name = data.azurerm_resource_group.shared.name
}

# Read a secret from Key Vault
data "azurerm_key_vault_secret" "db_password" {
  name         = "database-password"
  key_vault_id = data.azurerm_key_vault.main.id
}

# Use the secret
resource "azurerm_postgresql_flexible_server" "main" {
  administrator_password = data.azurerm_key_vault_secret.db_password.value
  # ...
}
```

**Common data sources:**
```hcl
# Current client (who is running Terraform)
data "azurerm_client_config" "current" {}
# Use: data.azurerm_client_config.current.tenant_id
#      data.azurerm_client_config.current.subscription_id
#      data.azurerm_client_config.current.object_id

# Existing VNet (to deploy into)
data "azurerm_virtual_network" "shared" {
  name                = "shared-vnet"
  resource_group_name = "network-rg"
}

# Existing subnet
data "azurerm_subnet" "app" {
  name                 = "app-subnet"
  virtual_network_name = data.azurerm_virtual_network.shared.name
  resource_group_name  = "network-rg"
}

# Available VM sizes in a region
data "azurerm_location" "main" {
  location = var.location
}

# Latest Ubuntu image
data "azurerm_platform_image" "ubuntu" {
  location  = var.location
  publisher = "Canonical"
  offer     = "0001-com-ubuntu-server-jammy"
  sku       = "22_04-lts-gen2"
}
```

---

### 7.2 Understanding Terraform Dependencies

Terraform builds a dependency graph from your configuration and applies changes in the correct order.

**Implicit dependencies (automatic — preferred):**
```hcl
# VNet depends on resource group because it REFERENCES it
resource "azurerm_resource_group" "main" {
  name     = "myapp-rg"
  location = "centralindia"
}

resource "azurerm_virtual_network" "main" {
  resource_group_name = azurerm_resource_group.main.name  # ← implicit dependency
  # Terraform sees this reference and knows: create RG first, then VNet
}
```

**Explicit dependencies (when needed):**
```hcl
# Role assignment should happen after AKS is fully configured
# even though it doesn't reference AKS directly
resource "azurerm_role_assignment" "aks_acr" {
  scope                = azurerm_container_registry.main.id
  role_definition_name = "AcrPull"
  principal_id         = azurerm_kubernetes_cluster.main.kubelet_identity[0].object_id

  depends_on = [azurerm_kubernetes_cluster.main]  # Explicit — wait for AKS
}
```

---

### 7.3 The `terraform graph` Command

```bash
# Generate dependency graph in DOT format
terraform graph

# Save and render as SVG
terraform graph | dot -Tsvg > infrastructure-graph.svg

# View in browser
open infrastructure-graph.svg

# Graph with specific module
terraform graph -module-depth=2
```

---

---

## Lesson 8 — Remote State and State Locking

> **Level:** Intermediate
> **Goal:** Set up production-grade shared state management

---

### 8.1 Why Remote State is Non-Negotiable in Teams

Local state (`terraform.tfstate` on your laptop) breaks the moment you have:
- More than one engineer on the team
- CI/CD pipelines running Terraform
- Multiple environments managed by the same team

**Remote state solves three problems:**

| Problem | Remote State Solution |
|---|---|
| State file on one laptop | State stored in shared cloud storage |
| Two people running at once | State locking prevents concurrent operations |
| Reading state from other projects | `terraform_remote_state` data source |

---

### 8.2 Azure Backend — Remote State in Azure Blob Storage

```bash
# Step 1: Create the storage for state (do this ONCE, manually or with a bootstrap script)
az group create --name terraform-state-rg --location centralindia

az storage account create \
  --name tfstate$(date +%s) \
  --resource-group terraform-state-rg \
  --location centralindia \
  --sku Standard_ZRS \              # Zone-redundant — state is critical data
  --encryption-services blob \
  --allow-blob-public-access false  # Never public

az storage container create \
  --name tfstate \
  --account-name <storage-account-name>

# Enable versioning — critical for state recovery
az storage account blob-service-properties update \
  --account-name <storage-account-name> \
  --resource-group terraform-state-rg \
  --enable-versioning true

# Enable soft delete — 30 day recovery window
az storage account blob-service-properties update \
  --account-name <storage-account-name> \
  --resource-group terraform-state-rg \
  --enable-delete-retention true \
  --delete-retention-days 30
```

**backend.tf:**
```hcl
terraform {
  backend "azurerm" {
    resource_group_name  = "terraform-state-rg"
    storage_account_name = "tfstate1234567890"      # Your unique storage account
    container_name       = "tfstate"
    key                  = "myapp/production/terraform.tfstate"
    # State file path within the container:
    # <project>/<environment>/terraform.tfstate
    # Organise with forward slashes for logical grouping
  }
}
```

```bash
# Migrate from local to remote state
terraform init
# Terraform detects new backend and asks if you want to migrate local state
# Type 'yes'
```

---

### 8.3 State Locking

When using Azure Blob backend, Terraform automatically uses **Azure Blob Lease** for state locking. Only one `terraform apply` can run at a time.

```bash
# See current lock (if someone else is running)
terraform plan
# Error: Error locking state: Error acquiring the state lock
# ...
# Lock ID: <lock-id>

# Force-unlock (only if you're SURE the lock is stale — e.g., a crashed pipeline)
terraform force-unlock <lock-id>
# WARNING: Only use this if you're certain no operation is in progress
```

---

### 8.4 Cross-Project State Reading

Read outputs from another project's state:

```hcl
# Read outputs from the networking project's state
data "terraform_remote_state" "networking" {
  backend = "azurerm"
  config = {
    resource_group_name  = "terraform-state-rg"
    storage_account_name = "tfstate1234567890"
    container_name       = "tfstate"
    key                  = "networking/production/terraform.tfstate"
  }
}

# Use the networking outputs
resource "azurerm_linux_web_app" "main" {
  virtual_network_subnet_id = data.terraform_remote_state.networking.outputs.app_subnet_id
  # ...
}
```

---

### 8.5 State Backend for AWS and GCP

**AWS S3 Backend:**
```hcl
terraform {
  backend "s3" {
    bucket         = "mycompany-terraform-state"
    key            = "myapp/production/terraform.tfstate"
    region         = "ap-south-1"
    encrypt        = true       # Encrypt state at rest
    dynamodb_table = "terraform-state-lock"  # DynamoDB for locking
  }
}
```

**GCP GCS Backend:**
```hcl
terraform {
  backend "gcs" {
    bucket = "mycompany-terraform-state"
    prefix = "myapp/production"
  }
}
```

**Terraform Cloud Backend (fully managed):**
```hcl
terraform {
  cloud {
    organization = "my-company"
    workspaces {
      name = "myapp-production"
    }
  }
}
```


---

---

## Lesson 9 — Terraform Functions and Expressions

> **Level:** Intermediate
> **Goal:** Use built-in functions to write powerful, dynamic configurations

---

### 9.1 Why Functions?

Real infrastructure is never perfectly static. Storage account names must be globally unique. VM sizes differ between environments. IP ranges are computed from a base CIDR. Functions let you express this dynamically without hardcoding or duplicating values.

---

### 9.2 String Functions

```hcl
locals {
  # lower / upper / title case
  name_lower = lower("MyApp")          # "myapp"
  name_upper = upper("myapp")          # "MYAPP"
  name_title = title("my app name")    # "My App Name"

  # trim whitespace
  clean = trimspace("  hello  ")       # "hello"

  # replace characters
  safe_name = replace(var.name, " ", "-")   # "my app" → "my-app"

  # string contains check
  is_prod = strcontains(var.environment, "prod")  # true/false

  # format (like printf)
  padded_id = format("%03d", 7)        # "007"
  message   = format("Hello, %s! You have %d messages", var.name, var.count)

  # string split and join
  parts    = split(",", "a,b,c")       # ["a", "b", "c"]
  rejoined = join("-", ["a", "b", "c"]) # "a-b-c"

  # substring
  short = substr("hello world", 0, 5)  # "hello"

  # starts/ends with
  is_dev = startswith(var.environment, "dev")
  is_rg  = endswith(var.resource_id, "-rg")
}
```

---

### 9.3 Numeric Functions

```hcl
locals {
  # min, max
  smallest = min(3, 1, 4, 1, 5)    # 1
  largest  = max(3, 1, 4, 1, 5)    # 5

  # absolute value
  distance = abs(-42)               # 42

  # ceiling / floor
  rounded_up   = ceil(1.1)         # 2
  rounded_down = floor(1.9)        # 1

  # convert to number
  num = tonumber("42")             # 42
}
```

---

### 9.4 Collection Functions

```hcl
locals {
  # length
  count = length(["a", "b", "c"])    # 3
  chars = length("hello")            # 5

  # contains (check if value is in list)
  has_web = contains(["web", "app", "data"], "web")   # true

  # lookup (safe map value access with default)
  size = lookup(var.vm_sizes, var.environment, "Standard_B2s")

  # merge maps
  all_tags = merge(local.base_tags, var.extra_tags)

  # keys and values
  tag_names   = keys(var.tags)      # ["Environment", "Project"]
  tag_values  = values(var.tags)    # ["production", "myapp"]

  # flatten — list of lists to flat list
  all_ips = flatten([
    ["10.0.1.1", "10.0.1.2"],
    ["10.0.2.1", "10.0.2.2"]
  ])   # ["10.0.1.1", "10.0.1.2", "10.0.2.1", "10.0.2.2"]

  # distinct — remove duplicates
  unique_regions = distinct(["centralindia", "southindia", "centralindia"])
  # ["centralindia", "southindia"]

  # compact — remove null/empty strings
  names = compact(["web", "", null, "api"])  # ["web", "api"]

  # slice — subset of a list
  first_two = slice(["a", "b", "c", "d"], 0, 2)  # ["a", "b"]

  # sort
  sorted_names = sort(["charlie", "alpha", "bravo"])  # ["alpha", "bravo", "charlie"]

  # zipmap — two lists into one map
  env_map = zipmap(
    ["web", "api", "db"],
    ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
  )
  # { "web" = "10.0.1.0/24", "api" = "10.0.2.0/24", "db" = "10.0.3.0/24" }

  # toset — list to set (unique, unordered)
  regions_set = toset(["centralindia", "southindia", "centralindia"])
  # {"centralindia", "southindia"}
}
```

---

### 9.5 Filesystem and Encoding Functions

```hcl
locals {
  # Read a file's content
  startup_script = file("${path.module}/scripts/startup.sh")
  nginx_config   = file("${path.module}/config/nginx.conf")

  # Read and base64-encode (for custom_data in VMs)
  encoded_script = filebase64("${path.module}/scripts/startup.sh")

  # JSON encode/decode
  config_json = jsonencode({
    database_host = azurerm_postgresql_flexible_server.main.fqdn
    redis_host    = azurerm_redis_cache.main.hostname
    environment   = var.environment
  })

  # YAML encode
  k8s_config = yamlencode({
    apiVersion = "v1"
    kind       = "ConfigMap"
  })

  # path references
  module_path = path.module    # Directory of the current module
  root_path   = path.root      # Directory of the root module
  cwd_path    = path.cwd       # Current working directory
}
```

---

### 9.6 Type Conversion Functions

```hcl
locals {
  # tostring, tonumber, tobool
  str_count = tostring(42)          # "42"
  num       = tonumber("3.14")      # 3.14
  flag      = tobool("true")        # true

  # tolist, toset, tomap
  my_list = tolist(toset(["c", "a", "b"]))  # ["a", "b", "c"] (sorted)

  # can — check if expression evaluates without error
  valid_number = can(tonumber(var.input))   # true if input is a number
}
```

---

### 9.7 Practical Function Examples

```hcl
# Generate a globally unique storage account name
resource "azurerm_storage_account" "main" {
  # Storage account names: 3-24 chars, lowercase alphanumeric only
  name = substr(
    lower(replace("${var.project_name}${var.environment}${random_id.suffix.hex}", "-", "")),
    0, 24
  )
  # ...
}

resource "random_id" "suffix" {
  byte_length = 4
}

# Dynamic subnet CIDR calculation
locals {
  subnets = {
    web  = cidrsubnet("10.0.0.0/16", 8, 1)   # 10.0.1.0/24
    app  = cidrsubnet("10.0.0.0/16", 8, 2)   # 10.0.2.0/24
    data = cidrsubnet("10.0.0.0/16", 8, 3)   # 10.0.3.0/24
    mgmt = cidrsubnet("10.0.0.0/16", 8, 4)   # 10.0.4.0/24
  }
}

# Count host addresses in a CIDR
locals {
  host_count = pow(2, 32 - parseint(split("/", "10.0.1.0/24")[1], 10)) - 2
  # = 254 usable hosts in a /24
}
```

---

---

## Lesson 10 — Workspaces and Environment Management

> **Level:** Intermediate

---

### 10.1 Terraform Workspaces

Workspaces allow you to have multiple state files for the same configuration. Each workspace has its own isolated state.

```bash
# List workspaces (default is always present)
terraform workspace list
# * default

# Create a new workspace
terraform workspace new dev
terraform workspace new staging
terraform workspace new production

# Switch workspace
terraform workspace select staging

# Show current workspace
terraform workspace show

# Delete workspace (must be empty — no resources)
terraform workspace delete dev
```

**Using workspace in configuration:**
```hcl
locals {
  # Use workspace name as environment
  environment = terraform.workspace

  # Different sizes per workspace
  vm_size = {
    default    = "Standard_B1s"
    dev        = "Standard_B2s"
    staging    = "Standard_D2s_v5"
    production = "Standard_D4s_v5"
  }[terraform.workspace]
}

resource "azurerm_resource_group" "main" {
  name     = "myapp-${terraform.workspace}-rg"
  location = var.location
}
```

---

### 10.2 Workspaces vs Separate Directories — When to Use Which

**Workspaces — good for:**
- Identical infrastructure in multiple environments (e.g., dev/staging/prod all use same module)
- Simple projects where all environments are nearly identical

**Separate directories — good for:**
- Environments with significantly different configurations
- When you want independent state and apply cycles
- When different teams own different environments
- Large organisations (this is the preferred enterprise pattern)

**Separate directories (recommended pattern):**
```
infrastructure/
├── modules/
│   ├── networking/
│   ├── compute/
│   └── database/
├── environments/
│   ├── dev/
│   │   ├── main.tf          ← Calls modules with dev config
│   │   ├── terraform.tfvars
│   │   └── backend.tf       ← Points to dev state
│   ├── staging/
│   │   ├── main.tf
│   │   ├── terraform.tfvars
│   │   └── backend.tf
│   └── production/
│       ├── main.tf
│       ├── terraform.tfvars
│       └── backend.tf       ← Points to production state
└── shared/
    ├── main.tf              ← Shared services (Key Vault, ACR, etc.)
    └── backend.tf
```

---

---

## Lesson 11 — Lifecycle Rules and Meta-Arguments

> **Level:** Intermediate

---

### 11.1 The Lifecycle Block

The `lifecycle` block controls how Terraform creates, updates, and destroys resources.

```hcl
resource "azurerm_postgresql_flexible_server" "main" {
  name     = "myapp-prod-db"
  # ...

  lifecycle {
    # Prevent accidental deletion — require explicit override to destroy
    prevent_destroy = true
    # Applying terraform destroy will fail with an error

    # Create the new resource BEFORE destroying the old one
    # Useful when you can't have any downtime during replacement
    create_before_destroy = true

    # Ignore changes to specific attributes (managed outside Terraform)
    ignore_changes = [
      tags["LastDeployment"],      # This tag changes on every deploy
      administrator_password,      # Managed by password rotation tool
    ]

    # Custom condition — plan fails if condition is false
    precondition {
      condition     = var.environment == "production" ? var.backup_retention_days >= 30 : true
      error_message = "Production databases must have at least 30 days of backup retention."
    }

    postcondition {
      condition     = self.fqdn != ""
      error_message = "Database FQDN was not assigned after creation."
    }
  }
}
```

---

### 11.2 `count` vs `for_each` — Choosing the Right One

```hcl
# count — use for simple numeric repetition
resource "azurerm_linux_virtual_machine" "web" {
  count = var.vm_count   # Creates vm_count identical VMs
  name  = "web-vm-${count.index}"
  # ...
}
# Access: azurerm_linux_virtual_machine.web[0], web[1], etc.
# Problem: If you remove item at index 1, Terraform recreates all VMs with index >= 1

# for_each — use when each resource has a unique identity
resource "azurerm_linux_virtual_machine" "web" {
  for_each = toset(["web-1", "web-2", "web-3"])
  name     = each.value
  # ...
}
# Access: azurerm_linux_virtual_machine.web["web-1"], web["web-2"], etc.
# Advantage: Removing "web-2" only removes that VM — others unchanged
```

> **Production Rule:** Prefer `for_each` over `count` for resources where each instance has a meaningful identity. `count` is fine for truly identical, interchangeable resources. The key difference: `for_each` tracks resources by key (stable), `count` tracks by index (unstable when items are removed from the middle).

---

### 11.3 `moved` Block — Refactoring Without Destroying

When you rename a resource in code or move it into a module, Terraform would normally destroy the old resource and create a new one. The `moved` block tells Terraform it's the same resource — just in a new location.

```hcl
# You renamed azurerm_resource_group.rg to azurerm_resource_group.main
moved {
  from = azurerm_resource_group.rg
  to   = azurerm_resource_group.main
}

# You moved a resource into a module
moved {
  from = azurerm_virtual_network.main
  to   = module.networking.azurerm_virtual_network.main
}

# You renamed a for_each resource key
moved {
  from = azurerm_subnet.main["old-name"]
  to   = azurerm_subnet.main["new-name"]
}
```

```bash
terraform plan
# Shows: azurerm_resource_group.rg will be moved to azurerm_resource_group.main
# No destroy, no create — just state update
```

---

---

# PHASE 3 — DEVOPS LEVEL

---

## Lesson 12 — Terraform with Azure (Deep Dive)

> **Level:** DevOps Engineer
> **Goal:** Build a complete, production-grade Azure infrastructure

---

### 12.1 Authentication Methods

```bash
# Method 1: Azure CLI (dev/local work)
az login
# Terraform automatically uses your az login session

# Method 2: Service Principal with client secret (CI/CD)
export ARM_CLIENT_ID="<app-id>"
export ARM_CLIENT_SECRET="<secret>"
export ARM_SUBSCRIPTION_ID="<subscription-id>"
export ARM_TENANT_ID="<tenant-id>"

# Method 3: Service Principal with certificate (more secure)
export ARM_CLIENT_ID="<app-id>"
export ARM_CLIENT_CERTIFICATE_PATH="/path/to/cert.pfx"
export ARM_SUBSCRIPTION_ID="<subscription-id>"
export ARM_TENANT_ID="<tenant-id>"

# Method 4: Managed Identity (Azure VMs/pipelines — no credentials!)
# Just configure the provider — authentication is automatic
provider "azurerm" {
  use_msi = true
  features {}
}

# Method 5: OIDC / Workload Identity Federation (GitHub Actions — no secrets!)
provider "azurerm" {
  use_oidc = true
  features {}
}
```

**Create a service principal for Terraform CI/CD:**
```bash
# Create service principal with Contributor on subscription
az ad sp create-for-rbac \
  --name "terraform-ci" \
  --role Contributor \
  --scopes /subscriptions/<subscription-id> \
  --output json
# Save the output: appId, password, tenant

# Narrow the scope to resource group level (least privilege)
az ad sp create-for-rbac \
  --name "terraform-ci-myapp" \
  --role Contributor \
  --scopes /subscriptions/<sub-id>/resourceGroups/myapp-prod-rg \
  --output json
```

---

### 12.2 Complete Azure Web Application Infrastructure

```hcl
# Complete production web app stack
# Resource Group → VNet → App Service → PostgreSQL → Key Vault → Storage

terraform {
  required_version = ">= 1.5.0"
  required_providers {
    azurerm = { source = "hashicorp/azurerm", version = "~> 3.80" }
    random  = { source = "hashicorp/random",  version = "~> 3.5"  }
  }
  backend "azurerm" {
    resource_group_name  = "terraform-state-rg"
    storage_account_name = "tfstatemycompany"
    container_name       = "tfstate"
    key                  = "myapp/production/terraform.tfstate"
  }
}

provider "azurerm" { features {} }

locals {
  prefix = "${var.project_name}-${var.environment}"
  tags = {
    Project     = var.project_name
    Environment = var.environment
    ManagedBy   = "Terraform"
  }
}

# ─── RESOURCE GROUP ──────────────────────────────────────────────────
resource "azurerm_resource_group" "main" {
  name     = "${local.prefix}-rg"
  location = var.location
  tags     = local.tags
}

# ─── NETWORKING ──────────────────────────────────────────────────────
resource "azurerm_virtual_network" "main" {
  name                = "${local.prefix}-vnet"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  address_space       = ["10.0.0.0/16"]
  tags                = local.tags
}

resource "azurerm_subnet" "app" {
  name                 = "app-subnet"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = ["10.0.1.0/24"]

  delegation {
    name = "app-service-delegation"
    service_delegation {
      name    = "Microsoft.Web/serverFarms"
      actions = ["Microsoft.Network/virtualNetworks/subnets/action"]
    }
  }
}

resource "azurerm_subnet" "data" {
  name                 = "data-subnet"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = ["10.0.2.0/24"]

  service_endpoints = ["Microsoft.Storage", "Microsoft.Sql", "Microsoft.KeyVault"]
}

# ─── KEY VAULT ────────────────────────────────────────────────────────
data "azurerm_client_config" "current" {}

resource "azurerm_key_vault" "main" {
  name                = "${local.prefix}-kv"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  tenant_id           = data.azurerm_client_config.current.tenant_id
  sku_name            = "standard"

  enable_rbac_authorization = true
  purge_protection_enabled  = var.environment == "production"

  network_acls {
    default_action             = "Deny"
    bypass                     = "AzureServices"
    virtual_network_subnet_ids = [azurerm_subnet.data.id]
  }

  tags = local.tags
}

# ─── STORAGE ACCOUNT ─────────────────────────────────────────────────
resource "azurerm_storage_account" "main" {
  name                = lower(replace("${var.project_name}${var.environment}stor", "-", ""))
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location

  account_tier             = "Standard"
  account_replication_type = var.environment == "production" ? "ZRS" : "LRS"

  allow_nested_items_to_be_public = false
  min_tls_version                 = "TLS1_2"
  https_traffic_only_enabled      = true

  network_rules {
    default_action             = "Deny"
    virtual_network_subnet_ids = [azurerm_subnet.data.id]
    bypass                     = ["AzureServices"]
  }

  tags = local.tags
}

# ─── APP SERVICE ─────────────────────────────────────────────────────
resource "azurerm_service_plan" "main" {
  name                = "${local.prefix}-plan"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  os_type             = "Linux"
  sku_name            = var.environment == "production" ? "P2v3" : "B2"
  tags                = local.tags
}

resource "azurerm_linux_web_app" "main" {
  name                = "${local.prefix}-webapp"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  service_plan_id     = azurerm_service_plan.main.id

  https_only = true

  identity {
    type = "SystemAssigned"
  }

  site_config {
    always_on = var.environment == "production"

    application_stack {
      node_version = "18-lts"
    }

    health_check_path                 = "/health"
    health_check_eviction_time_in_min = 5
  }

  app_settings = {
    "ENVIRONMENT"                          = var.environment
    "STORAGE_ACCOUNT_NAME"                 = azurerm_storage_account.main.name
    "KEY_VAULT_URI"                        = azurerm_key_vault.main.vault_uri
    "APPLICATIONINSIGHTS_CONNECTION_STRING" = azurerm_application_insights.main.connection_string
  }

  virtual_network_subnet_id = azurerm_subnet.app.id

  tags = local.tags
}

# Give App Service access to Key Vault
resource "azurerm_role_assignment" "app_kv_reader" {
  scope                = azurerm_key_vault.main.id
  role_definition_name = "Key Vault Secrets User"
  principal_id         = azurerm_linux_web_app.main.identity[0].principal_id
}

# ─── APPLICATION INSIGHTS ─────────────────────────────────────────────
resource "azurerm_log_analytics_workspace" "main" {
  name                = "${local.prefix}-law"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  sku                 = "PerGB2018"
  retention_in_days   = var.environment == "production" ? 90 : 30
  tags                = local.tags
}

resource "azurerm_application_insights" "main" {
  name                = "${local.prefix}-insights"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  workspace_id        = azurerm_log_analytics_workspace.main.id
  application_type    = "web"
  tags                = local.tags
}

# ─── POSTGRESQL DATABASE ──────────────────────────────────────────────
resource "random_password" "db" {
  length           = 24
  special          = true
  override_special = "!#$%&*()-_=+[]{}<>?"
}

resource "azurerm_key_vault_secret" "db_password" {
  name         = "database-password"
  value        = random_password.db.result
  key_vault_id = azurerm_key_vault.main.id

  depends_on = [azurerm_role_assignment.tf_kv_admin]
}

resource "azurerm_postgresql_flexible_server" "main" {
  name                = "${local.prefix}-db"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location

  administrator_login    = "dbadmin"
  administrator_password = random_password.db.result

  sku_name   = var.environment == "production" ? "GP_Standard_D4s_v3" : "B_Standard_B1ms"
  version    = "15"
  storage_mb = var.environment == "production" ? 131072 : 32768

  backup_retention_days        = var.environment == "production" ? 35 : 7
  geo_redundant_backup_enabled = var.environment == "production"

  high_availability {
    mode                      = var.environment == "production" ? "ZoneRedundant" : "Disabled"
    standby_availability_zone = var.environment == "production" ? "2" : null
  }

  tags = local.tags

  lifecycle {
    prevent_destroy = true
    ignore_changes  = [administrator_password, zone, high_availability[0].standby_availability_zone]
  }
}
```

---

---

## Lesson 13 — Terraform with AWS

> **Level:** DevOps Engineer

---

### 13.1 AWS Provider Setup

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
  backend "s3" {
    bucket         = "mycompany-terraform-state"
    key            = "myapp/production/terraform.tfstate"
    region         = "ap-south-1"
    encrypt        = true
    dynamodb_table = "terraform-locks"
  }
}

provider "aws" {
  region = var.aws_region
  # Authentication via environment variables:
  # AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_SESSION_TOKEN
  # Or via AWS profile: profile = "mycompany-production"
  # Or Managed Identity / OIDC in CI/CD — no credentials needed
}
```

---

### 13.2 AWS Infrastructure — Complete Example

```hcl
# ─── VPC ────────────────────────────────────────────────────────────
resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  enable_dns_support   = true

  tags = merge(local.tags, { Name = "${local.prefix}-vpc" })
}

resource "aws_internet_gateway" "main" {
  vpc_id = aws_vpc.main.id
  tags   = merge(local.tags, { Name = "${local.prefix}-igw" })
}

# Public subnets (one per AZ)
resource "aws_subnet" "public" {
  count             = length(data.aws_availability_zones.available.names)
  vpc_id            = aws_vpc.main.id
  cidr_block        = cidrsubnet("10.0.0.0/16", 8, count.index)
  availability_zone = data.aws_availability_zones.available.names[count.index]
  map_public_ip_on_launch = true

  tags = merge(local.tags, {
    Name = "${local.prefix}-public-${count.index + 1}"
    "kubernetes.io/role/elb" = "1"   # Required for EKS load balancers
  })
}

# Private subnets
resource "aws_subnet" "private" {
  count             = length(data.aws_availability_zones.available.names)
  vpc_id            = aws_vpc.main.id
  cidr_block        = cidrsubnet("10.0.0.0/16", 8, count.index + 10)
  availability_zone = data.aws_availability_zones.available.names[count.index]

  tags = merge(local.tags, {
    Name = "${local.prefix}-private-${count.index + 1}"
    "kubernetes.io/role/internal-elb" = "1"
  })
}

# ─── SECURITY GROUP ──────────────────────────────────────────────────
resource "aws_security_group" "web" {
  name        = "${local.prefix}-web-sg"
  description = "Security group for web tier"
  vpc_id      = aws_vpc.main.id

  ingress {
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = local.tags
}

# ─── EC2 ─────────────────────────────────────────────────────────────
data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["099720109477"]   # Canonical
  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-*"]
  }
}

resource "aws_instance" "web" {
  count         = var.instance_count
  ami           = data.aws_ami.ubuntu.id
  instance_type = var.environment == "production" ? "t3.medium" : "t3.micro"
  subnet_id     = aws_subnet.private[count.index % length(aws_subnet.private)].id

  vpc_security_group_ids = [aws_security_group.web.id]
  iam_instance_profile   = aws_iam_instance_profile.web.name

  root_block_device {
    volume_type           = "gp3"
    volume_size           = 20
    delete_on_termination = true
    encrypted             = true
  }

  user_data = base64encode(templatefile("${path.module}/scripts/startup.sh", {
    environment = var.environment
    db_host     = aws_db_instance.main.endpoint
  }))

  tags = merge(local.tags, { Name = "${local.prefix}-web-${count.index + 1}" })
}

# ─── RDS DATABASE ────────────────────────────────────────────────────
resource "aws_db_subnet_group" "main" {
  name       = "${local.prefix}-db-subnet"
  subnet_ids = aws_subnet.private[*].id
  tags       = local.tags
}

resource "aws_db_instance" "main" {
  identifier        = "${local.prefix}-db"
  engine            = "postgres"
  engine_version    = "15.3"
  instance_class    = var.environment == "production" ? "db.r6g.xlarge" : "db.t3.micro"
  allocated_storage = var.environment == "production" ? 100 : 20
  storage_encrypted = true

  db_name  = var.db_name
  username = var.db_username
  password = random_password.db.result

  db_subnet_group_name   = aws_db_subnet_group.main.name
  vpc_security_group_ids = [aws_security_group.db.id]

  multi_az               = var.environment == "production"
  backup_retention_period = var.environment == "production" ? 35 : 7
  deletion_protection    = var.environment == "production"
  skip_final_snapshot    = var.environment != "production"

  tags = local.tags

  lifecycle {
    prevent_destroy = true
  }
}
```

---

---

## Lesson 14 — Terraform with GCP

> **Level:** DevOps Engineer

---

### 14.1 GCP Provider Setup

```hcl
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "~> 5.0"
    }
  }
  backend "gcs" {
    bucket = "mycompany-terraform-state"
    prefix = "myapp/production"
  }
}

provider "google" {
  project = var.gcp_project_id
  region  = var.gcp_region
  # Auth: GOOGLE_APPLICATION_CREDENTIALS env var pointing to service account JSON
  # Or: Workload Identity (no credentials in CI/CD)
  # Or: gcloud auth application-default login (local dev)
}
```

---

### 14.2 GCP Infrastructure Example

```hcl
# ─── VPC ────────────────────────────────────────────────────────────
resource "google_compute_network" "main" {
  name                    = "${local.prefix}-vpc"
  auto_create_subnetworks = false
  project                 = var.gcp_project_id
}

resource "google_compute_subnetwork" "app" {
  name          = "${local.prefix}-app-subnet"
  ip_cidr_range = "10.0.1.0/24"
  region        = var.gcp_region
  network       = google_compute_network.main.id
  project       = var.gcp_project_id

  log_config {
    aggregation_interval = "INTERVAL_5_SEC"
    flow_sampling        = 0.5
    metadata             = "INCLUDE_ALL_METADATA"
  }
}

# ─── FIREWALL RULES ──────────────────────────────────────────────────
resource "google_compute_firewall" "allow_https" {
  name    = "${local.prefix}-allow-https"
  network = google_compute_network.main.name
  project = var.gcp_project_id

  allow {
    protocol = "tcp"
    ports    = ["443"]
  }

  source_ranges = ["0.0.0.0/0"]
  target_tags   = ["web-server"]
}

# ─── COMPUTE ─────────────────────────────────────────────────────────
resource "google_compute_instance" "web" {
  name         = "${local.prefix}-web"
  machine_type = var.environment == "production" ? "n2-standard-4" : "e2-micro"
  zone         = "${var.gcp_region}-a"
  project      = var.gcp_project_id

  boot_disk {
    initialize_params {
      image = "ubuntu-os-cloud/ubuntu-2204-lts"
      size  = 20
      type  = "pd-ssd"
    }
  }

  network_interface {
    subnetwork = google_compute_subnetwork.app.id
  }

  service_account {
    email  = google_service_account.web.email
    scopes = ["cloud-platform"]
  }

  tags = ["web-server"]

  labels = {
    environment = var.environment
    managed_by  = "terraform"
  }
}

# ─── CLOUD SQL ───────────────────────────────────────────────────────
resource "google_sql_database_instance" "main" {
  name             = "${local.prefix}-db"
  database_version = "POSTGRES_15"
  region           = var.gcp_region
  project          = var.gcp_project_id

  settings {
    tier = var.environment == "production" ? "db-custom-4-15360" : "db-f1-micro"

    backup_configuration {
      enabled                        = true
      start_time                     = "03:00"
      point_in_time_recovery_enabled = var.environment == "production"
      backup_retention_settings {
        retained_backups = var.environment == "production" ? 35 : 7
      }
    }

    availability_type = var.environment == "production" ? "REGIONAL" : "ZONAL"

    ip_configuration {
      ipv4_enabled    = false
      private_network = google_compute_network.main.id
    }
  }

  deletion_protection = var.environment == "production"

  lifecycle {
    prevent_destroy = true
  }
}
```

---

---

## Lesson 15 — Terraform in CI/CD Pipelines

> **Level:** DevOps Engineer
> **Goal:** Automate infrastructure deployments safely

---

### 15.1 The Terraform CI/CD Pattern

```
Code pushed to feature branch
          │
          ▼
PR opened → CI runs:
  terraform fmt -check     ← Fail if not formatted
  terraform validate       ← Fail if syntax error
  terraform plan           ← Post plan as PR comment
          │
          ▼
PR reviewed and approved
          │
          ▼
Merged to main → CD runs:
  terraform plan -out=tfplan    ← Save plan
  manual/auto approval gate
  terraform apply tfplan        ← Apply EXACTLY the reviewed plan
          │
          ▼
State updated, infrastructure changed
```

---

### 15.2 GitHub Actions — Complete Terraform Pipeline

**.github/workflows/terraform.yml:**
```yaml
name: Terraform CI/CD

on:
  push:
    branches: [main]
    paths: ['infrastructure/**']
  pull_request:
    branches: [main]
    paths: ['infrastructure/**']

permissions:
  contents: read
  pull-requests: write   # Comment plan on PRs
  id-token: write        # OIDC auth to Azure

env:
  TF_WORKING_DIR: infrastructure/environments/production
  ARM_SUBSCRIPTION_ID: ${{ secrets.ARM_SUBSCRIPTION_ID }}
  ARM_TENANT_ID: ${{ secrets.ARM_TENANT_ID }}
  ARM_CLIENT_ID: ${{ secrets.ARM_CLIENT_ID }}   # For OIDC

jobs:
  # ─── VALIDATE AND PLAN ─────────────────────────────────────────────
  terraform-plan:
    name: Terraform Plan
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: ${{ env.TF_WORKING_DIR }}

    steps:
      - uses: actions/checkout@v4

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v3
        with:
          terraform_version: "1.6.0"

      - name: Azure Login (OIDC)
        uses: azure/login@v2
        with:
          client-id: ${{ secrets.ARM_CLIENT_ID }}
          tenant-id: ${{ secrets.ARM_TENANT_ID }}
          subscription-id: ${{ secrets.ARM_SUBSCRIPTION_ID }}

      - name: Terraform Format Check
        id: fmt
        run: terraform fmt -check -recursive
        continue-on-error: true

      - name: Terraform Init
        id: init
        run: terraform init

      - name: Terraform Validate
        id: validate
        run: terraform validate

      - name: Terraform Plan
        id: plan
        run: |
          terraform plan \
            -var-file="terraform.tfvars" \
            -out=tfplan \
            -no-color
        continue-on-error: true

      - name: Comment Plan on PR
        uses: actions/github-script@v7
        if: github.event_name == 'pull_request'
        with:
          script: |
            const output = `#### Terraform Format: \`${{ steps.fmt.outcome }}\`
            #### Terraform Init: \`${{ steps.init.outcome }}\`
            #### Terraform Validate: \`${{ steps.validate.outcome }}\`
            #### Terraform Plan: \`${{ steps.plan.outcome }}\`

            <details><summary>Show Plan</summary>

            \`\`\`terraform
            ${{ steps.plan.outputs.stdout }}
            \`\`\`

            </details>

            *Pushed by: @${{ github.actor }}, Action: \`${{ github.event_name }}\`*`;

            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: output
            })

      - name: Upload plan artifact
        uses: actions/upload-artifact@v4
        with:
          name: tfplan
          path: ${{ env.TF_WORKING_DIR }}/tfplan
          retention-days: 5

      - name: Fail if plan failed
        if: steps.plan.outcome == 'failure'
        run: exit 1

  # ─── APPLY (main branch only, after approval) ──────────────────────
  terraform-apply:
    name: Terraform Apply
    runs-on: ubuntu-latest
    needs: terraform-plan
    if: github.ref == 'refs/heads/main' && github.event_name == 'push'
    environment: production   # Requires approval in GitHub Environments
    defaults:
      run:
        working-directory: ${{ env.TF_WORKING_DIR }}

    steps:
      - uses: actions/checkout@v4

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v3
        with:
          terraform_version: "1.6.0"

      - name: Azure Login (OIDC)
        uses: azure/login@v2
        with:
          client-id: ${{ secrets.ARM_CLIENT_ID }}
          tenant-id: ${{ secrets.ARM_TENANT_ID }}
          subscription-id: ${{ secrets.ARM_SUBSCRIPTION_ID }}

      - name: Download plan artifact
        uses: actions/download-artifact@v4
        with:
          name: tfplan
          path: ${{ env.TF_WORKING_DIR }}

      - name: Terraform Init
        run: terraform init

      - name: Terraform Apply
        run: terraform apply -auto-approve tfplan
```

---

### 15.3 Azure DevOps Pipeline

```yaml
trigger:
  branches:
    include: [main]
  paths:
    include: ['infrastructure/*']

variables:
  TF_VERSION: '1.6.0'
  TF_WORKING_DIR: 'infrastructure/environments/production'
  BACKEND_RG: 'terraform-state-rg'
  BACKEND_SA: 'tfstatemycompany'
  BACKEND_CONTAINER: 'tfstate'
  BACKEND_KEY: 'myapp/production/terraform.tfstate'

stages:
  - stage: Plan
    jobs:
      - job: TerraformPlan
        pool:
          vmImage: ubuntu-latest
        steps:
          - task: TerraformInstaller@1
            inputs:
              terraformVersion: $(TF_VERSION)

          - task: TerraformTaskV4@4
            displayName: Terraform Init
            inputs:
              provider: azurerm
              command: init
              workingDirectory: $(TF_WORKING_DIR)
              backendServiceArm: MyAzureServiceConnection
              backendAzureRmResourceGroupName: $(BACKEND_RG)
              backendAzureRmStorageAccountName: $(BACKEND_SA)
              backendAzureRmContainerName: $(BACKEND_CONTAINER)
              backendAzureRmKey: $(BACKEND_KEY)

          - task: TerraformTaskV4@4
            displayName: Terraform Plan
            inputs:
              provider: azurerm
              command: plan
              workingDirectory: $(TF_WORKING_DIR)
              environmentServiceNameAzureRM: MyAzureServiceConnection
              commandOptions: '-var-file=terraform.tfvars -out=tfplan'

          - task: PublishPipelineArtifact@1
            inputs:
              targetPath: '$(TF_WORKING_DIR)/tfplan'
              artifact: 'tfplan'

  - stage: Apply
    dependsOn: Plan
    condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/main'))
    jobs:
      - deployment: TerraformApply
        environment: 'Production'   # Has approval gate in ADO Environments
        pool:
          vmImage: ubuntu-latest
        strategy:
          runOnce:
            deploy:
              steps:
                - task: DownloadPipelineArtifact@2
                  inputs:
                    artifact: 'tfplan'
                    path: $(TF_WORKING_DIR)

                - task: TerraformInstaller@1
                  inputs:
                    terraformVersion: $(TF_VERSION)

                - task: TerraformTaskV4@4
                  displayName: Terraform Init
                  inputs:
                    provider: azurerm
                    command: init
                    workingDirectory: $(TF_WORKING_DIR)
                    backendServiceArm: MyAzureServiceConnection
                    backendAzureRmResourceGroupName: $(BACKEND_RG)
                    backendAzureRmStorageAccountName: $(BACKEND_SA)
                    backendAzureRmContainerName: $(BACKEND_CONTAINER)
                    backendAzureRmKey: $(BACKEND_KEY)

                - task: TerraformTaskV4@4
                  displayName: Terraform Apply
                  inputs:
                    provider: azurerm
                    command: apply
                    workingDirectory: $(TF_WORKING_DIR)
                    environmentServiceNameAzureRM: MyAzureServiceConnection
                    commandOptions: '-auto-approve tfplan'
```

---

---

## Lesson 16 — Terraform Secrets Management

> **Level:** DevOps Engineer

---

### 16.1 The Golden Rule

> **Never store secrets in Terraform code, `.tfvars` files, or state files.**

Secrets in Terraform are tricky because even if you pass them as variables, the values can end up in:
- The state file (often in plaintext)
- Plan output logs
- CI/CD pipeline logs

---

### 16.2 Patterns for Secrets

**Pattern 1 — Environment Variables (simplest, for CI/CD):**
```bash
# Set in CI/CD pipeline (GitHub Actions secrets, Azure DevOps variables)
export TF_VAR_db_password="$DB_PASSWORD"
export TF_VAR_api_key="$API_KEY"
terraform apply
```

**Pattern 2 — Retrieve from Key Vault at apply time:**
```hcl
# Read from Azure Key Vault during plan/apply
# The value is used but never written to .tf files
data "azurerm_key_vault_secret" "db_password" {
  name         = "database-password"
  key_vault_id = data.azurerm_key_vault.main.id
}

resource "azurerm_postgresql_flexible_server" "main" {
  administrator_password = data.azurerm_key_vault_secret.db_password.value
  # ...
}
```

**Pattern 3 — Generate secrets with Terraform and store in Key Vault:**
```hcl
resource "random_password" "db" {
  length           = 32
  special          = true
  override_special = "!#$%&*()-_=+[]{}<>?"
}

# Store in Key Vault
resource "azurerm_key_vault_secret" "db_password" {
  name         = "database-password"
  value        = random_password.db.result
  key_vault_id = azurerm_key_vault.main.id

  # Note: random_password.db.result IS in the state file
  # Secure your state file with encryption and access controls
}

resource "azurerm_postgresql_flexible_server" "main" {
  administrator_password = random_password.db.result
  # ...
}
```

**Securing the state file (Azure):**
```bash
# Enable storage account encryption (default on Azure, verify it's enabled)
az storage account show \
  --name tfstatemycompany \
  --query "encryption.services.blob.enabled"

# Enable soft delete and versioning (already covered in Lesson 8)
# Restrict access to state storage — only CI/CD identity should have access
az role assignment create \
  --assignee <ci-cd-service-principal-id> \
  --role "Storage Blob Data Contributor" \
  --scope /subscriptions/<sub-id>/resourceGroups/terraform-state-rg/providers/Microsoft.Storage/storageAccounts/tfstatemycompany
```

---

---

## Lesson 17 — Terraform Drift Detection and Remediation

> **Level:** DevOps Engineer

---

### 17.1 What is Infrastructure Drift?

Drift occurs when the actual state of infrastructure diverges from what Terraform expects. Common causes:
- Someone made a manual change in the cloud console
- Another automation tool modified a resource
- The cloud provider changed a default value
- A resource was modified during an incident response

---

### 17.2 Detecting Drift

```bash
# Method 1: terraform plan (always run this)
terraform plan
# If drift exists, plan shows changes needed to get back to desired state

# Method 2: refresh-only plan (explicit drift check)
terraform plan -refresh-only
# Shows only changes to the state file — not your code
# "Changes to Outputs" and "Objects have changed outside of Terraform"

# Method 3: Apply refresh-only (update state to match reality, without changing infra)
terraform apply -refresh-only
# Useful when you WANT to accept the manual changes and update state to match
```

---

### 17.3 Drift Remediation Strategies

**Option 1 — Revert to Terraform's desired state:**
```bash
terraform plan   # Shows what manual changes were made
terraform apply  # Reverts manual changes, restores declared configuration
```

**Option 2 — Accept the manual change (update code to match):**
```bash
# 1. Run refresh-only to update state
terraform apply -refresh-only

# 2. Run plan to see what code changes are needed to match reality
terraform plan

# 3. Update .tf files to match the new reality
# 4. Run plan again — should show "No changes"
terraform plan
```

**Option 3 — Scheduled drift detection in CI/CD:**
```yaml
# GitHub Actions — run drift detection daily
name: Drift Detection

on:
  schedule:
    - cron: '0 6 * * *'   # Every day at 6am UTC

jobs:
  drift-check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: hashicorp/setup-terraform@v3

      - name: Terraform Init
        run: terraform init
        working-directory: infrastructure/environments/production

      - name: Check for Drift
        id: drift
        run: |
          terraform plan -refresh-only -detailed-exitcode
          # Exit code 0: no changes
          # Exit code 1: error
          # Exit code 2: changes detected (drift!)
        working-directory: infrastructure/environments/production
        continue-on-error: true

      - name: Alert on Drift
        if: steps.drift.outputs.exitcode == '2'
        uses: actions/github-script@v7
        with:
          script: |
            github.rest.issues.create({
              owner: context.repo.owner,
              repo: context.repo.repo,
              title: '⚠️ Infrastructure Drift Detected in Production',
              body: 'Terraform drift detected. Run `terraform plan -refresh-only` for details.',
              labels: ['infrastructure', 'urgent']
            })
```


---

---

# PHASE 4 — ADVANCED ARCHITECTURE

---

## Lesson 18 — Designing Reusable Module Libraries

> **Level:** Advanced
> **Goal:** Build an enterprise-grade module library

---

### 18.1 Module Design Principles

A well-designed module library is the foundation of a scalable IaC practice. These principles are what separate a team with consistent, reliable infrastructure from one that rewrites the same patterns in every project.

**The SOLID principles applied to Terraform modules:**

| Principle | In Terraform Terms |
|---|---|
| **Single Responsibility** | Each module does one thing well — `networking`, not `everything` |
| **Open/Closed** | Extendable via variables without modifying the module itself |
| **Interface Segregation** | Don't expose variables users don't need |
| **Dependency Inversion** | Modules take IDs as inputs, not resource objects |

---

### 18.2 Module Versioning Strategy

```hcl
# Use versioned modules from a registry or Git tag
# NEVER use unversioned sources in production
module "networking" {
  # BAD — no version, module can change unexpectedly
  source = "git::https://github.com/myorg/terraform-modules.git//networking"

  # GOOD — pinned to a specific release tag
  source = "git::https://github.com/myorg/terraform-modules.git//networking?ref=v2.3.0"
}

# Internal registry module with version constraint
module "networking" {
  source  = "registry.example.com/myorg/networking/azurerm"
  version = "~> 2.3"    # Accept 2.3.x but not 3.0.0
}
```

**Semantic versioning for modules:**
```
v1.0.0 — Initial release
v1.1.0 — New optional feature (backward compatible — bump minor)
v1.1.1 — Bug fix (backward compatible — bump patch)
v2.0.0 — Breaking change (required variable added, output removed — bump major)
```

---

### 18.3 Enterprise Module Library Structure

```
terraform-modules/               ← One Git repo for all modules
├── README.md
├── CHANGELOG.md
│
├── modules/
│   ├── networking/              ← VNet, subnets, NSGs
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   ├── README.md            ← REQUIRED: inputs, outputs, examples
│   │   └── examples/
│   │       └── basic/
│   │           └── main.tf      ← Working example consumers can copy
│   │
│   ├── compute/                 ← VMs, scale sets
│   ├── database/                ← PostgreSQL, SQL, Cosmos DB
│   ├── security/                ← Key Vault, managed identities
│   ├── monitoring/              ← Log Analytics, App Insights, alerts
│   ├── kubernetes/              ← AKS cluster
│   └── app-service/             ← App Service + Plan
│
└── .github/
    └── workflows/
        └── test.yml             ← Automated module testing with Terratest
```

---

### 18.4 Module README Template

Every module must have a README. This is non-negotiable in a team environment.

**modules/networking/README.md:**
```markdown
# Networking Module

Creates a Virtual Network with configurable subnets and NSGs.

## Usage

```hcl
module "networking" {
  source = "git::https://github.com/myorg/terraform-modules.git//modules/networking?ref=v2.3.0"

  project_name = "myapp"
  environment  = "production"
  location     = "centralindia"
  vnet_cidr    = "10.0.0.0/16"

  subnet_config = {
    web  = { cidr = "10.0.1.0/24", service_endpoints = [] }
    app  = { cidr = "10.0.2.0/24", service_endpoints = ["Microsoft.Sql"] }
    data = { cidr = "10.0.3.0/24", service_endpoints = ["Microsoft.Sql", "Microsoft.Storage"] }
  }
}
```

## Inputs

| Name | Type | Default | Description |
|---|---|---|---|
| project_name | string | — | Project name for resource naming |
| environment | string | — | Deployment environment |
| location | string | centralindia | Azure region |
| vnet_cidr | string | 10.0.0.0/16 | VNet address space |
| subnet_config | map(object) | see variables.tf | Subnet definitions |

## Outputs

| Name | Description |
|---|---|
| vnet_id | Resource ID of the created VNet |
| subnet_ids | Map of subnet name to subnet ID |
| nsg_ids | Map of NSG name to NSG ID |

## Requirements

| Terraform | azurerm provider |
|---|---|
| >= 1.5.0 | ~> 3.80 |
```
```

---

### 18.5 Testing Modules with Terratest

```go
// modules/networking/tests/networking_test.go
package test

import (
    "testing"
    "github.com/gruntwork-io/terratest/modules/terraform"
    "github.com/stretchr/testify/assert"
)

func TestNetworkingModule(t *testing.T) {
    t.Parallel()

    terraformOptions := &terraform.Options{
        TerraformDir: "../examples/basic",
        Vars: map[string]interface{}{
            "project_name": "test",
            "environment":  "terratest",
            "location":     "centralindia",
        },
    }

    defer terraform.Destroy(t, terraformOptions)
    terraform.InitAndApply(t, terraformOptions)

    vnetId := terraform.Output(t, terraformOptions, "vnet_id")
    assert.Contains(t, vnetId, "virtualNetworks")

    subnetIds := terraform.OutputMap(t, terraformOptions, "subnet_ids")
    assert.Contains(t, subnetIds, "web")
    assert.Contains(t, subnetIds, "app")
    assert.Contains(t, subnetIds, "data")
}
```

---

---

## Lesson 19 — Multi-Environment Infrastructure

> **Level:** Advanced

---

### 19.1 The Reference Architecture

```
infrastructure/
├── modules/                     ← Shared module library (or separate repo)
│   ├── networking/
│   ├── compute/
│   ├── database/
│   └── monitoring/
│
├── environments/
│   ├── _shared/                 ← Shared services (ACR, Key Vault, Log Analytics)
│   │   ├── main.tf
│   │   ├── outputs.tf
│   │   └── backend.tf           ← State: shared/terraform.tfstate
│   │
│   ├── dev/
│   │   ├── main.tf              ← Calls modules with dev-specific config
│   │   ├── terraform.tfvars     ← Dev variable values
│   │   └── backend.tf           ← State: environments/dev/terraform.tfstate
│   │
│   ├── staging/
│   │   ├── main.tf
│   │   ├── terraform.tfvars
│   │   └── backend.tf
│   │
│   └── production/
│       ├── main.tf
│       ├── terraform.tfvars
│       ├── backend.tf
│       └── PRODUCTION_NOTES.md  ← Document production-specific considerations
│
└── scripts/
    ├── deploy.sh                ← Wrapper script for CI/CD
    └── check-drift.sh
```

---

### 19.2 Environment Configuration Comparison

**environments/dev/terraform.tfvars:**
```hcl
environment = "dev"
location    = "centralindia"

# Compute — smaller, cheaper
vm_size     = "Standard_B2s"
vm_count    = 1
app_service_sku = "B1"

# Database — smallest tier, no HA
db_sku               = "B_Standard_B1ms"
db_storage_mb        = 32768
db_backup_days       = 7
db_geo_backup        = false
db_high_availability = false

# Storage — LRS (cheapest)
storage_replication = "LRS"

# Monitoring — short retention
log_retention_days = 30
```

**environments/production/terraform.tfvars:**
```hcl
environment = "production"
location    = "centralindia"

# Compute — production-grade
vm_size     = "Standard_D4s_v5"
vm_count    = 3
app_service_sku = "P2v3"

# Database — production HA with geo-backup
db_sku               = "GP_Standard_D4s_v3"
db_storage_mb        = 131072
db_backup_days       = 35
db_geo_backup        = true
db_high_availability = true

# Storage — ZRS (zone-redundant)
storage_replication = "ZRS"

# Monitoring — long retention for compliance
log_retention_days = 90
```

---

---

## Lesson 20 — Multi-Region Deployments

> **Level:** Advanced

---

### 20.1 Multi-Region with Provider Aliases

```hcl
# Configure two regions
provider "azurerm" {
  alias           = "primary"
  subscription_id = var.subscription_id
  features {}
}

provider "azurerm" {
  alias           = "secondary"
  subscription_id = var.subscription_id
  features {}
}

# Primary region resources
resource "azurerm_resource_group" "primary" {
  provider = azurerm.primary
  name     = "${local.prefix}-primary-rg"
  location = "centralindia"
}

resource "azurerm_resource_group" "secondary" {
  provider = azurerm.secondary
  name     = "${local.prefix}-secondary-rg"
  location = "southindia"
}

# Module called twice for each region
module "app_primary" {
  source = "./modules/app-service"
  providers = {
    azurerm = azurerm.primary
  }
  resource_group_name = azurerm_resource_group.primary.name
  location            = azurerm_resource_group.primary.location
  environment         = var.environment
  is_primary          = true
}

module "app_secondary" {
  source = "./modules/app-service"
  providers = {
    azurerm = azurerm.secondary
  }
  resource_group_name = azurerm_resource_group.secondary.name
  location            = azurerm_resource_group.secondary.location
  environment         = var.environment
  is_primary          = false
}

# Azure Front Door routing to both regions
resource "azurerm_cdn_frontdoor_profile" "main" {
  name                = "${local.prefix}-afd"
  resource_group_name = azurerm_resource_group.primary.name
  sku_name            = "Standard_AzureFrontDoor"
}

resource "azurerm_cdn_frontdoor_origin_group" "main" {
  name                     = "app-origins"
  cdn_frontdoor_profile_id = azurerm_cdn_frontdoor_profile.main.id
  session_affinity_enabled = false

  load_balancing {
    sample_size                        = 4
    successful_samples_required        = 3
    additional_latency_in_milliseconds = 50
  }

  health_probe {
    path                = "/health"
    request_type        = "HEAD"
    protocol            = "Https"
    interval_in_seconds = 30
  }
}

resource "azurerm_cdn_frontdoor_origin" "primary" {
  name                          = "primary-origin"
  cdn_frontdoor_origin_group_id = azurerm_cdn_frontdoor_origin_group.main.id
  enabled                       = true
  host_name                     = module.app_primary.default_hostname
  priority                      = 1
  weight                        = 1000
}

resource "azurerm_cdn_frontdoor_origin" "secondary" {
  name                          = "secondary-origin"
  cdn_frontdoor_origin_group_id = azurerm_cdn_frontdoor_origin_group.main.id
  enabled                       = true
  host_name                     = module.app_secondary.default_hostname
  priority                      = 2    # Lower priority — failover only
  weight                        = 1000
}
```

---

---

## Lesson 21 — Infrastructure Cost Optimisation

> **Level:** Advanced

---

### 21.1 Cost-Optimised Terraform Patterns

```hcl
# 1. Environment-conditional resource sizes
locals {
  is_prod = var.environment == "production"

  app_sku   = local.is_prod ? "P2v3"              : "B1"
  db_sku    = local.is_prod ? "GP_Standard_D4s_v3" : "B_Standard_B1ms"
  vm_size   = local.is_prod ? "Standard_D4s_v5"   : "Standard_B2s"
  redundancy = local.is_prod ? "ZRS"               : "LRS"
}

# 2. Auto-shutdown for non-production VMs (saves ~60% cost)
resource "azurerm_dev_test_global_vm_shutdown_schedule" "dev_vm" {
  count              = var.environment != "production" ? 1 : 0
  virtual_machine_id = azurerm_linux_virtual_machine.main.id
  location           = var.location

  enabled                        = true
  daily_recurrence_time          = "1900"  # 7pm
  timezone                       = "India Standard Time"
  notification_settings { enabled = false }
}

# 3. Spot instances for non-critical workloads
resource "azurerm_linux_virtual_machine" "worker" {
  # ...
  priority        = var.environment != "production" ? "Spot" : "Regular"
  eviction_policy = var.environment != "production" ? "Deallocate" : null
  max_bid_price   = var.environment != "production" ? 0.05 : -1
}

# 4. Lifecycle management for storage (move blobs to cheaper tiers)
resource "azurerm_storage_management_policy" "main" {
  storage_account_id = azurerm_storage_account.main.id

  rule {
    name    = "lifecycle-to-cool-and-archive"
    enabled = true
    filters {
      blob_types = ["blockBlob"]
    }
    actions {
      base_blob {
        tier_to_cool_after_days_since_modification_greater_than    = 30
        tier_to_archive_after_days_since_modification_greater_than = 90
        delete_after_days_since_modification_greater_than          = 365
      }
      snapshot {
        delete_after_days_since_creation_greater_than = 30
      }
    }
  }
}

# 5. Reserved capacity for production (up to 72% savings vs pay-as-you-go)
# Configure Azure Reservations in the portal for your known base capacity
# Terraform manages the infrastructure — reservations are a billing concept
```

---

### 21.2 Infracost — Cost Estimation in CI/CD

```bash
# Install infracost
brew install infracost
infracost auth login

# Estimate cost before applying
infracost breakdown --path .
infracost diff --path . --compare-to previous_plan.json
```

```yaml
# GitHub Actions — add cost estimate to PR
- name: Infracost estimate
  uses: infracost/actions/setup@v2
  with:
    api-key: ${{ secrets.INFRACOST_API_KEY }}

- name: Generate cost estimate
  run: |
    infracost diff \
      --path ${{ env.TF_WORKING_DIR }} \
      --format json \
      --out-file /tmp/infracost.json
    infracost comment github \
      --path /tmp/infracost.json \
      --repo $GITHUB_REPOSITORY \
      --pull-request ${{ github.event.pull_request.number }} \
      --github-token ${{ secrets.GITHUB_TOKEN }}
```

---

---

## Lesson 22 — Infrastructure Dependency Graphs and Change Management

> **Level:** Advanced

---

### 22.1 Understanding the Dependency Graph

```bash
# Generate dependency graph
terraform graph > graph.dot

# Visualise (requires graphviz)
terraform graph | dot -Tsvg > graph.svg
open graph.svg

# Generate just the plan graph
terraform graph -type=plan | dot -Tsvg > plan-graph.svg

# Generate destroy graph
terraform graph -type=plan-destroy | dot -Tsvg > destroy-graph.svg
```

---

### 22.2 Targeted Operations — Change One Resource at a Time

```bash
# Plan only specific resources
terraform plan -target=azurerm_linux_web_app.main
terraform plan -target=module.networking
terraform plan -target=azurerm_subnet.main[\"web\"]

# Apply only specific resources (use sparingly)
terraform apply -target=azurerm_linux_web_app.main -auto-approve

# Destroy only specific resource
terraform destroy -target=azurerm_linux_virtual_machine.test -auto-approve
```

> **Warning:** `-target` is a last resort for production incidents. Regular use leads to state drift and partial configuration. Always follow up with a full `terraform apply` to ensure consistency.

---

### 22.3 Replace Force Recreate

```bash
# Force recreation of a specific resource (replace in-place)
terraform apply -replace=azurerm_linux_virtual_machine.web[0]

# Useful when: VM is in a bad state, cert needs rotation, disk corruption
# Equivalent to destroy + create, but done in the right order
```

---

---

# PHASE 5 — EXPERT LEVEL

---

## Lesson 23 — Terraform Internals

> **Level:** Expert

---

### 23.1 How Terraform Plan Works Internally

```
Step 1: Parse .tf files
  └── Read all .tf files in working directory
  └── Build abstract syntax tree
  └── Resolve references, validate types

Step 2: Load state
  └── Read terraform.tfstate (local or remote)
  └── Build "prior state" object

Step 3: Refresh (optional — enabled by default)
  └── For each resource in state:
        └── Call provider READ function
        └── Compare returned attributes to state
        └── Note any "refreshed" differences

Step 4: Build dependency graph
  └── Create directed acyclic graph (DAG)
  └── Nodes = resources
  └── Edges = dependencies (implicit + explicit)
  └── Topological sort = apply order

Step 5: Compute diff
  └── For each resource:
        └── Not in state + in config = CREATE
        └── In state + not in config = DESTROY
        └── In both = compute attribute diff = UPDATE or REPLACE

Step 6: Output plan
  └── Show create/update/destroy actions
  └── Optionally save to .tfplan binary file
```

---

### 23.2 Provider Plugin Architecture

```
Terraform Core
      │  gRPC (HashiCorp Plugin Protocol v5/v6)
      ▼
Provider Plugin (azurerm, aws, google)
      │
      │  Provider SDK
      ▼
Provider REST API calls
      │
      ▼
Cloud API (Azure Resource Manager, AWS, GCP)
```

```bash
# See provider plugin details
cat .terraform/providers/registry.terraform.io/hashicorp/azurerm/3.80.0/linux_amd64/terraform-provider-azurerm_v3.80.0_x5

# Provider protocol version
terraform providers schema -json | jq '.provider_schemas | keys'

# Download provider without init
terraform providers lock -platform=linux_amd64 -platform=darwin_amd64
```

---

### 23.3 The Lock File

`.terraform.lock.hcl` pins exact provider versions and checksums. Always commit it to Git.

```hcl
# .terraform.lock.hcl (auto-generated, commit to Git)
provider "registry.terraform.io/hashicorp/azurerm" {
  version     = "3.80.0"
  constraints = "~> 3.80"
  hashes = [
    "h1:abc123...",       # Hash of provider binary for this platform
    "zh:def456...",       # Hash for different platforms
  ]
}
```

```bash
# Update lock file after changing version constraints
terraform providers lock \
  -platform=linux_amd64 \
  -platform=darwin_amd64 \
  -platform=windows_amd64
```

---

---

## Lesson 24 — State Debugging and Corruption Recovery

> **Level:** Expert

---

### 24.1 State Corruption Scenarios and Recovery

**Scenario 1 — Resource in state but not in config (orphaned state):**
```bash
terraform state list
# Shows azurerm_resource_group.old_rg — but it's not in your .tf files

# Option A: Remove from state (resource stays in Azure, unmanaged)
terraform state rm azurerm_resource_group.old_rg

# Option B: Add back to config to bring under management again
# Write the resource block, then run: terraform plan (should show no changes)
```

**Scenario 2 — Resource in config but Terraform says it already exists:**
```bash
terraform apply
# Error: A resource with the ID "/subscriptions/.../resourceGroups/myapp-rg" already exists

# The resource exists in Azure but not in Terraform state
# Import it:
terraform import azurerm_resource_group.main \
  /subscriptions/<sub-id>/resourceGroups/myapp-rg

# Then run plan — should show no changes if config matches reality
terraform plan
```

**Scenario 3 — State file is corrupted or lost:**
```bash
# With Azure Blob backend — recover from versioning
az storage blob list \
  --account-name tfstatemycompany \
  --container-name tfstate \
  --include v \
  --query "[?name=='myapp/production/terraform.tfstate']" \
  --output table

# Download a previous version
az storage blob download \
  --account-name tfstatemycompany \
  --container-name tfstate \
  --name "myapp/production/terraform.tfstate" \
  --version-id <version-id> \
  --file recovered_state.json

# Push recovered state
terraform state push recovered_state.json
```

**Scenario 4 — Stale lock file (crashed pipeline left lock):**
```bash
terraform plan
# Error: Error acquiring the state lock
# ...
# Lock Info:
#   ID: abc123-def456
#   Who: runner@github-actions

# Verify the pipeline is actually dead (not still running!)
# Then force-unlock:
terraform force-unlock abc123-def456
```

---

### 24.2 Advanced State Manipulation

```bash
# Pull state to local file for inspection
terraform state pull > current_state.json

# Examine state structure
cat current_state.json | jq '.resources[] | {type, name, mode}'
cat current_state.json | jq '.resources[] | select(.type == "azurerm_resource_group")'

# Move resource between modules (refactoring)
terraform state mv \
  azurerm_virtual_network.main \
  module.networking.azurerm_virtual_network.main

# Move resource between two state files
terraform state mv \
  -state=state1.tfstate \
  -state-out=state2.tfstate \
  azurerm_resource_group.shared \
  azurerm_resource_group.shared

# Rename resource in state (both state and code must be updated)
# Step 1: Update code (rename resource block)
# Step 2: Use moved block OR state mv
terraform state mv azurerm_resource_group.rg azurerm_resource_group.main

# Remove multiple resources at once
terraform state list | grep "azurerm_subnet" | xargs -I{} terraform state rm {}
```

---

---

## Lesson 25 — Large-Scale Infrastructure Management

> **Level:** Expert

---

### 25.1 Splitting State for Scale

A single state file for an entire organisation is an anti-pattern:
- `terraform plan` takes minutes querying hundreds of resources
- One team's change can break another team's apply
- The blast radius of a mistake is enormous

**Layer your state by lifecycle and team:**

```
State File 1: foundation/        ← VNet, DNS zones, shared services
State File 2: identity/          ← Azure AD, RBAC, managed identities
State File 3: security/          ← Key Vault, Defender, policies
State File 4: platform/          ← AKS, ACR, App Service environments
State File 5: app-team-a/        ← Application team A's resources
State File 6: app-team-b/        ← Application team B's resources
State File 7: databases/         ← Production databases (high sensitivity)
State File 8: monitoring/        ← Log Analytics, alerting
```

**Cross-state references:**
```hcl
# App team reads from platform state
data "terraform_remote_state" "platform" {
  backend = "azurerm"
  config = {
    resource_group_name  = "terraform-state-rg"
    storage_account_name = "tfstatemycompany"
    container_name       = "tfstate"
    key                  = "platform/terraform.tfstate"
  }
}

resource "azurerm_container_app" "api" {
  container_app_environment_id = data.terraform_remote_state.platform.outputs.container_app_env_id
  # ...
}
```

---

### 25.2 Terragrunt — DRY at Scale

Terragrunt is a thin wrapper around Terraform that adds DRY (Don't Repeat Yourself) patterns for backend config and common variables across many Terraform projects.

```
infrastructure/
├── terragrunt.hcl              ← Root config: backend, common vars
├── _envcommon/
│   ├── networking.hcl          ← Common networking config
│   └── app-service.hcl         ← Common app service config
├── dev/
│   ├── account.hcl             ← Dev-specific vars
│   ├── networking/
│   │   └── terragrunt.hcl      ← Includes _envcommon/networking.hcl
│   └── app-service/
│       └── terragrunt.hcl
└── production/
    ├── account.hcl
    ├── networking/
    │   └── terragrunt.hcl
    └── app-service/
        └── terragrunt.hcl
```

**Root terragrunt.hcl:**
```hcl
locals {
  account_vars = read_terragrunt_config(find_in_parent_folders("account.hcl"))
  environment  = local.account_vars.locals.environment
}

generate "backend" {
  path      = "backend.tf"
  if_exists = "overwrite_terragrunt"
  contents = <<EOF
terraform {
  backend "azurerm" {
    resource_group_name  = "terraform-state-rg"
    storage_account_name = "tfstatemycompany"
    container_name       = "tfstate"
    key                  = "${path_relative_to_include()}/terraform.tfstate"
  }
}
EOF
}

inputs = {
  environment = local.environment
}
```

```bash
# Apply all modules in a directory
terragrunt run-all apply

# Plan across all environments
terragrunt run-all plan --terragrunt-working-dir environments/

# Only plan for changed modules (dependency-aware)
terragrunt run-all plan --terragrunt-strict-include
```

---

### 25.3 Performance Optimisation

```bash
# Parallelism — default is 10 concurrent operations
terraform apply -parallelism=20   # More parallel ops (use carefully)
terraform apply -parallelism=5    # Reduce if hitting API rate limits

# Disable refresh on large state files when you're sure state is accurate
terraform plan -refresh=false     # 3-5x faster on large deployments

# Target specific resources to reduce scope
terraform apply -target=module.app_service

# Use partial configuration for backends (useful in CI/CD)
# Don't put backend config in code — pass at runtime:
terraform init \
  -backend-config="resource_group_name=terraform-state-rg" \
  -backend-config="storage_account_name=tfstatemycompany" \
  -backend-config="container_name=tfstate" \
  -backend-config="key=myapp/production/terraform.tfstate"
```

---

---

## Lesson 26 — Terraform Security Hardening

> **Level:** Expert

---

### 26.1 Least-Privilege Service Principal

```bash
# Instead of Contributor on the entire subscription:
# Create a custom role with only what Terraform needs

az role definition create --role-definition '{
  "Name": "Terraform Infrastructure Manager",
  "Description": "Minimal permissions for Terraform CI/CD",
  "Actions": [
    "Microsoft.Resources/subscriptions/resourceGroups/*",
    "Microsoft.Network/*",
    "Microsoft.Compute/*",
    "Microsoft.Web/*",
    "Microsoft.DBforPostgreSQL/*",
    "Microsoft.Storage/storageAccounts/*",
    "Microsoft.KeyVault/*",
    "Microsoft.Authorization/roleAssignments/read",
    "Microsoft.Insights/*"
  ],
  "NotActions": [
    "Microsoft.Authorization/*/Delete",
    "Microsoft.Authorization/elevateAccess/Action"
  ],
  "AssignableScopes": [
    "/subscriptions/<subscription-id>/resourceGroups/myapp-prod-rg"
  ]
}'
```

---

### 26.2 Sensitive Variables and State Encryption

```hcl
# Mark variables as sensitive — Terraform won't print them
variable "db_password" {
  type      = string
  sensitive = true
}

# Mark outputs as sensitive
output "connection_string" {
  value     = "Server=${azurerm_postgresql_flexible_server.main.fqdn};Password=${var.db_password}"
  sensitive = true
}
```

```bash
# Encrypt state at rest — Azure Blob Storage
# (Storage Service Encryption is on by default — verify it)
az storage account show \
  --name tfstatemycompany \
  --query "encryption" \
  --output json

# Enable customer-managed keys for state encryption
az storage account update \
  --name tfstatemycompany \
  --resource-group terraform-state-rg \
  --encryption-key-source Microsoft.Keyvault \
  --encryption-key-vault https://mycompany-kv.vault.azure.net \
  --encryption-key-name terraform-state-key \
  --encryption-key-version latest
```

---

### 26.3 OPA / Sentinel Policy as Code

Policy as code enforces governance rules BEFORE infrastructure is applied.

**Example with Open Policy Agent (OPA):**
```rego
# policies/require_tags.rego
package terraform.required_tags

import input.planned_values.root_module.resources as resources

required_tags := ["Environment", "Project", "ManagedBy"]

deny[msg] {
  resource := resources[_]
  tag := required_tags[_]
  not resource.values.tags[tag]
  msg := sprintf("Resource '%s' is missing required tag '%s'", [resource.address, tag])
}

deny[msg] {
  resource := resources[_]
  resource.type == "azurerm_resource_group"
  resource.values.location != "centralindia"
  resource.values.location != "southindia"
  msg := sprintf("Resource '%s' must be in an approved India region", [resource.address])
}
```

```bash
# Evaluate policy against terraform plan
terraform plan -out=tfplan
terraform show -json tfplan > tfplan.json
opa eval -d policies/ -i tfplan.json "data.terraform.required_tags.deny"
```

---

---

## Lesson 27 — DevOps Interview Preparation — Terraform Edition

> **Level:** Senior Engineer

---

### 27.1 Core Interview Questions — With Strong Answers

**Q: "What is Terraform state and why is it important?"**
> Terraform state is a JSON file that maps the resources in your Terraform configuration to real infrastructure objects in the cloud. It stores the resource IDs, current attribute values, and dependencies. Terraform uses state for three things: first, to determine what already exists so it can compute a diff between desired and actual state; second, to track metadata like resource dependencies; and third, to improve performance by caching attribute values rather than querying the cloud API for every plan. Without state, Terraform would have no way to know that `azurerm_resource_group.main` in your code corresponds to the `/subscriptions/xxx/resourceGroups/myapp-rg` that already exists in Azure. In team environments, state must be stored remotely with locking enabled — local state on one person's laptop breaks collaborative workflows.

---

**Q: "Explain the difference between terraform plan and terraform apply."**
> `terraform plan` is a read-only operation. It reads your `.tf` files, reads the current state (optionally refreshing against the cloud), computes a diff, and prints what would be created, changed, or destroyed — without making any changes. Think of it as `git diff` for infrastructure. `terraform apply` executes the changes — it calls provider APIs to create, modify, or delete resources, then updates the state file to reflect the new reality. In production CI/CD, the best practice is to save the plan to a file with `terraform plan -out=tfplan` and then apply exactly that plan with `terraform apply tfplan`. This ensures what was reviewed and approved is exactly what gets applied, with no window for changes to sneak in between the plan and apply steps.

---

**Q: "How do you manage secrets in Terraform?"**
> I never put secret values in `.tf` files or commit them to Git. The patterns I use depend on the environment. For local development, I use environment variables prefixed with `TF_VAR_` — Terraform automatically picks these up. For CI/CD pipelines, I inject secrets as masked environment variables from the pipeline's secret store (GitHub Actions Secrets, Azure DevOps variable groups). For infrastructure that needs to provision secrets, I use the `random_password` resource to generate them and store them in Azure Key Vault as a `azurerm_key_vault_secret` — the application then reads from Key Vault directly using Managed Identity, never from Terraform outputs. The tricky part is that the random password ends up in the state file, so state itself must be treated as sensitive — encrypted at rest, access controlled, and never printed in logs. I mark sensitive outputs with `sensitive = true` to prevent them from appearing in `terraform output`.

---

**Q: "A terraform apply is running in CI/CD and the pipeline crashes mid-way. What do you do?"**
> First, I check whether Terraform left a state lock. If the pipeline crashed, the lock might still be held. I'd check with `terraform plan` — if it errors with a lock message, I'd verify the original pipeline is truly dead (not just slow), then run `terraform force-unlock <lock-id>`. Second, I'd assess the state of the deployment: since Terraform writes state after each successful resource operation, not at the end, some resources may have been created while others weren't. Running `terraform plan` shows me exactly what was and wasn't created. Third, I'd re-run the pipeline — Terraform is idempotent, so applying again will create the missing resources and leave the already-created ones untouched. If the partial apply left resources in a broken configuration, I might need to use `terraform apply -target` to fix specific resources first.

---

**Q: "What is the difference between count and for_each? When do you use each?"**
> Both create multiple instances of a resource, but they track instances differently. `count` uses numeric indices — resources are `resource[0]`, `resource[1]`, etc. `for_each` uses map keys or set values — resources are `resource["web"]`, `resource["api"]`, etc. The critical difference is what happens when you remove an item from the middle. With `count = 3`, if you remove index 1, Terraform sees indices 0 and 1 remaining and tries to destroy `resource[2]` and update `resource[1]` to be what `resource[2]` was. This often means unnecessary destroys and recreates. With `for_each`, removing `"web"` only removes `resource["web"]` — all other resources are unaffected. I use `for_each` for almost everything, because resources almost always have a meaningful identity. I only use `count` for truly interchangeable, anonymous instances — like adding N extra worker nodes to a pool where none has a special identity.

---

**Q: "Walk me through how you'd structure Terraform for a team of 20 engineers managing infrastructure for 10 applications across dev, staging, and production."**

Strong answer structure:
1. **Module library** — shared Git repo with versioned modules for common patterns (networking, compute, database, monitoring). All teams consume the same modules. Breaking changes bump the major version.
2. **Separate state per environment and layer** — foundation, networking, security, each app. State stored in Azure Blob with versioning and soft delete enabled.
3. **Separate directories per environment** — `environments/dev/`, `environments/staging/`, `environments/production/`. Each has its own backend config and `.tfvars` file.
4. **CI/CD automation** — PRs run `fmt`, `validate`, `plan`. Plan is posted as a PR comment. Merging to main triggers apply with an approval gate for production. All via OIDC — no static credentials in CI.
5. **Drift detection** — daily scheduled pipeline runs `terraform plan -refresh-only` and opens an issue if drift is detected.
6. **Governance** — OPA policies enforced in CI to require tags, enforce region restrictions, and prevent public IP creation without approval.
7. **Module testing** — Terratest integration tests run against every module PR, spinning up and tearing down real infrastructure in a test subscription.

---

### 27.2 Terraform CLI Cheat Sheet — Commands You Must Know Cold

```bash
# ─── CORE WORKFLOW ───────────────────────────────────────────────────
terraform init                              # Initialise — download providers
terraform init -upgrade                     # Upgrade providers within constraints
terraform fmt                               # Format code
terraform fmt -recursive                    # Format all subdirectories
terraform validate                          # Validate syntax
terraform plan                              # Preview changes
terraform plan -out=tfplan                  # Save plan to file
terraform plan -refresh=false               # Skip cloud refresh (faster)
terraform plan -target=module.networking    # Plan specific resource/module
terraform plan -refresh-only               # Check for drift only
terraform apply                             # Apply (prompts for confirmation)
terraform apply -auto-approve               # Apply without prompt (CI/CD)
terraform apply tfplan                      # Apply saved plan
terraform apply -target=azurerm_resource_group.main  # Apply specific resource
terraform apply -replace=azurerm_vm.web[0] # Force-replace (recreate) resource
terraform destroy                           # Destroy all
terraform destroy -auto-approve             # Destroy without prompt
terraform destroy -target=azurerm_vm.test   # Destroy specific resource

# ─── STATE MANAGEMENT ────────────────────────────────────────────────
terraform state list                        # List all resources in state
terraform state show <resource>             # Show resource details
terraform state mv <from> <to>              # Move/rename in state
terraform state rm <resource>               # Remove from state (not cloud)
terraform state pull                        # Print state JSON
terraform state push state.json             # Overwrite state (dangerous)
terraform import <resource> <id>            # Import existing resource
terraform force-unlock <lock-id>            # Force-release state lock

# ─── OUTPUTS AND VARIABLES ───────────────────────────────────────────
terraform output                            # Show all outputs
terraform output <name>                     # Show specific output
terraform output -json                      # All outputs as JSON
terraform output -raw <name>                # Raw value (for scripting)
terraform console                           # Interactive expression evaluator

# ─── WORKSPACES ──────────────────────────────────────────────────────
terraform workspace list                    # List workspaces
terraform workspace new <name>              # Create workspace
terraform workspace select <name>           # Switch workspace
terraform workspace show                    # Current workspace
terraform workspace delete <name>           # Delete empty workspace

# ─── DEBUGGING ───────────────────────────────────────────────────────
TF_LOG=DEBUG terraform plan                 # Full debug output
TF_LOG=INFO terraform apply                 # Info-level logging
TF_LOG_PATH=./terraform.log terraform plan  # Log to file
terraform graph | dot -Tsvg > graph.svg     # Dependency graph
terraform providers                         # Show required providers
terraform version                           # Terraform version

# ─── PROVIDERS ───────────────────────────────────────────────────────
terraform providers                         # List providers in config
terraform providers schema -json            # Full provider schema
terraform providers lock                    # Update lock file
```

---

### 27.3 Terraform Best Practices Checklist

```
□ Use specific provider version constraints (~> not =)
□ Commit .terraform.lock.hcl to Git
□ Use remote state with locking for all team work
□ Enable storage versioning and soft-delete on state bucket
□ Store state per environment — not one file for all environments
□ Use modules for all repeated infrastructure patterns
□ Version your modules with semantic versioning
□ Write README.md for every module (inputs, outputs, examples)
□ Use for_each instead of count wherever resources have identity
□ Use the moved block when renaming resources to avoid destroy/create
□ Mark sensitive variables and outputs with sensitive = true
□ Never store secrets in .tf files or commit .tfvars with secrets
□ Use lifecycle.prevent_destroy on production databases and key vaults
□ Use lifecycle.ignore_changes for externally-managed attributes
□ Run terraform fmt and validate in CI on every PR
□ Post terraform plan output as PR comment for review
□ Use saved plan files in CI/CD (plan -out + apply tfplan)
□ Use OIDC / Workload Identity in CI/CD — no static credentials
□ Enforce least-privilege for service principals
□ Run drift detection on a schedule
□ Use OPA or Sentinel for policy-as-code governance
□ Use -target sparingly — only for incident response
□ Tag all resources consistently (Environment, Project, ManagedBy)
□ Add validation blocks to variables for early error detection
□ Document non-obvious decisions in comments
```

---

## Official Terraform Documentation Reference

| Topic | URL |
|---|---|
| Terraform Documentation | https://developer.hashicorp.com/terraform/docs |
| Terraform CLI | https://developer.hashicorp.com/terraform/cli |
| HCL Language | https://developer.hashicorp.com/terraform/language |
| Terraform Registry | https://registry.terraform.io/ |
| Azure Provider | https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs |
| AWS Provider | https://registry.terraform.io/providers/hashicorp/aws/latest/docs |
| GCP Provider | https://registry.terraform.io/providers/hashicorp/google/latest/docs |
| Terraform Modules | https://developer.hashicorp.com/terraform/language/modules |
| Backends | https://developer.hashicorp.com/terraform/language/backend |
| Terraform Cloud | https://developer.hashicorp.com/terraform/cloud-docs |
| Terratest | https://terratest.gruntwork.io/ |
| Terragrunt | https://terragrunt.gruntwork.io/ |
| Infracost | https://www.infracost.io/docs/ |
| OPA (Open Policy Agent) | https://www.openpolicyagent.org/docs/latest/ |

---

## Learning Path from Here

```
Week 1–2:   Lessons 1–5    Install Terraform, write first configs, variables, outputs
Week 3–4:   Lessons 6–8    Modules, data sources, remote state — set up remote backend
Week 5–6:   Lessons 9–11   Functions, workspaces, lifecycle rules
Week 7–8:   Lessons 12–14  Multi-cloud practice (deploy on Azure + AWS)
Week 9–10:  Lessons 15–17  CI/CD pipeline, secrets management, drift detection
Week 11–12: Lessons 18–20  Module library design, multi-environment, multi-region
Week 13–14: Lessons 21–22  Cost optimisation, dependency management
Week 15–16: Lessons 23–26  Internals, state debugging, large-scale, security
Week 17–18: Lesson 27      Interview prep + build a real portfolio project
```

**Build Something Real:**
Build a complete IaC project:
- Three environments (dev, staging, production) with separate state
- Module library with at least 3 reusable modules
- Full CI/CD pipeline in GitHub Actions with plan-on-PR and apply-on-merge
- Drift detection scheduled job
- Remote state with locking in Azure Blob or S3
- OPA policy enforcing required tags and approved regions

Put it on GitHub. This is your portfolio proof-of-work.

---

*Built on: Official HashiCorp Terraform Documentation — https://developer.hashicorp.com/terraform/docs | Production IaC Patterns | Microsoft Well-Architected Framework*
