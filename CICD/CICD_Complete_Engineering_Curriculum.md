# CI/CD Mastery — Complete Engineering Curriculum
## Zero to Senior DevOps / Pipeline Architect

> **Covers:** DevOps Fundamentals · CI/CD Concepts · Jenkins · GitHub Actions · GitLab CI · Docker Pipelines · Kubernetes Deployments · Terraform in CI/CD · Artifact Management · Security · GitOps · Enterprise Architecture
> **Track:** DevOps Career Path | Beginner → Senior Engineer
> **Tools:** Jenkins · GitHub Actions · GitLab CI/CD · Bitbucket Pipelines · Docker · Kubernetes · Helm · Terraform · Nexus · Artifactory
> **Based on:** Official Documentation for Jenkins, GitHub Actions, GitLab CI, Docker, Kubernetes, Terraform

---

## How to Use This Document

- Work through every lesson in order — each concept builds on the previous
- Run every pipeline and lab yourself — reading is passive, building is learning
- Attempt every practice question before reading the answer
- Labs are tool-agnostic where possible — adapt to whichever CI/CD tool your team uses
- Real pipeline YAML is provided for GitHub Actions, GitLab CI, and Jenkins for every pattern

---

## Table of Contents

### PHASE 1 — Foundations (Beginner)
- [Lesson 1 — CI/CD Fundamentals and DevOps Pipeline Architecture](#lesson-1--cicd-fundamentals-and-devops-pipeline-architecture)
- [Lesson 2 — Version Control Integration and Branch Strategies](#lesson-2--version-control-integration-and-branch-strategies)
- [Lesson 3 — Build Automation — Maven, Gradle, npm](#lesson-3--build-automation--maven-gradle-npm)
- [Lesson 4 — Testing Automation in CI/CD](#lesson-4--testing-automation-in-cicd)
- [Lesson 5 — Artifact Management — Nexus and Artifactory](#lesson-5--artifact-management--nexus-and-artifactory)

### PHASE 2 — CI/CD Tools (Intermediate)
- [Lesson 6 — Jenkins — Architecture and Fundamentals](#lesson-6--jenkins--architecture-and-fundamentals)
- [Lesson 7 — Jenkins Pipelines — Declarative and Scripted](#lesson-7--jenkins-pipelines--declarative-and-scripted)
- [Lesson 8 — GitHub Actions — Complete Guide](#lesson-8--github-actions--complete-guide)
- [Lesson 9 — GitLab CI/CD — Complete Guide](#lesson-9--gitlab-cicd--complete-guide)
- [Lesson 10 — Bitbucket Pipelines](#lesson-10--bitbucket-pipelines)

### PHASE 3 — DevOps Level (Production CI/CD)
- [Lesson 11 — Docker in CI/CD Pipelines](#lesson-11--docker-in-cicd-pipelines)
- [Lesson 12 — Kubernetes Deployments Through CI/CD](#lesson-12--kubernetes-deployments-through-cicd)
- [Lesson 13 — Terraform in CI/CD Pipelines](#lesson-13--terraform-in-cicd-pipelines)
- [Lesson 14 — Blue-Green and Canary Deployments](#lesson-14--blue-green-and-canary-deployments)
- [Lesson 15 — CI/CD Security Best Practices](#lesson-15--cicd-security-best-practices)
- [Lesson 16 — Pipeline Optimisation and Caching](#lesson-16--pipeline-optimisation-and-caching)

### PHASE 4 — Advanced Architecture
- [Lesson 17 — Multi-Environment Pipelines](#lesson-17--multi-environment-pipelines)
- [Lesson 18 — Microservices CI/CD Pipelines](#lesson-18--microservices-cicd-pipelines)
- [Lesson 19 — GitOps Workflows](#lesson-19--gitops-workflows)
- [Lesson 20 — Pipeline Monitoring and Observability](#lesson-20--pipeline-monitoring-and-observability)
- [Lesson 21 — Managing Pipeline Secrets](#lesson-21--managing-pipeline-secrets)

### PHASE 5 — Expert Level
- [Lesson 22 — Debugging Failed Pipelines and Deployments](#lesson-22--debugging-failed-pipelines-and-deployments)
- [Lesson 23 — Disaster Recovery in CI/CD](#lesson-23--disaster-recovery-in-cicd)
- [Lesson 24 — Enterprise CI/CD Architecture](#lesson-24--enterprise-cicd-architecture)
- [Lesson 25 — Secure Pipeline Design](#lesson-25--secure-pipeline-design)
- [Lesson 26 — DevOps Interview Preparation — CI/CD Edition](#lesson-26--devops-interview-preparation--cicd-edition)

---

---

# PHASE 1 — FOUNDATIONS
## CI/CD Beginner Level

---

## Lesson 1 — CI/CD Fundamentals and DevOps Pipeline Architecture

> **Level:** Absolute Beginner
> **Goal:** Understand what CI/CD is, why it exists, and how a pipeline is structured

---

### 1.1 The World Before CI/CD

To understand why CI/CD matters, understand what development looked like without it.

**The Old Way — "Integration Hell":**
- 10 developers work in isolation for 2–4 weeks on their own branches
- On "release day" everyone merges their code together
- Conflicts everywhere — code that worked in isolation breaks when combined
- Manual deployment: a single engineer SSHs into production servers at midnight and copies files
- If something breaks: manual rollback, 4am phone calls, no sleep
- One deployment every 2–3 months

**The cost of this approach:**
- Bugs found 3 months after they were written — impossible to remember context
- Manual processes are error-prone — humans make mistakes under pressure
- No confidence in deployments — teams afraid to release
- Slow feedback loop — developers don't know if code works until weeks later
- No repeatability — "it works on my machine"

> **CI/CD replaces this with an automated, repeatable, fast feedback loop.** Code changes are automatically built, tested, and deployed multiple times per day with confidence.

---

### 1.2 What is DevOps?

DevOps is a culture and practice that brings Development and Operations teams together. Before DevOps, these teams were separated — developers wrote code, operations deployed it, and the two teams blamed each other when things went wrong.

```
BEFORE DEVOPS:
Dev Team  →  "Here's the code" (throws over the wall)
Ops Team  →  "It broke in production"
Dev Team  →  "Works on my machine"
(Repeat indefinitely)

WITH DEVOPS:
Shared responsibility: code quality AND deployment reliability
Automation replaces manual handoffs
Fast feedback: know within minutes if a change is safe
```

**DevOps core practices:**
- Continuous Integration — merge and test code continuously
- Continuous Delivery/Deployment — automate deployment
- Infrastructure as Code — version-control infrastructure
- Monitoring and Observability — know what's happening in production
- Collaboration — shared ownership between dev and ops

---

### 1.3 CI vs CD vs CD — The Three Terms

These three terms are often confused. Here is the precise definition of each.

**Continuous Integration (CI):**
> Developers integrate (merge) their code changes into a shared branch frequently — at least daily. Each merge automatically triggers a build and test run. The goal is to detect integration problems early.

```
Developer commits code
         │
         ▼
Automated build (compile, package)
         │
         ▼
Automated tests (unit, integration)
         │
         ▼
Fast feedback: PASS or FAIL within minutes
```

**Continuous Delivery (CD):**
> Every code change that passes CI is automatically prepared for release to production. The deployment to production is a manual decision/trigger, but the process itself is automated.

```
CI passes
   │
   ▼
Automated deployment to staging
   │
   ▼
Automated acceptance tests on staging
   │
   ▼
[MANUAL APPROVAL] ← human decides when to release
   │
   ▼
Automated deployment to production
```

**Continuous Deployment:**
> Every change that passes all automated tests is automatically deployed to production without any manual intervention. No human approval step.

```
CI passes → staging passes → production AUTOMATICALLY ← no human needed
```

| Aspect | Continuous Integration | Continuous Delivery | Continuous Deployment |
|---|---|---|---|
| **Goal** | Always have working code | Always be ready to release | Always release automatically |
| **Human step** | Code review only | Manual production approval | None |
| **Who uses it** | All teams | Most product companies | High-confidence, mature teams |
| **Release cadence** | Many times/day (builds) | On-demand | Every passing commit |

> **Which one do most companies use?** Continuous Delivery is the most common in enterprise. Full Continuous Deployment is used by companies like Netflix, Google, Amazon, and teams with very mature testing. Many companies aim for Continuous Delivery and deploy to production multiple times per week on demand.

---

### 1.4 The CI/CD Pipeline — Stage by Stage

A pipeline is the automated workflow that takes code from a developer's commit to running in production.

```
                    THE COMPLETE CI/CD PIPELINE
                    
 Developer                                              Production
    │                                                        │
    ▼                                                        │
 git push                                                    │
    │                                                        │
    ▼                                                        │
┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐  │
│  SOURCE  │ → │  BUILD   │ → │   TEST   │ → │ PACKAGE  │  │
│  STAGE   │   │  STAGE   │   │  STAGE   │   │  STAGE   │  │
│          │   │          │   │          │   │          │  │
│ • Pull   │   │ • Compile│   │ • Unit   │   │ • Docker │  │
│   code   │   │ • Lint   │   │ • Integ. │   │   build  │  │
│ • Check  │   │ • SAST   │   │ • E2E    │   │ • Push   │  │
│   branch │   │ • Build  │   │ • Perf.  │   │   image  │  │
└──────────┘   └──────────┘   └──────────┘   └──────────┘  │
                                                             │
┌──────────┐   ┌──────────┐   ┌──────────┐                  │
│ DEPLOY   │ → │ DEPLOY   │ → │ DEPLOY   │ ─────────────────┘
│   DEV    │   │ STAGING  │   │ PROD     │
│          │   │          │   │          │
│ • Auto   │   │ • Auto   │   │ • Manual │
│ • Smoke  │   │ • Full   │   │   gate   │
│   tests  │   │   tests  │   │ • Verify │
└──────────┘   └──────────┘   └──────────┘
```

**Stage descriptions:**

**Source Stage:**
- Triggered by: `git push`, pull request open/update, scheduled cron
- Actions: checkout code, check branch rules, validate PR has required reviewers
- Gate: code must be on valid branch, PR must have approval

**Build Stage:**
- Compile source code (Java → .class, TypeScript → JavaScript)
- Run linting (code style checks)
- Run SAST (Static Application Security Testing — check code for vulnerabilities)
- Output: build artifact (JAR, WAR, binary, or compiled JS)

**Test Stage:**
- **Unit tests:** Test individual functions in isolation (fast, ~seconds)
- **Integration tests:** Test components working together with real databases/APIs (minutes)
- **End-to-end tests:** Test full user journeys in a browser or API client (slow, minutes to hours)
- **Performance tests:** Confirm the app handles expected load
- Gate: all tests must pass. Any failure stops the pipeline.

**Package Stage:**
- Build Docker image from compiled code
- Scan image for vulnerabilities (Trivy, Snyk)
- Push image to container registry (ACR, ECR, GHCR)
- Store versioned artifact in artifact repository (Nexus, Artifactory)

**Deploy Stages:**
- Deploy to dev (automatic, every build)
- Deploy to staging (automatic, after dev passes)
- Deploy to production (manual approval gate, or automatic in Continuous Deployment)
- Run smoke tests after each deployment to verify the environment

---

### 1.5 Key CI/CD Concepts

| Concept | Definition | Why It Matters |
|---|---|---|
| **Pipeline** | Automated workflow from code to production | Removes manual, error-prone steps |
| **Stage** | A logical group of steps in a pipeline | Organises pipeline into phases |
| **Job** | A unit of work that runs on one agent | Parallelisable unit |
| **Step/Task** | A single command or action within a job | The actual work |
| **Trigger** | Event that starts a pipeline | Push, PR, schedule, manual |
| **Artifact** | Output of a build stage (JAR, Docker image) | Passed between stages |
| **Agent/Runner** | Machine that executes pipeline jobs | Where the actual work runs |
| **Environment** | A deployment target (dev, staging, prod) | Isolates deployment concerns |
| **Gate** | A checkpoint requiring approval or criteria | Prevents bad code reaching prod |
| **Rollback** | Revert to a previous working version | Recover from bad deployments |

---

### 1.6 Choosing the Right CI/CD Tool

| Tool | Best For | Hosted/Self-hosted | Pricing |
|---|---|---|---|
| **GitHub Actions** | GitHub repos, open source, modern teams | Both | Free tier + paid |
| **GitLab CI/CD** | GitLab repos, all-in-one DevOps | Both | Free tier + paid |
| **Jenkins** | Enterprise, complex customisation, legacy systems | Self-hosted | Free (infra cost) |
| **Bitbucket Pipelines** | Bitbucket repos, Atlassian stack | Hosted | Free tier + paid |
| **Azure DevOps** | Microsoft/Azure shops | Both | Free tier + paid |
| **CircleCI** | Fast pipelines, Docker-first | Both | Free tier + paid |
| **TeamCity** | JetBrains ecosystem, Java teams | Both | Free + paid |

> **Career advice:** Learn GitHub Actions first — it's the most widely used in modern teams. Learn Jenkins second — it's dominant in enterprise/legacy environments. Every DevOps job description will list one or both.

---

### 1.7 Hands-On Lab 1 — Your First GitHub Actions Pipeline

**Objective:** Create a real working CI pipeline with a failing and passing state.

**Step 1 — Create a GitHub repository:**
1. Go to github.com → New Repository → name it `cicd-lab`
2. Add a README.md
3. Clone it locally: `git clone https://github.com/yourusername/cicd-lab.git`

**Step 2 — Create a simple Node.js application:**
```bash
cd cicd-lab
mkdir src && cat > src/calculator.js << 'EOF'
function add(a, b) { return a + b; }
function subtract(a, b) { return a - b; }
function multiply(a, b) { return a * b; }
module.exports = { add, subtract, multiply };
EOF

cat > src/calculator.test.js << 'EOF'
const { add, subtract, multiply } = require('./calculator');
test('add: 2 + 3 = 5', () => expect(add(2, 3)).toBe(5));
test('subtract: 5 - 3 = 2', () => expect(subtract(5, 3)).toBe(2));
test('multiply: 4 * 3 = 12', () => expect(multiply(4, 3)).toBe(12));
EOF

cat > package.json << 'EOF'
{
  "name": "cicd-lab",
  "version": "1.0.0",
  "scripts": {
    "test": "jest",
    "lint": "echo 'Linting passed'"
  },
  "devDependencies": {
    "jest": "^29.0.0"
  }
}
EOF
```

**Step 3 — Create your first pipeline:**
```bash
mkdir -p .github/workflows
cat > .github/workflows/ci.yml << 'EOF'
name: CI Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  build-and-test:
    name: Build and Test
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'

      - name: Install dependencies
        run: npm install

      - name: Run linting
        run: npm run lint

      - name: Run tests
        run: npm test

      - name: Upload test results
        uses: actions/upload-artifact@v4
        if: always()
        with:
          name: test-results
          path: coverage/
EOF
```

**Step 4 — Push and watch it run:**
```bash
git add .
git commit -m "Add calculator app and CI pipeline"
git push origin main
# Go to GitHub → Actions tab → watch your pipeline run
```

**Step 5 — Create a failing build (intentionally):**
```bash
# Introduce a failing test
cat >> src/calculator.test.js << 'EOF'
test('intentional failure: 1 + 1 = 3', () => expect(add(1, 1)).toBe(3));
EOF

git add . && git commit -m "Introduce failing test" && git push
# Watch the pipeline fail — this is exactly what CI is designed to catch
```

**Step 6 — Fix it and see green:**
```bash
# Remove the failing test, push again, watch it go green
```

---

### 1.8 Practice Questions — Lesson 1

**Q1.** What is the difference between Continuous Delivery and Continuous Deployment?

- A) They are the same thing
- B) Continuous Delivery requires a manual approval step before production; Continuous Deployment deploys automatically on every passing build
- C) Continuous Deployment requires manual approval; Continuous Delivery deploys automatically
- D) Continuous Delivery only covers the build stage; Continuous Deployment covers deployment

<details>
<summary>Answer and Explanation</summary>

**Answer: B.**

Continuous Delivery: code is always ready to deploy, but a human makes the final decision to push to production. Continuous Deployment: every commit that passes tests goes to production automatically — no human step. Most companies use Continuous Delivery. Full Continuous Deployment requires extremely high test confidence and mature monitoring.

</details>

---

**Q2 — Scenario.** A company deploys software manually once a month. The deployment takes 8 hours, frequently breaks production, and requires an all-hands war room to fix. They ask you to help. What is the first principle you would apply and why?

<details>
<summary>Answer</summary>

**Automate and deploy more frequently.** Counter-intuitively, the solution to painful, risky deployments is to deploy more often, not less. Each deployment carries accumulated changes — more changes = more risk. By deploying smaller, automated changes continuously, each deployment is trivial to verify or roll back. Automation removes human error from the process. The long deployment time and war rooms are symptoms of infrequent, manual, large-batch releases.

</details>

---

---

## Lesson 2 — Version Control Integration and Branch Strategies

> **Level:** Beginner → Intermediate
> **Goal:** Understand how CI/CD connects to Git and how branch strategies shape pipelines

---

### 2.1 Why Version Control is the Foundation of CI/CD

Every CI/CD pipeline starts with a Git event. There is no CI/CD without version control. The pipeline trigger IS the git event.

```
Developer pushes code  →  Git event  →  Pipeline triggered
Developer opens PR     →  Git event  →  Pipeline triggered
Tag v1.2.0 created     →  Git event  →  Release pipeline triggered
Scheduled cron         →  Timer      →  Nightly pipeline triggered
```

---

### 2.2 Branching Strategies — How They Shape Your Pipeline

**Strategy 1 — Trunk-Based Development (Google, Facebook, Netflix):**
```
main (trunk)  ←  developers commit directly or via very short-lived branches (< 1 day)

Pipeline behaviour:
Every commit to main → full CI → deploy to staging → optional auto-deploy to prod
Feature flags control which features are visible to users
```
- **Pros:** Maximum velocity, no merge hell, true continuous integration
- **Cons:** Requires mature test suite, feature flags, strong engineering discipline
- **Used by:** Google, Facebook, Netflix, Etsy

**Strategy 2 — GitFlow (traditional enterprise):**
```
main          ←  production code only, tagged releases
develop       ←  integration branch for features
feature/*     ←  individual feature branches
release/*     ←  release preparation branches
hotfix/*      ←  emergency production fixes

Pipeline behaviour:
feature/* push  → build + unit tests
develop push    → full CI + deploy to dev
release/* push  → full CI + deploy to staging
main push       → full CI + deploy to production (manual gate)
hotfix/* push   → full CI + deploy to staging → fast-track to production
```
- **Pros:** Clear release process, good for scheduled releases
- **Cons:** Complex, long-lived branches, merge conflicts common
- **Used by:** Traditional enterprise, software with versioned releases

**Strategy 3 — GitHub Flow (most common modern approach):**
```
main           ←  always deployable
feature/*      ←  all work done here, merged via PR

Pipeline behaviour:
feature/* push/PR update  → build + test (blocks PR merge on failure)
main push (merged PR)     → full CI + deploy to staging → deploy to production
```
- **Pros:** Simple, fast, works well with CI/CD
- **Cons:** Requires mature deployment process
- **Used by:** GitHub, most modern SaaS companies, small-medium teams

---

### 2.3 Pipeline Triggers — Complete Reference

**GitHub Actions triggers:**
```yaml
on:
  # Trigger on push to specific branches
  push:
    branches:
      - main
      - develop
      - 'release/**'
    paths:
      - 'src/**'         # Only trigger if src/ files changed
      - 'package.json'
    paths-ignore:
      - '**.md'          # Ignore documentation-only changes

  # Trigger on pull request events
  pull_request:
    branches: [main]
    types: [opened, synchronize, reopened, ready_for_review]

  # Trigger on tag creation (releases)
  push:
    tags:
      - 'v*.*.*'         # v1.0.0, v2.3.1, etc.

  # Scheduled trigger (cron)
  schedule:
    - cron: '0 2 * * 1-5'   # 2am Mon-Fri UTC

  # Manual trigger (with optional inputs)
  workflow_dispatch:
    inputs:
      environment:
        description: 'Deployment target'
        required: true
        default: 'staging'
        type: choice
        options: [staging, production]
      version:
        description: 'Version to deploy'
        required: false

  # Trigger from another workflow
  workflow_call:
    inputs:
      image-tag:
        required: true
        type: string
```

---

### 2.4 Branch Protection Rules — Enforce Quality Gates

Branch protection rules prevent bad code from reaching main. Configure in GitHub: Settings → Branches → Add rule for `main`.

```
Required for merging to main:
  ✅ Require pull request reviews (minimum 1 reviewer)
  ✅ Require status checks to pass before merging
     ✅ CI Pipeline (build-and-test job must pass)
     ✅ Security Scan
  ✅ Require branches to be up to date before merging
  ✅ Require linear history (no merge commits, only squash/rebase)
  ✅ Include administrators (rules apply to everyone, including repo owners)
```

> **Why this matters in production:** Without branch protection, a developer can push untested code directly to main and trigger a broken deployment. Branch protection makes CI/CD gates mandatory — the pipeline IS the quality gate.

---

---

## Lesson 3 — Build Automation — Maven, Gradle, npm

> **Level:** Beginner → Intermediate
> **Goal:** Understand build tools and how they integrate into CI pipelines

---

### 3.1 Why Build Tools Matter in CI/CD

A build tool automates compilation, dependency management, testing, and packaging. In a CI pipeline, the build tool is what the pipeline calls. The pipeline orchestrates; the build tool does the actual work.

```
CI Pipeline calls:  mvn clean package
Build tool does:    1. Download dependencies from Maven Central
                    2. Compile Java source → .class files
                    3. Run unit tests
                    4. Package → .jar file
                    5. Report results
```

---

### 3.2 Maven — Java Projects

```xml
<!-- pom.xml — Maven project configuration -->
<project>
  <groupId>com.mycompany</groupId>
  <artifactId>my-api</artifactId>
  <version>1.2.3</version>
  <packaging>jar</packaging>

  <properties>
    <java.version>17</java.version>
    <spring-boot.version>3.2.0</spring-boot.version>
  </properties>

  <dependencies>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <!-- Test dependencies -->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-test</artifactId>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-maven-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
</project>
```

**Maven in CI pipelines:**
```bash
# Clean and compile only
mvn clean compile

# Run unit tests
mvn test

# Full build: compile + test + package
mvn clean package

# Skip tests (never do this in CI — only for local speed)
mvn clean package -DskipTests

# Install to local repo (needed when modules depend on each other)
mvn clean install

# Deploy artifact to Nexus/Artifactory
mvn deploy

# Run with a specific profile
mvn clean package -P production
```

**In GitHub Actions:**
```yaml
- name: Setup Java
  uses: actions/setup-java@v4
  with:
    java-version: '17'
    distribution: 'temurin'
    cache: 'maven'   # Cache .m2/repository between runs

- name: Build with Maven
  run: mvn clean package -B   # -B = batch mode (no interactive prompts)

- name: Upload artifact
  uses: actions/upload-artifact@v4
  with:
    name: jar-artifact
    path: target/*.jar
```

---

### 3.3 Gradle — Modern Java/Android/Kotlin Projects

```groovy
// build.gradle
plugins {
    id 'java'
    id 'org.springframework.boot' version '3.2.0'
    id 'io.spring.dependency-management' version '1.1.4'
}

group = 'com.mycompany'
version = '1.2.3'
sourceCompatibility = '17'

repositories {
    mavenCentral()
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
}

test {
    useJUnitPlatform()
    testLogging {
        events 'passed', 'skipped', 'failed'
    }
}
```

**Gradle in CI pipelines:**
```bash
# Build and test
./gradlew build

# Test only
./gradlew test

# Build without tests
./gradlew build -x test

# Package JAR
./gradlew bootJar

# Publish to artifact repository
./gradlew publish
```

**In GitHub Actions:**
```yaml
- name: Setup Java
  uses: actions/setup-java@v4
  with:
    java-version: '17'
    distribution: 'temurin'
    cache: 'gradle'

- name: Grant execute permission for gradlew
  run: chmod +x gradlew

- name: Build with Gradle
  run: ./gradlew build
```

---

### 3.4 npm — Node.js Projects

```json
{
  "name": "my-api",
  "version": "1.2.3",
  "scripts": {
    "build": "tsc",
    "test": "jest --coverage --ci",
    "lint": "eslint src/ --ext .ts",
    "start": "node dist/server.js"
  },
  "dependencies": {
    "express": "^4.18.0"
  },
  "devDependencies": {
    "typescript": "^5.0.0",
    "jest": "^29.0.0",
    "@types/express": "^4.17.0",
    "eslint": "^8.0.0"
  }
}
```

**npm in CI pipelines:**
```bash
# Install exact versions from package-lock.json (CI-safe)
npm ci             # Always use npm ci in CI, never npm install

# Run linting
npm run lint

# Run tests with coverage
npm test -- --coverage

# Build TypeScript
npm run build

# Audit for security vulnerabilities
npm audit --audit-level=high
```

**In GitHub Actions:**
```yaml
- name: Setup Node.js
  uses: actions/setup-node@v4
  with:
    node-version: '18'
    cache: 'npm'

- name: Install dependencies
  run: npm ci    # NOT npm install — ci uses lockfile exactly

- name: Lint
  run: npm run lint

- name: Test
  run: npm test -- --coverage --ci

- name: Build
  run: npm run build
```

> **npm ci vs npm install:** `npm ci` deletes `node_modules` and installs exactly what's in `package-lock.json`. It's deterministic, faster in CI, and won't accidentally update packages. Always use `npm ci` in pipelines.

---

---

## Lesson 4 — Testing Automation in CI/CD

> **Level:** Intermediate
> **Goal:** Build a comprehensive automated test strategy in pipelines

---

### 4.1 The Testing Pyramid in CI/CD

```
                    /\
                   /  \
                  / E2E \         ← Few, slow, high confidence
                 /________\       ← Run in staging only
                /          \
               / Integration \    ← Some, medium speed
              /______________\    ← Run after each merge
             /                \
            /    Unit Tests    \  ← Many, fast, cheap
           /____________________\ ← Run on every commit
```

**The rule:** More tests at the bottom of the pyramid. Each level tests at a different scope.

| Test Type | What It Tests | Speed | Run When |
|---|---|---|---|
| **Unit** | Single function/method in isolation | < 1ms each | Every commit |
| **Integration** | Multiple components with real DB/APIs | Seconds | Every merge to develop |
| **E2E/UI** | Full user journeys in a real browser | Minutes | Before release, nightly |
| **Performance** | Response times under load | Minutes to hours | Before major release |
| **Security/SAST** | Code vulnerabilities | Seconds to minutes | Every commit |
| **Contract** | API contracts between services | Seconds | Every commit (microservices) |

---

### 4.2 Testing in GitHub Actions — Complete Example

```yaml
name: Full Test Suite

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  # ─── UNIT TESTS ───────────────────────────────────────────────────
  unit-tests:
    name: Unit Tests
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'
      - run: npm ci
      - name: Run unit tests
        run: npm test -- --coverage --ci --testPathPattern=unit
      - name: Upload coverage report
        uses: codecov/codecov-action@v3
        with:
          file: ./coverage/lcov.info

  # ─── INTEGRATION TESTS (needs real services) ─────────────────────
  integration-tests:
    name: Integration Tests
    runs-on: ubuntu-latest
    services:
      # Spin up a real PostgreSQL database for integration tests
      postgres:
        image: postgres:15-alpine
        env:
          POSTGRES_USER: testuser
          POSTGRES_PASSWORD: testpassword
          POSTGRES_DB: testdb
        ports:
          - 5432:5432
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
      # Redis for cache integration tests
      redis:
        image: redis:7-alpine
        ports:
          - 6379:6379
        options: --health-cmd "redis-cli ping" --health-interval 10s

    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'
      - run: npm ci
      - name: Run integration tests
        run: npm test -- --testPathPattern=integration
        env:
          DB_HOST: localhost
          DB_PORT: 5432
          DB_USER: testuser
          DB_PASS: testpassword
          DB_NAME: testdb
          REDIS_HOST: localhost

  # ─── SECURITY SCAN ────────────────────────────────────────────────
  security-scan:
    name: Security Scan
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run Trivy vulnerability scanner
        uses: aquasecurity/trivy-action@master
        with:
          scan-type: 'fs'
          scan-ref: '.'
          severity: 'CRITICAL,HIGH'
          exit-code: '1'
      - name: Run npm audit
        run: |
          npm ci
          npm audit --audit-level=high

  # ─── CODE QUALITY ─────────────────────────────────────────────────
  code-quality:
    name: Code Quality
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0    # Full history needed for SonarCloud
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'
      - run: npm ci
      - name: Run ESLint
        run: npm run lint -- --format=json --output-file=eslint-report.json
      - name: SonarCloud Scan
        uses: SonarSource/sonarcloud-github-action@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```

---

### 4.3 Test Parallelisation — Faster Pipelines

```yaml
# Run tests across 4 parallel workers
jobs:
  test:
    name: Test (shard ${{ matrix.shard }})
    runs-on: ubuntu-latest
    strategy:
      matrix:
        shard: [1, 2, 3, 4]   # 4 parallel jobs

    steps:
      - uses: actions/checkout@v4
      - run: npm ci
      - name: Run shard ${{ matrix.shard }} of 4
        run: npx jest --shard=${{ matrix.shard }}/4 --ci

  # Merge results from all shards
  test-results:
    needs: test
    runs-on: ubuntu-latest
    if: always()
    steps:
      - name: Merge test results
        run: echo "All shards complete"
```

---

---

## Lesson 5 — Artifact Management — Nexus and Artifactory

> **Level:** Intermediate
> **Goal:** Store, version, and distribute build artifacts professionally

---

### 5.1 What is an Artifact Repository?

An artifact repository is a central storage system for build outputs — JARs, WARs, Docker images, npm packages, Python packages, Helm charts. It provides:
- **Versioned storage:** Every build creates a versioned artifact
- **Proxying:** Cache external packages (Maven Central, npm registry) internally
- **Security:** Scan artifacts for vulnerabilities before use
- **Traceability:** Know exactly which artifact is deployed where
- **Promotion:** Move artifact from dev → staging → production repository

---

### 5.2 Nexus Repository Manager

```bash
# Run Nexus locally with Docker
docker run -d \
  --name nexus \
  -p 8081:8081 \
  -v nexus-data:/nexus-data \
  sonatype/nexus3:latest

# Access: http://localhost:8081
# Default admin password:
docker exec nexus cat /nexus-data/admin.password
```

**Maven settings.xml — publish to Nexus:**
```xml
<!-- ~/.m2/settings.xml -->
<settings>
  <servers>
    <server>
      <id>nexus-releases</id>
      <username>deployer</username>
      <password>${env.NEXUS_PASSWORD}</password>
    </server>
    <server>
      <id>nexus-snapshots</id>
      <username>deployer</username>
      <password>${env.NEXUS_PASSWORD}</password>
    </server>
  </servers>
</settings>
```

**pom.xml distribution management:**
```xml
<distributionManagement>
  <repository>
    <id>nexus-releases</id>
    <url>http://nexus:8081/repository/maven-releases/</url>
  </repository>
  <snapshotRepository>
    <id>nexus-snapshots</id>
    <url>http://nexus:8081/repository/maven-snapshots/</url>
  </snapshotRepository>
</distributionManagement>
```

---

### 5.3 Publishing Artifacts in CI/CD

```yaml
# GitHub Actions — publish Java artifact to Nexus
- name: Publish to Nexus
  run: mvn deploy -B -DskipTests
  env:
    NEXUS_PASSWORD: ${{ secrets.NEXUS_PASSWORD }}

# Publish npm package to Artifactory
- name: Configure npm registry
  run: |
    echo "@mycompany:registry=https://mycompany.jfrog.io/artifactory/api/npm/npm-local/" >> ~/.npmrc
    echo "//mycompany.jfrog.io/artifactory/api/npm/npm-local/:_authToken=${ARTIFACTORY_TOKEN}" >> ~/.npmrc
  env:
    ARTIFACTORY_TOKEN: ${{ secrets.ARTIFACTORY_TOKEN }}

- name: Publish npm package
  run: npm publish
```

---

### 5.4 Semantic Versioning in Pipelines

```yaml
# Automatically determine version from Git tags
- name: Get version
  id: version
  run: |
    # Get latest git tag, default to 0.0.0 if no tags
    VERSION=$(git describe --tags --abbrev=0 2>/dev/null || echo "0.0.0")
    # Add commit count for pre-release builds
    COMMITS=$(git rev-list --count HEAD)
    SHORT_SHA=$(git rev-parse --short HEAD)
    echo "version=${VERSION}" >> $GITHUB_OUTPUT
    echo "full-version=${VERSION}-${COMMITS}-${SHORT_SHA}" >> $GITHUB_OUTPUT

# Use the version
- name: Build with version
  run: mvn clean package -Dversion=${{ steps.version.outputs.version }}
```

---

### 5.5 Practice Questions — Lessons 2–5

**Q1.** Your team uses GitHub Flow. A developer pushes to a `feature/payment-api` branch. What should the CI pipeline do at this point?

<details>
<summary>Answer</summary>

The pipeline should run the fast feedback loop: checkout code, install dependencies, run linting, run unit tests. It should NOT deploy to any environment (this is a feature branch). The goal is fast feedback (< 5 minutes) so the developer knows immediately if their change is safe. Integration tests might run if they're fast enough. No deployment — only the main branch triggers deployments in GitHub Flow.

</details>

---

**Q2.** Why should you always use `npm ci` instead of `npm install` in CI pipelines?

<details>
<summary>Answer</summary>

`npm ci` installs exactly what is in `package-lock.json` without modifying it. It deletes and reinstalls `node_modules` entirely, giving a clean, reproducible environment. `npm install` may upgrade packages to newer compatible versions, potentially introducing new bugs or breaking changes between pipeline runs. CI pipelines must be deterministic — same code should always produce the same build. `npm ci` enforces this determinism.

</details>

---

---

# PHASE 2 — CI/CD TOOLS (INTERMEDIATE)

---

## Lesson 6 — Jenkins — Architecture and Fundamentals

> **Level:** Intermediate
> **Goal:** Set up and understand Jenkins for enterprise CI/CD

---

### 6.1 Why Jenkins Still Matters

Jenkins was released in 2011 and remains the most widely deployed CI/CD tool in enterprise environments. Understanding Jenkins is required for most enterprise DevOps roles. Key reasons it persists:

- Massive plugin ecosystem (1,800+ plugins)
- Runs anywhere — any OS, any cloud, any on-premises environment
- Deeply customisable — can integrate with any system
- No vendor lock-in — self-hosted
- Most enterprise job descriptions still list Jenkins

**Jenkins weaknesses:**
- Requires significant maintenance (JVM memory, plugin updates, security patches)
- YAML-based alternatives (GitHub Actions, GitLab CI) are simpler to learn
- Jenkins X (cloud-native Jenkins) never gained widespread adoption

---

### 6.2 Jenkins Architecture

```
                    JENKINS MASTER (Controller)
                    ┌────────────────────────────────────────┐
                    │                                         │
  Browser/API  ──►  │  Web UI   REST API   Pipeline Engine   │
                    │                                         │
                    │  Job Queue    Build History    Plugins  │
                    │                                         │
                    └────────────┬────────────────────────────┘
                                 │ Agent Protocol (JNLP/SSH)
              ┌──────────────────┼──────────────────────┐
              │                  │                       │
     ┌────────▼──────┐  ┌────────▼──────┐  ┌────────────▼──────┐
     │  AGENT 1      │  │  AGENT 2      │  │  AGENT 3 (Docker) │
     │  Linux VM     │  │  Windows VM   │  │  Dynamic pods     │
     │  Java builds  │  │  .NET builds  │  │  Kubernetes       │
     └───────────────┘  └───────────────┘  └───────────────────┘
```

**Controller (Master):**
- Orchestrates pipelines — does NOT run builds
- Manages job queue, build history, credentials
- Serves the web UI and REST API
- Routes builds to appropriate agents

**Agents:**
- Execute the actual build steps
- Can be static (dedicated VMs) or dynamic (Docker containers, Kubernetes pods)
- Multiple agents allow parallel execution

---

### 6.3 Installing Jenkins

```bash
# Option 1: Docker (recommended for learning)
docker run -d \
  --name jenkins \
  -p 8080:8080 \
  -p 50000:50000 \
  -v jenkins-data:/var/jenkins_home \
  jenkins/jenkins:lts

# Get initial admin password
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
# Open http://localhost:8080

# Option 2: Kubernetes (production)
helm repo add jenkins https://charts.jenkins.io
helm repo update

helm install jenkins jenkins/jenkins \
  --namespace jenkins \
  --create-namespace \
  --set controller.serviceType=LoadBalancer \
  --set persistence.enabled=true \
  --set persistence.size=20Gi
```

---

### 6.4 Essential Jenkins Configuration

**Configure credentials (never hardcode secrets):**
1. Jenkins → Manage Jenkins → Manage Credentials
2. Add: Username/Password, SSH key, Secret text, Docker registry

**Install essential plugins:**
- Pipeline (built-in)
- Git (built-in)
- Docker Pipeline
- Kubernetes Plugin
- Blue Ocean (better UI)
- AnsiColor (coloured logs)
- Timestamper (timestamps in logs)
- Slack Notification

---

---

## Lesson 7 — Jenkins Pipelines — Declarative and Scripted

> **Level:** Intermediate
> **Goal:** Write production-grade Jenkins pipelines

---

### 7.1 Jenkinsfile — Pipeline as Code

A Jenkinsfile is stored in your repository root. It defines the pipeline. This means your CI/CD configuration is version-controlled alongside your code — every change is tracked, reviewed, and auditable.

**Two syntax types:**

| Aspect | Declarative | Scripted |
|---|---|---|
| **Syntax** | Structured, opinionated | Groovy scripting |
| **Learning curve** | Easier | Steeper |
| **Error handling** | Built-in directives | Try/catch blocks |
| **Flexibility** | Good | Maximum |
| **Recommendation** | Start here | For complex requirements |

---

### 7.2 Declarative Pipeline — Complete Reference

```groovy
// Jenkinsfile (Declarative)
pipeline {
    // Where to run: any agent, specific label, Docker container
    agent {
        docker {
            image 'node:18-alpine'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    // Pipeline-level environment variables
    environment {
        APP_NAME        = 'my-api'
        DOCKER_REGISTRY = 'mycompany.azurecr.io'
        IMAGE_TAG       = "${BUILD_NUMBER}-${GIT_COMMIT[0..6]}"
        // Credential binding (value not printed in logs)
        NEXUS_CREDS     = credentials('nexus-credentials')  // sets NEXUS_CREDS_USR and NEXUS_CREDS_PSW
        SONAR_TOKEN     = credentials('sonar-token')
    }

    // Build options
    options {
        timeout(time: 30, unit: 'MINUTES')   // Fail build if it takes > 30 min
        buildDiscarder(logRotator(numToKeepStr: '20'))  // Keep last 20 builds
        disableConcurrentBuilds()            // No parallel builds of same branch
        timestamps()                         // Add timestamps to all log lines
        ansiColor('xterm')                   // Coloured log output
    }

    // Parameterised builds
    parameters {
        choice(name: 'DEPLOY_ENV', choices: ['dev', 'staging', 'production'], description: 'Deploy to environment')
        booleanParam(name: 'RUN_E2E', defaultValue: false, description: 'Run E2E tests')
        string(name: 'VERSION_TAG', defaultValue: '', description: 'Override version tag')
    }

    // Trigger configuration
    triggers {
        pollSCM('H/5 * * * *')      // Poll git every 5 minutes (legacy — prefer webhooks)
        cron('H 2 * * 1-5')         // Nightly build Mon-Fri at ~2am
    }

    stages {
        // ─── STAGE 1: CHECKOUT ──────────────────────────────────────
        stage('Checkout') {
            steps {
                checkout scm
                sh 'git log -1 --format="%H %s"'  // Print last commit
            }
        }

        // ─── STAGE 2: INSTALL ───────────────────────────────────────
        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
                sh 'npm audit --audit-level=high'
            }
        }

        // ─── STAGE 3: BUILD AND TEST (parallel) ─────────────────────
        stage('Build and Test') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        sh 'npm run test:unit -- --ci --coverage'
                    }
                    post {
                        always {
                            junit 'coverage/junit.xml'
                            publishCoverage adapters: [coberturaAdapter('coverage/cobertura-coverage.xml')]
                        }
                    }
                }
                stage('Lint') {
                    steps {
                        sh 'npm run lint'
                    }
                }
                stage('Security Scan') {
                    steps {
                        sh 'npm audit --audit-level=critical'
                    }
                }
            }
        }

        // ─── STAGE 4: BUILD ─────────────────────────────────────────
        stage('Build Application') {
            steps {
                sh 'npm run build'
            }
        }

        // ─── STAGE 5: DOCKER BUILD AND PUSH ─────────────────────────
        stage('Docker Build and Push') {
            when {
                anyOf {
                    branch 'main'
                    branch 'develop'
                }
            }
            steps {
                script {
                    docker.withRegistry("https://${DOCKER_REGISTRY}", 'acr-credentials') {
                        def image = docker.build("${DOCKER_REGISTRY}/${APP_NAME}:${IMAGE_TAG}")
                        image.push()
                        image.push('latest')
                    }
                }
            }
        }

        // ─── STAGE 6: DEPLOY TO STAGING ─────────────────────────────
        stage('Deploy to Staging') {
            when { branch 'main' }
            steps {
                withKubeConfig([credentialsId: 'kubeconfig-staging']) {
                    sh """
                        helm upgrade --install ${APP_NAME} ./helm/${APP_NAME} \
                          --namespace staging \
                          --set image.tag=${IMAGE_TAG} \
                          --set environment=staging \
                          --wait --timeout=5m
                    """
                }
            }
        }

        // ─── STAGE 7: APPROVAL GATE ─────────────────────────────────
        stage('Production Approval') {
            when { branch 'main' }
            steps {
                timeout(time: 24, unit: 'HOURS') {
                    input(
                        message: "Deploy ${APP_NAME}:${IMAGE_TAG} to PRODUCTION?",
                        submitter: 'lead-engineers,release-managers',
                        parameters: [
                            booleanParam(name: 'CONFIRM', defaultValue: false, description: 'Confirm production deployment')
                        ]
                    )
                }
            }
        }

        // ─── STAGE 8: DEPLOY TO PRODUCTION ──────────────────────────
        stage('Deploy to Production') {
            when { branch 'main' }
            steps {
                withKubeConfig([credentialsId: 'kubeconfig-production']) {
                    sh """
                        helm upgrade --install ${APP_NAME} ./helm/${APP_NAME} \
                          --namespace production \
                          --set image.tag=${IMAGE_TAG} \
                          --set environment=production \
                          --set replicaCount=5 \
                          --wait --timeout=10m
                    """
                }
            }
        }
    }

    // ─── POST-STAGE ACTIONS ──────────────────────────────────────────
    post {
        success {
            slackSend(
                channel: '#deployments',
                color: 'good',
                message: "✅ ${APP_NAME} ${IMAGE_TAG} deployed to production by ${BUILD_USER}"
            )
        }
        failure {
            slackSend(
                channel: '#alerts',
                color: 'danger',
                message: "❌ ${APP_NAME} build FAILED: ${BUILD_URL}"
            )
            emailext(
                to: 'devops-team@company.com',
                subject: "Jenkins Build Failed: ${JOB_NAME} #${BUILD_NUMBER}",
                body: "Build failed. See: ${BUILD_URL}"
            )
        }
        always {
            cleanWs()   // Clean workspace after every build
        }
    }
}
```

---

### 7.3 Jenkins Shared Libraries — Reusable Pipeline Code

Shared libraries let you write pipeline functions once and use them across all pipelines. Store in a separate Git repo.

**Library structure:**
```
jenkins-shared-library/
├── vars/
│   ├── buildDockerImage.groovy    ← Global function
│   ├── deployToKubernetes.groovy
│   └── sendSlackNotification.groovy
└── src/
    └── com/mycompany/
        └── PipelineUtils.groovy   ← Groovy class
```

**vars/buildDockerImage.groovy:**
```groovy
def call(Map config) {
    def registry = config.registry ?: 'mycompany.azurecr.io'
    def imageName = config.imageName
    def imageTag = config.imageTag ?: env.BUILD_NUMBER

    docker.withRegistry("https://${registry}", 'acr-credentials') {
        def image = docker.build("${registry}/${imageName}:${imageTag}")
        image.push()
        image.push('latest')
        return image
    }
}
```

**Using the shared library in any Jenkinsfile:**
```groovy
@Library('jenkins-shared-library@main') _

pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                buildDockerImage(
                    imageName: 'my-api',
                    imageTag: "${BUILD_NUMBER}"
                )
            }
        }
    }
}
```


---

---

## Lesson 8 — GitHub Actions — Complete Guide

> **Level:** Intermediate
> **Goal:** Master GitHub Actions for modern CI/CD workflows

---

### 8.1 GitHub Actions Architecture

```
Repository Event (push, PR, tag, schedule)
              │
              ▼
         Workflow (.github/workflows/*.yml)
              │
     ┌────────┼────────┐
     ▼        ▼        ▼
   Job 1    Job 2    Job 3    ← Run in parallel by default
     │                         unless 'needs:' defined
     ▼
  Runner (ubuntu-latest / windows / macos / self-hosted)
     │
  ┌──┴──────────────┐
  │ Steps           │
  │  - uses: action │  ← Reusable action from Marketplace
  │  - run: command │  ← Shell command
  └─────────────────┘
```

**Key concepts:**

| Concept | Description |
|---|---|
| **Workflow** | YAML file in `.github/workflows/` — defines the automation |
| **Event** | Trigger: push, pull_request, schedule, workflow_dispatch |
| **Job** | A set of steps running on one runner |
| **Step** | Individual task — a `uses:` action or `run:` shell command |
| **Runner** | The machine executing the job (GitHub-hosted or self-hosted) |
| **Action** | Reusable step from GitHub Marketplace |
| **Secret** | Encrypted environment variable set in repo/org settings |
| **Environment** | Deployment target with protection rules and secrets |
| **Artifact** | Files passed between jobs or downloaded after a run |
| **Cache** | Persist files between runs (node_modules, .m2, etc.) |

---

### 8.2 Complete Production GitHub Actions Workflow

```yaml
# .github/workflows/production-pipeline.yml
name: Production CI/CD Pipeline

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  workflow_dispatch:
    inputs:
      environment:
        description: 'Deploy to environment'
        required: true
        default: 'staging'
        type: choice
        options: [staging, production]

env:
  REGISTRY: mycompany.azurecr.io
  IMAGE_NAME: my-api
  NODE_VERSION: '18'

# Cancel in-progress runs on the same branch
concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  # ─── JOB 1: VALIDATE ─────────────────────────────────────────────
  validate:
    name: Validate Code
    runs-on: ubuntu-latest
    outputs:
      version: ${{ steps.version.outputs.tag }}

    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0   # Full history for version calculation

      - uses: actions/setup-node@v4
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Lint code
        run: npm run lint

      - name: Check types
        run: npm run type-check

      - name: Calculate version
        id: version
        run: |
          TAG=$(git describe --tags --abbrev=0 2>/dev/null || echo "0.0.0")
          SHA=$(git rev-parse --short HEAD)
          echo "tag=${TAG}-${SHA}" >> $GITHUB_OUTPUT
          echo "Version: ${TAG}-${SHA}"

  # ─── JOB 2: TEST ──────────────────────────────────────────────────
  test:
    name: Test Suite
    runs-on: ubuntu-latest
    needs: validate
    services:
      postgres:
        image: postgres:15-alpine
        env:
          POSTGRES_PASSWORD: testpass
          POSTGRES_DB: testdb
        options: --health-cmd pg_isready --health-interval 10s --health-retries 5
        ports:
          - 5432:5432

    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: 'npm'

      - run: npm ci

      - name: Run all tests
        run: npm test -- --coverage --ci
        env:
          DB_URL: postgresql://postgres:testpass@localhost:5432/testdb

      - name: Upload coverage
        uses: codecov/codecov-action@v3
        if: always()

  # ─── JOB 3: SECURITY ─────────────────────────────────────────────
  security:
    name: Security Scan
    runs-on: ubuntu-latest
    needs: validate
    permissions:
      security-events: write

    steps:
      - uses: actions/checkout@v4

      - name: Run Trivy filesystem scan
        uses: aquasecurity/trivy-action@master
        with:
          scan-type: fs
          severity: CRITICAL,HIGH
          format: sarif
          output: trivy-results.sarif
          exit-code: 1

      - name: Upload security results
        uses: github/codeql-action/upload-sarif@v3
        if: always()
        with:
          sarif_file: trivy-results.sarif

  # ─── JOB 4: BUILD DOCKER IMAGE ───────────────────────────────────
  build:
    name: Build and Push Image
    runs-on: ubuntu-latest
    needs: [test, security]
    if: github.event_name != 'pull_request'
    outputs:
      image-digest: ${{ steps.build.outputs.digest }}

    permissions:
      contents: read
      packages: write
      id-token: write   # OIDC for Azure login

    steps:
      - uses: actions/checkout@v4

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Azure Login (OIDC — no secrets!)
        uses: azure/login@v2
        with:
          client-id: ${{ secrets.AZURE_CLIENT_ID }}
          tenant-id: ${{ secrets.AZURE_TENANT_ID }}
          subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}

      - name: Login to Azure Container Registry
        run: az acr login --name mycompany

      - name: Extract metadata
        id: meta
        uses: docker/metadata-action@v5
        with:
          images: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}
          tags: |
            type=sha,prefix=,format=short
            type=ref,event=branch
            type=semver,pattern={{version}}

      - name: Build and push
        id: build
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
          cache-from: type=gha
          cache-to: type=gha,mode=max
          build-args: |
            BUILD_DATE=${{ github.event.head_commit.timestamp }}
            GIT_SHA=${{ github.sha }}

      - name: Scan pushed image
        uses: aquasecurity/trivy-action@master
        with:
          image-ref: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}:${{ github.sha }}
          severity: CRITICAL
          exit-code: 1

  # ─── JOB 5: DEPLOY STAGING ───────────────────────────────────────
  deploy-staging:
    name: Deploy to Staging
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: staging
      url: https://staging.myapp.com

    steps:
      - uses: actions/checkout@v4

      - name: Azure Login
        uses: azure/login@v2
        with:
          client-id: ${{ secrets.AZURE_CLIENT_ID }}
          tenant-id: ${{ secrets.AZURE_TENANT_ID }}
          subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}

      - name: Get AKS credentials
        run: |
          az aks get-credentials \
            --resource-group myapp-rg \
            --name myapp-staging-aks

      - name: Deploy with Helm
        run: |
          helm upgrade --install ${{ env.IMAGE_NAME }} ./helm \
            --namespace staging \
            --create-namespace \
            --set image.repository=${{ env.REGISTRY }}/${{ env.IMAGE_NAME }} \
            --set image.tag=${{ github.sha }} \
            --set environment=staging \
            --wait --timeout=5m

      - name: Run smoke tests
        run: |
          sleep 30
          curl -f https://staging.myapp.com/health || exit 1

  # ─── JOB 6: DEPLOY PRODUCTION ────────────────────────────────────
  deploy-production:
    name: Deploy to Production
    runs-on: ubuntu-latest
    needs: deploy-staging
    environment:
      name: production          # Configure approval in GitHub Environments
      url: https://myapp.com

    steps:
      - uses: actions/checkout@v4

      - name: Azure Login
        uses: azure/login@v2
        with:
          client-id: ${{ secrets.AZURE_CLIENT_ID }}
          tenant-id: ${{ secrets.AZURE_TENANT_ID }}
          subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}

      - name: Get AKS credentials
        run: az aks get-credentials --resource-group myapp-rg --name myapp-prod-aks

      - name: Deploy with Helm
        run: |
          helm upgrade --install ${{ env.IMAGE_NAME }} ./helm \
            --namespace production \
            --set image.tag=${{ github.sha }} \
            --set environment=production \
            --set replicaCount=5 \
            --wait --timeout=10m

      - name: Verify deployment
        run: |
          kubectl rollout status deployment/${{ env.IMAGE_NAME }} -n production
          curl -f https://myapp.com/health || exit 1
```

---

### 8.3 Reusable Workflows — DRY Pipelines

```yaml
# .github/workflows/reusable-deploy.yml
name: Reusable Deploy Workflow

on:
  workflow_call:
    inputs:
      environment:
        required: true
        type: string
      image-tag:
        required: true
        type: string
      replicas:
        required: false
        type: number
        default: 2
    secrets:
      AZURE_CLIENT_ID:
        required: true
      KUBECONFIG:
        required: true
    outputs:
      deployment-url:
        description: URL of the deployed application
        value: ${{ jobs.deploy.outputs.url }}

jobs:
  deploy:
    runs-on: ubuntu-latest
    environment: ${{ inputs.environment }}
    outputs:
      url: ${{ steps.get-url.outputs.url }}
    steps:
      - uses: actions/checkout@v4
      - name: Deploy
        run: |
          helm upgrade --install myapp ./helm \
            --set image.tag=${{ inputs.image-tag }} \
            --set replicaCount=${{ inputs.replicas }}
      - name: Get URL
        id: get-url
        run: echo "url=https://${{ inputs.environment }}.myapp.com" >> $GITHUB_OUTPUT
```

**Calling the reusable workflow:**
```yaml
jobs:
  deploy-staging:
    uses: ./.github/workflows/reusable-deploy.yml
    with:
      environment: staging
      image-tag: ${{ github.sha }}
      replicas: 2
    secrets:
      AZURE_CLIENT_ID: ${{ secrets.AZURE_CLIENT_ID }}
      KUBECONFIG: ${{ secrets.STAGING_KUBECONFIG }}

  deploy-production:
    needs: deploy-staging
    uses: ./.github/workflows/reusable-deploy.yml
    with:
      environment: production
      image-tag: ${{ github.sha }}
      replicas: 5
    secrets:
      AZURE_CLIENT_ID: ${{ secrets.AZURE_CLIENT_ID }}
      KUBECONFIG: ${{ secrets.PROD_KUBECONFIG }}
```

---

---

## Lesson 9 — GitLab CI/CD — Complete Guide

> **Level:** Intermediate
> **Goal:** Master GitLab CI/CD for full DevOps workflows

---

### 9.1 GitLab CI/CD Architecture

GitLab CI/CD uses a `.gitlab-ci.yml` file in the repository root. GitLab Runners (similar to GitHub Actions runners) execute jobs.

```yaml
# .gitlab-ci.yml structure
stages:
  - validate
  - test
  - build
  - deploy-staging
  - deploy-production

variables:
  DOCKER_DRIVER: overlay2
  DOCKER_TLS_CERTDIR: "/certs"
  IMAGE_NAME: $CI_REGISTRY_IMAGE:$CI_COMMIT_SHORT_SHA

# Global settings applied to all jobs
default:
  image: node:18-alpine
  before_script:
    - echo "Pipeline started for ${CI_COMMIT_REF_NAME}"
  interruptible: true     # Cancel older pipelines when new commit pushed
  retry:
    max: 1
    when: runner_system_failure
```

---

### 9.2 Complete GitLab CI/CD Pipeline

```yaml
# .gitlab-ci.yml — Complete production pipeline

stages:
  - validate
  - test
  - security
  - build
  - deploy-staging
  - integration-test
  - deploy-production

variables:
  IMAGE: $CI_REGISTRY_IMAGE:$CI_COMMIT_SHORT_SHA
  HELM_CHART: ./helm/myapp

# ─── STAGE: VALIDATE ──────────────────────────────────────────────
lint:
  stage: validate
  image: node:18-alpine
  script:
    - npm ci
    - npm run lint
  cache:
    key: ${CI_COMMIT_REF_SLUG}
    paths:
      - node_modules/
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == "main"

# ─── STAGE: TEST ──────────────────────────────────────────────────
unit-tests:
  stage: test
  image: node:18-alpine
  services:
    - name: postgres:15-alpine
      alias: postgres
      variables:
        POSTGRES_PASSWORD: testpass
        POSTGRES_DB: testdb
  variables:
    DB_URL: postgresql://postgres:testpass@postgres:5432/testdb
  script:
    - npm ci
    - npm test -- --coverage --ci
  coverage: '/Lines\s*:\s*(\d+\.?\d*)%/'   # Extract coverage % from output
  artifacts:
    when: always
    reports:
      junit: coverage/junit.xml
      coverage_report:
        coverage_format: cobertura
        path: coverage/cobertura-coverage.xml
    paths:
      - coverage/
    expire_in: 1 week

integration-tests:
  stage: test
  image: node:18-alpine
  services:
    - postgres:15-alpine
    - redis:7-alpine
  script:
    - npm ci
    - npm run test:integration
  rules:
    - if: $CI_COMMIT_BRANCH == "main"
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"

# ─── STAGE: SECURITY ──────────────────────────────────────────────
dependency-scanning:
  stage: security
  image:
    name: aquasec/trivy:latest
    entrypoint: [""]
  script:
    - trivy fs --exit-code 1 --severity CRITICAL,HIGH .
  allow_failure: false

sast:
  stage: security
  # GitLab built-in SAST (requires Ultimate license or use open-source tools)
  include:
    - template: Security/SAST.gitlab-ci.yml

# ─── STAGE: BUILD ─────────────────────────────────────────────────
docker-build:
  stage: build
  image: docker:24
  services:
    - docker:24-dind
  variables:
    DOCKER_BUILDKIT: "1"
  before_script:
    - docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY
  script:
    - |
      docker build \
        --cache-from $CI_REGISTRY_IMAGE:cache \
        --build-arg BUILDKIT_INLINE_CACHE=1 \
        --tag $IMAGE \
        --tag $CI_REGISTRY_IMAGE:latest \
        .
    - docker push $IMAGE
    - docker push $CI_REGISTRY_IMAGE:latest
    # Scan the pushed image
    - docker run --rm aquasec/trivy:latest image --exit-code 1 --severity CRITICAL $IMAGE
  rules:
    - if: $CI_COMMIT_BRANCH == "main"

# ─── STAGE: DEPLOY STAGING ────────────────────────────────────────
deploy-staging:
  stage: deploy-staging
  image: dtzar/helm-kubectl:3.13
  environment:
    name: staging
    url: https://staging.myapp.com
    on_stop: stop-staging
  script:
    - echo "$KUBECONFIG_STAGING" | base64 -d > kubeconfig
    - export KUBECONFIG=kubeconfig
    - |
      helm upgrade --install myapp $HELM_CHART \
        --namespace staging \
        --create-namespace \
        --set image.repository=$CI_REGISTRY_IMAGE \
        --set image.tag=$CI_COMMIT_SHORT_SHA \
        --set environment=staging \
        --wait --timeout=5m
    - kubectl rollout status deployment/myapp -n staging
  rules:
    - if: $CI_COMMIT_BRANCH == "main"

stop-staging:
  stage: deploy-staging
  environment:
    name: staging
    action: stop
  script:
    - helm uninstall myapp --namespace staging
  when: manual
  rules:
    - if: $CI_COMMIT_BRANCH == "main"

# ─── STAGE: INTEGRATION TEST ON STAGING ───────────────────────────
smoke-tests:
  stage: integration-test
  image: curlimages/curl:latest
  script:
    - sleep 30
    - curl -f https://staging.myapp.com/health
    - curl -f https://staging.myapp.com/api/version
  rules:
    - if: $CI_COMMIT_BRANCH == "main"

# ─── STAGE: DEPLOY PRODUCTION ─────────────────────────────────────
deploy-production:
  stage: deploy-production
  image: dtzar/helm-kubectl:3.13
  environment:
    name: production
    url: https://myapp.com
  script:
    - echo "$KUBECONFIG_PROD" | base64 -d > kubeconfig
    - export KUBECONFIG=kubeconfig
    - |
      helm upgrade --install myapp $HELM_CHART \
        --namespace production \
        --set image.tag=$CI_COMMIT_SHORT_SHA \
        --set environment=production \
        --set replicaCount=5 \
        --wait --timeout=10m
  when: manual   # Manual trigger for production
  rules:
    - if: $CI_COMMIT_BRANCH == "main"
```

---

### 9.3 GitLab CI/CD Key Features

**Environments with rollback:**
```yaml
deploy-production:
  environment:
    name: production
    url: https://myapp.com
  # GitLab tracks deployment history — rollback from UI or:
  script:
    - helm upgrade --install --atomic myapp ./helm
    # --atomic: rollback automatically if deployment fails
```

**Dynamic child pipelines:**
```yaml
# Parent pipeline generates child pipelines dynamically
generate-pipeline:
  stage: generate
  script:
    - python scripts/generate-pipeline.py > generated-pipeline.yml
  artifacts:
    paths:
      - generated-pipeline.yml

trigger-generated:
  stage: run
  trigger:
    include:
      - artifact: generated-pipeline.yml
        job: generate-pipeline
    strategy: depend
```

---

---

## Lesson 10 — Bitbucket Pipelines

> **Level:** Intermediate

---

### 10.1 Bitbucket Pipelines Configuration

```yaml
# bitbucket-pipelines.yml
image: node:18-alpine

options:
  max-time: 30   # Global timeout in minutes

definitions:
  caches:
    npm: node_modules   # Define custom cache

  steps:
    - step: &install-deps
        name: Install Dependencies
        script:
          - npm ci
        caches:
          - npm

    - step: &unit-tests
        name: Unit Tests
        script:
          - npm ci
          - npm test -- --ci
        caches:
          - npm
        artifacts:
          - coverage/**

pipelines:
  # PR pipelines
  pull-requests:
    '**':
      - step: *install-deps
      - step: *unit-tests
      - step:
          name: Code Quality
          script:
            - npm run lint

  # Branch-specific pipelines
  branches:
    main:
      - step: *install-deps
      - step: *unit-tests
      - step:
          name: Build Docker Image
          services:
            - docker
          script:
            - docker login -u $DOCKER_HUB_USER -p $DOCKER_HUB_PASSWORD
            - docker build -t mycompany/myapp:$BITBUCKET_COMMIT .
            - docker push mycompany/myapp:$BITBUCKET_COMMIT

      - step:
          name: Deploy to Staging
          deployment: staging
          script:
            - pipe: atlassian/aws-eks-kubectl-run:2.2.0
              variables:
                AWS_ACCESS_KEY_ID: $AWS_ACCESS_KEY_ID
                AWS_SECRET_ACCESS_KEY: $AWS_SECRET_ACCESS_KEY
                CLUSTER_NAME: myapp-staging
                KUBECTL_COMMAND: |
                  kubectl set image deployment/myapp \
                    myapp=mycompany/myapp:$BITBUCKET_COMMIT \
                    -n staging

      - step:
          name: Deploy to Production
          deployment: production
          trigger: manual
          script:
            - echo "Deploying to production..."

  # Release pipeline (triggered by tag)
  tags:
    'v*.*.*':
      - step:
          name: Release Build
          script:
            - echo "Building release ${BITBUCKET_TAG}"
            - npm run build
```

---

---

# PHASE 3 — DEVOPS LEVEL (PRODUCTION CI/CD)

---

## Lesson 11 — Docker in CI/CD Pipelines

> **Level:** DevOps Engineer
> **Goal:** Build production-quality Docker image pipelines

---

### 11.1 The Docker CI/CD Pattern

```
Source Code
     │
     ▼
docker build      ← Build image from Dockerfile
     │
     ▼
Image scanning    ← Trivy, Snyk, Anchore
     │
     ▼
docker push       ← Push to registry (ACR, ECR, GHCR)
     │
     ▼
Deploy            ← Update Kubernetes deployment to new image tag
```

---

### 11.2 Multi-Stage Dockerfile for CI

```dockerfile
# ─── Stage 1: Dependencies ────────────────────────────────────────
FROM node:18-alpine AS deps
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

# ─── Stage 2: Builder ─────────────────────────────────────────────
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# ─── Stage 3: Test ────────────────────────────────────────────────
# Run tests as a separate stage — fail the build if tests fail
FROM builder AS test
RUN npm test -- --ci
RUN npm run lint

# ─── Stage 4: Production ──────────────────────────────────────────
FROM node:18-alpine AS production
WORKDIR /app

# Security: non-root user
RUN addgroup -g 1001 -S nodejs && adduser -S nodejs -u 1001

# Copy only production artifacts
COPY --from=deps --chown=nodejs:nodejs /app/node_modules ./node_modules
COPY --from=builder --chown=nodejs:nodejs /app/dist ./dist

USER nodejs
EXPOSE 3000
HEALTHCHECK --interval=30s --timeout=5s CMD wget -qO- http://localhost:3000/health || exit 1
CMD ["node", "dist/server.js"]
```

---

### 11.3 Complete Docker Build Pipeline

```yaml
# GitHub Actions — production Docker pipeline
name: Docker Pipeline

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

env:
  REGISTRY: ghcr.io
  IMAGE_NAME: ${{ github.repository }}

jobs:
  docker-build:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write
      security-events: write

    steps:
      - uses: actions/checkout@v4

      # Layer caching — dramatically speeds up builds
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Cache Docker layers
        uses: actions/cache@v3
        with:
          path: /tmp/.buildx-cache
          key: ${{ runner.os }}-buildx-${{ github.sha }}
          restore-keys: |
            ${{ runner.os }}-buildx-

      - name: Login to GHCR
        uses: docker/login-action@v3
        with:
          registry: ${{ env.REGISTRY }}
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Extract metadata
        id: meta
        uses: docker/metadata-action@v5
        with:
          images: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}
          tags: |
            type=sha,format=short
            type=ref,event=branch
            type=semver,pattern={{version}}
            type=raw,value=latest,enable=${{ github.ref == 'refs/heads/main' }}

      # Build test stage first — fail fast if tests fail
      - name: Build test stage
        uses: docker/build-push-action@v5
        with:
          context: .
          target: test    # Only build up to test stage
          push: false
          cache-from: type=local,src=/tmp/.buildx-cache

      # Build and push production image only if tests passed
      - name: Build and push production image
        id: build
        uses: docker/build-push-action@v5
        with:
          context: .
          target: production
          push: ${{ github.event_name != 'pull_request' }}
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
          cache-from: type=local,src=/tmp/.buildx-cache
          cache-to: type=local,dest=/tmp/.buildx-cache-new,mode=max

      # Prevent cache from growing indefinitely
      - name: Move cache
        run: |
          rm -rf /tmp/.buildx-cache
          mv /tmp/.buildx-cache-new /tmp/.buildx-cache

      # Scan the produced image
      - name: Scan image for vulnerabilities
        uses: aquasecurity/trivy-action@master
        if: github.event_name != 'pull_request'
        with:
          image-ref: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}:${{ github.sha }}
          format: sarif
          output: trivy-results.sarif
          severity: CRITICAL,HIGH
          exit-code: 1

      - name: Upload scan results to GitHub Security
        uses: github/codeql-action/upload-sarif@v3
        if: always()
        with:
          sarif_file: trivy-results.sarif
```

---

---

## Lesson 12 — Kubernetes Deployments Through CI/CD

> **Level:** DevOps Engineer
> **Goal:** Deploy applications to Kubernetes automatically and safely

---

### 12.1 The Kubernetes Deployment Pipeline

```
Build Docker Image → Push to Registry
           │
           ▼
Update Helm values with new image tag
           │
           ▼
helm upgrade --install (staging)
           │
           ▼
Wait for rollout: kubectl rollout status
           │
           ▼
Run smoke tests
           │
           ▼
[Manual approval gate]
           │
           ▼
helm upgrade --install (production)
           │
           ▼
Verify deployment: health check
           │
If fails → helm rollback automatically
```

---

### 12.2 Helm-Based Deployment in GitHub Actions

```yaml
# Reusable deployment job
deploy:
  name: Deploy to ${{ inputs.environment }}
  runs-on: ubuntu-latest
  environment:
    name: ${{ inputs.environment }}

  steps:
    - uses: actions/checkout@v4

    - name: Install Helm
      uses: azure/setup-helm@v3
      with:
        version: v3.13.0

    - name: Get AKS credentials
      uses: azure/aks-set-context@v3
      with:
        resource-group: myapp-rg
        cluster-name: myapp-${{ inputs.environment }}-aks

    - name: Deploy with Helm
      run: |
        helm upgrade --install myapp ./helm \
          --namespace ${{ inputs.environment }} \
          --create-namespace \
          --set image.repository=${{ env.REGISTRY }}/myapp \
          --set image.tag=${{ github.sha }} \
          --set replicaCount=${{ inputs.replicas }} \
          --set environment=${{ inputs.environment }} \
          --atomic \             # Auto-rollback if deployment fails
          --wait \               # Wait for all pods to be ready
          --timeout=10m \
          --history-max=10       # Keep last 10 release revisions

    - name: Verify deployment
      run: |
        kubectl rollout status deployment/myapp -n ${{ inputs.environment }} --timeout=5m
        echo "Checking application health..."
        kubectl run smoke-test \
          --image=curlimages/curl:latest \
          --rm \
          --restart=Never \
          -it \
          --namespace=${{ inputs.environment }} \
          -- curl -f http://myapp/health

    - name: Rollback on failure
      if: failure()
      run: |
        echo "Deployment failed, rolling back..."
        helm rollback myapp -n ${{ inputs.environment }}
        kubectl rollout status deployment/myapp -n ${{ inputs.environment }}
```

---

### 12.3 kubectl Rollout Strategies in CI/CD

```yaml
# Deployment YAML configured for zero-downtime
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 5
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1            # Create 1 extra pod before removing old ones
      maxUnavailable: 0      # Never remove old pods until new ones are ready
  template:
    spec:
      containers:
        - name: myapp
          image: myapp:NEW_TAG
          readinessProbe:
            httpGet:
              path: /ready
              port: 3000
            initialDelaySeconds: 10
            periodSeconds: 5
            failureThreshold: 3
          # Graceful shutdown: wait for in-flight requests
          lifecycle:
            preStop:
              exec:
                command: ["/bin/sh", "-c", "sleep 5"]
      terminationGracePeriodSeconds: 30
```

```bash
# In pipeline: wait for rollout to complete
kubectl set image deployment/myapp myapp=myapp:${NEW_TAG}
kubectl rollout status deployment/myapp --timeout=10m

# Rollback if health checks fail
if ! curl -f https://myapp.com/health; then
  echo "Health check failed, rolling back"
  kubectl rollout undo deployment/myapp
  exit 1
fi
```

---

---

## Lesson 13 — Terraform in CI/CD Pipelines

> **Level:** DevOps Engineer
> **Goal:** Automate infrastructure changes safely through CI/CD

---

### 13.1 The Infrastructure Pipeline Pattern

```
PR opened
    │
    ▼
terraform fmt -check   ← Fail if not formatted
terraform validate     ← Fail if syntax error
terraform plan         ← Post plan as PR comment
    │
    ▼
PR reviewed and APPROVED
    │
    ▼
Merged to main
    │
    ▼
terraform plan -out=tfplan   ← Save the exact plan
    │
    ▼
[Optional: Manual approval gate for production]
    │
    ▼
terraform apply tfplan        ← Apply EXACTLY the reviewed plan
    │
    ▼
State stored in Azure Blob / S3
```

---

### 13.2 Complete Terraform CI/CD Pipeline

```yaml
# .github/workflows/terraform.yml
name: Terraform Infrastructure Pipeline

on:
  push:
    branches: [main]
    paths: ['infrastructure/**']
  pull_request:
    branches: [main]
    paths: ['infrastructure/**']

permissions:
  contents: read
  pull-requests: write
  id-token: write

env:
  TF_DIR: infrastructure/environments/production
  TF_VERSION: 1.6.0
  ARM_SUBSCRIPTION_ID: ${{ secrets.ARM_SUBSCRIPTION_ID }}
  ARM_TENANT_ID: ${{ secrets.ARM_TENANT_ID }}
  ARM_CLIENT_ID: ${{ secrets.ARM_CLIENT_ID }}   # OIDC

jobs:
  terraform-plan:
    name: Terraform Plan
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: hashicorp/setup-terraform@v3
        with:
          terraform_version: ${{ env.TF_VERSION }}

      - name: Azure Login
        uses: azure/login@v2
        with:
          client-id: ${{ secrets.ARM_CLIENT_ID }}
          tenant-id: ${{ secrets.ARM_TENANT_ID }}
          subscription-id: ${{ secrets.ARM_SUBSCRIPTION_ID }}

      - name: Terraform Format Check
        id: fmt
        run: terraform fmt -check -recursive
        working-directory: ${{ env.TF_DIR }}
        continue-on-error: true

      - name: Terraform Init
        id: init
        run: terraform init
        working-directory: ${{ env.TF_DIR }}

      - name: Terraform Validate
        id: validate
        run: terraform validate
        working-directory: ${{ env.TF_DIR }}

      - name: Terraform Plan
        id: plan
        run: |
          terraform plan \
            -var-file="terraform.tfvars" \
            -out=tfplan \
            -no-color 2>&1 | tee plan-output.txt
        working-directory: ${{ env.TF_DIR }}
        continue-on-error: true

      - name: Comment Plan on PR
        uses: actions/github-script@v7
        if: github.event_name == 'pull_request'
        with:
          script: |
            const fs = require('fs');
            const plan = fs.readFileSync('${{ env.TF_DIR }}/plan-output.txt', 'utf8');
            const truncated = plan.length > 65000 ? plan.substring(0, 65000) + '\n...(truncated)' : plan;
            const output = `## Terraform Plan Results
            
            | Step | Status |
            |------|--------|
            | Format | ${{ steps.fmt.outcome == 'success' && '✅' || '❌' }} \`${{ steps.fmt.outcome }}\` |
            | Init | ${{ steps.init.outcome == 'success' && '✅' || '❌' }} \`${{ steps.init.outcome }}\` |
            | Validate | ${{ steps.validate.outcome == 'success' && '✅' || '❌' }} \`${{ steps.validate.outcome }}\` |
            | Plan | ${{ steps.plan.outcome == 'success' && '✅' || '❌' }} \`${{ steps.plan.outcome }}\` |
            
            <details><summary>Show Plan</summary>
            
            \`\`\`hcl
            ${truncated}
            \`\`\`
            </details>
            
            *Triggered by @${{ github.actor }} on \`${{ github.event_name }}\`*`;
            
            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: output
            });

      - name: Save plan artifact
        uses: actions/upload-artifact@v4
        with:
          name: tfplan
          path: ${{ env.TF_DIR }}/tfplan
          retention-days: 3

      - name: Fail if plan failed
        if: steps.plan.outcome == 'failure'
        run: exit 1

  terraform-apply:
    name: Terraform Apply
    runs-on: ubuntu-latest
    needs: terraform-plan
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    environment: production

    steps:
      - uses: actions/checkout@v4

      - uses: hashicorp/setup-terraform@v3
        with:
          terraform_version: ${{ env.TF_VERSION }}

      - name: Azure Login
        uses: azure/login@v2
        with:
          client-id: ${{ secrets.ARM_CLIENT_ID }}
          tenant-id: ${{ secrets.ARM_TENANT_ID }}
          subscription-id: ${{ secrets.ARM_SUBSCRIPTION_ID }}

      - name: Download plan
        uses: actions/download-artifact@v4
        with:
          name: tfplan
          path: ${{ env.TF_DIR }}

      - name: Terraform Init
        run: terraform init
        working-directory: ${{ env.TF_DIR }}

      - name: Terraform Apply
        run: terraform apply -auto-approve tfplan
        working-directory: ${{ env.TF_DIR }}
```

---

---

## Lesson 14 — Blue-Green and Canary Deployments

> **Level:** DevOps Engineer
> **Goal:** Implement zero-risk deployment strategies

---

### 14.1 Blue-Green Deployments

Blue-Green runs two identical environments — blue (current production) and green (new version). Traffic switches instantly between them.

```
                         Load Balancer
                              │
                    ┌─────────┴─────────┐
            (100%) ▼                   ▼ (0%)
           ┌──────────────┐   ┌──────────────┐
           │   BLUE       │   │   GREEN      │
           │  (v1 - LIVE) │   │  (v2 - IDLE) │
           └──────────────┘   └──────────────┘

Deploy v2 to GREEN:
  1. Deploy v2 to green environment (no traffic)
  2. Run smoke tests on green
  3. Switch load balancer: blue (0%) → green (100%)
  4. Monitor green for issues
  5. If good: blue becomes idle (ready for next release)
  6. If bad: switch back to blue instantly
```

**Blue-Green with Kubernetes and Helm:**
```yaml
# Blue-Green deployment script in pipeline
CURRENT_COLOR=$(kubectl get service myapp -n production -o jsonpath='{.spec.selector.color}')
NEW_COLOR=$([ "$CURRENT_COLOR" = "blue" ] && echo "green" || echo "blue")

# Deploy new version to inactive color
helm upgrade --install myapp-${NEW_COLOR} ./helm \
  --namespace production \
  --set color=${NEW_COLOR} \
  --set image.tag=${NEW_TAG} \
  --set service.enabled=false \    # No service — not receiving traffic yet
  --wait

# Run smoke tests on new deployment
kubectl run smoke \
  --image=curlimages/curl \
  --rm -it --restart=Never \
  -- curl -f http://myapp-${NEW_COLOR}/health

# Switch traffic to new deployment
kubectl patch service myapp -n production \
  -p "{\"spec\":{\"selector\":{\"color\":\"${NEW_COLOR}\"}}}"

echo "Traffic switched to ${NEW_COLOR} (${NEW_TAG})"
echo "Old ${CURRENT_COLOR} is still running for rollback"
```

---

### 14.2 Canary Deployments

Canary releases send a small percentage of traffic to the new version while most traffic stays on the stable version.

```
Users: 1000/second
         │
         ▼
    Load Balancer
    ┌────────────────────────────────────┐
    │                                    │
    ▼ (950/sec, 95%)                    ▼ (50/sec, 5%)
┌──────────────┐                ┌──────────────┐
│  STABLE      │                │   CANARY     │
│  (v1)        │                │   (v2)       │
│  3 replicas  │                │  1 replica   │
└──────────────┘                └──────────────┘
```

**Canary with Kubernetes (replica-based):**
```yaml
# Canary deployment YAML
# Main deployment (v1): 9 replicas
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-stable
spec:
  replicas: 9
  selector:
    matchLabels:
      app: myapp
      track: stable
  template:
    metadata:
      labels:
        app: myapp
        track: stable
    spec:
      containers:
        - image: myapp:v1
---
# Canary deployment (v2): 1 replica = 10% of traffic
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-canary
spec:
  replicas: 1   # 1 out of 10 total = 10%
  selector:
    matchLabels:
      app: myapp
      track: canary
  template:
    metadata:
      labels:
        app: myapp
        track: canary
    spec:
      containers:
        - image: myapp:v2
---
# Service selects BOTH deployments by app label only
apiVersion: v1
kind: Service
metadata:
  name: myapp
spec:
  selector:
    app: myapp   # Matches both stable and canary pods
```

**Progressive canary pipeline:**
```yaml
# Pipeline stages for progressive canary
deploy-canary-10:
  script:
    - kubectl scale deployment myapp-canary --replicas=1
    - kubectl scale deployment myapp-stable --replicas=9
    - echo "Canary at 10% — monitoring for 10 minutes"
    - sleep 600
    - check-error-rate.sh  # Custom script checking Prometheus metrics

deploy-canary-50:
  script:
    - kubectl scale deployment myapp-canary --replicas=5
    - kubectl scale deployment myapp-stable --replicas=5
    - sleep 600
    - check-error-rate.sh

deploy-full:
  script:
    - kubectl set image deployment/myapp-stable myapp=myapp:v2
    - kubectl scale deployment myapp-canary --replicas=0
```

---

---

## Lesson 15 — CI/CD Security Best Practices

> **Level:** DevOps Engineer
> **Goal:** Build secure pipelines that don't become attack vectors

---

### 15.1 The Pipeline Attack Surface

CI/CD pipelines are high-value targets:
- They have credentials for every environment
- They run arbitrary code from commits
- A compromised pipeline can deploy malicious code to production
- A developer with pipeline access can exfiltrate secrets

**Real incidents:** SolarWinds attack (malicious code injected into build pipeline), CodeCov breach (secrets stolen from CI environment), countless supply chain attacks via compromised npm packages.

---

### 15.2 Secrets Management in Pipelines

```yaml
# WRONG — secret in code (never do this)
env:
  DB_PASSWORD: "mysecretpassword123"

# WRONG — secret in environment variable visible in logs
- run: echo $DB_PASSWORD    # This prints the secret!

# RIGHT — use repository/org secrets
env:
  DB_PASSWORD: ${{ secrets.DB_PASSWORD }}
  # GitHub masks this value in logs automatically

# RIGHT — use OIDC (no stored credentials at all)
- name: Azure Login
  uses: azure/login@v2
  with:
    client-id: ${{ secrets.AZURE_CLIENT_ID }}
    tenant-id: ${{ secrets.AZURE_TENANT_ID }}
    subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}
  # No client secret — uses federated identity (OIDC)
```

**Never print secrets in pipeline logs:**
```yaml
# WRONG
- run: |
    echo "Connecting to DB: $DB_PASSWORD"  # Secret exposed in logs!
    
# RIGHT — mask or don't print at all
- run: |
    echo "Connecting to database..."
    # Just don't print secrets
    
# In Jenkins — mask credentials
withCredentials([string(credentialsId: 'db-password', variable: 'DB_PASS')]) {
    sh 'connect-to-db.sh'   # $DB_PASS never appears in logs
}
```

---

### 15.3 Dependency Security

```yaml
# Lock dependencies — prevent supply chain attacks
- name: Install dependencies
  run: npm ci    # Uses package-lock.json exactly

# Check for known vulnerabilities
- name: Security audit
  run: npm audit --audit-level=high

# Dependabot — automated dependency updates with security patches
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: npm
    directory: /
    schedule:
      interval: weekly
    open-pull-requests-limit: 5
    labels:
      - "dependencies"
      - "security"
  - package-ecosystem: docker
    directory: /
    schedule:
      interval: weekly
  - package-ecosystem: github-actions
    directory: /.github/workflows
    schedule:
      interval: weekly
```

---

### 15.4 Pipeline Permissions — Least Privilege

```yaml
# GitHub Actions — restrict permissions at workflow level
permissions:
  contents: read      # Read-only to repo (default is read-write!)
  packages: write     # Write to GHCR (only if needed)
  id-token: write     # For OIDC
  security-events: write  # For SARIF uploads

# Further restrict at job level
jobs:
  build:
    permissions:
      contents: read
      packages: write
  
  test:
    permissions:
      contents: read    # Test job has no write access at all
```

---

### 15.5 Pin Action Versions to Commit SHA

```yaml
# WRONG — mutable tag, can be changed by action author
- uses: actions/checkout@v4

# RIGHT — pinned to immutable commit SHA
- uses: actions/checkout@b4ffde65f46336ab88eb53be808477a3936bae11  # v4.1.1
  # The action cannot change without the SHA changing
  # Protects against compromised action tags
```

---

---

## Lesson 16 — Pipeline Optimisation and Caching

> **Level:** DevOps Engineer
> **Goal:** Make pipelines fast — slow pipelines get ignored

---

### 16.1 Why Pipeline Speed Matters

**The feedback loop cost:**
- 5-minute pipeline: developer waits at desk, maintains context
- 30-minute pipeline: developer switches tasks, loses context
- 60-minute pipeline: developer has forgotten what they changed

**The economics:** If 20 developers each trigger 5 pipeline runs per day and each run takes 15 minutes, that's 25 hours of developer waiting time daily. Cut pipeline time to 5 minutes and you save 17 hours/day.

---

### 16.2 Caching Strategies

```yaml
# GitHub Actions — comprehensive caching

# npm packages
- uses: actions/cache@v3
  with:
    path: ~/.npm
    key: ${{ runner.os }}-npm-${{ hashFiles('**/package-lock.json') }}
    restore-keys: |
      ${{ runner.os }}-npm-

# Maven (.m2 repository)
- uses: actions/cache@v3
  with:
    path: ~/.m2/repository
    key: ${{ runner.os }}-maven-${{ hashFiles('**/pom.xml') }}
    restore-keys: |
      ${{ runner.os }}-maven-

# Gradle
- uses: actions/cache@v3
  with:
    path: |
      ~/.gradle/caches
      ~/.gradle/wrapper
    key: ${{ runner.os }}-gradle-${{ hashFiles('**/*.gradle*') }}

# pip (Python)
- uses: actions/cache@v3
  with:
    path: ~/.cache/pip
    key: ${{ runner.os }}-pip-${{ hashFiles('requirements.txt') }}

# Docker layers (BuildKit)
- uses: docker/setup-buildx-action@v3
- name: Build with layer caching
  uses: docker/build-push-action@v5
  with:
    cache-from: type=gha   # Use GitHub Actions cache
    cache-to: type=gha,mode=max
```

---

### 16.3 Parallel Jobs

```yaml
# Run independent jobs in parallel
jobs:
  unit-tests:
    runs-on: ubuntu-latest
    steps: [...]

  integration-tests:
    runs-on: ubuntu-latest
    steps: [...]

  security-scan:
    runs-on: ubuntu-latest
    steps: [...]

  lint:
    runs-on: ubuntu-latest
    steps: [...]

  # Only runs after ALL of the above pass
  build:
    needs: [unit-tests, integration-tests, security-scan, lint]
    runs-on: ubuntu-latest
    steps: [...]
```

---

### 16.4 Conditional Steps — Skip Unnecessary Work

```yaml
# Only rebuild Docker image if relevant files changed
- name: Check if Docker rebuild needed
  id: changed-files
  uses: tj-actions/changed-files@v40
  with:
    files: |
      Dockerfile
      src/**
      package*.json

- name: Build Docker image
  if: steps.changed-files.outputs.any_changed == 'true'
  run: docker build -t myapp .

# Skip E2E tests on non-main branches
- name: Run E2E tests
  if: github.ref == 'refs/heads/main' || github.event_name == 'workflow_dispatch'
  run: npm run test:e2e
```


---

---

# PHASE 4 — ADVANCED ARCHITECTURE

---

## Lesson 17 — Multi-Environment Pipelines

> **Level:** Advanced
> **Goal:** Design pipelines that safely promote artifacts across dev, staging, and production

---

### 17.1 The Promotion Model

The key principle: **build once, deploy many times**. The same artifact (Docker image, JAR) travels through environments. What changes between environments is only configuration, not the artifact itself.

```
                BUILD ONCE
                     │
                     ▼
         myapp:abc123def (immutable image)
                     │
         ┌───────────┼───────────┐
         ▼           ▼           ▼
       DEV         STAGING    PRODUCTION
     (same image)  (same image) (same image)
      config-dev   config-stag  config-prod
```

**Why this matters:**
- "Works in staging but breaks in prod" → you deployed different artifacts
- If you rebuild the image for production, you're not deploying what was tested
- Image tag = immutable identifier = deployment audit trail

---

### 17.2 Environment Configuration Pattern

```yaml
# environments/dev/values.yaml
replicaCount: 1
resources:
  requests: { cpu: 100m, memory: 128Mi }
  limits: { cpu: 200m, memory: 256Mi }
ingress:
  host: dev.myapp.com
config:
  logLevel: debug
  featureFlags:
    newCheckout: true
    betaUI: true

# environments/staging/values.yaml
replicaCount: 2
resources:
  requests: { cpu: 200m, memory: 256Mi }
  limits: { cpu: 500m, memory: 512Mi }
ingress:
  host: staging.myapp.com
config:
  logLevel: info
  featureFlags:
    newCheckout: true
    betaUI: false

# environments/production/values.yaml
replicaCount: 5
resources:
  requests: { cpu: 500m, memory: 512Mi }
  limits: { cpu: 1000m, memory: 1Gi }
ingress:
  host: myapp.com
config:
  logLevel: warn
  featureFlags:
    newCheckout: false
    betaUI: false
```

---

### 17.3 Complete Multi-Environment Pipeline

```yaml
# .github/workflows/multi-env-pipeline.yml
name: Multi-Environment CI/CD

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

env:
  IMAGE_TAG: ${{ github.sha }}
  REGISTRY: mycompany.azurecr.io

jobs:
  # ─── BUILD ONCE ───────────────────────────────────────────────────
  build:
    name: Build and Publish Artifact
    runs-on: ubuntu-latest
    if: github.event_name == 'push'
    outputs:
      image-tag: ${{ env.IMAGE_TAG }}

    steps:
      - uses: actions/checkout@v4
      - uses: docker/setup-buildx-action@v3
      - name: Build and push immutable image
        uses: docker/build-push-action@v5
        with:
          push: true
          tags: |
            ${{ env.REGISTRY }}/myapp:${{ env.IMAGE_TAG }}
          cache-from: type=gha
          cache-to: type=gha,mode=max

  # ─── DEPLOY DEV (automatic on every push) ─────────────────────────
  deploy-dev:
    name: Deploy to Development
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: development
      url: https://dev.myapp.com

    steps:
      - uses: actions/checkout@v4
      - name: Deploy to dev cluster
        run: |
          helm upgrade --install myapp ./helm \
            --namespace dev \
            --values environments/dev/values.yaml \
            --set image.tag=${{ env.IMAGE_TAG }} \
            --atomic --wait --timeout=5m

      - name: Dev smoke tests
        run: |
          curl -f https://dev.myapp.com/health
          curl -f https://dev.myapp.com/api/version

  # ─── DEPLOY STAGING (automatic after dev) ─────────────────────────
  deploy-staging:
    name: Deploy to Staging
    runs-on: ubuntu-latest
    needs: deploy-dev
    environment:
      name: staging
      url: https://staging.myapp.com

    steps:
      - uses: actions/checkout@v4
      - name: Deploy to staging cluster
        run: |
          helm upgrade --install myapp ./helm \
            --namespace staging \
            --values environments/staging/values.yaml \
            --set image.tag=${{ env.IMAGE_TAG }} \
            --atomic --wait --timeout=5m

      - name: Full regression suite on staging
        run: |
          npm run test:e2e -- --baseUrl=https://staging.myapp.com
          npm run test:performance -- --baseUrl=https://staging.myapp.com

      - name: Create GitHub Release
        uses: actions/create-release@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          tag_name: deploy-${{ github.run_number }}
          release_name: Staging validated - ${{ env.IMAGE_TAG }}
          body: "Staging deployment validated. Ready for production."

  # ─── DEPLOY PRODUCTION (manual approval) ──────────────────────────
  deploy-production:
    name: Deploy to Production
    runs-on: ubuntu-latest
    needs: deploy-staging
    environment:
      name: production       # Configure required reviewers in GitHub Environments
      url: https://myapp.com

    steps:
      - uses: actions/checkout@v4

      - name: Pre-deployment checks
        run: |
          # Check current production health before deploying
          curl -f https://myapp.com/health
          # Check no active incidents
          python scripts/check-incidents.py

      - name: Deploy to production
        run: |
          helm upgrade --install myapp ./helm \
            --namespace production \
            --values environments/production/values.yaml \
            --set image.tag=${{ env.IMAGE_TAG }} \
            --atomic --wait --timeout=10m

      - name: Post-deployment verification
        run: |
          sleep 30
          curl -f https://myapp.com/health
          # Check key business metrics haven't dropped
          python scripts/verify-metrics.py

      - name: Tag production release
        run: |
          git tag -a "prod-${{ github.run_number }}" \
            -m "Production deployment: ${{ env.IMAGE_TAG }}"
          git push origin "prod-${{ github.run_number }}"
```

---

---

## Lesson 18 — Microservices CI/CD Pipelines

> **Level:** Advanced
> **Goal:** Design independent, scalable pipelines for microservice architectures

---

### 18.1 The Microservices Pipeline Challenge

A monolith has one pipeline. A microservices architecture with 20 services has unique challenges:
- Each service has its own pipeline, language, build tool
- Services depend on each other — changing Service A may break Service B
- Rebuilding all 20 services on every commit is expensive and slow
- Integration testing requires multiple services running together

---

### 18.2 Monorepo Strategy — Build Only Changed Services

```yaml
# .github/workflows/monorepo-ci.yml
name: Monorepo CI/CD

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  detect-changes:
    name: Detect Changed Services
    runs-on: ubuntu-latest
    outputs:
      user-service: ${{ steps.changes.outputs.user-service }}
      order-service: ${{ steps.changes.outputs.order-service }}
      payment-service: ${{ steps.changes.outputs.payment-service }}
      api-gateway: ${{ steps.changes.outputs.api-gateway }}

    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Detect changed services
        id: changes
        uses: dorny/paths-filter@v2
        with:
          filters: |
            user-service:
              - 'services/user-service/**'
              - 'shared/auth/**'           # Shared lib change triggers user-service
            order-service:
              - 'services/order-service/**'
              - 'shared/messaging/**'
            payment-service:
              - 'services/payment-service/**'
            api-gateway:
              - 'services/api-gateway/**'
              - 'services/*/openapi.yaml'  # API change triggers gateway rebuild

  # ─── BUILD CHANGED SERVICES IN PARALLEL ───────────────────────────
  build-user-service:
    name: User Service
    needs: detect-changes
    if: needs.detect-changes.outputs.user-service == 'true'
    uses: ./.github/workflows/service-pipeline.yml
    with:
      service-name: user-service
      service-path: services/user-service
      image-tag: ${{ github.sha }}
    secrets: inherit

  build-order-service:
    name: Order Service
    needs: detect-changes
    if: needs.detect-changes.outputs.order-service == 'true'
    uses: ./.github/workflows/service-pipeline.yml
    with:
      service-name: order-service
      service-path: services/order-service
      image-tag: ${{ github.sha }}
    secrets: inherit

  build-payment-service:
    name: Payment Service
    needs: detect-changes
    if: needs.detect-changes.outputs.payment-service == 'true'
    uses: ./.github/workflows/service-pipeline.yml
    with:
      service-name: payment-service
      service-path: services/payment-service
      image-tag: ${{ github.sha }}
    secrets: inherit

  # ─── INTEGRATION TESTS (only if any service changed) ──────────────
  integration-tests:
    name: Integration Tests
    runs-on: ubuntu-latest
    needs: [build-user-service, build-order-service, build-payment-service]
    if: |
      always() &&
      (needs.build-user-service.result == 'success' ||
       needs.build-order-service.result == 'success' ||
       needs.build-payment-service.result == 'success')

    steps:
      - uses: actions/checkout@v4
      - name: Run integration test suite
        run: |
          docker compose -f docker-compose.integration.yml up -d
          sleep 30
          npm run test:integration
        env:
          USER_IMAGE_TAG: ${{ github.sha }}
          ORDER_IMAGE_TAG: ${{ github.sha }}
          PAYMENT_IMAGE_TAG: ${{ github.sha }}
```

---

### 18.3 Contract Testing in Microservices Pipelines

```yaml
# Contract testing with Pact — verify service contracts before deployment
contract-tests:
  runs-on: ubuntu-latest
  steps:
    - uses: actions/checkout@v4

    # Consumer-driven contract tests
    - name: Run Pact consumer tests
      run: npm run test:pact:consumer
      # This generates pact files in ./pacts/

    - name: Publish pacts to Pact Broker
      run: |
        npx pact-broker publish ./pacts \
          --broker-base-url=https://pact-broker.mycompany.com \
          --consumer-app-version=${{ github.sha }} \
          --branch=${{ github.ref_name }}
      env:
        PACT_BROKER_TOKEN: ${{ secrets.PACT_BROKER_TOKEN }}

    - name: Verify provider contracts
      run: npm run test:pact:provider

    - name: Can I deploy? (Pact Broker compatibility check)
      run: |
        npx pact-broker can-i-deploy \
          --pacticipant order-service \
          --version ${{ github.sha }} \
          --to-environment production
      env:
        PACT_BROKER_TOKEN: ${{ secrets.PACT_BROKER_TOKEN }}
```

---

---

## Lesson 19 — GitOps Workflows

> **Level:** Advanced
> **Goal:** Implement Git-driven infrastructure and application state management

---

### 19.1 What is GitOps?

GitOps is a practice where:
- Git is the single source of truth for both application code and cluster state
- All changes happen through pull requests — no direct `kubectl` or `helm` commands in production
- An operator (ArgoCD, Flux) continuously reconciles the cluster state with what's in Git
- Drift is automatically corrected — manual changes are reverted

```
Developer changes Helm values in Git
              │
              ▼
          Pull Request
              │
              ▼
       Code Review + CI checks pass
              │
              ▼
        Merged to main
              │
              ▼
       ArgoCD detects change
       (watches Git repo)
              │
              ▼
       ArgoCD applies changes to cluster
              │
              ▼
       If cluster state drifts from Git
       (someone ran kubectl manually)
              │
              ▼
       ArgoCD automatically reverts the drift
```

---

### 19.2 ArgoCD Application Setup

```yaml
# ArgoCD Application definition
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: myapp-production
  namespace: argocd
  finalizers:
    - resources-finalizer.argocd.argoproj.io  # Cascade delete resources
spec:
  project: production

  source:
    repoURL: https://github.com/myorg/k8s-configs.git
    targetRevision: main
    path: environments/production
    helm:
      valueFiles:
        - values.yaml
        - secrets.yaml   # Managed by Sealed Secrets or External Secrets

  destination:
    server: https://kubernetes.default.svc
    namespace: production

  syncPolicy:
    automated:
      prune: true           # Delete resources removed from Git
      selfHeal: true        # Revert manual kubectl changes
      allowEmpty: false     # Never sync an empty state (safety)
    syncOptions:
      - CreateNamespace=true
      - PruneLast=true       # Delete old resources only after new ones are healthy
      - RespectIgnoreDifferences=true
    retry:
      limit: 5
      backoff:
        duration: 5s
        factor: 2
        maxDuration: 3m

  ignoreDifferences:
    # Ignore fields managed by other controllers
    - group: apps
      kind: Deployment
      jsonPointers:
        - /spec/replicas    # HPA manages this — ignore drift from ArgoCD
```

---

### 19.3 CI/CD + GitOps — The Combined Pattern

```yaml
# Phase 1: CI Pipeline — build and push image
# (runs in application repo)
name: CI — Build and Update Config

jobs:
  build:
    steps:
      - name: Build and push image
        run: |
          docker build -t myregistry/myapp:${{ github.sha }} .
          docker push myregistry/myapp:${{ github.sha }}

      # Update image tag in separate GitOps repo
      - name: Checkout GitOps config repo
        uses: actions/checkout@v4
        with:
          repository: myorg/k8s-configs
          token: ${{ secrets.GITOPS_TOKEN }}
          path: k8s-configs

      - name: Update image tag
        run: |
          cd k8s-configs
          # Update the image tag in the values file
          yq e '.image.tag = "${{ github.sha }}"' \
            -i environments/staging/values.yaml
          git config user.email "ci@mycompany.com"
          git config user.name "CI Bot"
          git add .
          git commit -m "chore: update myapp to ${{ github.sha }} [skip ci]"
          git push
```

```
# Phase 2: ArgoCD sees the change in k8s-configs repo
# Automatically deploys updated values to cluster
# No separate "deploy" step needed in CI pipeline
```

---

---

## Lesson 20 — Pipeline Monitoring and Observability

> **Level:** Advanced
> **Goal:** Know what your pipelines are doing and catch problems early

---

### 20.1 Pipeline Metrics to Track

| Metric | What It Tells You | Target |
|---|---|---|
| **Pipeline duration** | Build speed, developer experience | < 10 min for PR pipelines |
| **Success rate** | Pipeline reliability | > 90% |
| **Mean time to recovery** | How fast failures are fixed | < 1 hour |
| **Deployment frequency** | How often you ship | Daily or more |
| **Change failure rate** | How often deployments break prod | < 5% |
| **Lead time** | Commit to production time | Hours, not days |

> These are the **DORA metrics** — industry-standard measures of DevOps performance from the DevOps Research and Assessment team.

---

### 20.2 Pipeline Notifications

```yaml
# Slack notifications for pipeline events
- name: Notify deployment start
  uses: slackapi/slack-github-action@v1.25.0
  with:
    payload: |
      {
        "text": "🚀 Deploying ${{ env.IMAGE_NAME }}:${{ github.sha }} to production",
        "attachments": [{
          "color": "warning",
          "fields": [
            {"title": "Triggered by", "value": "${{ github.actor }}", "short": true},
            {"title": "Branch", "value": "${{ github.ref_name }}", "short": true},
            {"title": "Build", "value": "<${{ github.server_url }}/${{ github.repository }}/actions/runs/${{ github.run_id }}|#${{ github.run_number }}>", "short": true}
          ]
        }]
      }
  env:
    SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK }}

# Post-deployment success/failure
- name: Notify success
  if: success()
  uses: slackapi/slack-github-action@v1.25.0
  with:
    payload: |
      {"text": "✅ ${{ env.IMAGE_NAME }} deployed successfully to production"}
  env:
    SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK }}

- name: Notify failure
  if: failure()
  uses: slackapi/slack-github-action@v1.25.0
  with:
    payload: |
      {"text": "❌ Deployment FAILED: ${{ env.IMAGE_NAME }} — <${{ github.server_url }}/${{ github.repository }}/actions/runs/${{ github.run_id }}|View logs>"}
  env:
    SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK }}
```

---

---

## Lesson 21 — Managing Pipeline Secrets

> **Level:** Advanced
> **Goal:** Centralise and secure all pipeline credentials

---

### 21.1 Secrets Hierarchy in GitHub Actions

```
GitHub Organisation Secrets
    └── Available to all repositories (ideal for shared infrastructure creds)

GitHub Repository Secrets
    └── Available only to that repository

GitHub Environment Secrets
    └── Available only when deploying to that named environment
    └── Best for environment-specific credentials (prod DB, prod registry)
```

**When to use each:**
```yaml
# Organisation secret — shared across all repos
secrets.ARTIFACTORY_TOKEN    # Shared artifact repository access

# Repository secret — this repo only
secrets.DB_CONNECTION_STRING  # App-specific database

# Environment secret — production environment only
secrets.PROD_KUBECONFIG       # Only available when deploying to production
secrets.PROD_DB_PASSWORD      # Only available during production deployment
```

---

### 21.2 External Secret Management (Production Standard)

```yaml
# Store secrets in Azure Key Vault, retrieve at pipeline runtime
- name: Get secrets from Key Vault
  uses: azure/get-keyvault-secrets@v1
  with:
    keyvault: mycompany-kv
    secrets: 'db-password, api-key, jwt-secret'
  id: keyvault-secrets

- name: Use secrets
  run: |
    echo "Deploying with database connection..."
  env:
    DB_PASSWORD: ${{ steps.keyvault-secrets.outputs.db-password }}
    API_KEY: ${{ steps.keyvault-secrets.outputs.api-key }}
```

**Jenkins with HashiCorp Vault:**
```groovy
// Jenkinsfile — fetch secrets from Vault at runtime
withVault(vaultSecrets: [
    [path: 'secret/myapp/production',
     secretValues: [
         [envVar: 'DB_PASSWORD', vaultKey: 'database_password'],
         [envVar: 'API_KEY', vaultKey: 'api_key']
     ]]
]) {
    sh 'deploy.sh'
    // DB_PASSWORD and API_KEY are available but never logged
}
```

---

---

# PHASE 5 — EXPERT LEVEL

---

## Lesson 22 — Debugging Failed Pipelines and Deployments

> **Level:** Expert
> **Goal:** Systematically diagnose and fix any pipeline failure

---

### 22.1 The Debugging Framework

```
STEP 1: Find the failure point
  → Which stage failed? What was the last successful stage?
  → What is the exact error message?

STEP 2: Reproduce locally if possible
  → Can you run the failing command locally?
  → Is it environment-specific (only fails in CI)?

STEP 3: Check environmental factors
  → Did any dependency change? (package updates, base image change)
  → Did any infrastructure change? (new cluster, rotated credentials)
  → Is it a flaky test or consistent failure?

STEP 4: Fix and verify
  → Make minimal change to fix
  → Does the fix work in isolation?
  → Does it pass all pipeline stages?

STEP 5: Prevent recurrence
  → Add monitoring/alerting for this class of failure
  → Update documentation
  → Consider if a test should be added
```

---

### 22.2 Common Pipeline Failures and Solutions

**Failure: npm/Maven/Gradle dependency download failure**
```bash
# Symptoms: "unable to download package", "connection refused"
# Causes: registry outage, network issue, authentication failure

# Debug steps:
# 1. Check if registry is up (Nexus/Artifactory status page)
# 2. Check credentials are still valid
# 3. Check network policies haven't changed

# Fix for transient failures: add retry logic
npm install --prefer-offline || npm install   # Use cache first, retry without
```

**Failure: Docker build OOM (Out of Memory)**
```yaml
# Symptoms: "Killed" during build, exit code 137
# Cause: Build process needs more RAM than the runner has

# Fix: Use larger runner
jobs:
  build:
    runs-on: ubuntu-latest-8-cores   # Larger runner
    # OR for GitHub-hosted runners:
    runs-on: [self-hosted, large]    # Custom runner with more RAM
```

**Failure: kubectl connection refused in pipeline**
```bash
# Symptoms: "Unable to connect to the server"
# Debug:
kubectl cluster-info --context=prod
# Check kubeconfig is valid and not expired
kubectl auth can-i get pods -n production

# Common causes:
# 1. Kubeconfig credentials expired (rotate service account token)
# 2. Cluster endpoint changed (update kubeconfig)
# 3. Network policy blocks pipeline runner IPs
```

**Failure: Helm deployment fails with "another operation in progress"**
```bash
# Cause: Previous helm operation never completed — release is in PENDING state
# Check:
helm list -a -n production | grep PENDING

# Fix: Roll back the stuck release
helm rollback myapp -n production

# Or if no previous revision:
helm history myapp -n production
helm uninstall myapp -n production --no-hooks
# Re-run the deployment
```

**Failure: Tests pass locally but fail in CI**
```bash
# Most common causes:
# 1. Timing: tests have race conditions, CI is slower
# 2. Environment: different env vars, missing secrets
# 3. Dependencies: different versions (npm install vs npm ci)
# 4. State: tests assume clean state but CI has residual state

# Debug: add verbose logging to pipeline
- name: Debug environment
  run: |
    node --version
    npm --version
    env | sort | grep -v SECRET   # Print env vars (excluding secrets)
    cat package-lock.json | jq '.lockfileVersion'
```

---

### 22.3 Rollback Strategies

```bash
# ─── Kubernetes Rollback ──────────────────────────────────────────
# Immediate rollback via Kubernetes
kubectl rollout undo deployment/myapp -n production
kubectl rollout status deployment/myapp -n production

# ─── Helm Rollback ────────────────────────────────────────────────
# List revision history
helm history myapp -n production

# Rollback to specific revision
helm rollback myapp 3 -n production --wait

# ─── GitOps Rollback ──────────────────────────────────────────────
# Revert the commit in the GitOps repo
git revert HEAD
git push origin main
# ArgoCD automatically deploys the reverted state

# ─── Blue-Green Rollback ──────────────────────────────────────────
# Switch traffic back to previous color
kubectl patch service myapp -n production \
  -p '{"spec":{"selector":{"color":"blue"}}}'
# Instant — no rebuilding, no redeploying
```

---

---

## Lesson 23 — Disaster Recovery in CI/CD

> **Level:** Expert
> **Goal:** Recover CI/CD infrastructure and pipeline history from catastrophic failures

---

### 23.1 What to Protect

| Component | Risk | Recovery Method |
|---|---|---|
| **Pipeline definitions** | Low — stored in Git | Git restore |
| **Jenkins configuration** | High — stored on disk | Backup + restore scripts |
| **Secrets/credentials** | Critical | Vault backup, break-glass procedures |
| **Artifact repository** | High — build artifacts | Replication, backups |
| **Container registry** | Medium — can rebuild images | Geo-replication |
| **Build history/logs** | Low — can be lost | Archive to S3/Blob |

---

### 23.2 Jenkins Disaster Recovery

```bash
# Backup Jenkins home directory
# /var/jenkins_home contains: all jobs, configs, plugins, credentials, build history

# Automated backup script
#!/bin/bash
TIMESTAMP=$(date +%Y%m%d_%H%M%S)
BACKUP_DEST="s3://mycompany-backups/jenkins/${TIMESTAMP}"

# Backup Jenkins home
tar -czf /tmp/jenkins-backup-${TIMESTAMP}.tar.gz \
  -C /var/jenkins_home \
  --exclude="workspace" \    # Skip build workspaces (can be rebuilt)
  --exclude="builds" \       # Skip old build logs (optional — keep if needed)
  .

aws s3 cp /tmp/jenkins-backup-${TIMESTAMP}.tar.gz ${BACKUP_DEST}/
echo "Backup complete: ${BACKUP_DEST}"

# Restore Jenkins
tar -xzf jenkins-backup-20240115_020000.tar.gz -C /var/jenkins_home/
# Restart Jenkins
```

**Jenkins Configuration as Code (JCasC) — prevent the need for manual backup:**
```yaml
# jenkins.yaml — declarative Jenkins configuration
jenkins:
  systemMessage: "Jenkins managed by JCasC"
  numExecutors: 0   # Controller should not run builds

  agentProtocols:
    - "JNLP4-connect"

  securityRealm:
    ldap:
      configurations:
        - server: ldap://ldap.mycompany.com
          rootDN: "dc=mycompany,dc=com"

  authorizationStrategy:
    roleBased:
      roles:
        global:
          - name: "admin"
            permissions:
              - "Overall/Administer"
            assignments:
              - "devops-team"

credentials:
  system:
    domainCredentials:
      - credentials:
          - usernamePassword:
              id: "nexus-credentials"
              username: "deployer"
              password: "${NEXUS_PASSWORD}"  # From env var
              description: "Nexus deployment user"

jobs:
  - script: |
      pipelineJob('myapp-pipeline') {
        definition {
          cpsScm {
            scm {
              git {
                remote { url('https://github.com/myorg/myapp.git') }
                branch('main')
              }
            }
            scriptPath('Jenkinsfile')
          }
        }
      }
```

---

---

## Lesson 24 — Enterprise CI/CD Architecture

> **Level:** Expert
> **Goal:** Design CI/CD for large organisations with many teams and services

---

### 24.1 Enterprise Pipeline Architecture

```
PLATFORM TEAM manages:
  ┌──────────────────────────────────────────────────────────┐
  │  Shared Infrastructure                                    │
  │                                                           │
  │  Jenkins/GitHub Org  →  Shared Runners/Agents            │
  │  Artifact Repository (Nexus/Artifactory)                 │
  │  Container Registry (ACR/ECR)                            │
  │  Shared pipeline libraries                               │
  │  Pipeline templates/standards                            │
  └──────────────────────────────────────────────────────────┘
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
    TEAM A pipeline    TEAM B pipeline    TEAM C pipeline
    (extends shared    (extends shared    (extends shared
     template)          template)          template)
```

---

### 24.2 Pipeline Templates — Standardise Without Restricting

```yaml
# .github/workflows/standard-microservice.yml
# Platform team publishes this template — teams consume it

name: Standard Microservice Pipeline

on:
  workflow_call:
    inputs:
      service-name:
        required: true
        type: string
      dockerfile-path:
        required: false
        type: string
        default: './Dockerfile'
      run-e2e:
        required: false
        type: boolean
        default: false
      target-environments:
        required: false
        type: string
        default: 'dev,staging'

jobs:
  standard-build:
    uses: myorg/platform-pipelines/.github/workflows/build.yml@main
    with:
      service-name: ${{ inputs.service-name }}
    secrets: inherit

  standard-test:
    uses: myorg/platform-pipelines/.github/workflows/test.yml@main
    needs: standard-build
    with:
      service-name: ${{ inputs.service-name }}
      run-e2e: ${{ inputs.run-e2e }}
    secrets: inherit

  standard-deploy:
    uses: myorg/platform-pipelines/.github/workflows/deploy.yml@main
    needs: standard-test
    with:
      service-name: ${{ inputs.service-name }}
      environments: ${{ inputs.target-environments }}
    secrets: inherit
```

**Team consuming the template:**
```yaml
# myapp/.github/workflows/ci-cd.yml (owned by application team)
name: MyApp Pipeline

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  pipeline:
    uses: myorg/platform-pipelines/.github/workflows/standard-microservice.yml@main
    with:
      service-name: myapp
      run-e2e: true
      target-environments: 'dev,staging,production'
    secrets: inherit
```

---

### 24.3 Self-Service Developer Platform

```yaml
# Developers provision environments and deploy via PRs
# No direct kubectl/helm access to production

# Developer opens PR to k8s-configs repo:
# environments/myapp/staging/values.yaml
replicaCount: 2
image:
  tag: abc123def   # Developer updates this

# Platform team's pipeline validates + applies
```

---

---

## Lesson 25 — Secure Pipeline Design

> **Level:** Expert
> **Goal:** Build pipelines that cannot be weaponised against your infrastructure

---

### 25.1 Supply Chain Security — SLSA Framework

SLSA (Supply-chain Levels for Software Artifacts) is a framework for supply chain security. The goal: cryptographic proof of how an artifact was built.

```yaml
# SLSA Level 3 — signed, verifiable provenance
- name: Generate SLSA provenance
  uses: slsa-framework/slsa-github-generator/.github/workflows/generator_generic_slsa3.yml@v1.9.0
  with:
    base64-subjects: "${{ needs.build.outputs.hashes }}"
    upload-assets: true

# This creates a signed attestation that says:
# "This artifact was built from this Git commit,
#  by this workflow, at this time,
#  on this GitHub-hosted runner"
# Anyone can verify this cryptographically
```

---

### 25.2 Signed Docker Images

```yaml
# Sign Docker images with Cosign (SLSA-compliant)
- name: Install Cosign
  uses: sigstore/cosign-installer@v3.3.0

- name: Sign the image
  run: |
    cosign sign \
      --key ${{ secrets.COSIGN_KEY }} \
      ${{ env.REGISTRY }}/myapp:${{ github.sha }}

# Verify before deploying (in deployment pipeline)
- name: Verify image signature
  run: |
    cosign verify \
      --key ${{ secrets.COSIGN_PUBLIC_KEY }} \
      ${{ env.REGISTRY }}/myapp:${{ env.IMAGE_TAG }}
    echo "Image signature verified — safe to deploy"
```

---

### 25.3 Pipeline Hardening Checklist

```
□ All workflow triggers are specific (not 'on: push' to all branches)
□ Permissions set to minimum (contents: read by default)
□ Actions pinned to commit SHAs, not mutable tags
□ Secrets stored in GitHub Secrets, Key Vault, or Vault (not in code)
□ No secrets printed in logs (all masked or not logged)
□ OIDC used for cloud authentication (no static credentials)
□ Dependabot enabled for action version updates
□ Code review required before pipeline code changes merge
□ Branch protection rules prevent direct push to main
□ Image scanning before push and before deploy
□ Docker images signed and verified before deployment
□ SAST/dependency scanning on every commit
□ Pipeline logs retained and monitored
□ Separate service principals per environment (prod != staging)
□ Manual approval gate for production deployments
□ Rollback tested and documented (not just theorised)
```

---

---

## Lesson 26 — DevOps Interview Preparation — CI/CD Edition

> **Level:** Senior Engineer

---

### 26.1 Core Interview Questions — With Strong Answers

**Q: "Explain your ideal CI/CD pipeline for a new microservice."**

> I start with a simple but complete pipeline: on every push to a feature branch, run linting and unit tests within 3-5 minutes — fast feedback that the developer sees before switching tasks. When a PR is raised, integration tests also run, including security scanning. The PR cannot merge without these passing. On merge to main, I build a Docker image tagged with the commit SHA — immutable and traceable — scan it for vulnerabilities, and push to the private registry. I then deploy automatically to dev, run smoke tests, then automatically to staging for a full regression suite. Production requires a manual approval gate, but the actual deployment is automated: Helm upgrade with `--atomic` so it auto-rollbacks on failure. Post-deployment, I verify health endpoints and key metrics. The whole thing from commit to production is under 20 minutes, with humans only involved in code review and production approval.

---

**Q: "What's the difference between blue-green and canary deployments?"**

> Both are zero-downtime deployment strategies but solve different risk profiles. Blue-green maintains two complete environments. You deploy the new version to the inactive environment, test it, then switch all traffic instantly. The old version stays warm for immediate rollback. It's great for breaking changes because there's no period where both versions serve traffic. The downside is cost — you maintain double the infrastructure. Canary deployment sends a small percentage of real traffic to the new version — say 5% — while 95% still goes to the old version. You observe metrics, error rates, latency. If everything looks good, you gradually increase the canary percentage. This is better for testing with real user behaviour and finding issues that staging environments don't catch. The risk is that 5% of users experience the new (potentially broken) version. I choose blue-green for changes that are hard to test in staging and where instant rollback is paramount. I choose canary for data-driven risk reduction where I want to observe real production behaviour progressively.

---

**Q: "A deployment is failing in production. Walk me through how you respond."**

> First, I assess whether to roll back immediately or investigate. If users are impacted, rollback is always the first action — customer impact outweighs root cause analysis. In Kubernetes, that's `kubectl rollout undo` or `helm rollback`. The old image is still in the registry and the old Helm revision is in history, so rollback is instant. Once production is stable, I look at the pipeline logs: what stage failed, what was the last successful build, what changed between the last good deploy and this one. I check application logs and metrics for the new version. I look at git blame to understand what code changed. I reproduce the issue in staging before attempting a second production deployment. I also add a monitoring alert so I'm notified next time this class of issue happens, and I consider whether a test should be added to the pipeline to prevent regression.

---

**Q: "How do you handle secrets in a CI/CD pipeline?"**

> The most important principle is that secrets should never appear in pipeline code, configuration files, or logs. For GitHub Actions, I use GitHub Secrets or GitHub Environments for environment-specific secrets. For cloud authentication, I prefer OIDC-based federated identity — no stored credentials at all, Azure or AWS generates a short-lived token for each pipeline run. For application secrets needed at deploy time, I use Azure Key Vault or HashiCorp Vault and retrieve them at runtime in the pipeline, passing them as masked environment variables. I never print secrets in echo statements. I regularly audit who has access to repository and environment secrets. I rotate credentials on a schedule. I use different service principals for different environments so a compromised staging credential cannot access production.

---

**Q: "What is GitOps and why would you use it?"**

> GitOps is a practice where Git is the single source of truth for both application code and infrastructure/cluster state. Every change to a deployed environment goes through a Git pull request — not direct kubectl commands. A tool like ArgoCD or Flux watches the Git repository and continuously reconciles the cluster state with what's in Git. If someone manually runs kubectl to change something, ArgoCD automatically reverts it to what Git says. The benefits are significant: every change is peer-reviewed and has a complete audit trail. Rollback is simply reverting a Git commit. Drift detection is automatic and continuous. Developer access to production kubectl is not required — the GitOps operator handles all deployments. For regulated industries or teams with strict compliance requirements, this is invaluable because you have a complete, immutable history of every change ever made to production.

---

### 26.2 Scenario-Based Interview Questions

**Q: "Your CI pipeline takes 45 minutes. Developers are complaining they don't get fast feedback. How do you fix it?"**

Strong answer covers:
- Profile first — which stage takes the most time
- Parallelise independent stages (unit tests, linting, security scan run in parallel)
- Add dependency caching (npm ci with cached node_modules is 10x faster)
- Split test suite into fast (unit) and slow (e2e) — run fast tests first
- Run slow tests only on merge to main, not on every PR push
- Use Docker layer caching
- Consider larger/faster runners for compute-heavy steps
- Target: PR pipeline < 5 minutes, full pipeline < 15 minutes

---

### 26.3 CI/CD Tools Comparison Cheat Sheet

```
GITHUB ACTIONS:
  ✅ Native GitHub integration, no setup for GitHub repos
  ✅ OIDC to Azure/AWS without static credentials
  ✅ Massive marketplace (25,000+ actions)
  ✅ Generous free tier (2,000 mins/month)
  ❌ Only for GitHub repos
  ❌ Self-hosted runners add operational burden

GITLAB CI/CD:
  ✅ All-in-one platform: git + CI + registry + package registry + CD
  ✅ Best built-in security scanning (SAST, DAST, container scanning)
  ✅ Dynamic environments (review apps per PR)
  ✅ Built-in artifact management
  ❌ Requires GitLab for code hosting
  ❌ Complex yaml for advanced pipelines

JENKINS:
  ✅ Maximum flexibility and customisation
  ✅ 1,800+ plugins for any integration
  ✅ Runs anywhere — no vendor dependency
  ✅ Dominant in enterprise
  ❌ Requires significant maintenance and expertise
  ❌ UI is dated, shared library learning curve is steep
  ❌ Security patching is your responsibility

BITBUCKET PIPELINES:
  ✅ Native Atlassian integration (Jira, Confluence)
  ✅ Simple YAML, quick to get started
  ✅ Good for small/medium teams on Atlassian stack
  ❌ Only for Bitbucket repos
  ❌ Less powerful than GitHub Actions or GitLab
```

---

### 26.4 CI/CD Pipeline Quick Reference

```yaml
# GitHub Actions — structure reminder
name: Pipeline Name
on: [push, pull_request]
env:
  GLOBAL_VAR: value
jobs:
  job-name:
    runs-on: ubuntu-latest
    needs: [other-job]           # Dependency
    if: github.ref == 'refs/heads/main'  # Condition
    environment: production       # Deployment environment
    strategy:
      matrix:
        node: [16, 18, 20]       # Matrix builds
    steps:
      - uses: actions/checkout@v4
      - run: echo "Hello"
      - name: Step name
        run: |
          multi
          line
          command
        env:
          SECRET: ${{ secrets.MY_SECRET }}
        if: success()
```

```groovy
// Jenkins Declarative — structure reminder
pipeline {
    agent { docker { image 'node:18' } }
    environment { VAR = 'value' }
    options { timeout(time: 30, unit: 'MINUTES') }
    parameters { string(name: 'ENV', defaultValue: 'dev') }
    stages {
        stage('Name') {
            when { branch 'main' }
            parallel {
                stage('A') { steps { sh 'cmd' } }
                stage('B') { steps { sh 'cmd' } }
            }
        }
    }
    post {
        success { echo 'Done' }
        failure { slackSend message: 'Failed' }
        always { cleanWs() }
    }
}
```

```yaml
# GitLab CI — structure reminder
stages: [build, test, deploy]
variables:
  VAR: value
.template: &template   # Anchor for reuse
  script: echo "base"

job-name:
  stage: build
  image: node:18
  <<: *template        # Extend template
  script:
    - npm ci
    - npm run build
  cache:
    key: ${CI_COMMIT_REF_SLUG}
    paths: [node_modules/]
  artifacts:
    paths: [dist/]
    expire_in: 1 week
  rules:
    - if: $CI_COMMIT_BRANCH == "main"
  environment:
    name: production
    url: https://myapp.com
```

---

## Official Documentation Reference

| Tool | Documentation URL |
|---|---|
| GitHub Actions | https://docs.github.com/en/actions |
| GitLab CI/CD | https://docs.gitlab.com/ee/ci/ |
| Jenkins | https://www.jenkins.io/doc/ |
| Bitbucket Pipelines | https://support.atlassian.com/bitbucket-cloud/docs/build-test-and-deploy-with-pipelines/ |
| Docker in CI/CD | https://docs.docker.com/build/ci/ |
| Kubernetes Deployments | https://kubernetes.io/docs/concepts/workloads/controllers/deployment/ |
| Helm | https://helm.sh/docs/ |
| Terraform in CI/CD | https://developer.hashicorp.com/terraform/tutorials/automation |
| ArgoCD | https://argo-cd.readthedocs.io/ |
| Trivy (Security) | https://aquasecurity.github.io/trivy/ |
| SLSA Framework | https://slsa.dev/ |
| DORA Metrics | https://dora.dev/ |
| Cosign (Image Signing) | https://docs.sigstore.dev/cosign/overview/ |
| Nexus Repository | https://help.sonatype.com/repomanager3 |
| JFrog Artifactory | https://jfrog.com/help/r/jfrog-artifactory-documentation |

---

## Learning Path

```
Week 1–2:   Lessons 1–5   CI/CD fundamentals, branching, build tools, testing, artifacts
Week 3–4:   Lessons 6–7   Jenkins setup, Declarative Jenkinsfile, shared libraries
Week 5–6:   Lesson 8      GitHub Actions — build complete production workflow
Week 7–8:   Lesson 9      GitLab CI/CD — build complete pipeline
Week 9–10:  Lessons 11–12 Docker in CI/CD, Kubernetes deployments with Helm
Week 11–12: Lessons 13–14 Terraform pipeline, Blue-Green and Canary deployments
Week 13–14: Lessons 15–16 Security hardening, pipeline optimisation
Week 15–16: Lessons 17–19 Multi-environment, Microservices, GitOps with ArgoCD
Week 17–18: Lessons 20–21 Monitoring, secrets management
Week 19–20: Lessons 22–23 Debugging, disaster recovery
Week 21–22: Lessons 24–25 Enterprise architecture, secure pipeline design
Week 23–24: Lesson 26     Interview prep + build portfolio project
```

**Build Something Real:**
Create a complete CI/CD portfolio project:
- Node.js or Java microservice with unit + integration tests
- Dockerfile with multi-stage build
- GitHub Actions pipeline: lint → test → security scan → docker build → deploy
- Helm chart for Kubernetes deployment
- Multi-environment values (dev/staging/prod)
- Blue-green or canary deployment strategy
- ArgoCD GitOps setup
- Monitoring with Prometheus alerts on pipeline failures

Put it on GitHub. This is your portfolio proof-of-work.

---

*Built on: Jenkins Documentation · GitHub Actions Documentation · GitLab CI/CD Documentation · Docker Documentation · DORA Research · SLSA Framework*
