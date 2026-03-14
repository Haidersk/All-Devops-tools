# Kubernetes Mastery — Complete Engineering Curriculum
## Zero to Senior DevOps / Platform Engineer

> **Covers:** Container Orchestration · Cluster Architecture · Workloads · Networking · Storage · Security · Helm · RBAC · Autoscaling · Production Operations · Expert Internals
> **Track:** DevOps Career Path | Beginner → Senior Engineer
> **Certifications:** CKA (Certified Kubernetes Administrator) · CKAD (Certified Kubernetes Application Developer) · CKS (Certified Kubernetes Security Specialist)
> **Based on:** Official Kubernetes Documentation — https://kubernetes.io/docs/

---

## How to Use This Document

- Work through every lesson in order — each concept builds on the last
- Run every kubectl command yourself — reading alone will not make you job-ready
- Complete every hands-on lab — this is where real learning happens
- Attempt every practice question before reading the answer
- Labs use a local cluster (kind or minikube) — cloud cluster (AKS/EKS/GKE) for advanced lessons

---

## Table of Contents

### PHASE 1 — Foundations (Beginner)
- [Lesson 1 — Container Orchestration and Kubernetes Architecture](#lesson-1--container-orchestration-and-kubernetes-architecture)
- [Lesson 2 — Pods — The Atomic Unit](#lesson-2--pods--the-atomic-unit)
- [Lesson 3 — ReplicaSets and Deployments](#lesson-3--replicasets-and-deployments)
- [Lesson 4 — Labels, Selectors, and Namespaces](#lesson-4--labels-selectors-and-namespaces)
- [Lesson 5 — Basic Troubleshooting](#lesson-5--basic-troubleshooting)

### PHASE 2 — Intermediate
- [Lesson 6 — Kubernetes Services](#lesson-6--kubernetes-services)
- [Lesson 7 — Ingress](#lesson-7--ingress)
- [Lesson 8 — ConfigMaps and Secrets](#lesson-8--configmaps-and-secrets)
- [Lesson 9 — Resource Limits, Probes, and Rolling Updates](#lesson-9--resource-limits-probes-and-rolling-updates)

### PHASE 3 — DevOps Level
- [Lesson 10 — Horizontal Pod Autoscaler](#lesson-10--horizontal-pod-autoscaler)
- [Lesson 11 — Kubernetes Networking Deep Dive](#lesson-11--kubernetes-networking-deep-dive)
- [Lesson 12 — Persistent Volumes and Storage](#lesson-12--persistent-volumes-and-storage)
- [Lesson 13 — Helm Package Manager](#lesson-13--helm-package-manager)
- [Lesson 14 — Kubernetes RBAC](#lesson-14--kubernetes-rbac)
- [Lesson 15 — Logging and Monitoring](#lesson-15--logging-and-monitoring)

### PHASE 4 — Advanced Architecture
- [Lesson 16 — High Availability Clusters](#lesson-16--high-availability-clusters)
- [Lesson 17 — Kubernetes Security Best Practices](#lesson-17--kubernetes-security-best-practices)
- [Lesson 18 — Service Mesh with Istio](#lesson-18--service-mesh-with-istio)
- [Lesson 19 — Multi-Environment Deployments](#lesson-19--multi-environment-deployments)
- [Lesson 20 — Cluster Upgrades and Maintenance](#lesson-20--cluster-upgrades-and-maintenance)

### PHASE 5 — Expert Level
- [Lesson 21 — Kubernetes Internals](#lesson-21--kubernetes-internals)
- [Lesson 22 — etcd Architecture and Operations](#lesson-22--etcd-architecture-and-operations)
- [Lesson 23 — Scheduler Internals and Custom Scheduling](#lesson-23--scheduler-internals-and-custom-scheduling)
- [Lesson 24 — Debugging Cluster Failures](#lesson-24--debugging-cluster-failures)
- [Lesson 25 — Production Performance Optimisation](#lesson-25--production-performance-optimisation)
- [Lesson 26 — Advanced Cluster Security](#lesson-26--advanced-cluster-security)
- [Lesson 27 — DevOps Interview Preparation — Kubernetes Edition](#lesson-27--devops-interview-preparation--kubernetes-edition)

---

---

# PHASE 1 — FOUNDATIONS
## Kubernetes Beginner Level

---

## Lesson 1 — Container Orchestration and Kubernetes Architecture

> **Level:** Absolute Beginner
> **Goal:** Understand why Kubernetes exists and how it is structured

---

### 1.1 The Problem Kubernetes Solves

You have learned Docker. You can run containers. Now imagine you are running a real production application:

- **10 microservices**, each running as a Docker container
- Each service needs **3 replicas** for high availability = 30 containers
- Containers crash and must **restart automatically**
- Traffic spikes on Friday — you need to **scale from 3 to 20 replicas** instantly
- Deploy a new version of the API with **zero downtime**
- If the database container crashes, API containers must **wait for it to recover** before routing traffic
- All 30 containers need to **find and talk to each other**
- Services need **rolling updates** where old version handles traffic while new version starts

Managing this manually with `docker run` commands is impossible at scale. Someone would have to watch every container, manually restart crashes, manually update configs. This is a full-time job for a large team.

> **Kubernetes solves the entire list above — automatically, continuously, declaratively.**

You describe the desired state ("I want 3 replicas of this API, always running, with this health check"). Kubernetes works continuously to make reality match your description. If a container crashes, Kubernetes restarts it. If a node dies, Kubernetes reschedules the containers on other nodes.

---

### 1.2 What is Kubernetes?

Kubernetes (K8s — "K", 8 letters, "s") is an open-source container orchestration platform originally designed by Google (based on their internal Borg system), donated to the Cloud Native Computing Foundation (CNCF) in 2014.

**Kubernetes in one sentence:**
> Kubernetes is a system for automating the deployment, scaling, and management of containerised applications across a cluster of machines.

**Key capabilities:**
- **Self-healing:** Restarts failed containers, reschedules containers from failed nodes
- **Horizontal scaling:** Scale workloads up/down manually or automatically based on CPU/memory/custom metrics
- **Automated rollouts:** Deploy new versions progressively, roll back on failure
- **Service discovery:** Built-in DNS — services find each other by name
- **Load balancing:** Distribute traffic across healthy pod replicas automatically
- **Secret and config management:** Store and manage sensitive information
- **Storage orchestration:** Mount cloud storage, NFS, or local storage automatically

---

### 1.3 Kubernetes Architecture — The Complete Picture

A Kubernetes cluster consists of two types of machines:

```
┌─────────────────────────────────────────────────────────────────┐
│                    KUBERNETES CLUSTER                            │
│                                                                  │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │                  CONTROL PLANE                           │    │
│  │                                                          │    │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │    │
│  │  │  API Server  │  │  Scheduler   │  │  Controller  │  │    │
│  │  │  (kube-      │  │  (kube-      │  │  Manager     │  │    │
│  │  │   apiserver) │  │   scheduler) │  │  (kube-cm)   │  │    │
│  │  └──────────────┘  └──────────────┘  └──────────────┘  │    │
│  │  ┌──────────────┐  ┌──────────────┐                     │    │
│  │  │     etcd     │  │ Cloud Control│                     │    │
│  │  │  (cluster    │  │  Manager     │                     │    │
│  │  │   database)  │  │  (cloud-cm)  │                     │    │
│  │  └──────────────┘  └──────────────┘                     │    │
│  └─────────────────────────────────────────────────────────┘    │
│                              │                                   │
│         ┌────────────────────┼────────────────────┐             │
│         ▼                    ▼                    ▼             │
│  ┌─────────────┐   ┌─────────────┐   ┌─────────────┐          │
│  │  WORKER     │   │  WORKER     │   │  WORKER     │          │
│  │  NODE 1     │   │  NODE 2     │   │  NODE 3     │          │
│  │             │   │             │   │             │          │
│  │  kubelet    │   │  kubelet    │   │  kubelet    │          │
│  │  kube-proxy │   │  kube-proxy │   │  kube-proxy │          │
│  │  container  │   │  container  │   │  container  │          │
│  │  runtime    │   │  runtime    │   │  runtime    │          │
│  │             │   │             │   │             │          │
│  │  [Pod][Pod] │   │  [Pod][Pod] │   │  [Pod][Pod] │          │
│  └─────────────┘   └─────────────┘   └─────────────┘          │
└─────────────────────────────────────────────────────────────────┘
```

---

### 1.4 Control Plane Components — Deep Dive

**kube-apiserver — The Front Door:**
- Every interaction with Kubernetes goes through the API Server
- REST API — `kubectl` is just an HTTP client that talks to this API
- Authentication, authorisation, and admission control happen here
- The only component that reads/writes to etcd
- Horizontally scalable — run multiple instances for HA

**etcd — The Cluster Brain:**
- A distributed key-value store — Kubernetes' database
- Stores ALL cluster state: nodes, pods, deployments, secrets, configmaps, everything
- Strong consistency using the Raft consensus algorithm
- If etcd data is lost, the entire cluster state is lost
- Must be backed up regularly in production

**kube-scheduler — The Placement Engine:**
- Watches for newly created Pods with no assigned node
- Selects the best node for each Pod based on: resource availability, affinity rules, taints/tolerations, policies
- Does NOT run the Pod — it just decides where it should run

**kube-controller-manager — The Reconciliation Engine:**
- Runs multiple controllers, each watching a specific resource type
- **Node Controller:** Detects and responds when nodes go down
- **ReplicaSet Controller:** Ensures correct number of Pod replicas exist
- **Deployment Controller:** Manages rolling updates
- **Endpoints Controller:** Populates Service endpoints with Pod IPs
- **Job Controller:** Manages batch Jobs
- All controllers follow the same loop: observe → compare desired vs actual → act to reconcile

**cloud-controller-manager:**
- Integrates Kubernetes with cloud provider APIs (AWS, Azure, GCP)
- Manages cloud load balancers, storage volumes, node lifecycle
- Allows cloud providers to add platform-specific logic without modifying core Kubernetes

---

### 1.5 Worker Node Components

**kubelet — The Node Agent:**
- Runs on every worker node
- Receives PodSpecs from the API Server
- Ensures containers described in PodSpecs are running and healthy
- Reports node and Pod status back to the API Server
- Does NOT manage containers not created by Kubernetes

**kube-proxy — The Network Rules Manager:**
- Runs on every node (as a DaemonSet)
- Maintains network rules that implement Kubernetes Services
- Uses Linux iptables or IPVS to route traffic to the correct Pod
- When you hit a Service IP, kube-proxy routes it to a healthy backend Pod

**Container Runtime:**
- The software that actually runs containers
- Kubernetes uses the Container Runtime Interface (CRI)
- **containerd** — most common (Docker uses this internally)
- **CRI-O** — lightweight, designed for Kubernetes
- Kubernetes 1.24+ removed direct Docker support (but containerd still works)

---

### 1.6 The Kubernetes Request Flow

When you run `kubectl apply -f deployment.yaml`:

```
1. kubectl → HTTPS → kube-apiserver
2. kube-apiserver authenticates your request (certificate / token)
3. kube-apiserver authorises your request (RBAC)
4. Admission controllers validate/mutate the request
5. kube-apiserver writes the Deployment to etcd
6. Deployment Controller (in kube-controller-manager) sees new Deployment
7. Deployment Controller creates a ReplicaSet
8. ReplicaSet Controller sees the ReplicaSet — creates Pod objects
9. kube-scheduler sees unscheduled Pods — assigns them to nodes
10. kubelet on selected nodes sees their assigned Pods
11. kubelet tells container runtime (containerd) to pull image and start containers
12. kubelet reports Pod status back to API Server → stored in etcd
13. kubectl get pods shows Running
```

---

### 1.7 Installing Kubernetes Locally

**Option 1: kind (Kubernetes in Docker) — Recommended for learning**
```bash
# Install kind
# macOS
brew install kind

# Linux
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x kind && sudo mv kind /usr/local/bin/

# Create a single-node cluster
kind create cluster --name learning

# Create a multi-node cluster
cat > kind-config.yaml << 'EOF'
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
EOF
kind create cluster --name multi-node --config kind-config.yaml

# List clusters
kind get clusters

# Delete cluster
kind delete cluster --name learning
```

**Option 2: minikube — Alternative**
```bash
# Install minikube
# macOS
brew install minikube

# Linux
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Start cluster
minikube start

# With specific Kubernetes version
minikube start --kubernetes-version=v1.29.0

# Dashboard (visual UI)
minikube dashboard
```

**Install kubectl:**
```bash
# macOS
brew install kubectl

# Linux
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install kubectl /usr/local/bin/kubectl

# Windows
winget install Kubernetes.kubectl

# Verify
kubectl version --client
```

**kubectl Autocompletion (essential for speed):**
```bash
# bash
echo 'source <(kubectl completion bash)' >> ~/.bashrc
echo 'alias k=kubectl' >> ~/.bashrc
echo 'complete -o default -F __start_kubectl k' >> ~/.bashrc
source ~/.bashrc

# zsh
echo 'source <(kubectl completion zsh)' >> ~/.zshrc
echo 'alias k=kubectl' >> ~/.zshrc
source ~/.zshrc
```

---

### 1.8 kubeconfig — Managing Cluster Access

```bash
# kubeconfig file: ~/.kube/config
# Contains: clusters, users, contexts (cluster+user combinations)

# View current config
kubectl config view

# List contexts (cluster connections)
kubectl config get-contexts

# Switch context (switch cluster)
kubectl config use-context kind-multi-node
kubectl config use-context minikube

# Set default namespace for current context
kubectl config set-context --current --namespace=production

# View current context
kubectl config current-context

# Short form (with alias k=kubectl)
k config get-contexts
```

---

### 1.9 Hands-On Lab 1 — Explore Your Cluster

```bash
# Step 1: Create a cluster
kind create cluster --name lab1

# Step 2: Verify kubectl connects
kubectl cluster-info
kubectl version

# Step 3: Explore the nodes
kubectl get nodes
kubectl get nodes -o wide    # Show more details: IPs, OS, container runtime
kubectl describe node <node-name>   # Full node details

# Step 4: Explore control plane components
kubectl get pods -n kube-system
# You'll see: etcd, kube-apiserver, kube-controller-manager, kube-scheduler
# Also: coredns, kube-proxy

kubectl describe pod kube-apiserver-lab1-control-plane -n kube-system
kubectl logs kube-apiserver-lab1-control-plane -n kube-system --tail=20

# Step 5: Explore cluster info
kubectl get all --all-namespaces
kubectl api-resources    # Every resource type Kubernetes knows about
kubectl api-versions     # API versions available

# Step 6: Check component status
kubectl get componentstatuses    # (deprecated but still shows info)
kubectl get events --all-namespaces | head -30

# Cleanup
kind delete cluster --name lab1
```

---

### 1.10 Practice Questions — Lesson 1

**Q1.** A pod crashes repeatedly on one node. Which control plane component is responsible for detecting this and scheduling the pod on a different healthy node?

- A) kube-apiserver
- B) kube-scheduler
- C) Node Controller in kube-controller-manager
- D) kubelet

<details>
<summary>Answer and Explanation</summary>

**Answer: C — Node Controller in kube-controller-manager.**

The Node Controller monitors node health. When a node becomes unresponsive (no heartbeat for the NodeMonitorGracePeriod, default 40s), it marks the node as NotReady. After PodEvictionTimeout (default 5 minutes), it evicts the pods. The kube-scheduler then places evicted pods on healthy nodes. The kubelet reports the status but doesn't make scheduling decisions. The kube-scheduler assigns nodes but only for unscheduled pods.

</details>

---

**Q2.** What is stored in etcd? What happens to the cluster if etcd data is permanently lost?

<details>
<summary>Answer</summary>

etcd stores the complete cluster state: all Kubernetes API objects (pods, deployments, services, configmaps, secrets, namespaces, RBAC policies, nodes, etc.) and their current state/configuration.

If etcd data is permanently lost: the control plane loses all knowledge of what should be running. Existing running containers on worker nodes continue running (kubelet keeps them alive), but the cluster cannot manage them — it doesn't know they exist. All configuration, secrets, and desired state are gone. Recovery requires restoring from a backup or rebuilding from scratch. This is why etcd backups are critical in production.

</details>

---

---

## Lesson 2 — Pods — The Atomic Unit

> **Level:** Beginner
> **Goal:** Understand Pods — Kubernetes' fundamental unit of deployment

---

### 2.1 What is a Pod?

A Pod is the smallest deployable unit in Kubernetes. It is a wrapper around one or more containers that share:
- **Network namespace:** Same IP address and port space (containers communicate via localhost)
- **Storage:** Can share volumes
- **Lifecycle:** Created and destroyed together

> **The container analogy:** If a container is a house, a Pod is the land plot the house sits on. Multiple containers (houses) can share the same plot (network, storage).

**When to put multiple containers in one Pod:**
- A main application container and a **sidecar** (log shipper, proxy, sync agent) that must be co-located
- An **init container** that runs setup before the main container starts
- A main container and an **ambassador** container that proxies external requests

**When NOT to put multiple containers in one Pod:**
- Services that can scale independently
- Services that have different resource requirements
- Services that don't need to share localhost networking

> **Production Rule:** One main container per Pod in the vast majority of cases. Multi-container pods are the exception, not the rule. Each microservice gets its own Pod (and its own Deployment).

---

### 2.2 Pod YAML — Complete Reference

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app-pod
  namespace: default
  labels:
    app: my-app
    environment: production
    version: "1.0"
  annotations:
    description: "Main application pod"
    prometheus.io/scrape: "true"
    prometheus.io/port: "8080"
spec:
  # Init containers run to completion BEFORE main containers start
  initContainers:
    - name: wait-for-db
      image: busybox:1.36
      command: ['sh', '-c', 'until nc -z db-service 5432; do echo waiting; sleep 2; done']

  containers:
    - name: api
      image: mycompany/api:v1.2.3    # Always use specific tags!
      imagePullPolicy: IfNotPresent   # Always, IfNotPresent, Never

      ports:
        - containerPort: 3000
          name: http
          protocol: TCP

      # Environment variables
      env:
        - name: NODE_ENV
          value: "production"
        - name: DB_HOST
          valueFrom:
            configMapKeyRef:
              name: app-config
              key: database_host
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: db-secret
              key: password

      # Resource requests and limits (ALWAYS set these)
      resources:
        requests:
          memory: "128Mi"
          cpu: "100m"
        limits:
          memory: "256Mi"
          cpu: "500m"

      # Liveness probe — is the container alive?
      livenessProbe:
        httpGet:
          path: /health
          port: 3000
        initialDelaySeconds: 15
        periodSeconds: 20
        failureThreshold: 3

      # Readiness probe — is the container ready for traffic?
      readinessProbe:
        httpGet:
          path: /ready
          port: 3000
        initialDelaySeconds: 5
        periodSeconds: 10

      # Volume mounts
      volumeMounts:
        - name: config-volume
          mountPath: /app/config
          readOnly: true
        - name: data-volume
          mountPath: /app/data

  # Volumes available to containers
  volumes:
    - name: config-volume
      configMap:
        name: app-config
    - name: data-volume
      persistentVolumeClaim:
        claimName: app-data-pvc

  # Pod-level settings
  restartPolicy: Always       # Always, OnFailure, Never
  terminationGracePeriodSeconds: 30
  serviceAccountName: api-service-account
  imagePullSecrets:
    - name: registry-credentials
  nodeSelector:
    kubernetes.io/os: linux
```

---

### 2.3 Essential Pod Commands

```bash
# Create a pod from YAML
kubectl apply -f pod.yaml

# Quick imperative pod creation (learning/testing only)
kubectl run nginx --image=nginx:alpine
kubectl run debug --image=busybox:1.36 --restart=Never --rm -it -- sh

# List pods
kubectl get pods
kubectl get pods -o wide             # Show node, IP, nominated node
kubectl get pods -A                  # All namespaces
kubectl get pods -n kube-system      # Specific namespace
kubectl get pods --watch             # Live updates
kubectl get pods -l app=my-app       # Filter by label

# Get pod details
kubectl describe pod my-app-pod
kubectl describe pod my-app-pod | grep -A 10 Events:

# Pod logs
kubectl logs my-app-pod
kubectl logs my-app-pod -c api       # Specific container in multi-container pod
kubectl logs my-app-pod --previous   # Logs from previous (crashed) container
kubectl logs my-app-pod -f --tail=50 # Follow last 50 lines
kubectl logs -l app=my-app           # Logs from all pods with label

# Execute commands in pod
kubectl exec -it my-app-pod -- bash
kubectl exec -it my-app-pod -c api -- sh     # Specific container
kubectl exec my-app-pod -- env               # Non-interactive
kubectl exec my-app-pod -- cat /etc/config   # Read file

# Copy files
kubectl cp my-app-pod:/app/logs/error.log ./error.log
kubectl cp ./config.json my-app-pod:/app/config.json

# Delete pods
kubectl delete pod my-app-pod
kubectl delete pod my-app-pod --grace-period=0  # Force delete (emergency only)
kubectl delete pods -l app=my-app               # Delete by label
```

---

### 2.4 Pod Lifecycle and Status

| Phase | Meaning |
|---|---|
| **Pending** | Pod accepted, but containers not yet running (scheduling, image pull in progress) |
| **Running** | Pod bound to node, at least one container running |
| **Succeeded** | All containers exited successfully (exit code 0). For Jobs. |
| **Failed** | All containers terminated, at least one with failure |
| **Unknown** | Pod status cannot be obtained (node communication problem) |

**Container States:**

| State | Meaning |
|---|---|
| **Waiting** | Not yet running — image pull, init containers running |
| **Running** | Container executing |
| **Terminated** | Container exited |

**Common error statuses:**
```bash
kubectl get pods
# NAME            READY   STATUS             RESTARTS   AGE
# api-pod         0/1     CrashLoopBackOff   5          3m     ← Crashing repeatedly
# api-pod         0/1     OOMKilled           2          5m     ← Out of memory
# api-pod         0/1     ImagePullBackOff    0          1m     ← Can't pull image
# api-pod         0/1     Pending             0          10m    ← Not scheduled
# api-pod         0/1     Terminating         0          2m     ← Being deleted
```

---

### 2.5 Hands-On Lab 2 — Pod Operations

```bash
# Step 1: Create cluster
kind create cluster --name lab2

# Step 2: Run your first pod
kubectl run nginx --image=nginx:alpine --port=80
kubectl get pods --watch

# Step 3: Examine the pod
kubectl describe pod nginx
kubectl get pod nginx -o yaml    # Full spec and status

# Step 4: Access the pod
kubectl exec -it nginx -- sh
# Inside: nginx -v, ls /etc/nginx/, exit

# Step 5: View logs
kubectl logs nginx
# Port-forward to test the app locally
kubectl port-forward pod/nginx 8080:80
# Open http://localhost:8080 in browser (or curl http://localhost:8080)

# Step 6: Create a pod with YAML
cat > my-pod.yaml << 'EOF'
apiVersion: v1
kind: Pod
metadata:
  name: my-app
  labels:
    app: demo
    environment: lab
spec:
  containers:
    - name: web
      image: nginx:alpine
      ports:
        - containerPort: 80
      resources:
        requests:
          memory: "32Mi"
          cpu: "50m"
        limits:
          memory: "64Mi"
          cpu: "100m"
EOF

kubectl apply -f my-pod.yaml
kubectl get pods -o wide

# Step 7: Force a pod crash and watch restart
kubectl exec my-app -- kill 1    # Kill the main process
kubectl get pods --watch         # Watch it restart

# Step 8: Create a failing pod to practice troubleshooting
cat > bad-pod.yaml << 'EOF'
apiVersion: v1
kind: Pod
metadata:
  name: bad-image
spec:
  containers:
    - name: app
      image: nginx:doesnotexist
EOF

kubectl apply -f bad-pod.yaml
kubectl get pods          # ImagePullBackOff
kubectl describe pod bad-image | grep -A 5 Events:

# Cleanup
kind delete cluster --name lab2
```

---

---

## Lesson 3 — ReplicaSets and Deployments

> **Level:** Beginner → Intermediate
> **Goal:** Manage scalable, self-healing workloads

---

### 3.1 Why You Almost Never Create Pods Directly

Pods are mortal. If a Pod is deleted or its node fails, the Pod is gone. There is no automatic replacement. For production workloads, you need something that ensures your desired number of Pods is always running.

**The hierarchy:**
```
Deployment          ← You create and manage this
    └── ReplicaSet  ← Deployment creates and manages this
            └── Pods ← ReplicaSet creates and manages these
```

---

### 3.2 ReplicaSet

A ReplicaSet ensures a specified number of Pod replicas are running at all times. If a Pod is deleted or crashes, the ReplicaSet creates a replacement.

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: api-rs
spec:
  replicas: 3
  selector:
    matchLabels:
      app: api       # ReplicaSet manages Pods with this label
  template:          # Pod template — used when creating new Pods
    metadata:
      labels:
        app: api     # MUST match selector.matchLabels
    spec:
      containers:
        - name: api
          image: nginx:alpine
          ports:
            - containerPort: 80
```

> **Why not use ReplicaSets directly?** ReplicaSets don't support rolling updates. If you change the image in a ReplicaSet, existing Pods are not updated — only new Pods get the new image. You'd have to manually delete old Pods. Deployments solve this with automatic rolling updates and rollback capability.

---

### 3.3 Deployments — What You Actually Use

A Deployment provides declarative updates for Pods and ReplicaSets. It owns a ReplicaSet which owns the Pods.

**What Deployments add over ReplicaSets:**
- Rolling updates (new pods start before old ones stop)
- Rollback (go back to previous version with one command)
- Pause and resume rollouts
- History of past deployments

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api-deployment
  labels:
    app: api
spec:
  replicas: 3
  selector:
    matchLabels:
      app: api
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1         # Max extra pods during update (above desired count)
      maxUnavailable: 0   # Max pods that can be unavailable during update (zero downtime)
  template:
    metadata:
      labels:
        app: api
    spec:
      containers:
        - name: api
          image: nginx:1.25-alpine
          ports:
            - containerPort: 80
          resources:
            requests:
              memory: "64Mi"
              cpu: "100m"
            limits:
              memory: "128Mi"
              cpu: "200m"
          readinessProbe:
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 5
            periodSeconds: 10
```

---

### 3.4 Deployment Strategy Types

**RollingUpdate (default — zero downtime):**
```
Start: [v1] [v1] [v1]
Step 1: [v1] [v1] [v1] [v2]   ← new pod starts (maxSurge: 1)
Step 2: [v1] [v1] [v2]        ← old pod removed after new is ready (maxUnavailable: 0)
Step 3: [v1] [v1] [v2] [v2]   ← another new pod starts
Step 4: [v1] [v2] [v2]        ← another old removed
Step 5: [v1] [v2] [v2] [v2]   ← last new pod
Step 6: [v2] [v2] [v2]        ← complete
```

**Recreate (with downtime — rarely used):**
```
Start: [v1] [v1] [v1]
Step 1: []                ← ALL old pods deleted
Step 2: [v2] [v2] [v2]   ← ALL new pods started
Use when: new and old version cannot coexist (e.g., database schema changes)
```

---

### 3.5 Essential Deployment Commands

```bash
# Create deployment
kubectl apply -f deployment.yaml

# Imperative creation (learning/quick testing)
kubectl create deployment nginx --image=nginx:alpine --replicas=3

# Get deployments
kubectl get deployments
kubectl get deploy         # Short form
kubectl get deploy -o wide

# Describe deployment
kubectl describe deployment api-deployment

# Scale
kubectl scale deployment api-deployment --replicas=5

# Update image (triggers rolling update)
kubectl set image deployment/api-deployment api=nginx:1.26-alpine

# Watch rollout progress
kubectl rollout status deployment/api-deployment

# Rollout history
kubectl rollout history deployment/api-deployment
kubectl rollout history deployment/api-deployment --revision=2

# Rollback to previous version
kubectl rollout undo deployment/api-deployment

# Rollback to specific revision
kubectl rollout undo deployment/api-deployment --to-revision=2

# Pause a rollout (canary testing mid-rollout)
kubectl rollout pause deployment/api-deployment

# Resume a paused rollout
kubectl rollout resume deployment/api-deployment

# Restart all pods (triggers rolling restart — useful for config reload)
kubectl rollout restart deployment/api-deployment
```

---

### 3.6 Hands-On Lab 3 — Deployments and Rolling Updates

```bash
kind create cluster --name lab3

# Step 1: Create a deployment
cat > deployment.yaml << 'EOF'
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-app
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
        - name: web
          image: nginx:1.24-alpine
          ports:
            - containerPort: 80
          resources:
            requests: { memory: "32Mi", cpu: "50m" }
            limits: { memory: "64Mi", cpu: "100m" }
EOF

kubectl apply -f deployment.yaml
kubectl get pods --watch

# Step 2: Understand the hierarchy
kubectl get replicasets
kubectl get pods -l app=web-app
kubectl describe deployment web-app

# Step 3: Scale it
kubectl scale deployment web-app --replicas=5
kubectl get pods -w

# Step 4: Perform a rolling update
kubectl set image deployment/web-app web=nginx:1.25-alpine
kubectl rollout status deployment/web-app    # Watch progress
kubectl get pods -w                          # Watch pods being replaced

# Step 5: Check history
kubectl rollout history deployment/web-app

# Step 6: Simulate a bad update
kubectl set image deployment/web-app web=nginx:doesnotexist
kubectl rollout status deployment/web-app    # This will hang (image pull failing)
kubectl get pods                             # Some old, some ImagePullBackOff

# Step 7: Rollback!
kubectl rollout undo deployment/web-app
kubectl rollout status deployment/web-app
kubectl get pods    # All back to running

# Step 8: Self-healing demonstration
kubectl delete pod <one-of-the-pod-names>
kubectl get pods --watch   # ReplicaSet creates a replacement immediately

kind delete cluster --name lab3
```

---

### 3.7 Practice Questions — Lessons 2–3

**Q1.** You deploy version v1 of your app (3 replicas). You update to v2 with `maxSurge: 1, maxUnavailable: 0`. During the rollout, what is the maximum number of pods running simultaneously?

<details>
<summary>Answer</summary>

**4 pods.** maxSurge: 1 means at most 1 extra pod above the desired count (3) can exist. maxUnavailable: 0 means all 3 current pods must remain available. So: up to 3 (current) + 1 (surge) = 4 pods running simultaneously. This ensures zero downtime because old pods are only removed after new ones pass readiness probes.

</details>

---

**Q2 — Scenario.** A pod has status `CrashLoopBackOff`. What are the most likely causes and how do you investigate?

<details>
<summary>Answer</summary>

CrashLoopBackOff means the container keeps crashing and Kubernetes keeps restarting it with exponential backoff (10s, 20s, 40s, up to 5 minutes between restarts).

**Investigation steps:**
1. `kubectl logs <pod>` — see the application's last output before crash
2. `kubectl logs <pod> --previous` — see logs from the previous (crashed) container instance
3. `kubectl describe pod <pod>` — check Events section, see exit code, last state
4. Check exit code: 1 = application error, 137 = OOM killed, 139 = segfault

**Common causes:** Application startup error (bad config, missing env var, failed DB connection), OOM (memory limit too low), misconfigured command/entrypoint, missing required files/secrets.

</details>

---

---

## Lesson 4 — Labels, Selectors, and Namespaces

> **Level:** Beginner → Intermediate
> **Goal:** Organise and select Kubernetes resources

---

### 4.1 Labels — The Kubernetes Glue

Labels are key-value pairs attached to objects. They are the primary mechanism for organising objects and defining relationships between them. **Services find Pods via labels. Deployments manage Pods via labels.**

```yaml
metadata:
  labels:
    app: api                    # Application name
    version: "v2.1.0"          # Version
    environment: production     # Environment
    tier: backend               # Architecture tier
    team: platform-engineering  # Owning team
```

**Label selectors:**
```bash
# Equality-based selectors
kubectl get pods -l app=api
kubectl get pods -l app=api,environment=production    # AND condition
kubectl get pods -l environment!=staging              # NOT equal

# Set-based selectors
kubectl get pods -l 'environment in (production, staging)'
kubectl get pods -l 'environment notin (dev)'
kubectl get pods -l 'app'              # Has the label 'app' (any value)
kubectl get pods -l '!deprecated'     # Does NOT have label 'deprecated'

# Apply label to existing resource
kubectl label pod my-pod version=v2
kubectl label pod my-pod version=v3 --overwrite

# Remove label
kubectl label pod my-pod version-    # Trailing dash removes label
```

---

### 4.2 Annotations — Non-Identifying Metadata

Unlike labels (used for selection), annotations store arbitrary metadata that tools and humans read. They cannot be used in selectors.

```yaml
metadata:
  annotations:
    # Human-readable info
    description: "Main API service"
    documentation: "https://wiki.company.com/api"

    # Tool-specific config
    prometheus.io/scrape: "true"
    prometheus.io/port: "8080"
    prometheus.io/path: "/metrics"

    # Deployment metadata
    kubernetes.io/change-cause: "Update API to v2.1.0 - fix payment bug"
    deployment.kubernetes.io/revision: "5"
    git-commit: "abc123def456"
```

---

### 4.3 Namespaces — Cluster-Level Isolation

Namespaces partition a single physical Kubernetes cluster into multiple virtual clusters. They provide:
- **Isolation:** Resources in different namespaces don't conflict by name
- **Access control:** RBAC can be applied per namespace
- **Resource quotas:** Limit CPU/memory usage per namespace
- **Organised structure:** One namespace per team, environment, or application

**Default namespaces:**
- `default` — where resources go if you don't specify a namespace
- `kube-system` — Kubernetes system components (api-server, dns, scheduler)
- `kube-public` — publicly readable cluster info (kubeconfig bootstrap)
- `kube-node-lease` — node heartbeat leases (for faster node failure detection)

```bash
# Create a namespace
kubectl create namespace production
kubectl create namespace staging
kubectl create namespace development

# Or via YAML
cat > namespaces.yaml << 'EOF'
apiVersion: v1
kind: Namespace
metadata:
  name: production
  labels:
    environment: production
    team: platform
EOF
kubectl apply -f namespaces.yaml

# List namespaces
kubectl get namespaces
kubectl get ns    # Short form

# Work in a specific namespace
kubectl get pods -n production
kubectl apply -f deployment.yaml -n production

# Set default namespace for current context
kubectl config set-context --current --namespace=production
kubectl get pods    # Now shows production namespace by default

# List resources in all namespaces
kubectl get pods --all-namespaces
kubectl get pods -A

# Delete namespace (deletes ALL resources in it)
kubectl delete namespace development
```

---

### 4.4 Production Namespace Structure

```bash
# Recommended namespace structure for a team:

# System namespaces (don't touch)
kube-system
kube-public
kube-node-lease

# Infrastructure namespaces
monitoring          # Prometheus, Grafana, alerting
logging             # Fluentd, Elasticsearch, Kibana
ingress-nginx       # Ingress controller
cert-manager        # TLS certificate automation

# Application namespaces
production          # Production workloads
staging             # Staging/pre-prod
development         # Development workloads
```

---

---

## Lesson 5 — Basic Troubleshooting

> **Level:** Beginner → Intermediate
> **Goal:** Diagnose and fix common Kubernetes problems

---

### 5.1 The Troubleshooting Mindset

Always work top-down: cluster → node → pod → container → application.

```
Is the cluster healthy?           kubectl get nodes
           │
Is the pod scheduled?             kubectl get pods
           │
Is the pod running?               kubectl describe pod <name>
           │
Is the container starting?        kubectl logs <pod> --previous
           │
Is the application working?       kubectl exec -it <pod> -- curl localhost:8080
```

---

### 5.2 Essential Troubleshooting Commands

```bash
# ─── CLUSTER HEALTH ─────────────────────────────────────────────────
kubectl get nodes
kubectl describe node <node-name>   # Check conditions, capacity, allocated resources
kubectl get events --sort-by='.lastTimestamp'   # Cluster-wide events, newest last
kubectl get events -A --field-selector type=Warning   # Warnings only

# ─── POD ISSUES ──────────────────────────────────────────────────────
# Get ALL details about a pod
kubectl describe pod <pod-name>
# Look at: Events section, State, Last State, Exit Code, Conditions

# Check logs
kubectl logs <pod-name>
kubectl logs <pod-name> --previous      # Previous container instance
kubectl logs <pod-name> -c <container>  # Specific container
kubectl logs <pod-name> -f              # Follow (live)

# Get pod status details as JSON
kubectl get pod <pod-name> -o jsonpath='{.status.conditions}'
kubectl get pod <pod-name> -o jsonpath='{.status.containerStatuses[0].state}'

# Interactive debugging
kubectl exec -it <pod-name> -- sh

# Run ephemeral debug container (K8s 1.23+)
kubectl debug -it <pod-name> --image=busybox --target=<container-name>

# ─── COMMON STATUS DIAGNOSIS ─────────────────────────────────────────
# Pending → not scheduled
#   kubectl describe pod <n> → check Events for scheduling failures
#   Common causes: insufficient resources, no matching nodes, PVC not bound

# ImagePullBackOff → can't pull image
#   Wrong image name/tag? Private registry without imagePullSecret?
#   kubectl describe pod <n> → Events show exact error

# CrashLoopBackOff → container keeps crashing
#   kubectl logs <pod> --previous → see crash reason

# OOMKilled → exit code 137
#   kubectl describe pod <n> → "OOMKilled"
#   Increase memory limit or fix memory leak

# Terminating (stuck) → pod won't delete
#   kubectl delete pod <n> --grace-period=0 --force

# ─── DEPLOYMENT ISSUES ───────────────────────────────────────────────
kubectl rollout status deployment/<name>
kubectl rollout history deployment/<name>
kubectl describe deployment <name>
```

---

### 5.3 Hands-On Lab 5 — Troubleshooting Practice

```bash
kind create cluster --name lab5

# Scenario 1: Fix ImagePullBackOff
cat > broken-1.yaml << 'EOF'
apiVersion: v1
kind: Pod
metadata:
  name: broken-image
spec:
  containers:
    - name: app
      image: nginx:99.99.99
EOF
kubectl apply -f broken-1.yaml
kubectl get pods
kubectl describe pod broken-image
# Fix: change image to nginx:alpine, apply again

# Scenario 2: Fix CrashLoopBackOff
cat > broken-2.yaml << 'EOF'
apiVersion: v1
kind: Pod
metadata:
  name: crash-loop
spec:
  containers:
    - name: app
      image: busybox
      command: ['sh', '-c', 'echo "starting"; exit 1']
EOF
kubectl apply -f broken-2.yaml
kubectl get pods --watch
kubectl logs crash-loop
kubectl logs crash-loop --previous
# Fix: change exit 1 to sleep 3600

# Scenario 3: Fix Pending pod (resource request too high)
cat > broken-3.yaml << 'EOF'
apiVersion: v1
kind: Pod
metadata:
  name: too-big
spec:
  containers:
    - name: app
      image: nginx:alpine
      resources:
        requests:
          memory: "100Gi"   # No node has this much memory!
          cpu: "100"
EOF
kubectl apply -f broken-3.yaml
kubectl describe pod too-big
# Fix: reduce to 64Mi memory, 100m CPU

kind delete cluster --name lab5
```

---

---

# PHASE 2 — INTERMEDIATE

---

## Lesson 6 — Kubernetes Services

> **Level:** Intermediate
> **Goal:** Expose and connect applications within and outside the cluster

---

### 6.1 Why Services Exist

Pods are ephemeral. Their IP addresses change every time they restart. When you scale a deployment from 1 to 5 replicas, you have 5 different IPs. How does your frontend know which Pod IP to call?

> **A Service is a stable network endpoint** that load balances traffic across a dynamic set of Pods. The Service IP never changes. Kubernetes DNS resolves the Service name to its IP. Your app calls `http://api-service:3000` — it always works, regardless of how many Pods exist or what their IPs are.

---

### 6.2 The Four Service Types

**ClusterIP (default) — Internal only:**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: api-service
spec:
  type: ClusterIP          # Default — only reachable within cluster
  selector:
    app: api               # Routes to all Pods with this label
  ports:
    - protocol: TCP
      port: 80             # Port the Service listens on
      targetPort: 3000     # Port the Pod containers listen on
```

```bash
# DNS: api-service.default.svc.cluster.local
# Short form within same namespace: api-service
# From another namespace: api-service.default
```

**NodePort — External via node IP:**
```yaml
spec:
  type: NodePort
  selector:
    app: api
  ports:
    - port: 80
      targetPort: 3000
      nodePort: 30080    # Optional — Kubernetes picks 30000-32767 if not specified
```
```
External traffic → NodeIP:30080 → Service (80) → Pod:3000
```

**LoadBalancer — External via cloud load balancer:**
```yaml
spec:
  type: LoadBalancer
  selector:
    app: api
  ports:
    - port: 80
      targetPort: 3000
```
```
External traffic → Cloud LB (public IP) → NodePort → Service → Pod
```
> Works natively on AKS, EKS, GKE. On bare metal / kind: use MetalLB or cloud-provider-kind.

**ExternalName — Map to external DNS:**
```yaml
spec:
  type: ExternalName
  externalName: mydb.company.com   # Returns a CNAME record
```
> Used to integrate external services (like a managed database) into Kubernetes DNS.

---

### 6.3 Headless Services — Direct Pod Discovery

A headless service (clusterIP: None) returns the individual Pod IPs via DNS rather than a single virtual IP. Used for stateful applications (databases) where you need to connect to a specific Pod.

```yaml
spec:
  clusterIP: None   # Headless
  selector:
    app: postgres
```

```
DNS query: postgres-service.default.svc.cluster.local
Returns: 10.0.1.5, 10.0.1.6, 10.0.1.7   (individual Pod IPs)
vs. regular service: always returns single VIP 10.96.45.12
```

---

### 6.4 Hands-On Lab 6 — Services

```bash
kind create cluster --name lab6

# Step 1: Deploy an application
cat > app.yaml << 'EOF'
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
        - name: web
          image: nginx:alpine
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: web-service
spec:
  type: ClusterIP
  selector:
    app: web-app
  ports:
    - port: 80
      targetPort: 80
EOF
kubectl apply -f app.yaml

# Step 2: Verify service endpoints (IPs of pods behind service)
kubectl get services
kubectl describe service web-service   # See Endpoints field
kubectl get endpoints web-service

# Step 3: Test service from inside cluster
kubectl run test-pod --image=busybox --rm -it -- sh
# Inside: wget -qO- http://web-service
# Inside: nslookup web-service   (DNS resolution)

# Step 4: Port-forward to test locally
kubectl port-forward service/web-service 8080:80
# curl http://localhost:8080

# Step 5: Create NodePort service
kubectl expose deployment web-app --type=NodePort --port=80 --name=web-nodeport
kubectl get service web-nodeport
# Access via: kubectl get nodes -o wide → use node IP + node port

kind delete cluster --name lab6
```

---

---

## Lesson 7 — Ingress

> **Level:** Intermediate
> **Goal:** Route HTTP/HTTPS traffic to multiple services

---

### 7.1 Why Ingress?

If you have 10 microservices each exposed as a LoadBalancer Service, you get 10 cloud load balancers = 10 public IPs = expensive and hard to manage.

> **Ingress uses one load balancer** to route HTTP/HTTPS traffic to multiple backend services based on hostname and URL path.

```
Internet → Load Balancer (1 IP) → Ingress Controller
                                        │
                          ┌─────────────┼──────────────────┐
                          ▼             ▼                  ▼
                  api.myapp.com  app.myapp.com   admin.myapp.com
                     /v1/*          /*                /*
                       │              │                  │
                   api-service    web-service       admin-service
```

---

### 7.2 Ingress Components

**Ingress Controller:** The actual reverse proxy that runs in the cluster (nginx, traefik, HAProxy). Does the routing. Must be deployed separately.

**Ingress Resource:** Kubernetes object defining routing rules. The Ingress Controller reads these rules.

---

### 7.3 Setting Up NGINX Ingress Controller

```bash
# For kind clusters
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml

# For AKS
helm install ingress-nginx ingress-nginx/ingress-nginx \
  --namespace ingress-nginx \
  --create-namespace \
  --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz

# For general (cloud)
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.9.4/deploy/static/provider/cloud/deploy.yaml
```

---

### 7.4 Ingress Resource — Complete Examples

**Path-based routing:**
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
spec:
  ingressClassName: nginx
  rules:
    - host: myapp.example.com
      http:
        paths:
          - path: /api
            pathType: Prefix
            backend:
              service:
                name: api-service
                port:
                  number: 80
          - path: /
            pathType: Prefix
            backend:
              service:
                name: web-service
                port:
                  number: 80
```

**Host-based routing with TLS:**
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: multi-host-ingress
  annotations:
    cert-manager.io/cluster-issuer: letsencrypt-prod
spec:
  ingressClassName: nginx
  tls:
    - hosts:
        - api.myapp.com
        - app.myapp.com
      secretName: myapp-tls-secret    # cert-manager creates this automatically
  rules:
    - host: api.myapp.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: api-service
                port:
                  number: 80
    - host: app.myapp.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: web-service
                port:
                  number: 80
```

---

---

## Lesson 8 — ConfigMaps and Secrets

> **Level:** Intermediate
> **Goal:** Manage application configuration and sensitive data

---

### 8.1 ConfigMaps — Externalise Configuration

ConfigMaps decouple configuration from container images. Store non-sensitive config data.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  # Simple key-value pairs
  database_host: "postgres-service.default.svc.cluster.local"
  database_port: "5432"
  log_level: "info"
  max_connections: "100"

  # Multi-line config file
  nginx.conf: |
    server {
      listen 80;
      location / {
        proxy_pass http://backend;
      }
    }

  # JSON config
  app-settings.json: |
    {
      "featureFlags": {
        "newUI": true,
        "betaFeatures": false
      }
    }
```

**Using ConfigMaps in Pods:**
```yaml
spec:
  containers:
    - name: app
      # Method 1: As environment variables (individual keys)
      env:
        - name: DB_HOST
          valueFrom:
            configMapKeyRef:
              name: app-config
              key: database_host

      # Method 2: All keys as env vars
      envFrom:
        - configMapRef:
            name: app-config

      # Method 3: As files mounted in a volume
      volumeMounts:
        - name: config-files
          mountPath: /etc/app/config
          readOnly: true

  volumes:
    - name: config-files
      configMap:
        name: app-config
        # Optional: mount only specific keys as files
        items:
          - key: nginx.conf
            path: nginx.conf
```

```bash
# Create ConfigMap from literal values
kubectl create configmap app-config \
  --from-literal=database_host=postgres \
  --from-literal=log_level=info

# Create ConfigMap from a file
kubectl create configmap nginx-config --from-file=nginx.conf

# Create ConfigMap from a directory (all files become keys)
kubectl create configmap app-configs --from-file=./config-dir/

# View ConfigMap
kubectl get configmap app-config -o yaml
kubectl describe configmap app-config
```

---

### 8.2 Secrets — Sensitive Configuration

Secrets are like ConfigMaps but designed for sensitive data. Base64-encoded (NOT encrypted by default — configure encryption at rest separately).

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  # Values MUST be base64-encoded
  # echo -n "mysecretpassword" | base64
  password: bXlzZWNyZXRwYXNzd29yZA==
  username: YWRtaW4=

stringData:
  # Alternative: plain text (Kubernetes base64-encodes it automatically)
  api-key: "sk-1234567890abcdef"
  connection-string: "postgresql://admin:secret@db:5432/myapp"
```

```bash
# Create secret from literal
kubectl create secret generic db-secret \
  --from-literal=password=mysecretpassword \
  --from-literal=username=admin

# Create TLS secret
kubectl create secret tls myapp-tls \
  --cert=tls.crt \
  --key=tls.key

# Create Docker registry secret (for private registries)
kubectl create secret docker-registry registry-creds \
  --docker-server=mycompany.azurecr.io \
  --docker-username=myapp \
  --docker-password=mypassword

# View secret (values shown base64 encoded)
kubectl get secret db-secret -o yaml

# Decode a secret value
kubectl get secret db-secret -o jsonpath='{.data.password}' | base64 --decode
```

**Using Secrets in Pods:**
```yaml
spec:
  containers:
    - name: app
      env:
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: db-secret
              key: password
      volumeMounts:
        - name: secret-files
          mountPath: /etc/secrets
          readOnly: true

  volumes:
    - name: secret-files
      secret:
        secretName: db-secret

  # For private image registries
  imagePullSecrets:
    - name: registry-creds
```

> **Important:** Base64 is NOT encryption. Kubernetes Secrets are only as secure as your etcd and RBAC. For true secret security: enable encryption at rest for etcd, use external secret management (HashiCorp Vault, Azure Key Vault, AWS Secrets Manager), and use the External Secrets Operator to sync them into Kubernetes Secrets.

---

### 8.3 Practice Questions — Lessons 6–8

**Q1.** What is the difference between a ClusterIP and a Headless Service? When would you use a Headless Service?

<details>
<summary>Answer</summary>

A ClusterIP service gets a virtual IP (VIP). DNS resolves the service name to this single VIP. kube-proxy load balances requests across the backend Pods. The client never sees individual Pod IPs.

A Headless Service (clusterIP: None) has no VIP. DNS returns the actual IPs of all Pods matching the selector. The client connects directly to individual Pods.

Use Headless Services for stateful applications where you need to address specific instances — for example, PostgreSQL with read replicas (you want to specifically call the primary vs. a replica), Kafka, Cassandra, Zookeeper, or StatefulSets in general where each Pod has a stable identity.

</details>

---

**Q2.** A ConfigMap is updated while pods are running. Do the pods automatically see the new values?

<details>
<summary>Answer</summary>

It depends on how the ConfigMap is consumed:
- **Mounted as a volume file:** Yes — Kubernetes updates the mounted files eventually (after kubelet sync period, typically 1-2 minutes). The application may need to detect file changes and reload (many apps do this with inotify or a config reload signal).
- **As environment variables (env/envFrom):** No — environment variables are set at container startup and do not update while the container is running. The Pod must be restarted to pick up new values.

Best practice: use volume mounts for config that changes frequently, and use `kubectl rollout restart deployment/<name>` to trigger a rolling restart when environment variable config changes.

</details>


---

---

## Lesson 9 — Resource Limits, Probes, and Rolling Updates

> **Level:** Intermediate → DevOps
> **Goal:** Build production-grade pod configurations

---

### 9.1 Resource Requests and Limits — Why They Are Mandatory

**Requests:** The minimum resources a container is guaranteed. The scheduler uses requests to decide which node can host the pod.

**Limits:** The maximum resources a container can use. If it exceeds the memory limit, it is OOM-killed. If it exceeds the CPU limit, it is throttled.

```yaml
resources:
  requests:
    memory: "128Mi"    # Scheduler guarantees this node has 128Mi available
    cpu: "100m"        # 100 millicores = 0.1 CPU core
  limits:
    memory: "256Mi"    # If container uses > 256Mi → OOMKilled
    cpu: "500m"        # If container wants > 500m → throttled (not killed)
```

**CPU units:**
- `1` = 1 CPU core = 1000m (millicores)
- `500m` = 0.5 CPU core
- `100m` = 0.1 CPU core

**Memory units:**
- `Mi` = Mebibytes (1 MiB = 1,048,576 bytes)
- `Gi` = Gibibytes
- `M` = Megabytes (1 MB = 1,000,000 bytes)
- Use `Mi`/`Gi` — they are unambiguous

**What happens without limits:**
- A memory leak in one container can consume all node memory, triggering the OS OOM killer — which may kill other containers or system processes
- One noisy CPU-hungry container starves all others
- The Kubernetes scheduler cannot make good placement decisions without requests

> **Production rule:** Always set both requests AND limits on every container. Start with `requests: 50% of limits` as a starting point, then tune based on actual usage from monitoring.

---

### 9.2 Resource Quotas — Namespace-Level Limits

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: production-quota
  namespace: production
spec:
  hard:
    # Pod count limits
    pods: "50"
    # Compute limits
    requests.cpu: "10"
    requests.memory: 20Gi
    limits.cpu: "20"
    limits.memory: 40Gi
    # Object count limits
    services: "20"
    persistentvolumeclaims: "10"
    secrets: "50"
    configmaps: "50"
```

```bash
kubectl apply -f resource-quota.yaml
kubectl describe resourcequota production-quota -n production
```

**LimitRange — Default limits for containers that don't specify them:**
```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: default-limits
  namespace: production
spec:
  limits:
    - type: Container
      default:           # Default limit if not specified
        memory: 256Mi
        cpu: 500m
      defaultRequest:    # Default request if not specified
        memory: 128Mi
        cpu: 100m
      max:               # Maximum allowed limit
        memory: 2Gi
        cpu: "2"
      min:               # Minimum allowed request
        memory: 64Mi
        cpu: 50m
```

---

### 9.3 Liveness and Readiness Probes

**Liveness Probe:** Is this container still alive and working? If it fails N times, Kubernetes restarts the container.

**Readiness Probe:** Is this container ready to receive traffic? If it fails, the Pod is removed from Service endpoints (no traffic sent) but NOT restarted.

**Startup Probe:** For slow-starting containers. Disables liveness until the startup probe passes. Prevents premature restarts during initialisation.

```yaml
spec:
  containers:
    - name: api
      image: myapp:v1.0

      # STARTUP PROBE — runs first, replaces liveness during startup
      startupProbe:
        httpGet:
          path: /health
          port: 3000
        failureThreshold: 30     # Allow up to 30*10 = 300s to start
        periodSeconds: 10

      # LIVENESS PROBE — is the container still alive?
      livenessProbe:
        httpGet:
          path: /health           # Returns 200 if healthy
          port: 3000
        initialDelaySeconds: 15   # Wait 15s before first check
        periodSeconds: 20         # Check every 20s
        timeoutSeconds: 5         # Fail if no response in 5s
        failureThreshold: 3       # Restart after 3 consecutive failures
        successThreshold: 1       # 1 success to mark healthy

      # READINESS PROBE — is the container ready for traffic?
      readinessProbe:
        httpGet:
          path: /ready            # Returns 200 only when truly ready
          port: 3000              # (e.g., after DB connections established)
        initialDelaySeconds: 5
        periodSeconds: 10
        timeoutSeconds: 3
        failureThreshold: 3
        successThreshold: 2       # Require 2 successes to mark ready
```

**Probe types:**
```yaml
# HTTP GET — most common for web services
httpGet:
  path: /health
  port: 8080
  httpHeaders:
    - name: Authorization
      value: "Bearer health-check-token"

# TCP Socket — check if port is listening
tcpSocket:
  port: 5432       # Good for databases

# Exec — run a command, success if exit code 0
exec:
  command:
    - sh
    - -c
    - "redis-cli ping | grep PONG"

# gRPC — for gRPC services (K8s 1.24+)
grpc:
  port: 50051
  service: "health.v1.Health"
```

---

### 9.4 Pod Disruption Budgets

PodDisruptionBudget (PDB) limits voluntary disruption — protecting workloads during cluster maintenance, node drains, and rolling updates.

```yaml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: api-pdb
spec:
  minAvailable: 2       # At least 2 pods must be available at all times
  # OR:
  # maxUnavailable: 1   # At most 1 pod can be unavailable
  selector:
    matchLabels:
      app: api
```

```bash
# During node drain, Kubernetes respects PDB
kubectl drain node-1 --ignore-daemonsets --delete-emptydir-data
# If draining would violate PDB, drain waits until it's safe
```

---

---

# PHASE 3 — DEVOPS LEVEL

---

## Lesson 10 — Horizontal Pod Autoscaler

> **Level:** DevOps Engineer
> **Goal:** Automatically scale workloads based on demand

---

### 10.1 How HPA Works

The Horizontal Pod Autoscaler automatically scales the number of Pod replicas based on observed metrics. It queries the Metrics Server every 15 seconds, compares current metric values to targets, and adjusts replica count accordingly.

```
HPA Loop (every 15s):
  Read metric (CPU %, memory %, custom metric)
  Calculate desired replicas = currentReplicas × (currentMetric / desiredMetric)
  If desired > current → scale up
  If desired < current (and cooldown passed) → scale down
```

**Prerequisites — Install Metrics Server:**
```bash
# For kind/minikube
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

# For kind specifically (needs insecure TLS)
kubectl patch deployment metrics-server -n kube-system \
  --type='json' \
  -p='[{"op": "add", "path": "/spec/template/spec/containers/0/args/-", "value": "--kubelet-insecure-tls"}]'

# Verify
kubectl top nodes
kubectl top pods
```

---

### 10.2 CPU-Based HPA

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: api-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: api-deployment
  minReplicas: 2
  maxReplicas: 20
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70    # Scale when average CPU > 70% of request
    - type: Resource
      resource:
        name: memory
        target:
          type: AverageValue
          averageValue: 200Mi       # Scale when average memory > 200Mi per pod
  behavior:
    scaleUp:
      stabilizationWindowSeconds: 60      # Wait 60s before scaling up again
      policies:
        - type: Percent
          value: 100                       # Can double replicas per scaling event
          periodSeconds: 60
    scaleDown:
      stabilizationWindowSeconds: 300     # Wait 5 min before scaling down (avoid flapping)
      policies:
        - type: Pods
          value: 1                         # Remove at most 1 pod per scaling event
          periodSeconds: 60
```

```bash
# Create HPA imperatively
kubectl autoscale deployment api-deployment --min=2 --max=20 --cpu-percent=70

# View HPA status
kubectl get hpa
kubectl describe hpa api-hpa
# Watch it in action
kubectl get hpa --watch
```

---

### 10.3 Custom Metrics HPA

Scale based on application-level metrics (queue depth, request latency, active connections):

```yaml
# Scale based on Prometheus custom metric
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: api-custom-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: api-deployment
  minReplicas: 2
  maxReplicas: 50
  metrics:
    # Custom metric from Prometheus adapter
    - type: Pods
      pods:
        metric:
          name: http_requests_per_second
        target:
          type: AverageValue
          averageValue: "100"    # Scale when avg > 100 requests/sec per pod

    # External metric (e.g., Azure Service Bus queue depth)
    - type: External
      external:
        metric:
          name: azure_servicebus_active_messages
          selector:
            matchLabels:
              queue: order-processing
        target:
          type: Value
          value: "1000"          # Scale when queue depth > 1000 messages
```

---

### 10.4 Vertical Pod Autoscaler (VPA)

VPA automatically adjusts CPU and memory requests/limits based on actual usage. Useful for right-sizing containers.

```yaml
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
  name: api-vpa
spec:
  targetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: api-deployment
  updatePolicy:
    updateMode: "Auto"     # Recreate pods with new resource settings
    # "Off" — only recommend, don't change
    # "Initial" — set on pod creation, don't update running pods
  resourcePolicy:
    containerPolicies:
      - containerName: api
        minAllowed:
          cpu: 50m
          memory: 64Mi
        maxAllowed:
          cpu: "2"
          memory: 2Gi
```

---

### 10.5 Hands-On Lab 10 — Load Test and Autoscaling

```bash
kind create cluster --name lab10
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
kubectl patch deployment metrics-server -n kube-system --type='json' \
  -p='[{"op":"add","path":"/spec/template/spec/containers/0/args/-","value":"--kubelet-insecure-tls"}]'

# Deploy app with CPU load endpoint
cat > load-app.yaml << 'EOF'
apiVersion: apps/v1
kind: Deployment
metadata:
  name: php-apache
spec:
  replicas: 1
  selector:
    matchLabels:
      app: php-apache
  template:
    metadata:
      labels:
        app: php-apache
    spec:
      containers:
        - name: php-apache
          image: registry.k8s.io/hpa-example
          ports:
            - containerPort: 80
          resources:
            requests:
              cpu: 200m
              memory: 64Mi
            limits:
              cpu: 500m
              memory: 128Mi
---
apiVersion: v1
kind: Service
metadata:
  name: php-apache
spec:
  selector:
    app: php-apache
  ports:
    - port: 80
EOF
kubectl apply -f load-app.yaml

# Create HPA
kubectl autoscale deployment php-apache --min=1 --max=10 --cpu-percent=50
kubectl get hpa --watch &

# Generate load (in another terminal)
kubectl run load-gen --image=busybox:1.36 --rm -it -- \
  sh -c "while true; do wget -q -O- http://php-apache; done"

# Watch HPA scale up
kubectl get pods --watch

# Stop load (Ctrl+C in load-gen terminal)
# Watch HPA scale back down (takes ~5min due to stabilization window)

kind delete cluster --name lab10
```

---

---

## Lesson 11 — Kubernetes Networking Deep Dive

> **Level:** DevOps Engineer
> **Goal:** Understand how Kubernetes networking works end to end

---

### 11.1 The Kubernetes Networking Model

Kubernetes enforces these rules:
1. Every Pod gets its own unique IP address
2. Pods can communicate with any other Pod without NAT
3. Nodes can communicate with all Pods without NAT
4. The IP a Pod sees for itself is the same IP others see for it

This is implemented by the **CNI (Container Network Interface)** plugin.

---

### 11.2 CNI Plugins

The CNI plugin is responsible for:
- Assigning IP addresses to Pods
- Setting up network routes between Pods on different nodes
- Implementing NetworkPolicy rules

| CNI Plugin | Key Feature | Use Case |
|---|---|---|
| **Calico** | NetworkPolicy support, BGP routing | Most common production choice |
| **Flannel** | Simple overlay network, no NetworkPolicy | Simple setups, learning |
| **Cilium** | eBPF-based, advanced observability, identity-based security | Modern production, high performance |
| **Weave** | Simple setup, encryption | Small clusters |
| **Azure CNI** | Native Azure VNet integration | AKS (recommended) |
| **AWS VPC CNI** | Native AWS VPC IPs | EKS |

---

### 11.3 NetworkPolicy — Pod-Level Firewall

By default, all Pods can communicate with all other Pods in the cluster (and across namespaces). NetworkPolicy restricts this.

> **Important:** NetworkPolicy is only enforced if your CNI plugin supports it (Calico, Cilium, Weave). Flannel does not support NetworkPolicy. Kind uses kindnet which supports it partially.

```yaml
# Deny all ingress traffic to pods in the 'production' namespace by default
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all-ingress
  namespace: production
spec:
  podSelector: {}    # Applies to all pods in namespace
  policyTypes:
    - Ingress
  # No ingress rules = deny all ingress
```

```yaml
# Allow only specific traffic to the API pods
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: api-policy
  namespace: production
spec:
  podSelector:
    matchLabels:
      app: api
  policyTypes:
    - Ingress
    - Egress
  ingress:
    # Allow from frontend pods in same namespace
    - from:
        - podSelector:
            matchLabels:
              app: frontend
      ports:
        - protocol: TCP
          port: 3000
    # Allow from monitoring namespace (Prometheus scraping)
    - from:
        - namespaceSelector:
            matchLabels:
              name: monitoring
      ports:
        - protocol: TCP
          port: 9090
  egress:
    # Allow to database
    - to:
        - podSelector:
            matchLabels:
              app: postgres
      ports:
        - protocol: TCP
          port: 5432
    # Allow DNS resolution
    - to: []
      ports:
        - protocol: UDP
          port: 53
```

---

### 11.4 DNS in Kubernetes — CoreDNS

CoreDNS runs as a deployment in `kube-system` and provides cluster-internal DNS.

**DNS naming format:**
```
<service-name>.<namespace>.svc.cluster.local

Examples:
api-service.default.svc.cluster.local        # Full FQDN
api-service.default                           # From different namespace
api-service                                   # From same namespace (search domain)

For Pods:
10-0-1-5.default.pod.cluster.local          # Pod DNS (rarely used)

For StatefulSets:
web-0.web-service.default.svc.cluster.local  # Specific StatefulSet pod
```

```bash
# Test DNS from inside a pod
kubectl run dns-test --image=busybox:1.36 --rm -it -- sh
# Inside:
nslookup kubernetes
nslookup kubernetes.default.svc.cluster.local
nslookup api-service.default.svc.cluster.local
cat /etc/resolv.conf    # Shows search domains
```

---

---

## Lesson 12 — Persistent Volumes and Storage

> **Level:** DevOps Engineer
> **Goal:** Provide durable storage for stateful applications

---

### 12.1 The Kubernetes Storage Architecture

```
ADMIN creates/configures:
  StorageClass         ← Defines HOW storage is provisioned (which cloud, what type)
  PersistentVolume     ← Represents actual storage (static provisioning)

DEVELOPER requests:
  PersistentVolumeClaim ← "I need 10Gi of SSD storage"

KUBERNETES binds:
  PVC ←──── bound ────→ PV   ← Automatic matching (or dynamic provisioning)

POD uses:
  volumes:
    - persistentVolumeClaim:
        claimName: my-pvc
```

---

### 12.2 StorageClasses

StorageClasses enable dynamic provisioning — Kubernetes automatically creates the underlying storage when a PVC is created.

```yaml
# Azure Managed Disk StorageClass (default on AKS)
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: managed-premium
  annotations:
    storageclass.kubernetes.io/is-default-class: "true"
provisioner: disk.csi.azure.com
parameters:
  skuName: Premium_LRS      # Managed disk type
reclaimPolicy: Delete       # Delete PV when PVC is deleted (or Retain)
volumeBindingMode: WaitForFirstConsumer  # Only provision when pod is scheduled
allowVolumeExpansion: true  # Allow resizing PVCs
```

```bash
# View available storage classes
kubectl get storageclass
kubectl describe storageclass managed-premium

# Set default storage class
kubectl patch storageclass managed-premium \
  -p '{"metadata": {"annotations": {"storageclass.kubernetes.io/is-default-class": "true"}}}'
```

---

### 12.3 PersistentVolumeClaims

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: postgres-data
  namespace: production
spec:
  accessModes:
    - ReadWriteOnce      # Only one node can mount read-write
    # ReadOnlyMany       # Multiple nodes read-only
    # ReadWriteMany      # Multiple nodes read-write (NFS, Azure Files)
  resources:
    requests:
      storage: 50Gi
  storageClassName: managed-premium  # Which StorageClass to use
  volumeMode: Filesystem   # Filesystem or Block
```

```bash
# View PVCs
kubectl get pvc
kubectl describe pvc postgres-data

# PVC states:
# Pending   → waiting to be bound to a PV (or dynamic provisioning in progress)
# Bound     → successfully bound to a PV
# Lost      → bound PV is no longer available (data may be lost)

# View PVs
kubectl get pv
kubectl describe pv <pv-name>
```

---

### 12.4 Using PVCs in Pods and StatefulSets

```yaml
# Pod using a PVC
apiVersion: v1
kind: Pod
metadata:
  name: postgres
spec:
  containers:
    - name: postgres
      image: postgres:15-alpine
      env:
        - name: POSTGRES_PASSWORD
          valueFrom:
            secretKeyRef:
              name: postgres-secret
              key: password
      volumeMounts:
        - name: data
          mountPath: /var/lib/postgresql/data
  volumes:
    - name: data
      persistentVolumeClaim:
        claimName: postgres-data
```

**StatefulSet with VolumeClaimTemplates (recommended for databases):**
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: postgres
spec:
  serviceName: postgres-headless
  replicas: 1
  selector:
    matchLabels:
      app: postgres
  template:
    metadata:
      labels:
        app: postgres
    spec:
      containers:
        - name: postgres
          image: postgres:15-alpine
          env:
            - name: POSTGRES_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: postgres-secret
                  key: password
          volumeMounts:
            - name: data
              mountPath: /var/lib/postgresql/data
  # VolumeClaimTemplates: creates a unique PVC for each pod replica
  volumeClaimTemplates:
    - metadata:
        name: data
      spec:
        accessModes: ["ReadWriteOnce"]
        storageClassName: managed-premium
        resources:
          requests:
            storage: 50Gi
```

---

---

## Lesson 13 — Helm Package Manager

> **Level:** DevOps Engineer
> **Goal:** Deploy and manage complex Kubernetes applications with Helm

---

### 13.1 What is Helm?

Helm is the package manager for Kubernetes. Instead of managing dozens of individual YAML files for a complex application, Helm bundles them into a **chart** — a reusable, configurable package.

**Problems Helm solves:**
- Deploying a complex app (e.g., Prometheus) requires 20+ YAML files — Helm installs it in one command
- Managing different configurations for dev/staging/prod environments
- Versioned, rollbackable releases
- Sharing infrastructure-as-code via a registry (Artifact Hub)

---

### 13.2 Helm Concepts

| Concept | Description |
|---|---|
| **Chart** | Package containing all Kubernetes resource templates |
| **Release** | A deployed instance of a chart |
| **Repository** | Collection of charts (like Docker Hub for Helm) |
| **Values** | Configuration variables that customise a chart |
| **Template** | YAML files with Go templating for dynamic values |

---

### 13.3 Helm CLI — Essential Commands

```bash
# Install Helm
brew install helm     # macOS
# Linux: curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

# Add repositories
helm repo add stable https://charts.helm.sh/stable
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add bitnami https://charts.bitnami.com/bitnami

# Update repos (like apt-get update)
helm repo update

# Search for charts
helm search repo nginx
helm search hub postgresql           # Search Artifact Hub

# Install a chart
helm install my-nginx ingress-nginx/ingress-nginx \
  --namespace ingress-nginx \
  --create-namespace

# Install with custom values
helm install my-postgres bitnami/postgresql \
  --namespace databases \
  --create-namespace \
  --set auth.postgresPassword=mysecretpassword \
  --set primary.persistence.size=50Gi

# Install with values file
helm install my-app ./my-chart --values production-values.yaml

# List releases
helm list
helm list --all-namespaces

# Get release status
helm status my-nginx

# Show values for a release
helm get values my-postgres

# Upgrade a release
helm upgrade my-postgres bitnami/postgresql \
  --set primary.persistence.size=100Gi

# Upgrade and install if not exists (--install flag)
helm upgrade --install my-app ./my-chart --values values.yaml

# Rollback
helm rollback my-postgres 1    # Roll back to release revision 1
helm history my-postgres       # See revision history

# Uninstall
helm uninstall my-nginx -n ingress-nginx

# Dry run (preview without applying)
helm install my-app ./my-chart --dry-run --debug
```

---

### 13.4 Creating Your Own Helm Chart

```bash
# Create chart scaffold
helm create my-app
```

```
my-app/
├── Chart.yaml         ← Chart metadata
├── values.yaml        ← Default values
├── charts/            ← Dependency charts
└── templates/
    ├── deployment.yaml
    ├── service.yaml
    ├── ingress.yaml
    ├── _helpers.tpl   ← Reusable template helpers
    ├── hpa.yaml
    ├── serviceaccount.yaml
    └── NOTES.txt      ← Post-install message
```

**Chart.yaml:**
```yaml
apiVersion: v2
name: my-app
description: My Application Helm Chart
type: application
version: 1.2.0          # Chart version
appVersion: "2.0.0"     # App version being deployed
```

**values.yaml:**
```yaml
replicaCount: 3

image:
  repository: mycompany/api
  tag: "v2.0.0"
  pullPolicy: IfNotPresent

service:
  type: ClusterIP
  port: 80
  targetPort: 3000

ingress:
  enabled: true
  className: nginx
  host: api.myapp.com

resources:
  requests:
    memory: 128Mi
    cpu: 100m
  limits:
    memory: 256Mi
    cpu: 500m

autoscaling:
  enabled: true
  minReplicas: 2
  maxReplicas: 20
  targetCPUUtilizationPercentage: 70

config:
  logLevel: info
  databaseHost: postgres-service

secrets:
  dbPassword: ""    # Set via --set or values file, never commit
```

**templates/deployment.yaml:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ include "my-app.fullname" . }}
  labels:
    {{- include "my-app.labels" . | nindent 4 }}
spec:
  replicas: {{ .Values.replicaCount }}
  selector:
    matchLabels:
      {{- include "my-app.selectorLabels" . | nindent 6 }}
  template:
    metadata:
      labels:
        {{- include "my-app.selectorLabels" . | nindent 8 }}
    spec:
      containers:
        - name: {{ .Chart.Name }}
          image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
          imagePullPolicy: {{ .Values.image.pullPolicy }}
          ports:
            - containerPort: {{ .Values.service.targetPort }}
          resources:
            {{- toYaml .Values.resources | nindent 12 }}
          env:
            - name: LOG_LEVEL
              value: {{ .Values.config.logLevel | quote }}
            - name: DB_HOST
              value: {{ .Values.config.databaseHost | quote }}
            {{- if .Values.secrets.dbPassword }}
            - name: DB_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: {{ include "my-app.fullname" . }}-secrets
                  key: dbPassword
            {{- end }}
```

---

---

## Lesson 14 — Kubernetes RBAC

> **Level:** DevOps Engineer
> **Goal:** Implement least-privilege access control

---

### 14.1 RBAC Architecture

RBAC (Role-Based Access Control) controls who can do what to which Kubernetes resources.

```
SUBJECT (who)    +   ROLE (what)    +   ROLEBINDING (connects them)
     │                    │                      │
     ▼                    ▼                      ▼
User/Group/           Rules:               Grants the Role
ServiceAccount    - apiGroups              to the Subject
                  - resources              in a Namespace
                  - verbs                  (or cluster-wide)
```

**Resource scope:**

| Resource | Scope | Example |
|---|---|---|
| **Role** | Namespace | Permissions within one namespace |
| **ClusterRole** | Cluster | Permissions across all namespaces or non-namespaced resources |
| **RoleBinding** | Namespace | Grants Role or ClusterRole to subject in one namespace |
| **ClusterRoleBinding** | Cluster | Grants ClusterRole to subject cluster-wide |

---

### 14.2 Roles and ClusterRoles

```yaml
# Role — namespace-scoped permissions
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: developer-role
  namespace: production
rules:
  # Allow getting, listing, watching pods and their logs
  - apiGroups: [""]              # "" = core API group
    resources: ["pods", "pods/log", "pods/exec"]
    verbs: ["get", "list", "watch", "create"]

  # Allow managing deployments
  - apiGroups: ["apps"]
    resources: ["deployments", "replicasets"]
    verbs: ["get", "list", "watch", "create", "update", "patch"]

  # Allow reading configmaps (not secrets)
  - apiGroups: [""]
    resources: ["configmaps"]
    verbs: ["get", "list"]
```

```yaml
# ClusterRole — cluster-wide permissions
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: monitoring-reader
rules:
  # Read pods across all namespaces (Prometheus needs this)
  - apiGroups: [""]
    resources: ["pods", "nodes", "services", "endpoints"]
    verbs: ["get", "list", "watch"]
  - apiGroups: ["apps"]
    resources: ["deployments", "daemonsets", "statefulsets", "replicasets"]
    verbs: ["get", "list", "watch"]
  # Non-resource URLs (Prometheus metrics endpoint)
  - nonResourceURLs: ["/metrics", "/healthz"]
    verbs: ["get"]
```

---

### 14.3 RoleBindings

```yaml
# Bind developer-role to a specific user
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: developer-binding
  namespace: production
subjects:
  - kind: User
    name: john.doe@company.com    # Matches the CN in the user's certificate
    apiGroup: rbac.authorization.k8s.io
  - kind: Group
    name: backend-developers
    apiGroup: rbac.authorization.k8s.io
  - kind: ServiceAccount
    name: ci-cd-deployer
    namespace: ci-cd
roleRef:
  kind: Role
  name: developer-role
  apiGroup: rbac.authorization.k8s.io
```

```yaml
# ClusterRoleBinding — give monitoring access cluster-wide
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: prometheus-binding
subjects:
  - kind: ServiceAccount
    name: prometheus
    namespace: monitoring
roleRef:
  kind: ClusterRole
  name: monitoring-reader
  apiGroup: rbac.authorization.k8s.io
```

---

### 14.4 Service Accounts

ServiceAccounts provide identity for Pods (as opposed to human users). Used for pod-to-API-server authentication.

```yaml
# Create a dedicated service account
apiVersion: v1
kind: ServiceAccount
metadata:
  name: api-service-account
  namespace: production
  annotations:
    # Azure Workload Identity annotation (for AKS)
    azure.workload.identity/client-id: "<managed-identity-client-id>"
```

```yaml
# Bind permissions to the service account
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: secret-reader
  namespace: production
rules:
  - apiGroups: [""]
    resources: ["secrets"]
    verbs: ["get"]
    resourceNames: ["db-secret", "api-key"]  # Restrict to specific secret names
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: api-secret-reader
  namespace: production
subjects:
  - kind: ServiceAccount
    name: api-service-account
    namespace: production
roleRef:
  kind: Role
  name: secret-reader
  apiGroup: rbac.authorization.k8s.io
```

```yaml
# Use the service account in a pod
spec:
  serviceAccountName: api-service-account
  automountServiceAccountToken: false   # Don't auto-mount if not needed
```

```bash
# Check RBAC permissions
kubectl auth can-i create deployments --namespace=production
kubectl auth can-i create deployments --namespace=production --as=john.doe@company.com
kubectl auth can-i '*' '*'   # Can the current user do everything?

# View RBAC rules
kubectl get roles,rolebindings -n production
kubectl describe role developer-role -n production
```

---

---

## Lesson 15 — Logging and Monitoring

> **Level:** DevOps Engineer
> **Goal:** Implement production-grade observability for Kubernetes

---

### 15.1 Kubernetes Logging Architecture

**Node-level logging** (default):
```
Container → stdout/stderr → Container Runtime → /var/log/containers/ on node
                                                        ↑
kubectl logs <pod>   ← reads from here via kubelet
```

**Cluster-level logging** (production requirement):
Logs need to survive pod deletion and be searchable across all nodes.

```
Containers → stdout/stderr
                   ↓
          Fluentd/Fluent Bit    ← DaemonSet on every node
          (log shipper)
                   ↓
     Elasticsearch / OpenSearch / CloudWatch / Azure Monitor
                   ↓
     Kibana / OpenSearch Dashboards / Grafana
```

---

### 15.2 kubectl Logging Commands

```bash
# Basic logs
kubectl logs <pod-name>
kubectl logs <pod-name> -c <container-name>    # Multi-container pod
kubectl logs <pod-name> --previous             # Crashed container logs
kubectl logs <pod-name> -f --tail=100          # Follow, last 100 lines

# Logs from all pods matching a selector
kubectl logs -l app=api -f --max-log-requests=10

# Logs with timestamps
kubectl logs <pod-name> --timestamps

# Logs since a specific time
kubectl logs <pod-name> --since=1h
kubectl logs <pod-name> --since-time="2024-01-15T10:00:00Z"
```

---

### 15.3 Prometheus + Grafana Stack

The industry standard for Kubernetes monitoring.

```bash
# Install kube-prometheus-stack via Helm (Prometheus + Grafana + Alertmanager + exporters)
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack \
  --namespace monitoring \
  --create-namespace \
  --set grafana.adminPassword=mygrafanapassword \
  --set prometheus.prometheusSpec.retention=15d \
  --set prometheus.prometheusSpec.storageSpec.volumeClaimTemplate.spec.storageClassName=standard \
  --set prometheus.prometheusSpec.storageSpec.volumeClaimTemplate.spec.resources.requests.storage=50Gi

# Access Grafana dashboard
kubectl port-forward svc/kube-prometheus-stack-grafana 3000:80 -n monitoring
# Open http://localhost:3000 (admin/mygrafanapassword)

# Access Prometheus
kubectl port-forward svc/kube-prometheus-stack-prometheus 9090:9090 -n monitoring
```

**Instrument your application for Prometheus:**
```javascript
// Node.js with prom-client
const client = require('prom-client');
const register = new client.Registry();
client.collectDefaultMetrics({ register });

const httpRequestDuration = new client.Histogram({
  name: 'http_request_duration_seconds',
  help: 'Duration of HTTP requests in seconds',
  labelNames: ['method', 'route', 'status_code'],
  buckets: [0.001, 0.01, 0.1, 0.5, 1, 5],
  registers: [register]
});

app.get('/metrics', async (req, res) => {
  res.set('Content-Type', register.contentType);
  res.end(await register.metrics());
});
```

**ServiceMonitor — tell Prometheus to scrape your app:**
```yaml
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: api-metrics
  namespace: monitoring
  labels:
    release: kube-prometheus-stack
spec:
  selector:
    matchLabels:
      app: api
  namespaceSelector:
    matchNames:
      - production
  endpoints:
    - port: http
      path: /metrics
      interval: 30s
```

---

### 15.4 Alerts with Alertmanager

```yaml
# PrometheusRule — define alerting rules
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
  name: api-alerts
  namespace: monitoring
  labels:
    release: kube-prometheus-stack
spec:
  groups:
    - name: api.rules
      rules:
        # Alert if pod restart rate is high
        - alert: PodCrashLooping
          expr: increase(kube_pod_container_status_restarts_total[15m]) > 3
          for: 5m
          labels:
            severity: critical
          annotations:
            summary: "Pod {{ $labels.pod }} is crash looping"
            description: "Pod {{ $labels.pod }} has restarted {{ $value }} times in 15 minutes"

        # Alert if any deployment has 0 available replicas
        - alert: DeploymentUnavailable
          expr: kube_deployment_status_replicas_available == 0
          for: 2m
          labels:
            severity: critical
          annotations:
            summary: "Deployment {{ $labels.deployment }} has 0 available replicas"

        # Alert if CPU request utilization is very high
        - alert: HighCPUUtilization
          expr: |
            (sum(rate(container_cpu_usage_seconds_total[5m])) by (pod) /
            sum(kube_pod_container_resource_requests{resource="cpu"}) by (pod)) > 0.9
          for: 10m
          labels:
            severity: warning
          annotations:
            summary: "Pod {{ $labels.pod }} CPU utilization > 90%"
```

---

---

# PHASE 4 — ADVANCED ARCHITECTURE

---

## Lesson 16 — High Availability Clusters

> **Level:** Advanced
> **Goal:** Design and operate production HA Kubernetes clusters

---

### 16.1 HA Control Plane Architecture

```
                    ┌─────────────────────────────────┐
External Traffic    │  Load Balancer (HAProxy/Cloud LB) │
                    │  Endpoint: k8s-api.mycompany.com  │
                    └─────┬──────────┬──────────┬──────┘
                          │          │          │
                    ┌─────▼─┐  ┌─────▼─┐  ┌─────▼─┐
                    │Control│  │Control│  │Control│
                    │Plane 1│  │Plane 2│  │Plane 3│
                    │       │  │       │  │       │
                    │etcd   │  │etcd   │  │etcd   │  ← Raft consensus
                    │api-   │  │api-   │  │api-   │
                    │server │  │server │  │server │
                    │sched  │  │sched  │  │sched  │  ← Leader-elected
                    │ctrl-mg│  │ctrl-mg│  │ctrl-mg│  ← Leader-elected
                    └───────┘  └───────┘  └───────┘
                    ┌──────────────────────────────────┐
                    │           Worker Nodes            │
                    │  [Node1]   [Node2]   [Node3]     │
                    └──────────────────────────────────┘
```

**HA Requirements:**
- **Odd number of control plane nodes** (3, 5, or 7) — etcd requires majority quorum. 3 nodes tolerate 1 failure. 5 nodes tolerate 2 failures.
- **Load balancer in front of API servers** — clients (kubectl, kubelets) connect to the LB, not individual API servers
- **etcd:** Each control plane node runs one etcd member. All must form a healthy cluster.
- **Scheduler and Controller Manager:** Run on all control plane nodes but elect a leader — only the leader is active, others are standby

---

### 16.2 AKS High Availability Setup

```bash
# Create HA AKS cluster with availability zones
az aks create \
  --resource-group myapp-rg \
  --name myapp-aks \
  --node-count 3 \
  --node-vm-size Standard_D4s_v5 \
  --zones 1 2 3 \                  # Spread nodes across all 3 AZs
  --enable-cluster-autoscaler \    # Auto-scale node pool
  --min-count 3 \
  --max-count 10 \
  --network-plugin azure \         # Azure CNI — pods get real VNet IPs
  --network-policy calico \        # Enable NetworkPolicy
  --enable-managed-identity \
  --generate-ssh-keys \
  --uptime-sla                     # Paid tier with SLA for control plane

# Add a separate system node pool (run only system pods)
az aks nodepool add \
  --resource-group myapp-rg \
  --cluster-name myapp-aks \
  --name systempool \
  --node-count 3 \
  --node-vm-size Standard_D2s_v5 \
  --zones 1 2 3 \
  --mode System \
  --node-taints CriticalAddonsOnly=true:NoSchedule

# Add a user node pool for application workloads
az aks nodepool add \
  --resource-group myapp-rg \
  --cluster-name myapp-aks \
  --name apppool \
  --node-count 3 \
  --node-vm-size Standard_D8s_v5 \
  --zones 1 2 3 \
  --enable-cluster-autoscaler \
  --min-count 3 \
  --max-count 20 \
  --mode User
```

---

### 16.3 Node Affinity and Anti-Affinity

Spread pods across zones/nodes for HA:

```yaml
spec:
  # Pod Topology Spread Constraints (preferred way)
  topologySpreadConstraints:
    - maxSkew: 1                      # Max difference in pod count between zones
      topologyKey: topology.kubernetes.io/zone
      whenUnsatisfiable: DoNotSchedule
      labelSelector:
        matchLabels:
          app: api
    - maxSkew: 1
      topologyKey: kubernetes.io/hostname
      whenUnsatisfiable: DoNotSchedule
      labelSelector:
        matchLabels:
          app: api

  # OR: Pod Anti-Affinity (older approach)
  affinity:
    podAntiAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        - labelSelector:
            matchLabels:
              app: api
          topologyKey: kubernetes.io/hostname   # No two replicas on same node
      preferredDuringSchedulingIgnoredDuringExecution:
        - weight: 100
          podAffinityTerm:
            labelSelector:
              matchLabels:
                app: api
            topologyKey: topology.kubernetes.io/zone  # Prefer different zones
```

---

### 16.4 Taints and Tolerations

Taints repel pods from nodes. Tolerations allow pods to be scheduled on tainted nodes.

```bash
# Taint a node (only GPU workloads should run here)
kubectl taint node gpu-node-1 dedicated=gpu:NoSchedule
kubectl taint node gpu-node-1 dedicated=gpu:NoExecute    # Also evict existing pods

# Remove taint
kubectl taint node gpu-node-1 dedicated=gpu:NoSchedule-
```

```yaml
# Pod that tolerates the GPU taint (and requires it)
spec:
  tolerations:
    - key: "dedicated"
      operator: "Equal"
      value: "gpu"
      effect: "NoSchedule"
  nodeSelector:
    accelerator: nvidia-tesla-v100
```


---

---

## Lesson 17 — Kubernetes Security Best Practices

> **Level:** Advanced
> **Goal:** Harden Kubernetes clusters and workloads

---

### 17.1 The 4C Security Model

```
Cloud (infrastructure security)
  └── Cluster (Kubernetes security)
        └── Container (image security)
              └── Code (application security)
```

Each layer provides independent defence. No single layer is sufficient.

---

### 17.2 Pod Security — SecurityContext

```yaml
spec:
  # Pod-level security context
  securityContext:
    runAsNonRoot: true           # Fail if container tries to run as root
    runAsUser: 1000              # Run as this UID
    runAsGroup: 3000
    fsGroup: 2000                # Volume files owned by this GID
    seccompProfile:
      type: RuntimeDefault       # Apply default seccomp profile

  containers:
    - name: api
      # Container-level security context (overrides pod-level)
      securityContext:
        allowPrivilegeEscalation: false    # Cannot gain more privileges than parent
        readOnlyRootFilesystem: true       # Immutable filesystem
        runAsNonRoot: true
        capabilities:
          drop:
            - ALL                # Drop ALL Linux capabilities
          add:
            - NET_BIND_SERVICE   # Re-add only what's needed (bind to port < 1024)

      # If readOnlyRootFilesystem, add tmpfs for writable directories
      volumeMounts:
        - name: tmp
          mountPath: /tmp
        - name: varrun
          mountPath: /var/run

  volumes:
    - name: tmp
      emptyDir: {}
    - name: varrun
      emptyDir: {}
```

---

### 17.3 Pod Security Admission (PSA)

Kubernetes 1.25+ built-in admission controller that enforces Pod Security Standards.

**Three levels:**
- `privileged` — no restrictions
- `baseline` — prevents known privilege escalation
- `restricted` — heavily restricted, best practices required

```yaml
# Label a namespace to enforce security standards
apiVersion: v1
kind: Namespace
metadata:
  name: production
  labels:
    pod-security.kubernetes.io/enforce: restricted     # Enforce restricted
    pod-security.kubernetes.io/audit: restricted       # Audit but allow restricted
    pod-security.kubernetes.io/warn: restricted        # Warn but allow restricted
```

```bash
# Check if a workload would be admitted
kubectl label namespace test pod-security.kubernetes.io/enforce=restricted
kubectl apply -f deployment.yaml -n test
# Will reject if deployment doesn't meet restricted requirements
```

---

### 17.4 Secrets Encryption at Rest

By default, Kubernetes Secrets are base64-encoded in etcd — not encrypted. Enable encryption:

```yaml
# /etc/kubernetes/encryption-config.yaml (on control plane nodes)
apiVersion: apiserver.config.k8s.io/v1
kind: EncryptionConfiguration
resources:
  - resources:
      - secrets
      - configmaps
    providers:
      - aescbc:
          keys:
            - name: key1
              secret: <base64-encoded-32-byte-key>
      - identity: {}    # Fallback: unencrypted (for reading old data)
```

```bash
# Start kube-apiserver with encryption config
--encryption-provider-config=/etc/kubernetes/encryption-config.yaml

# Re-encrypt all existing secrets after enabling
kubectl get secrets --all-namespaces -o json | kubectl replace -f -
```

**External Secrets Operator (recommended for production):**
```yaml
# Sync secrets from Azure Key Vault into Kubernetes Secrets
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: db-credentials
  namespace: production
spec:
  refreshInterval: 1h
  secretStoreRef:
    name: azure-keyvault-store
    kind: ClusterSecretStore
  target:
    name: db-secret
    creationPolicy: Owner
  data:
    - secretKey: password
      remoteRef:
        key: database-password    # Key Vault secret name
```

---

### 17.5 Image Security

```yaml
# 1. Image pull policy — always re-check registry for :latest
spec:
  containers:
    - name: api
      image: myapp:v2.1.0         # Always use specific tags in production
      imagePullPolicy: IfNotPresent

# 2. Restrict registries with OPA/Kyverno policy
# Kyverno policy — block images from Docker Hub
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: restrict-image-registries
spec:
  validationFailureAction: Enforce
  rules:
    - name: validate-registries
      match:
        any:
          - resources:
              kinds: [Pod]
      validate:
        message: "Only images from approved registries are allowed"
        pattern:
          spec:
            containers:
              - image: "mycompany.azurecr.io/* | gcr.io/myproject/*"
```

```bash
# Scan images for vulnerabilities (in CI/CD pipeline)
trivy image mycompany.azurecr.io/myapp:v2.1.0 --severity HIGH,CRITICAL --exit-code 1

# Scan running cluster images
kubectl get pods -A -o jsonpath='{range .items[*]}{.spec.containers[*].image}{"\n"}{end}' | sort -u | \
  xargs -I{} trivy image {} --severity CRITICAL
```

---

---

## Lesson 18 — Service Mesh with Istio

> **Level:** Advanced
> **Goal:** Implement advanced traffic management, observability, and mTLS

---

### 18.1 Why Service Mesh?

As microservices grow, you face common challenges that belong to infrastructure, not application code:
- mTLS between every service pair (zero-trust networking)
- Traffic splitting for canary deployments (10% to v2, 90% to v1)
- Circuit breaking (stop calling a failing service)
- Retries with backoff
- Distributed tracing (track a request across 10 services)
- Rate limiting

A service mesh (Istio, Linkerd) handles all of this by injecting a sidecar proxy into every Pod, transparently intercepting all network traffic.

---

### 18.2 Istio Architecture

```
Pods (after sidecar injection):
  [App Container] [Envoy Proxy]   ← Sidecar proxy handles all network traffic

Control Plane (istiod):
  - Pilot: service discovery, traffic management
  - Citadel: certificate management, mTLS
  - Galley: configuration validation
```

```bash
# Install Istio
curl -L https://istio.io/downloadIstio | sh -
cd istio-1.*/
export PATH=$PWD/bin:$PATH
istioctl install --set profile=demo -y

# Enable sidecar injection for a namespace
kubectl label namespace production istio-injection=enabled

# Verify injection (pods now have 2/2 containers)
kubectl get pods -n production
# NAME          READY   STATUS    RESTARTS
# api-xxx       2/2     Running   0       ← app + envoy sidecar
```

---

### 18.3 Traffic Management

**VirtualService — Define traffic routing rules:**
```yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: api-vsvc
spec:
  hosts:
    - api-service
  http:
    # Canary deployment: 90% to v1, 10% to v2
    - route:
        - destination:
            host: api-service
            subset: v1
          weight: 90
        - destination:
            host: api-service
            subset: v2
          weight: 10

    # Retry policy
    - route:
        - destination:
            host: api-service
      retries:
        attempts: 3
        perTryTimeout: 2s
        retryOn: "5xx,connect-failure,reset"

    # Circuit breaker timeout
      timeout: 5s

    # Fault injection (for chaos testing)
    fault:
      delay:
        percentage:
          value: 10     # Inject 5s delay in 10% of requests
        fixedDelay: 5s
```

**DestinationRule — Define subsets (versions):**
```yaml
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: api-dr
spec:
  host: api-service
  trafficPolicy:
    connectionPool:
      tcp:
        maxConnections: 100
      http:
        h2UpgradePolicy: UPGRADE
    outlierDetection:            # Circuit breaker
      consecutiveGatewayErrors: 5
      interval: 30s
      baseEjectionTime: 30s
      maxEjectionPercent: 50
  subsets:
    - name: v1
      labels:
        version: v1
    - name: v2
      labels:
        version: v2
```

---

---

## Lesson 19 — Multi-Environment Deployments

> **Level:** Advanced
> **Goal:** Deploy consistently across dev, staging, and production

---

### 19.1 GitOps with ArgoCD

GitOps is the practice of using Git as the single source of truth for both application code and infrastructure. ArgoCD continuously reconciles the cluster state with what's in Git.

```bash
# Install ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Get initial admin password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

# Port-forward to UI
kubectl port-forward svc/argocd-server -n argocd 8080:443
# Login at https://localhost:8080 (admin/<password>)

# Install ArgoCD CLI
brew install argocd
argocd login localhost:8080

# Register a cluster
argocd cluster add <context-name>
```

**Application definition:**
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: myapp-production
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/myorg/k8s-configs.git
    targetRevision: main
    path: environments/production      # Directory in repo
    helm:
      valueFiles:
        - values.yaml
        - production-values.yaml
  destination:
    server: https://kubernetes.default.svc
    namespace: production
  syncPolicy:
    automated:
      prune: true       # Delete resources removed from Git
      selfHeal: true    # Revert manual cluster changes
    syncOptions:
      - CreateNamespace=true
```

---

### 19.2 Kustomize — Environment-Specific Overlays

Kustomize is built into kubectl. It allows environment-specific patches on top of a base configuration.

```
k8s-configs/
├── base/
│   ├── deployment.yaml    ← Base deployment (3 replicas, B2s VM)
│   ├── service.yaml
│   └── kustomization.yaml
└── overlays/
    ├── dev/
    │   ├── kustomization.yaml    ← Patches: 1 replica
    │   └── replica-patch.yaml
    ├── staging/
    │   ├── kustomization.yaml    ← Patches: 2 replicas
    │   └── replica-patch.yaml
    └── production/
        ├── kustomization.yaml    ← Patches: 5 replicas, HPA
        ├── replica-patch.yaml
        └── hpa.yaml
```

**base/kustomization.yaml:**
```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
resources:
  - deployment.yaml
  - service.yaml
```

**overlays/production/kustomization.yaml:**
```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
bases:
  - ../../base
namePrefix: prod-
commonLabels:
  environment: production
patches:
  - path: replica-patch.yaml
  - path: resource-patch.yaml
resources:
  - hpa.yaml
images:
  - name: mycompany/api
    newTag: v2.1.0
```

**overlays/production/replica-patch.yaml:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api-deployment
spec:
  replicas: 5
```

```bash
# Apply production overlay
kubectl apply -k overlays/production/

# Preview what will be applied
kubectl kustomize overlays/production/

# Used in ArgoCD source config
source:
  repoURL: https://github.com/myorg/k8s-configs.git
  path: overlays/production
  directory:
    recurse: true
```

---

---

## Lesson 20 — Cluster Upgrades and Maintenance

> **Level:** Advanced

---

### 20.1 Kubernetes Upgrade Strategy

Kubernetes supports upgrading one minor version at a time (e.g., 1.27 → 1.28, never 1.27 → 1.29 directly).

**Upgrade order:**
1. etcd
2. kube-apiserver
3. kube-controller-manager
4. kube-scheduler
5. Worker nodes (one at a time, drain first)
6. kubectl

**AKS Cluster Upgrade:**
```bash
# Check available upgrade versions
az aks get-upgrades \
  --resource-group myapp-rg \
  --name myapp-aks \
  --output table

# Upgrade control plane only first
az aks upgrade \
  --resource-group myapp-rg \
  --name myapp-aks \
  --kubernetes-version 1.29.0 \
  --control-plane-only

# Then upgrade node pools (one at a time in production)
az aks nodepool upgrade \
  --resource-group myapp-rg \
  --cluster-name myapp-aks \
  --name apppool \
  --kubernetes-version 1.29.0 \
  --no-wait    # Non-blocking
```

---

### 20.2 Node Maintenance — Drain and Uncordon

```bash
# Mark node as unschedulable (no new pods scheduled)
kubectl cordon node-1

# Drain node: evict all pods (respecting PDBs)
kubectl drain node-1 \
  --ignore-daemonsets \          # Don't evict DaemonSet pods (expected on every node)
  --delete-emptydir-data \       # Delete pods using emptyDir volumes
  --grace-period=300 \           # Allow 5 minutes for graceful shutdown
  --timeout=600s                 # Total timeout

# Perform maintenance (OS update, hardware replacement, etc.)

# Re-enable node for scheduling
kubectl uncordon node-1

# Check node status
kubectl get node node-1
kubectl describe node node-1 | grep -A 5 Conditions:
```

---

---

# PHASE 5 — EXPERT LEVEL

---

## Lesson 21 — Kubernetes Internals

> **Level:** Expert

---

### 21.1 The Controller Pattern

Every Kubernetes controller follows the same reconciliation loop:

```go
// Pseudocode for any Kubernetes controller
for {
    desired := readFromEtcd()      // What SHOULD exist (your YAML)
    actual := observeRealWorld()   // What ACTUALLY exists
    
    if desired != actual {
        reconcile(desired, actual)  // Make actual match desired
    }
    
    wait(resyncPeriod)             // Wait, then loop again
}
```

This loop runs continuously. If someone manually deletes a pod, the ReplicaSet controller sees the discrepancy on the next loop and creates a replacement. If you change a Deployment's image, the Deployment controller sees the difference and orchestrates a rolling update.

---

### 21.2 Watch Mechanism — How Controllers Get Notified

Controllers don't poll etcd every second. They use Kubernetes **watch** mechanism:

```bash
# See the watch mechanism in action
kubectl get pods --watch -v=7   # Verbose flag shows HTTP calls

# The output will show:
# GET /api/v1/namespaces/default/pods?watch=true&resourceVersion=12345
# The server sends events as they happen (HTTP streaming)
```

**Informers and WorkQueues:**
```
etcd emits event (Pod created/updated/deleted)
           │
     kube-apiserver broadcasts to all watchers
           │
     Controller's Informer receives event
           │
     Event added to WorkQueue
           │
     Worker goroutine picks up from WorkQueue
           │
     Reconcile function called
```

---

### 21.3 How kubectl Apply Works — Server-Side Apply

```bash
# Show what happens during kubectl apply
kubectl apply -f deployment.yaml --dry-run=server -v=8

# The HTTP interaction:
# 1. kubectl reads local YAML
# 2. kubectl sends PATCH to /apis/apps/v1/namespaces/default/deployments/my-deployment
# 3. API server runs admission controllers
# 4. API server persists to etcd
# 5. All controllers watching deployments get notified
# 6. kubectl displays result
```

**Server-Side Apply (SSA) — the modern approach:**
```bash
kubectl apply -f deployment.yaml --server-side
# Kubernetes tracks field ownership — multiple controllers can manage different fields
```

---

### 21.4 Client-Go — The Kubernetes Client Library

Understanding client-go helps you build Kubernetes operators and controllers:

```go
package main

import (
    "context"
    "fmt"
    metav1 "k8s.io/apimachinery/pkg/apis/meta/v1"
    "k8s.io/client-go/kubernetes"
    "k8s.io/client-go/tools/clientcmd"
)

func main() {
    // Load kubeconfig
    config, _ := clientcmd.BuildConfigFromFlags("", "/home/user/.kube/config")
    clientset, _ := kubernetes.NewForConfig(config)

    // List pods
    pods, _ := clientset.CoreV1().Pods("default").List(context.TODO(), metav1.ListOptions{})
    for _, pod := range pods.Items {
        fmt.Printf("Pod: %s, Status: %s\n", pod.Name, pod.Status.Phase)
    }

    // Watch pods
    watcher, _ := clientset.CoreV1().Pods("default").Watch(context.TODO(), metav1.ListOptions{})
    for event := range watcher.ResultChan() {
        fmt.Printf("Event: %s\n", event.Type)
    }
}
```

---

---

## Lesson 22 — etcd Architecture and Operations

> **Level:** Expert

---

### 22.1 etcd Deep Dive

etcd is a distributed key-value store using the **Raft consensus algorithm**. It guarantees:
- **Strong consistency:** All reads return the latest write (linearisability)
- **High availability:** Tolerates (N-1)/2 node failures (3 nodes = tolerate 1 failure)
- **Durability:** Writes are persisted to disk before acknowledging

**Raft Leader Election:**
```
All nodes start as followers
       │
One node becomes candidate (election timeout)
       │
Candidate requests votes from peers
       │
If majority vote received → becomes leader
       │
Leader handles all writes and heartbeats
       │
If leader fails → new election
```

---

### 22.2 etcd Backup and Restore — Critical Production Operation

```bash
# Backup etcd (run on control plane node)
ETCDCTL_API=3 etcdctl snapshot save /backup/etcd-snapshot-$(date +%Y%m%d%H%M%S).db \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key

# Verify backup integrity
ETCDCTL_API=3 etcdctl snapshot status /backup/etcd-snapshot.db -w table

# Restore etcd from backup (DISASTER RECOVERY)
# 1. Stop kube-apiserver
systemctl stop kube-apiserver

# 2. Restore snapshot
ETCDCTL_API=3 etcdctl snapshot restore /backup/etcd-snapshot.db \
  --data-dir=/var/lib/etcd-restored \
  --name=etcd-node-1 \
  --initial-cluster=etcd-node-1=https://192.168.1.1:2380 \
  --initial-cluster-token=etcd-cluster-restored \
  --initial-advertise-peer-urls=https://192.168.1.1:2380

# 3. Update etcd config to use new data dir
# 4. Restart etcd
# 5. Restart kube-apiserver

# Automate backup with CronJob
apiVersion: batch/v1
kind: CronJob
metadata:
  name: etcd-backup
  namespace: kube-system
spec:
  schedule: "0 2 * * *"    # Daily at 2am
  jobTemplate:
    spec:
      template:
        spec:
          hostNetwork: true    # Access etcd on host network
          hostPID: true
          containers:
            - name: backup
              image: bitnami/etcd:latest
              command:
                - /bin/sh
                - -c
                - |
                  ETCDCTL_API=3 etcdctl snapshot save /backup/etcd-$(date +%Y%m%d).db \
                    --endpoints=https://127.0.0.1:2379 \
                    --cacert=/etc/kubernetes/pki/etcd/ca.crt \
                    --cert=/etc/kubernetes/pki/etcd/server.crt \
                    --key=/etc/kubernetes/pki/etcd/server.key
```

---

---

## Lesson 23 — Scheduler Internals and Custom Scheduling

> **Level:** Expert

---

### 23.1 How the Scheduler Works

```
New Pod (no nodeName) created in etcd
           │
     kube-scheduler watches for unscheduled pods
           │
           ▼
     FILTERING PHASE (Predicates)
     For each node, apply ALL filter plugins:
     - NodeResourcesFit: node has enough CPU/memory?
     - NodeAffinity: does node match affinity rules?
     - TaintToleration: does pod tolerate node taints?
     - PodTopologySpread: spread constraint satisfied?
     - VolumeBinding: can PVCs be bound on this node?
     → Result: list of feasible nodes
           │
           ▼
     SCORING PHASE (Priorities)
     For each feasible node, score with ALL scorer plugins:
     - NodeResourcesBalancedAllocation: prefer balanced utilisation
     - ImageLocality: prefer nodes that already have the image
     - InterPodAffinity: score based on pod affinity preferences
     → Result: node with highest score wins
           │
           ▼
     BINDING PHASE
     scheduler writes nodeName to Pod spec in etcd
     kubelet on selected node sees the Pod → runs it
```

---

### 23.2 Custom Scheduler Configuration

```yaml
# KubeSchedulerConfiguration
apiVersion: kubescheduler.config.k8s.io/v1
kind: KubeSchedulerConfiguration
profiles:
  - schedulerName: default-scheduler
    plugins:
      score:
        enabled:
          - name: NodeResourcesBalancedAllocation
            weight: 2
          - name: ImageLocality
            weight: 1
        disabled:
          - name: NodeResourcesMostAllocated   # Pack nodes tightly (not default)
    pluginConfig:
      - name: NodeResourcesBalancedAllocation
        args:
          resources:
            - name: cpu
              weight: 1
            - name: memory
              weight: 1
```

---

### 23.3 Scheduling Techniques

```yaml
# 1. Node Selector — simplest, label-based
spec:
  nodeSelector:
    disktype: ssd
    kubernetes.io/arch: amd64

# 2. Node Affinity — more expressive
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
          - matchExpressions:
              - key: topology.kubernetes.io/zone
                operator: In
                values: ["centralindia-1", "centralindia-2"]
              - key: node.kubernetes.io/instance-type
                operator: In
                values: ["Standard_D4s_v5", "Standard_D8s_v5"]
      preferredDuringSchedulingIgnoredDuringExecution:
        - weight: 50
          preference:
            matchExpressions:
              - key: disktype
                operator: In
                values: ["ssd"]

# 3. Schedule on specific node by name
spec:
  nodeName: worker-node-1   # Bypass scheduler entirely
```

---

---

## Lesson 24 — Debugging Cluster Failures

> **Level:** Expert

---

### 24.1 The Debug Toolkit

```bash
# ─── CLUSTER HEALTH ──────────────────────────────────────────────────
kubectl get nodes
kubectl get nodes -o wide
kubectl describe node <n>    # Check Conditions, allocated resources, events

# ─── COMPONENT HEALTH ────────────────────────────────────────────────
kubectl get pods -n kube-system
kubectl logs kube-apiserver-<node> -n kube-system
kubectl logs kube-scheduler-<node> -n kube-system
kubectl logs kube-controller-manager-<node> -n kube-system

# ─── EVENTS ──────────────────────────────────────────────────────────
kubectl get events -A --sort-by='.lastTimestamp' | tail -30
kubectl get events -n production --field-selector type=Warning

# ─── NODE ISSUES ─────────────────────────────────────────────────────
# SSH to node, check system
ssh user@node-ip
systemctl status kubelet
journalctl -u kubelet -n 100 --no-pager
df -h        # Disk pressure?
free -h      # Memory pressure?
top          # CPU?

# ─── NETWORK DEBUGGING ───────────────────────────────────────────────
# Run a debug pod with network tools
kubectl run netdebug --image=nicolaka/netshoot --rm -it -- bash
# Inside: ping, nslookup, curl, traceroute, tcpdump

# Check DNS
kubectl run dnstest --image=busybox --rm -it -- nslookup kubernetes

# Check CoreDNS
kubectl logs -n kube-system -l k8s-app=kube-dns
kubectl get configmap coredns -n kube-system -o yaml
```

---

### 24.2 Common Production Failure Scenarios

**Scenario 1 — Node NotReady:**
```bash
kubectl get nodes
# node-1   NotReady   <none>   5m

kubectl describe node node-1
# Look for: "kubelet stopped posting node status"
# Conditions: MemoryPressure, DiskPressure, PIDPressure, Ready=False

# SSH to node
systemctl status kubelet
journalctl -u kubelet -f
# Common causes: disk full, out of memory, kubelet crashed, network to apiserver lost

# Fix disk pressure
df -h
# If /var/lib/docker is full:
docker system prune -a   # Clear unused images
# Or clear old logs:
find /var/log -name "*.gz" -delete
```

**Scenario 2 — Pods stuck in Terminating:**
```bash
kubectl get pods
# NAME    READY   STATUS        RESTARTS   AGE
# api-1   1/1     Terminating   0          2d    ← Stuck!

# Force delete (use sparingly — only if graceful delete is hung)
kubectl delete pod api-1 --grace-period=0 --force

# Check for finalizers blocking deletion
kubectl get pod api-1 -o jsonpath='{.metadata.finalizers}'
# If finalizer exists, remove it:
kubectl patch pod api-1 -p '{"metadata":{"finalizers":null}}'
```

**Scenario 3 — Service not reaching pods:**
```bash
# 1. Check Service selector matches Pod labels
kubectl describe service api-service    # Look at Selector
kubectl get pods -l app=api             # Do pods match selector?

# 2. Check Endpoints
kubectl get endpoints api-service       # Should show pod IPs
# If empty: selector doesn't match, or no pods are ready

# 3. Check readiness
kubectl get pods                        # READY column: 0/1 means not ready
kubectl describe pod api-pod | grep -A 5 Readiness

# 4. Check NetworkPolicy
kubectl get networkpolicy -n production
# Does any policy block traffic to your pods?

# 5. Test connectivity from inside cluster
kubectl run test --image=busybox --rm -it -- wget -qO- http://api-service:80
```

**Scenario 4 — Pending pods:**
```bash
kubectl describe pod pending-pod
# Events:
# Warning  FailedScheduling  No nodes available to schedule pods
#   → Insufficient cpu (requested 4, available 0.5)
#   → No nodes match node affinity

# Check resource requests vs available
kubectl describe nodes | grep -A 5 "Allocated resources"
# If nodes are full: add more nodes, reduce requests, or scale down other workloads

# Check for taints
kubectl describe nodes | grep Taints
```

---

---

## Lesson 25 — Production Performance Optimisation

> **Level:** Expert

---

### 25.1 API Server Optimisation

```yaml
# kube-apiserver flags for high-load clusters
--max-requests-inflight=800         # Max concurrent requests (default 400)
--max-mutating-requests-inflight=400 # Max concurrent write requests
--request-timeout=60s               # Request timeout
--watch-cache-sizes=pods#1000,nodes#500  # Larger watch caches
--etcd-servers=https://etcd1:2379,https://etcd2:2379,https://etcd3:2379
--etcd-compaction-interval=5m       # Compact etcd more frequently
```

---

### 25.2 etcd Performance

```bash
# Check etcd performance
etcdctl check perf

# Monitor etcd latency
etcdctl endpoint status -w table

# Defragment etcd (release disk space from historical revisions)
etcdctl defrag --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key

# Compact etcd (remove old revisions)
REVISION=$(etcdctl endpoint status -w json | jq '.[0].Status.header.revision')
etcdctl compact $REVISION
```

---

### 25.3 Large Cluster Best Practices

```bash
# Limit kubelet log verbosity in production (reduces I/O)
# /var/lib/kubelet/config.yaml
logging:
  verbosity: 2    # Default 4 is very verbose

# Increase QPS from controllers
# kube-controller-manager flags:
--kube-api-qps=100
--kube-api-burst=100

# Horizontal scaling: multiple API servers behind a load balancer
# Each API server is stateless and can be scaled independently

# Node sizing guidelines for large clusters:
# < 100 nodes: single etcd can work
# 100-500 nodes: 3 etcd nodes, monitor carefully
# 500+ nodes: 5 etcd nodes, dedicated etcd hardware, fast SSDs
# 1000+ nodes: consider multiple clusters, cluster federation
```

---

---

## Lesson 26 — Advanced Cluster Security

> **Level:** Expert

---

### 26.1 Audit Logging

Track every action in the cluster:

```yaml
# /etc/kubernetes/audit-policy.yaml
apiVersion: audit.k8s.io/v1
kind: Policy
rules:
  # Never log secrets content (prevent accidental exposure)
  - level: None
    resources:
      - group: ""
        resources: ["secrets"]
        verbs: ["get", "list", "watch"]

  # Log all changes to RBAC resources
  - level: RequestResponse
    resources:
      - group: "rbac.authorization.k8s.io"
        resources: ["roles", "rolebindings", "clusterroles", "clusterrolebindings"]

  # Log pod exec (potential security event)
  - level: RequestResponse
    resources:
      - group: ""
        resources: ["pods/exec", "pods/portforward", "pods/attach"]

  # Log all write operations at metadata level
  - level: Metadata
    verbs: ["create", "update", "patch", "delete"]

  # Don't log read-only operations on common resources
  - level: None
    verbs: ["get", "list", "watch"]
    resources:
      - group: ""
        resources: ["pods", "services", "endpoints"]

  # Default: log metadata for everything else
  - level: Metadata
```

```bash
# kube-apiserver flags for audit
--audit-policy-file=/etc/kubernetes/audit-policy.yaml
--audit-log-path=/var/log/kubernetes/audit.log
--audit-log-maxage=30
--audit-log-maxbackup=10
--audit-log-maxsize=100
```

---

### 26.2 Admission Controllers — Kyverno Policies

```yaml
# Require all deployments to have resource limits
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: require-pod-resources
spec:
  validationFailureAction: Enforce
  rules:
    - name: check-container-resources
      match:
        any:
          - resources:
              kinds: ["Deployment", "StatefulSet", "DaemonSet"]
      validate:
        message: "All containers must have CPU and memory limits and requests"
        pattern:
          spec:
            template:
              spec:
                containers:
                  - resources:
                      limits:
                        memory: "?*"
                        cpu: "?*"
                      requests:
                        memory: "?*"
                        cpu: "?*"

---
# Mutate: automatically add security context to all pods
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: add-security-context
spec:
  rules:
    - name: add-securitycontext
      match:
        any:
          - resources:
              kinds: ["Pod"]
      mutate:
        patchStrategicMerge:
          spec:
            securityContext:
              runAsNonRoot: true
            containers:
              - (name): "*"
                securityContext:
                  allowPrivilegeEscalation: false
                  capabilities:
                    drop: ["ALL"]
```

---

---

## Lesson 27 — DevOps Interview Preparation — Kubernetes Edition

> **Level:** Senior Engineer

---

### 27.1 Core Interview Questions — With Strong Answers

**Q: "Explain the difference between a Deployment and a StatefulSet."**
> A Deployment is for stateless workloads — each pod is interchangeable and can be replaced by a new pod on any node. Deployments provide rolling updates, rollbacks, and scaling for pods that don't need persistent identity. A StatefulSet is for stateful applications where each pod needs a stable, persistent identity — a predictable name (`web-0`, `web-1`, `web-2`), a stable hostname, a persistent volume that stays associated with that specific pod, and ordered, graceful deployment and scaling. I use Deployments for APIs, web servers, and microservices. I use StatefulSets for databases (Postgres, MySQL), distributed systems (Kafka, Zookeeper, Cassandra), and anything that needs to remember which pod is which across restarts.

---

**Q: "What is the difference between a liveness probe and a readiness probe?"**
> Both probes periodically check container health, but they trigger different actions. A readiness probe answers "is this container ready to receive traffic?" If it fails, the container's Pod IP is removed from the Service's endpoints — traffic stops going to it — but the container is NOT restarted. This is used when an app needs time to warm up, or temporarily can't handle traffic (e.g., loading a model, reconnecting to a DB). A liveness probe answers "is this container still alive?" If it fails N consecutive times, the container is restarted. Use it to detect deadlocks or hung states that the application can't recover from internally. Never make the liveness probe check external dependencies like databases — if the DB is down, you don't want all your pods restarting.

---

**Q: "A deployment has 3 pods. One node running 2 of them goes down. Walk me through what happens."**
> When the node becomes unreachable, the kubelet on that node stops sending heartbeats to the API server. After `NodeMonitorGracePeriod` (default 40 seconds), the Node Controller marks the node as `NotReady`. After the pod eviction timeout (default 5 minutes), pods on that node are marked as `Unknown` and then evicted — the Deployment's ReplicaSet controller sees that only 1 replica is running instead of 3, and creates 2 new pods. The scheduler places these on healthy nodes. The 5-minute delay is intentional — to prevent unnecessary rescheduling during brief network partitions. The old pods aren't immediately replaced because the cluster doesn't know if the node is permanently gone or just temporarily unreachable. If you need faster recovery, you can reduce the eviction timeout, but it increases false positives.

---

**Q: "How does Kubernetes service discovery work?"**
> Kubernetes runs CoreDNS as a cluster-internal DNS server. When a Service is created, an A record is automatically created: `<service-name>.<namespace>.svc.cluster.local` → ClusterIP of the Service. Every Pod has `/etc/resolv.conf` configured to search the cluster DNS, so a Pod in the `production` namespace can reach `api-service` by just using that short name — CoreDNS resolves it to the full FQDN. When the Pod's request hits the Service IP, kube-proxy (running on every node using iptables rules) intercepts the traffic and load-balances it to one of the healthy endpoints (Pod IPs) behind the Service. The endpoint list is maintained by the Endpoints controller, which watches Pods and updates the list based on which Pods have passing readiness probes.

---

**Q: "What is a DaemonSet and when would you use it?"**
> A DaemonSet ensures that exactly one Pod runs on every node (or a subset of nodes) in the cluster. When a new node is added, the DaemonSet controller automatically schedules the pod on it. When a node is removed, the pod is garbage collected. Use cases: log collection agents (Fluentd/Fluent Bit — needs to collect logs from each node's filesystem), monitoring agents (node-exporter, Datadog agent — needs to collect node-level metrics), network plugins (kube-proxy itself is a DaemonSet), security agents (Falco — needs to see all activity on each node), storage plugins. The key insight is: DaemonSets are for infrastructure agents that need to run on every node, not for application workloads.

---

**Q: "Explain Kubernetes RBAC. How would you give a developer read-only access to pods in the production namespace?"**
> Kubernetes RBAC has four objects: Role, ClusterRole, RoleBinding, ClusterRoleBinding. A Role defines WHAT actions are allowed on which resources within a namespace. A ClusterRole is similar but cluster-wide. RoleBindings grant a Role (or ClusterRole) to a subject (User, Group, or ServiceAccount) within a namespace.

> To give a developer read-only access to pods in production: create a Role in the production namespace with `get`, `list`, `watch` verbs on `pods` and `pods/log` resources. Then create a RoleBinding that grants this Role to the developer's username (which maps to the `CN` field in their client certificate). The developer can now `kubectl get pods -n production` and `kubectl logs -n production` but cannot create, delete, or exec into pods. I can also reuse a ClusterRole in a RoleBinding to limit a cluster-wide role to one namespace — for example, granting the built-in `view` ClusterRole via a namespace-scoped RoleBinding.

---

### 27.2 kubectl Cheat Sheet — Commands You Must Know Cold

```bash
# ─── CLUSTER INFO ────────────────────────────────────────────────────
kubectl cluster-info
kubectl get nodes -o wide
kubectl top nodes
kubectl api-resources
kubectl explain deployment.spec.strategy

# ─── PODS ────────────────────────────────────────────────────────────
kubectl get pods -A -o wide
kubectl describe pod <n>
kubectl logs <n> -f --tail=50
kubectl logs <n> --previous
kubectl exec -it <n> -- bash
kubectl exec <n> -- env
kubectl cp <n>:/app/log.txt ./log.txt
kubectl port-forward pod/<n> 8080:3000
kubectl delete pod <n> --grace-period=0 --force

# ─── DEPLOYMENTS ─────────────────────────────────────────────────────
kubectl apply -f deployment.yaml
kubectl create deployment nginx --image=nginx --replicas=3
kubectl scale deployment nginx --replicas=5
kubectl set image deployment/nginx nginx=nginx:1.26
kubectl rollout status deployment/nginx
kubectl rollout history deployment/nginx
kubectl rollout undo deployment/nginx
kubectl rollout undo deployment/nginx --to-revision=2
kubectl rollout restart deployment/nginx

# ─── SERVICES ────────────────────────────────────────────────────────
kubectl get svc -o wide
kubectl describe svc api-service
kubectl get endpoints api-service
kubectl expose deployment nginx --type=LoadBalancer --port=80
kubectl port-forward svc/nginx 8080:80

# ─── CONFIGMAPS AND SECRETS ──────────────────────────────────────────
kubectl create configmap app-config --from-literal=key=value
kubectl create secret generic db-secret --from-literal=password=secret
kubectl get secret db-secret -o jsonpath='{.data.password}' | base64 -d

# ─── NAMESPACES ──────────────────────────────────────────────────────
kubectl get all -n production
kubectl config set-context --current --namespace=production

# ─── LABELS AND SELECTORS ────────────────────────────────────────────
kubectl get pods -l app=api,env=production
kubectl label pod my-pod version=v2
kubectl annotate pod my-pod description="main api pod"

# ─── EVENTS AND DEBUGGING ────────────────────────────────────────────
kubectl get events --sort-by='.lastTimestamp' -n production
kubectl auth can-i create deployments -n production
kubectl auth can-i '*' '*' --as=system:serviceaccount:production:api-sa
kubectl debug -it <pod> --image=busybox:1.36 --target=<container>

# ─── STORAGE ─────────────────────────────────────────────────────────
kubectl get pvc -A
kubectl get pv
kubectl describe pvc my-pvc

# ─── RBAC ────────────────────────────────────────────────────────────
kubectl get roles,rolebindings -n production
kubectl get clusterroles,clusterrolebindings
kubectl describe role developer-role -n production

# ─── HPA ─────────────────────────────────────────────────────────────
kubectl autoscale deployment api --min=2 --max=20 --cpu-percent=70
kubectl get hpa
kubectl describe hpa api-hpa

# ─── HELM ────────────────────────────────────────────────────────────
helm list -A
helm install myapp ./chart --values values.yaml
helm upgrade --install myapp ./chart
helm rollback myapp 1
helm uninstall myapp

# ─── NODE MAINTENANCE ────────────────────────────────────────────────
kubectl cordon <node>
kubectl drain <node> --ignore-daemonsets --delete-emptydir-data
kubectl uncordon <node>
kubectl taint node <node> key=value:NoSchedule
kubectl taint node <node> key=value:NoSchedule-

# ─── ADVANCED ────────────────────────────────────────────────────────
kubectl diff -f deployment.yaml
kubectl apply --dry-run=client -f deployment.yaml
kubectl apply --dry-run=server -f deployment.yaml
kubectl kustomize overlays/production | kubectl apply -f -
kubectl get deployment nginx -o jsonpath='{.spec.replicas}'
kubectl patch deployment nginx -p '{"spec":{"replicas":5}}'
```

---

### 27.3 CKA Exam Tips

The CKA (Certified Kubernetes Administrator) exam is performance-based — 2 hours, real cluster, no multiple choice. These practices will save you significant time:

```bash
# Set these aliases at the start of the exam
alias k=kubectl
export do='--dry-run=client -o yaml'   # Generate YAML without applying
export now='--force --grace-period=0'  # Force delete immediately

# Generate resource YAML quickly
k create deployment nginx --image=nginx $do > deployment.yaml
k create service clusterip my-svc --tcp=80:80 $do > service.yaml
k create configmap my-cm --from-literal=key=value $do
k create secret generic my-secret --from-literal=password=secret $do

# Use explain for field reference (no internet in exam)
k explain pod.spec.containers.resources
k explain deployment.spec.strategy.rollingUpdate

# Quick namespace operations
k create ns production
k -n production get pods   # -n shorthand

# Quickly check RBAC permissions
k auth can-i list pods -n production --as=john
```

---

## Official Kubernetes Documentation Reference

| Topic | URL |
|---|---|
| Kubernetes Documentation | https://kubernetes.io/docs/ |
| Concepts | https://kubernetes.io/docs/concepts/ |
| Tasks | https://kubernetes.io/docs/tasks/ |
| kubectl Reference | https://kubernetes.io/docs/reference/kubectl/ |
| API Reference | https://kubernetes.io/docs/reference/kubernetes-api/ |
| Networking | https://kubernetes.io/docs/concepts/services-networking/ |
| Storage | https://kubernetes.io/docs/concepts/storage/ |
| Security | https://kubernetes.io/docs/concepts/security/ |
| Helm Documentation | https://helm.sh/docs/ |
| ArgoCD Documentation | https://argo-cd.readthedocs.io/ |
| Kyverno Documentation | https://kyverno.io/docs/ |
| Istio Documentation | https://istio.io/latest/docs/ |
| Prometheus Operator | https://prometheus-operator.dev/ |
| CKA Curriculum | https://github.com/cncf/curriculum |
| Killer.sh (CKA Practice) | https://killer.sh/ |

---

## Learning Path

```
Week 1–2:   Lessons 1–5    Cluster setup, pods, deployments, basic troubleshooting
Week 3–4:   Lessons 6–8    Services, Ingress, ConfigMaps, Secrets
Week 5–6:   Lesson 9       Resource limits, probes, rolling updates
Week 7–8:   Lessons 10–12  HPA, networking, persistent storage
Week 9–10:  Lessons 13–14  Helm, RBAC
Week 11–12: Lesson 15      Logging and monitoring with Prometheus+Grafana
Week 13–14: Lessons 16–17  HA clusters, security hardening
Week 15–16: Lessons 18–19  Istio service mesh, GitOps with ArgoCD
Week 17–18: Lesson 20      Cluster upgrades, node maintenance
Week 19–20: Lessons 21–23  Internals: etcd, scheduler, controllers
Week 21–22: Lessons 24–25  Production debugging, performance
Week 23–24: Lesson 26      Advanced security: audit, Kyverno, secrets encryption
Week 25–26: Lesson 27      Interview prep + CKA exam practice on killer.sh
```

**Build Something Real:**
Deploy a complete microservices platform:
- Multi-node kind cluster, then migrate to AKS
- 3+ microservices with Deployments, Services, Ingress
- PostgreSQL with StatefulSet and persistent volume
- Redis cache
- RBAC for dev and ops teams
- Prometheus + Grafana monitoring
- HPA on API service
- GitOps with ArgoCD syncing from a GitHub repo

This is your portfolio proof-of-work.

---

*Built on: Official Kubernetes Documentation — https://kubernetes.io/docs/ | CKA/CKAD/CKS Curriculum | Production Kubernetes Patterns*
