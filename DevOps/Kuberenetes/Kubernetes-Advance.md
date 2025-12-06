## Autoscaling
Autoscaling helps dynamically adjust the resources assigned to workloads based on demand. It is achieved using **HPA (Horizontal Pod Autoscaler), VPA (Vertical Pod Autoscaler), and KEDA**. These mechanisms rely on resource metrics to make scaling decisions.  


### Checking Resource Usage for Scaling Decisions
```sh
kubectl top pod   # Shows CPU and memory usage of pods
kubectl top node  # Shows resource usage of nodes
```

### Horizontal Pod Autoscaler (HPA) 
- **Scales pods horizontally** by increasing or decreasing the number of replicas based on CPU or memory usage.  
- Uses **metrics-server** to collect real-time resource usage.  
- Defined with a **minimum and maximum pod count** and a resource utilization threshold.  
- Works best for **stateless applications** like web services.  


### HPA Commands:
```bash
kubectl get hpa
kubectl delete hpa <hpa-name>
```

**Example**: `kubectl autoscale deployment <deployment-name> --cpu-percent=50 --min=2 --max=10`. In this case, if CPU usage exceeds **50%**, more pods will be created.  

### Vertical Pod Autoscaler (VPA) 
- **Adjusts CPU and memory requests for existing pods** instead of adding new pods.  
- Helps with **stateful applications** (like databases) where scaling horizontally is inefficient.  
- Works with three update modes:
  - **Off** – Only provides recommendations.
  - **Initial** – Applies recommended resources during pod creation.
  - **Auto** – Automatically updates running pods (requires restart).  
- The VPA **monitors resource usage** and adjusts pod CPU/memory requests automatically.  

#### VPA Commands:
```sh
kubectl get vpa
kubectl delete vpa vpa-example
```

### Kubernetes Event-Driven Autoscaling (KEDA) 
- **Dynamically chooses between HPA and VPA** based on event-driven metrics.  
- Can scale workloads to **zero** when no traffic exists.  
- Works with external metrics (e.g., Kafka, RabbitMQ, AWS SQS).  

- If Kafka message lag exceeds **5**, pods are **scaled up**.  
- When messages are processed, pods **scale down to 1** (or even **0**).  

### KEDA Commands:  
```sh
kubectl get scaledobjects
kubectl delete scaledobject kafka-scaler
```

#### When to Use which? 
| **Autoscaler** | **Best For** |
|--------------|-------------|
| HPA | Stateless applications with fluctuating traffic (e.g., web servers, APIs) |
| VPA | Stateful applications that require resource tuning (e.g., databases) |
| KEDA | Event-driven applications with unpredictable traffic (e.g., message queues, IoT events) |


## Node Affinity 
Node Affinity controls **pod scheduling** by specifying rules about which nodes a pod can run on. It is an extension of **nodeSelector**, allowing more advanced rules based on node labels.  

### Types of Node Affinity 
1. **Required (Hard) Affinity (`requiredDuringSchedulingIgnoredDuringExecution`)**  
   - Pods **must** be scheduled on nodes that match the defined labels.  
   - If no suitable node is found, scheduling will fail.  

2. **Preferred (Soft) Affinity (`preferredDuringSchedulingIgnoredDuringExecution`)**  
   - Pods **prefer** to be scheduled on specific nodes, but will still run elsewhere if needed.  

### When to Use Node Affinity?
| **Use Case** | **Example** |
|-------------|------------|
| Ensure workloads run on nodes with specific hardware | Assign GPU workloads to GPU-enabled nodes |
| Separate production and development workloads | Schedule production pods on dedicated nodes |
| Optimize for specific performance needs | Assign memory-intensive apps to high-memory nodes |

### Node Affinity vs. Taints & Tolerations 
| **Feature** | **Purpose** |
|------------|------------|
| **Node Affinity** | Helps **schedule** pods on preferred nodes |
| **Taints & Tolerations** | Helps **prevent** pods from being scheduled on certain nodes |

### Node Affinity Commands: 
- Label a Node (for affinity rules): `kubectl label node <node-name> environment=production` 
- List Nodes with Labels: `kubectl get nodes --show-labels`
- Remove a Label from a Node: `kubectl label node <node-name> environment-`
- Check Pod Scheduling Issues: `kubectl describe pod <pod-name>`


## Cluster Administration
- Managing access control, security, and configurations for efficient cluster operation. 

### RBAC (Role-Based Access Control) 
- Administrators use RBAC to define **who** can perform **what actions** on specific **resources** within the cluster.  

#### Key RBAC Components:
1. **Role**:
   - Defines permissions (what actions can be performed) within a **specific namespace**.  
   - Example: A role that allows reading pods in the `dev` namespace.  

2. **RoleBinding**:  
   - Binds a **Role** to a **user, group, or service account** within a **namespace**.  
   - Grants the user the permissions defined in the Role.  

3. **ClusterRole**:  
   - Similar to a Role but applies **cluster-wide** across all namespaces.  
   - Used for granting global access to resources like nodes, persistent volumes, etc.  

4. **ClusterRoleBinding**:  
   - Binds a **ClusterRole** to a **user, group, or service account**, giving cluster-wide permissions.  

5. **Service Account**: 
   - A special type of account for pods to interact securely with the API server.  
   - By default, every pod runs with a **service account** assigned by Kubernetes. These accounts are used by applications running inside pods to securely interact with the API server. 

### RBAC Commands
- Check Service Accounts: 
    ```sh
    kubectl get serviceaccount
    kubectl get serviceaccount -n <namespace>
    ```
- Check Your Current Permissions:
    ```sh
    kubectl auth can-i get pods
    kubectl auth can-i delete pods
    kubectl auth can-i get deployments
    kubectl auth can-i delete deployments
    ```
- Check Permissions for Another User:
    ```sh
    kubectl auth can-i get pods --as=alice
    kubectl auth can-i delete deployments --as=admin-user
    ```
- List All Roles and RoleBindings:  
    ```sh
    kubectl get roles -n <namespace>
    kubectl get rolebindings -n <namespace>
    ```
- List All ClusterRoles and ClusterRoleBindings: 
    ```sh
    kubectl get clusterroles
    kubectl get clusterrolebindings
    ```
- Delete a Role or ClusterRole:
    ```sh
    kubectl delete role <role-name> -n <namespace>
    kubectl delete clusterrole <clusterrole-name>
    ```
- Delete a RoleBinding or ClusterRoleBinding: 
    ```sh
    kubectl delete rolebinding <rolebinding-name> -n <namespace>
    kubectl delete clusterrolebinding <clusterrolebinding-name>
    ```

### When to Use RBAC?  
| **Use Case** | **Solution** |
|-------------|-------------|
| Limit access to specific resources in a namespace | Use **Role + RoleBinding** |
| Grant global permissions across all namespaces | Use **ClusterRole + ClusterRoleBinding** |
| Restrict API access to specific users | Use **RBAC rules with `kubectl auth can-i`** |
| Secure pods accessing the API | Use **Service Accounts** |


## CRDs (Custom Resource Definitions) 
- Custom Resource Definitions (CRDs) allow to **extend Kubernetes** by defining own resource types. 
- These resources behave just like built-in Kubernetes objects (e.g., Pods, Services).  
- Used when Kubernetes' **default objects** (like Pods, Deployments) don’t meet needs.  
- Allows developers to define **custom APIs** within the Kubernetes cluster.  
- Commonly used in **Operators** and **Custom Controllers** to automate tasks.  

## Commands: 
- Get all CRDs in the cluster: `kubectl get crd`
- Describe a specific CRD: `kubectl describe crd <crd-name>`
- Get details of all objects for a specific CRD type: `kubectl get <crd-name>`
- Delete a CRD: `kubectl delete crd <crd-name>`
- Delete all instances of a CRD: `kubectl delete <crd-name> --all`

## Operators
- Operators are custom controllers that extend Kubernetes functionality.
- They automate the deployment, scaling, and management of complex applications.
- Built using **Custom Resource Definitions (CRDs)** and **Custom Controllers**.
- Automates lifecycle management of applications like **databases, message queues, or monitoring tools**.
- Helps in **self-healing**, **automatic scaling**, and **backup/restore**.
- Useful for stateful applications like **PostgreSQL, Redis, Cassandra**.

### **Example of PostgreSQL Operator**:
```yaml
apiVersion: postgresql.example.com/v1
kind: PostgresCluster
metadata:
  name: my-db-cluster
spec:
  size: 3
  storage:
    size: 10Gi
```
- Here, the **PostgreSQL Operator** manages a **PostgresCluster** custom resource.

### Commands:
```sh
kubectl get crds                           # List all CRDs
kubectl get postgresclusters                # List custom resources managed by an operator
kubectl describe crd postgresclusters       # View details of a CRD
```


## Kubernetes API
- Core component that allows interaction with the cluster.
- Provides **RESTful endpoints** for managing resources like **Pods, Services, Deployments**.
- The `kube-apiserver` is the main API server that processes all cluster requests.

### API Request Workflow
1. User runs `kubectl` command (or API request).
2. Request goes to the **API Server (`kube-apiserver`)**.
3. The API Server authenticates & authorizes the request.
4. The request is processed by controllers and stored in **etcd**.

### Interacting with the Kubernetes API
#### 1. Using `kubectl`
```sh
kubectl api-resources            # Lists all API resources available
kubectl api-versions             # Lists available API versions
kubectl get --raw /api/v1/pods   # Fetch raw API response for pods
```

#### 2. Using `curl`
```sh
curl -k https://<kube-apiserver>:6443/api/v1/pods --header "Authorization: Bearer <TOKEN>"
```

### API Groups in Kubernetes
- The API is organized into different groups for managing various resources:
  |      API Group       |      Example Resources    | Example Version |
  |----------------------|---------------------------|-----------------|
  | `core` (default)     | Pods, Services, Nodes     | `v1`            |
  | `apps`               | Deployments, StatefulSets | `v1`            |
  | `batch`              | Jobs, CronJobs            | `v1`            |
  | `networking.k8s.io`  | Ingress, NetworkPolicy    | `v1`            |


## Sidecar Containers and Init Containers 
### Init Containers 
- Special containers that run **before** the main application container starts. 
- Help **set up the environment** or perform **pre-requisites** before the main container runs.  
- **Executed sequentially** (one after another).  
- Must **complete successfully** before the main application container starts.  
- Can be used for **setup tasks** like downloading dependencies, waiting for a service to be ready, or initializing configurations.  
- **Use Cases**  
  - Waiting for a database to become available before starting an app.  
  - Setting up configurations or fetching credentials.  
  - Downloading dependencies before the main container runs.  

### Sidecar Containers 
- Run **alongside** the main container and provide **additional functionality**. 
- Unlike Init Containers, Sidecars **run concurrently** with the main application.  
- Used to **enhance functionality** (e.g., logging, monitoring, or security).  
- Can **share storage** and **network** with the main container.  
- Stops **only when the entire Pod stops**.  
- **Use Cases**  
  - Logging and Monitoring
  - Like a service mesh proxy (e.g., Envoy in Istio) acts as a Sidecar to manage traffic.  
  - Data Sync


## Service Mesh
- An infrastructure layer that **manages service-to-service communication** in a **microservices** architecture. 
- Provides **traffic control, security, observability, and reliability** without modifying the application code.  
- **How It Works?**  
  - Uses **Sidecar proxies** (like Envoy) to manage communication between services.  
  - The control plane **configures and manages** the proxies.  
  - The data plane **handles traffic flow** between services.  

### Example Tool - Istio
- A popular open-source Service Mesh that provides **security, observability, and traffic control** for microservices.  

#### Istio Architecture
1. **Data Plane**:  
   - Uses **Envoy proxies** as sidecars in each Pod.  
   - Handles service-to-service traffic.  
2. **Control Plane**:  
   - Manages policies, security, and configuration.  
   - Components:  
     - **Pilot** (traffic routing)  
     - **Citadel** (security)  
     - **Galley** (configuration management)  

#### Istio Use Cases
- Secure communication with **mTLS encryption**.  
- **Traffic splitting** (A/B testing, canary deployments).  
- **Monitor service health** using telemetry.  
- **Rate limiting** to prevent overuse of resources.  

#### Istio Commands**  
1. **Install Istio**  
    ```sh
    istioctl install --set profile=demo -y
    ```
2. **Enable Istio Sidecar Injection**  
    ```sh
    kubectl label namespace default istio-injection=enabled
    ```
3. **Check Installed Istio Services**  
    ```sh
    kubectl get pods -n istio-system
    kubectl get svc -n istio-system
    ```
4. **Apply an Istio VirtualService for Traffic Routing**  
    ```yaml
    apiVersion: networking.istio.io/v1alpha3
    kind: VirtualService
    metadata:
    name: my-app
    spec:
    hosts:
    - my-app.example.com
    http:
    - route:
        - destination:
            host: my-app-v1
            weight: 80
        - destination:
            host: my-app-v2
            weight: 20
    ```


## Advanced Features in Kubernetes
### Metrics Server: 
- Collects resource metrics from nodes and pods (CPU, Memory).  
- Used for HPA (Horizontal Pod Autoscaler), performance monitoring.  
- **Commands**:  
  ```sh
  kubectl top node
  kubectl top pod
  ```

### Logging
- Capturing logs of containers, nodes, and applications.  
- Can use tools like Fluentd, Elasticsearch, Loki, EFK stack (Elasticsearch, Fluentd, Kibana).  
- **Commands**:  
  ```sh
  kubectl logs <pod-name>  
  kubectl logs -f <pod-name>  # Follow logs in real-time  
  ```

### Service Mesh
- Manages service-to-service communication, security, and observability.  
- Some popular tools are- Istio, Linkerd, Consul, Kuma.  
- Can be used for:
  - Secure traffic between microservices.  
  - Load balancing, retries, service discovery.  
  - Encryption and authentication between services.  


### Pod Security Standards (PSS)
- Defines security policies for pods in Kubernetes clusters.  
- Three Security Levels of PSS:
  - **Privileged**: No restrictions.  
  - **Baseline**: Minimal restrictions for common workloads.  
  - **Restricted**: Strongest security for sensitive workloads.  
- **Example Policy Implementation**:  
  ```yaml
  apiVersion: policy/v1beta1
  kind: PodSecurityPolicy
  metadata:
    name: restricted-psp
  spec:
    privileged: false
    runAsUser:
      rule: MustRunAsNonRoot
  ```

### Secrets Encryption
- Encrypts Kubernetes secrets at rest for security.  
- **Configuration in API Server (`kube-apiserver` flag)**:
  ```yaml
  apiVersion: apiserver.config.k8s.io/v1
  kind: EncryptionConfiguration
  resources:
    - resources:
        - secrets
      providers:
        - aescbc:
            keys:
              - name: key1
                secret: BASE64_ENCODED_KEY
  ```
- **Enable Encryption**:
  ```sh
  kubectl get secrets
  ```


