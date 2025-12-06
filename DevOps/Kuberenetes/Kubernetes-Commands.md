### `kubectl` Basic Commands:
- To check version of kubectl: `kubectl version --client`
- To get context: `kubectl config get-contexts`
- To change the context: `kubectl use-context [cluster-name]`
- To view the configurations: `kubectl config view`
- To view metrics: `kubectl top pod`
- Get information related to the cluster: `kubectl cluster-info --context [cluster-name]`
- Get all the kubernetes resources: `kubectl get all`
- Delete all the resources: `kubectl delete -f .`
- **Pods**:
  - Create pod: `kubectl run [pod-name] --image=[image-name]`
  - Edit pod: `kubectl edit pod [pod-name]`
  - Delete pod: `kubectl delete pod [pod-name]`
- Get the status of different kubernetes components: 
    - `kubectl get nodes`
    - `kubectl get pods`
    - `kubectl get services`  
    - `kubectl get secret`
    - `kubectl get replicaset`
    - `kubectl get deployment`
    - `kubectl get namespace` or `kubectl get ns`
- **Deployment**:
  - Create deployment: `kubectl create deployment [name] --image=[image]`
  - Edit deployment: `kubectl edit deployment [name]`
  - Delete deployment: `kubectl delete deployment [name]`
- Get logs: `kubectl logs [pod-name]`
- Get interactive terminal: `kubectl exec -it [pod-name] --bin/bash`
- Get additional information of pod: `kubectl describe pod [pod-name]`
- Use configuration file for operations: `kubectl apply -f [file-name]`
- Explain the details: `kubectl explain [pod/rc/rs/deployment]`
- **NameSpace**:
  - Create namespace: `kubectl create namespace [namespace-name]`
  - Delete namespace: `kubectl delete namespace [namespace-name]`
  - Get everything inside of a namespace: `kubectl get all --namespace=[namespace-name]`
- **Jobs**: 
  - To view jobs: `kubectl get jobs`
  - To describe jobs: `kubectl describe job [job-name]`
  - To delete jobs:  `kubectl delete job [job-name]`
- **CronJobs**:
  - To view cronjobs: `kubectl get cronjobs`
  - To describe cronjobs: `kubectl describe cronjob [job-name]`
  - To delete cronjobs:  `kubectl delete cronjob [job-name]`
- **StatefulSets**:
  - List StatefulSets: `kubectl get statefulsets`
  - List StatefulSets: `kubectl describe statefulset <statefulset-name>`
  - Delete a StatefulSet (without deleting PVCs): `kubectl delete statefulset <statefulset-name> --cascade=orphan`
  - Delete a StatefulSet (with deleting PVCs): 
    ```bash
    kubectl delete statefulset <statefulset-name>
    kubectl delete pvc -l app=example
    ```
  - Scale a StatefulSet: `kubectl scale statefulset <statefulset-name> --replicas=5`
- **ConfigMaps**:
  - List ConfigMaps: `kubectl get configmaps`
  - Describe a ConfigMap: `kubectl describe configmap <name>`
  - Delete a ConfigMap: `kubectl delete configmap <name>`
  - Create a ConfigMap from a File: `kubectl create configmap app-config --from-file=<file-name>` 
  - Create a ConfigMap from Literal Values: `kubectl create configmap app-config --from-literal=database_url="mysql://db:3306" --from-literal=log_level="debug"`
- **Secrets**:
  - List secrets: `kubectl get secrets` 
  - Describe a secret: `kubectl describe secret <name>` 
  - View Secret Data (Base64 Encoded): `kubectl get secret <name> -o yaml`
  - Delete a Secret: `kubectl delete secret <name>`
- Get YAML for Existing Resources:
  - **Pod**: `kubectl get pod <pod-name> -n <namespace> -o yaml`
  - **Deployment**: `kubectl get deployment <deployment-name> -n <namespace> -o yaml`
  - **Service**: `kubectl get service <service-name> -n <namespace> -o yaml`
  - **Secret**: `kubectl get secret <secret-name> -n <namespace> -o yaml`
  - **ConfigMap**: `kubectl get configmap <config-name> -n <namespace> -o yaml`
  - **ReplicaSet**: `kubectl get rs <replicaset-name> -n <namespace> -o yaml`
  - **PersistentVolumeClaim (PVC)**: `kubectl get pvc <pvc-name> -n <namespace> -o yaml`
  - **Ingress**: `kubectl get ingress <ingress-name> -n <namespace> -o yaml`
  - **Namespace**: `kubectl get namespace <namespace-name> -o yaml`
- To see echo output from an init container: `kubectl logs <pod-name> <container-name>`
  - **All resources in a namespace**: `kubectl get all -n <namespace> -o yaml`

### `kubectl` Advance Commands:
- Use the created pod: `kubectl exec -it [pod-name] -- bash`
- **Scaling**:
  - Deployments: `kubectl scale --replicas=3 deployment/my-deployment`
  - ReplicaSets: `kubectl scale --replicas=5 replicaset/my-replicaset`
  - StatefulSets: `kubectl scale --replicas=2 statefulset/my-statefulset`
- Change the image: `kubectl set image deployment/[deployment-name] [old-image]=[new-image]`
- Check the rollout history: `kubectl rollout history deployment/[deployment-name]`
- Rollback the changes: `kubectl rollout undo deployment/[deployment-name]`
- Rolling update: `kubectl set image deployment/[deployment-name] [container-name]=[new-image]:[tag]`. 
  - Example: `kubectl set image deployment/nginx-deployment nginx=nginx:1.2.3`
- **Resource Quota**:
  - List Resource Quotas: `kubectl get resourcequota -n <namespace>`
  - Describe a Resource Quota: `kubectl describe resourcequota <quota-name> -n <namespace>`
- **AutoScaling**:
  - Scale HPA: `kubectl get hpa`
  - Delete HPA: `kubectl delete hpa <hpa-name>`
  - Scale VPA: `kubectl get vpa`
  - Delete VPA: `kubectl delete vpa <vpa-name>`
- **Node Affinity**:
  - Label a Node (for affinity rules): `kubectl label node <node-name> environment=production` 
  - List Nodes with Labels: `kubectl get nodes --show-labels`
  - Remove a Label from a Node: `kubectl label node <node-name> environment-`
  - Check Pod Scheduling Issues: `kubectl describe pod <pod-name>`
- **RBAC Commands**
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
- **Node Management Commands**:
  - Mark a node unschedulable: `kubectl cordon <node>`
  - Mark a node schedulable again: `kubectl uncordon <node>`
  - Evict all pods from node and mark unschedulable: `kubectl drain <node>`
  - Drains a node without affecting DaemonSets (useful for maintenance): `kubectl drain --ignore-daemonsets <node>`  
- **Patching and Modifying Resources**  
  - Modify specific field of a resource without replacing the entire object: `kubectl patch <resource> <name> --type=json -p '<patch-data>'`
  - Open the resource definition in an editor: `kubectl edit <resource> <name>`  
  - Replace existing resource with a new definition: `kubectl replace -f <file.yaml>`  
  -  from a YAML file.  
- **API Proxy and Authentication**:
  - Start a local API server proxy to securely access the Kubernetes API: `kubectl proxy`  
  - Generate authentication token for a Service Account: `kubectl create token <serviceaccount>` 
- **Debugging and Troubleshooting**:   
  - Executes command inside a running pod: `kubectl exec -it <pod> -- <command>` 
  - Starts debugging pod on a node (troubleshooting): `kubectl debug node/<node-name> --image=busybox`  
- **CRD**:
  - Get all CRDs in the cluster: `kubectl get crd`
  - Describe a specific CRD: `kubectl describe crd <crd-name>`
  - Get details of all objects for a specific CRD type: `kubectl get <crd-name>`
  - Delete a CRD: `kubectl delete crd <crd-name>`
  - Delete all instances of a CRD: `kubectl delete <crd-name> --all`

## `minkube` Basic Commands:
- Start Container: `minikube start`
  - We can even define the hypervisor, using the --driver flag. Example: `--driver=docker`
- Get the status of nodes: `minikube status`
- Install ingress controller: `minikube addons enable ingress`
- Commands will be similar to kubectl 


## All Commands Reference Guide:
[Kubernetes Docs](https://kubernetes.io/docs/reference/kubectl/quick-reference/)
