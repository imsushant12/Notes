
## Configuration File
- Deployment:
  ```yml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: nginx-deployment
    namespace: nginx
  spec:
    replicas: 2
    selector: 
      matchLabels:
        app: nginx
    template: 
    # here we write what we define in pod.yaml
  ```
- Namespace:
  ```yml
  apiVersion: v1
  kind: Namespace
  metadata:
    name: nginx
  ```
- Pod:
  ```yml
  apiVersion: v1
  kind: Pod
  metadata:
    name: nginx-pod
    namespace: nginx
  spec:
    containers:
    - name: nginx
      image: nginx:latest
      ports:
      - containerPort: 80
  ```
- ReplicaSet:
  ```yml
  apiVersion: apps/v1
  kind: ReplicaSet
  metadata:
    name: nginx-replicasets
    namespace: nginx
  spec:
    replicas: 2
    selector: 
      matchLabels:
        app: nginx
    template: 
    # here we write what we define in pod.yaml
  ```
- DaemonSet: **It creates at least one pod is running on each pod**.
  ```yml
  apiVersion: apps/v1
  kind: DaemonSet
  metadata:
    name: nginx-daemonsets
    namespace: nginx
  spec:
    # we don't define replicas
    selector: 
      matchLabels:
        app: nginx
    template: 
    # here we write what we define in pod.yaml
  ```
- Jobs:
  ```yml
  apiVersion: batch/v1
  kind: Job
  metadata:
  name: demo-job
  namespace: nginx
  spec:
  completions: 3                          # Job needs 3 successful runs
  parallelism: 2                          # 2 Pods will run at the same time
  backoffLimit: 4                         # Retry 4 times before failing
  template:
      spec:
      containers:
      - name: job-container
          image: busybox
          command: ["echo", "Hello from Job"]
      restartPolicy: Never                # Ensures Pod doesn’t restart after completion
  ```
- CronJobs:
  ```yml
  apiVersion: batch/v1
  kind: CronJob
  metadata:
    name: demo-cronjob
    namespace: nginx
  spec:
    schedule: "*/5 * * * *"                 # Runs every 5 minutes
    jobTemplate:
      spec:
        completions: 3
        parallelism: 2
        backoffLimit: 4
        template:
          spec:
            containers:
              - name: job-container
                image: busybox
                command: ["echo", "Hello from CronJob"]
            restartPolicy: Never
  ```
- PersistentVolume
  ```yaml
  apiVersion: v1
  kind: PersistentVolume
  metadata:
    name: demo-pv
  spec:
    capacity:
      storage: 5Gi                          # 5GB Storage
    accessModes:
      - ReadWriteOnce                       # Can be mounted as read-write by a single node
    persistentVolumeReclaimPolicy: Retain   # Keeps data even after PVC is deleted
    storageClassName: manual
    hostPath:
      path: "/mnt/data"                     # Local storage path (for testing)
  ```
- PersistentVolumeClaim
  ```yaml
  apiVersion: v1
  kind: PersistentVolumeClaim
  metadata:
    name: demo-pvc
  spec:
    accessModes:
      - ReadWriteOnce
    resources:
      requests:
        storage: 5Gi                        # Requesting 5GB of storage
    storageClassName: manual
  ```
- Service:
  ```yml
  apiVersion: v1
  kind: Service
  metadata:
    name: demo-service
  spec:
    selector:
      app: demo-app                         # Matches Pods with this label
    ports:
      - protocol: TCP
        port: 80                            # Service Port
        targetPort: 8080                    # Pod's Container Port
  ```
- StatefulSet
  ```yml
  apiVersion: apps/v1
  kind: StatefulSet
  metadata:
    name: example-statefulset
  spec:
    serviceName: "example-service"
    replicas: 3
    selector:
      matchLabels:
        app: example
    template:
      metadata:
        labels:
          app: example
      spec:
        containers:
          - name: example-container
            image: busybox
            command: ["sleep", "3600"]
            volumeMounts:
              - name: data
                mountPath: /data
    volumeClaimTemplates:
      - metadata:
          name: data
        spec:
          accessModes: [ "ReadWriteOnce" ]
          resources:
            requests:
              storage: 1Gi
  ```
- ConfigMap
  ```yml
  apiVersion: v1
  kind: ConfigMap
  metadata:
    name: app-config
  data:
    database_url: "mysql://db:3306"
    log_level: "debug"
    feature_flag: "true"
  ```
- Secret
  ```yml
  apiVersion: v1
  kind: Secret
  metadata:
    name: my-secret
  type: Opaque
  data:
    username: dXNlcm5hbWU=   # base64-encoded value of "username"
    password: cGFzc3dvcmQ=   # base64-encoded value of "password"
  ```
  > Note: Values in `data` must be **base64-encoded**.
- ResourceQuota
  ```yml
  apiVersion: v1
  kind: ResourceQuota
  metadata:
    name: example-quota
    namespace: my-namespace
  spec:
    hard:
      requests.cpu: "2"          # Total CPU request limit in the namespace
      requests.memory: 4Gi       # Total memory request limit
      limits.cpu: "4"            # Max CPU a pod can use
      limits.memory: 8Gi         # Max memory a pod can use
  ```
- HPA
  ```yaml
  apiVersion: autoscaling/v2
  kind: HorizontalPodAutoscaler
  metadata:
    name: hpa-example
  spec:
    scaleTargetRef:
      apiVersion: apps/v1
      kind: Deployment
      name: my-deployment
    minReplicas: 2
    maxReplicas: 10
    metrics:
      - type: Resource
        resource:
          name: cpu
          target:
            type: Utilization
            averageUtilization: 50
  ```
- VPA
  ```yaml
  apiVersion: autoscaling.k8s.io/v1
  kind: VerticalPodAutoscaler
  metadata:
    name: vpa-example
  spec:
    targetRef:
      apiVersion: "apps/v1"
      kind: Deployment
      name: my-deployment
    updatePolicy:
      updateMode: "Auto"
  ```
- KEDA
  ```yaml
  apiVersion: keda.sh/v1alpha1
  kind: ScaledObject
  metadata:
    name: kafka-scaler
  spec:
    scaleTargetRef:
      kind: Deployment
      name: kafka-consumer
    minReplicaCount: 1
    maxReplicaCount: 10
    triggers:
      - type: kafka
        metadata:
          topic: my-topic
          bootstrapServers: kafka-service:9092
          consumerGroup: my-group
          lagThreshold: "5"
  ```

### Other components configuration:
- Ingress:
  ```yaml
  apiVersion: networking.k8s.io/v1
  kind: Ingress
  metadata:
    name: myapp-ingress
  spec:
    rules:
    - host: mpapp.com
      http:
        paths:
        - backend:
          serviceName: myapp-internal-service
          servicePort: 8080
  ```
- Template YAML Config file:
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: {{ .Values.name}}
  spec:
    containers:
    - name: {{ .Values.container.name}}
      image: {{ .Values.container.image}}
      port: {{ .Values.container.port}}
  ```
  We can set values using `--set` flag from console or We can use a template file (`Values.yaml`) which would look like:
  ```yaml
  name: my-app
  container:
    name: my-app-container
    image: nginx
    port: 80
  ```
- Specification
  ```yml
  spec:
    replicas: 2
    selector:
      matchLabels:
        app: nginx
    template:
      metadata:
        labels:
          app: nginx
    ports: 
      - protocol: TCP
        port: 80
        targetPort: 8080
  ```
- Status: It will be auto generated by Kubernetes itself.
  ```yml
  status:
    availableReplicas:
    conditions:
  ```

## RBAC YAML Examples 
1. Role and RoleBinding (Namespace Scoped) 
  ```yaml
  apiVersion: rbac.authorization.k8s.io/v1
  kind: Role
  metadata:
    namespace: dev
    name: pod-reader
  rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["get", "list", "watch"]
  ```
  ```yaml
  apiVersion: rbac.authorization.k8s.io/v1
  kind: RoleBinding
  metadata:
    namespace: dev
    name: pod-reader-binding
  subjects:
  - kind: User
    name: alice
    apiGroup: rbac.authorization.k8s.io
  roleRef:
    kind: Role
    name: pod-reader
    apiGroup: rbac.authorization.k8s.io
  ```
2. ClusterRole and ClusterRoleBinding (Cluster-Wide Permissions)
  ```yaml
  apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRole
  metadata:
    name: cluster-admin
  rules:
  - apiGroups: ["*"]
    resources: ["*"]
    verbs: ["*"]
  ```
  ```yaml
  apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRoleBinding
  metadata:
    name: cluster-admin-binding
  subjects:
  - kind: User
    name: admin-user
    apiGroup: rbac.authorization.k8s.io
  roleRef:
    kind: ClusterRole
    name: cluster-admin
    apiGroup: rbac.authorization.k8s.io
  ```
3. Service Account
  ```yaml
  apiVersion: v1
  kind: ServiceAccount
  metadata:
    name: custom-service-account
    namespace: default
  ```
4. Use a Service Account in a Pod
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: my-pod
    namespace: default
  spec:
    serviceAccountName: custom-service-account
    containers:
      - name: app-container
        image: nginx
  ```


#### CRD Example:
```yml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: databases.example.com  # CRD name (must be plural)
spec:
  group: example.com  # API group
  scope: Namespaced  # Can be "Cluster" or "Namespaced"
  names:
    plural: databases  # Used in `kubectl get databases`
    singular: database
    kind: Database
    shortNames:
      - db
  versions:
    - name: v1
      served: true
      storage: true
      schema:
        openAPIV3Schema:
          type: object
          properties:
            spec:
              type: object
              properties:
                engine:
                  type: string
                  enum: ["mysql", "postgres"]
                version:
                  type: string
                storage:
                  type: integer
                  description: "Storage in GB"
```

### Example of Init Container  
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: init-container-example
spec:
  initContainers:
  - name: init-db
    image: busybox
    command: ['sh', '-c', 'until nslookup my-database-service; do echo waiting for database; sleep 2; done;']
  containers:
  - name: main-app
    image: nginx
    ports:
    - containerPort: 80
```

### Example of Sidecar Container
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sidecar-example
spec:
  containers:
  - name: main-app
    image: nginx
    ports:
    - containerPort: 80
  - name: log-collector
    image: busybox
    command: ['sh', '-c', 'tail -f /var/log/app.log']
    volumeMounts:
    - name: log-volume
      mountPath: /var/log
  volumes:
  - name: log-volume
    emptyDir: {}
```