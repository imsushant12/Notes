## Stateful Application vs Stateless Application
Stateful Applications stores data like databases. For a stateless application, each request is a new request.

Stateless Application is deployed using deployment component and Stateful Application uses StatefulSet component for deployment. Both deployment and StatefulSet manages pods based on the container specification.

StatefulSet stores the identity, so if a pod dies, the new one gains the same identity. On the other hand, if we use deployment there is no identity saving mechanism. So, if we scale up and down, any random pod can be destroyed or added and the balancer will take care of the load.

Deployment pods names have random hashes at the end but StatefulSet has fixed ordered names. Syntax: `$(StatefulSet Name)-$(ordinal)`. For example: `mysql-0`. Next pod is only create, if previous one is up and running. 

```
Master    Slave     Slave     Slave
mysql-0   mysql-1   mysql-2   mysql-3
```
Deletion will be in same order 3 then 2 then 1 and so on.

StatefulSet has 2 main characteristics:
1. predictable pod name (mysql-0, mysql-1, and so on)
2. fixed individual DNS name (mysql-0.svc2)

- More differences between them.
- An example of both approach.
- How do we scale a database application?

Stateful applications are not perfect for containerized environments.


## ReplicaSet vs Replica Controller vs StatefulSet vs Deployment
| Feature  | **ReplicationController** | **ReplicaSet** | **Deployment** | **StatefulSet** |
|----------|---------------------------|----------------|----------------|-----------------|
| **Purpose**          | Ensures a fixed number of pods are running. | Modern replacement for ReplicationController, provides better selector support. | Manages ReplicaSets and handles rolling updates, rollbacks, and versioning. | Manages stateful applications with stable pod identities and persistent storage. |
| **Pod Identity**     | Pods are interchangeable, no stable identity. | Pods are interchangeable, no stable identity. | Pods are interchangeable, no stable identity. | Each pod gets a **unique, persistent identity** (e.g., `pod-0`, `pod-1`). |
| **Storage**         | No persistent storage, pods are ephemeral. | No persistent storage, pods are ephemeral. | No persistent storage, pods are ephemeral. | Each pod gets a **dedicated persistent volume (PVC)**, which is not shared. |
| **Scaling Behavior** | Manual or via Horizontal Pod Autoscaler (HPA). | Manual or via HPA, but no automated rollouts. | Automated scaling with built-in rollout strategies. | Ordered scaling—Pods start/stopped **one at a time** (ensuring stability). |
| **Rolling Updates**  | ❌ Not supported. | ❌ Not supported; requires manual updates. | ✅ Supported (zero downtime updates). | ✅ Supported but updates occur in **sequential order**. |
| **Rollback**        | ❌ Not supported. | ❌ Not supported. | ✅ Yes, maintains version history. | ✅ Yes, but **gradual** due to ordered updates. |
| **Node Placement**  | Random across cluster nodes. | Random across cluster nodes. | Random across cluster nodes. | Maintains **sticky identity**—pod reschedules to the **same PVC** on a different node. |
| **Selector Support** | Only **equality-based selectors** (e.g., `matchLabels`). | Supports both **equality-based and set-based selectors** (e.g., `matchExpressions`). | Same as ReplicaSet. | Same as ReplicaSet. |
| **Use Case**        | Legacy method for running multiple identical pods. | Ensures a set number of **stateless** pods are running. | Best for **stateless applications** with frequent updates (APIs, web apps, microservices). | Best for **stateful workloads** (databases like MySQL, Redis, Kafka, Zookeeper). |

## Jobs and CronJob
A Job in Kubernetes ensures that a task runs to completion. Unlike Deployments, which maintain running Pods, Jobs create Pods that run a task and exit when done.

**When and Why to Use Jobs?**
- When we need to run one-time or batch tasks, such as:
  - Data processing (e.g., ETL jobs, database migrations).
  - Scheduled tasks (when combined with a CronJob).
  - Sending emails, notifications, or reports.
- Ensures retries in case of failures.
- Can run parallel tasks if needed.
  
**Important Things to Define in a Job**:
- BackoffLimit: Maximum retries before the Job fails.
- Completions: Number of successful runs needed before Job is marked complete.
- Parallelism: Number of Pods to run simultaneously.

**CronJob** is used to run jobs on a schedule, similar to a traditional Linux cron job. It allows us to run a Job at a specific time or periodically.

### Commands
- To view jobs: `kubectl get jobs`
- To describe jobs: `kubectl describe job [job-name]`
- To delete jobs:  `kubectl delete job [job-name]`
- To view cronjobs: `kubectl get cronjobs`
- To describe cronjobs: `kubectl describe cronjob [job-name]`
- To delete cronjobs:  `kubectl delete cronjob [job-name]`


## Resource Quota, Requests, and Limits 
- Resource quotas, requests, and limits help in managing resource allocation across multiple workloads in a Kubernetes cluster.  
- Preventing one application from consuming all cluster resources.  
- Managing multi-tenant environments.  
- Ensuring fair resource distribution.  
- Avoiding over-provisioning of CPU and memory.  

1. **Resource Quota** – Enforces overall resource consumption at the namespace level.  
2. **Requests** – Defines the minimum guaranteed resources a container will get.  
3. **Limits** – Defines the maximum resources a container can use.  


## Commands: 
- List Resource Quotas: `kubectl get resourcequota -n <namespace>`
- Describe a Resource Quota: `kubectl describe resourcequota <quota-name> -n <namespace>`


## Probes
- Probes are used to check the health and availability of containers in a pod.
- Types:
- **Liveness Probe**  
  - Determines if a container is still **alive** and should be restarted if it is unresponsive.  
  - Used when an application might hang but not crash.  
  - Example:
    ```yaml1
    livenessProbe:
      httpGet:
        path: /health
        port: 8080
      initialDelaySeconds: 5
      periodSeconds: 10
    ```
- **Readiness Probe**  
  - Ensures that a container is **ready to serve traffic** before adding it to a service.  
  - Used when an application needs some time (like database connections) before handling traffic.  
  - Example:
    ```yaml
    readinessProbe:
      exec:
        command: ["cat", "/tmp/ready"]
      initialDelaySeconds: 5
      periodSeconds: 10
    ```
- **Startup Probe**  
  - Used for applications with **long startup times** (e.g., JVM applications).  
  - Ensures the container does not fail before it fully starts.  
  - Example:
    ```yaml
    startupProbe:
      tcpSocket:
        port: 8080
      failureThreshold: 30
      periodSeconds: 10
    ```

## Taints and Tolerations
- A taint is applied to a node to prevent certain pods from being scheduled on it unless the pod has a matching toleration.
- A toleration is applied to a pod, allowing it to bypass a taint on a node.
- Prevent regular workloads from running on **control-plane nodes**.  
- Keep special workloads on dedicated nodes (e.g., GPU nodes, security-sensitive workloads).  
- Taint Effects:
  - **NoSchedule** – (Only new ones): New pods will not be scheduled on the node unless they tolerate the taint.
  - **PreferNoSchedule** – (Try to schedule):  The scheduler will try to avoid placing pods on the node but may do so if necessary.
  - **NoExecute** – (Existing + new ones): Existing pods will be evicted unless they tolerate the taint, and new pods will not be scheduled.


> **Note**: By default, control-plane nodes are tainted.

### Commands:
- Taint a Node: `kubectl taint node <node-name> key=value:NoSchedule`
- Remove a Taint (Untaint a Node): `kubectl taint node <node-name> key=value:NoSchedule-` 

#### Toleration in Pod Definition:  
```yaml
tolerations:
  - key: "special-node"
    operator: "Exists"
    effect: "NoSchedule"
```

### Selectors vs Node Affinity vs. Taints & Tolerations


## Helm
- It is a package manager for Kubernetes that simplifies the deployment and management of applications.  
- Uses **Helm Charts**, which are pre-configured application templates.  
- A Helm Chart is a **collection of YAML files** that define a Kubernetes application.  
- It contains:
  - **Templates** (YAML manifests for deployments, services, etc.)
  - **Values** (configurable parameters)
  - **Dependencies** (other charts the app depends on)

### Problems Before Helm 
- Manually managing multiple Kubernetes YAML files is **tedious**.  
- Updating configurations across multiple resources is **error-prone**.  
- Managing dependencies is **difficult**.  

### How Helm Solves
- Packages Kubernetes resources into **Charts** for easy deployment.  
- Provides **templating** to avoid repetitive YAML.  
- Allows **version control and rollback** of deployments.  
- Supports **dependency management** for complex applications.  

### Helm 2 vs Helm 3
| Feature | Helm 2 | Helm 3 |
|---------|--------|--------|
| Tiller (Cluster Component) | Required | Removed |
| Security | RBAC-based, Tiller had cluster-wide access | More secure (no Tiller) |
| CRDs Handling | Manual | Automated |
| Secrets Storage | ConfigMaps | Secrets |
| Release Namespacing | Single Namespace | Namespace-scoped releases |

### Helm Architecture
Helm follows a client-server architecture (in Helm 2) but transitioned to a client-only architecture in Helm 3.  

#### Helm 2 Architecture (Client-Server Model)
In Helm 2, there were two main components:  
1. **Helm Client**  
   - A CLI tool that manages charts, repositories, releases, and configurations.  
   - Interacts with the **Tiller** server in the cluster.  

2. **Tiller (Server-Side Component, Removed in Helm 3)**  
   - A Kubernetes service running inside the cluster.  
   - Responsible for installing, upgrading, and managing releases.  
   - Had cluster-wide access, making it a security risk.  

#### Helm 3 Architecture (Client-Only Model)
Helm 3 removed Tiller, making Helm a **client-only** tool.  
1. **Helm Client (CLI)**  
   - Directly interacts with the Kubernetes API Server.  
   - Uses **YAML manifests** and **templating** to deploy applications.  
   - Manages **chart installations, upgrades, and rollbacks** without a server-side component.  

2. **Kubernetes API Server**  
   - Helm directly sends requests to the Kubernetes API server to manage resources.  

#### Helm Workflow in Helm 3
1. The user runs a Helm command (e.g., `helm install`).  
2. The Helm client processes the chart and renders the Kubernetes manifests.  
3. The Helm client sends the rendered manifests to the Kubernetes API server.  
4. The Kubernetes API server schedules and manages the application.  

This architecture **simplifies security**, **removes Tiller**, and **enhances usability** by directly interacting with Kubernetes.

### Tiller Issues in Helm 2
Tiller was the **server-side component** of Helm 2 that ran inside the Kubernetes cluster and managed releases. However, it introduced several issues that led to its removal in Helm 3.  

#### Key Issues with Tiller in Helm 2
1. **Security Risks (Cluster-Wide Access)**  
   - Tiller had **full cluster-wide access** by default, making it a security risk.  
   - Any user with access to Tiller could deploy or modify any resource in the cluster.  
   - Workarounds like Role-Based Access Control (RBAC) and TLS were required to restrict access.  

2. **Complexity and Overhead**  
   - Tiller required additional setup and configuration.  
   - Managing Tiller’s permissions and security policies added operational complexity.  

3. **Multi-Tenancy Issues**  
   - In shared Kubernetes clusters, multiple teams had to **share a single Tiller instance**, leading to conflicts.  
   - Workarounds included deploying **multiple Tillers per namespace**, increasing management overhead.  

4. **State Management Inside Kubernetes**  
   - Tiller stored Helm release information in Kubernetes ConfigMaps or Secrets.  
   - This added unnecessary complexity and potential synchronization issues.  

### Solution in Helm 3
Helm 3 **completely removed Tiller** and allowed the **Helm client to communicate directly with the Kubernetes API Server**. This resolved the security risks, simplified the architecture, and made Helm more **secure and easier to manage**.

### Commands: 
#### Installation and Setup
```sh
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash  # Install Helm
helm version  # Check Helm version
```

#### Helm Chart Operations  
```sh
helm repo add stable https://charts.helm.sh/stable  # Add a Helm repository
helm search repo nginx  # Search for a chart in a repository
helm install my-app stable/nginx  # Install a chart
helm list  # List all installed Helm releases
helm upgrade my-app stable/nginx  # Upgrade an existing release
helm rollback my-app 1  # Rollback to a previous version
helm uninstall my-app  # Uninstall a Helm release
```

#### Customizing Helm Charts
```sh
helm show values stable/nginx  # View configurable values of a chart
helm install my-app stable/nginx --values custom-values.yaml  # Install with custom values
```

#### Developing Helm Charts
```sh
helm create my-chart  # Create a new Helm chart
helm lint my-chart  # Validate a chart for syntax errors
helm package my-chart  # Package a chart for distribution
```

## Static Pods
Static Pods are the pods that are not scheduled by the scheduler. The etcd, kube-apiserver, kube-controller-manager, kube-scheduler present on the control plane are static pods.

There is a `kubelet` present on each control plane as well. It checks the location: `/etc/kubernetes/manifests/`. It has the manifest files for creating - etcd, kube-apiserver, kube-controller-manager, kube-scheduler. So, the `kubelet` on the control plane checks these manifests and schedules these components.

## Manual Scheduling
Even if the scheduler is down and we mention the name of the node a pod has to be scheduled then the pod will be scheduled. 

Example: `nodeName: [node-name]`