# Kubernetes Commands and YAML Examples

## 1. Get Nodes

### Command:
```sh
kubectl get nodes
```

### Description:
This command lists all nodes in the Kubernetes cluster. It provides basic details about each node, such as its status, roles, age, and version.

### Example Output:
```sh
NAME           STATUS   ROLES    AGE    VERSION
node-1        Ready    master   10d    v1.25.0
node-2        Ready    worker   5d     v1.25.0
node-3        Ready    worker   5d     v1.25.0
```

### Explanation of Output:
- **NAME** → Name of the node.
- **STATUS** → Whether the node is Ready (healthy) or NotReady (unhealthy).
- **ROLES** → The role of the node (master or worker).
- **AGE** → How long ago the node was created.
- **VERSION** → Kubernetes version running on the node.

---

## 2. Get Pods

### Command:
```sh
kubectl get pods
```

### Description:
This command lists all running and pending pods in the current namespace.

### Example Output:
```sh
NAME         READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          2h
db-pod      0/1     Pending   0          5m
```

### Explanation of Output:
- **NAME** → The name of the pod.
- **READY** → How many containers are running in the pod vs. the total number of containers.
- **STATUS** → The current status (Running, Pending, CrashLoopBackOff, etc.).
- **RESTARTS** → Number of times the pod has restarted.
- **AGE** → How long the pod has been running.

---

## 3. Basic `pod.yaml` File

### Example: `pod.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: webserver
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
```

### Explanation:
- **apiVersion: v1** → The Kubernetes API version.
- **kind: Pod** → The type of resource.
- **metadata:** → Contains the pod’s name and labels.
- **spec:** → Defines the specification for the pod.
- **containers:** → Specifies the container(s) inside the pod.
- **image: nginx:latest** → The image for the container.
- **ports:** → Exposes port 80 inside the container.

### Apply the YAML file:
```sh
kubectl apply -f pod.yaml
```

---

## 4. Get Pods with More Details

### Command:
```sh
kubectl get pods -o wide
```

### Description:
This command provides additional details about the pods, including node name, IP addresses, and container images.

### Example Output:
```sh
NAME         READY   STATUS    RESTARTS   AGE   IP           NODE        NOMINATED NODE   READINESS GATES
nginx-pod   1/1     Running   0          2h    10.42.0.5    node-1      <none>           <none>
db-pod      0/1     Pending   0          5m    <none>       node-2      <none>           <none>
```

### Explanation of Additional Fields:
- **IP** → The internal IP of the pod.
- **NODE** → The node on which the pod is running.
- **NOMINATED NODE** → Shows if a node has been nominated for scheduling.
- **READINESS GATES** → If the pod has readiness conditions to meet.

---

## 5. Describe a Pod

### Command:
```sh
kubectl describe pod nginx-pod
```

### Description:
This command provides detailed information about a specific pod, including events, labels, IP, node, and status.

### Example Output (Truncated):
```sh
Name:         nginx-pod
Namespace:    default
Node:         node-1/192.168.1.10
Start Time:   Thu, 30 Mar 2023 14:00:00 +0530
Labels:       app=webserver
Status:       Running
IP:           10.42.0.5
Containers:
  nginx-container:
    Container ID:   docker://abcdef12345
    Image:          nginx:latest
    Ports:          80/TCP
    State:          Running
Events:
  Type    Reason     Age   From              Message
  ----    ------     ---   ----              -------
  Normal  Scheduled  2h    default-scheduler Successfully assigned nginx-pod to node-1
  Normal  Pulled     2h    kubelet           Container image "nginx:latest" already present on machine
```

### Key Information:
- **Node:** The node on which the pod is running.
- **Labels:** Labels assigned to the pod.
- **Status:** The pod's status.
- **IP:** The internal IP of the pod.
- **Events:** Logs of actions related to the pod.

---

# Kubernetes Commands and YAML Examples

## 1. Apply a Pod Configuration

### Command:
```sh
kubectl apply -f pod.yaml
```

### Description:
This command applies the configuration defined in `pod.yaml` to create or update a Pod in the Kubernetes cluster. If the Pod does not exist, it is created. If it already exists, Kubernetes updates it to match the new configuration.

### Why do we use `-f`?
The `-f` flag specifies the file containing the desired configuration. It tells Kubernetes to read from `pod.yaml` and apply the changes accordingly.

When you run `kubectl apply -f pod.yaml`, Kubernetes reads the file and ensures that the defined resources are created or updated accordingly.

---

## 2. Delete a Pod

### Command:
```sh
kubectl delete pod <pod-name>
```

### Description:
This command deletes the specified pod from the cluster. Once deleted, the pod cannot be recovered, but if a Deployment or ReplicaSet is managing the pod, Kubernetes may automatically recreate it.

### Example:
```sh
kubectl delete pod nginx-pod
```

### Explanation:
- **kubectl delete pod nginx-pod** → Deletes the `nginx-pod`.
- **If the pod is managed by a Deployment or ReplicaSet**, it will be recreated automatically.
- **If the pod is standalone**, it will be permanently removed.

After deletion, you can verify using:
```sh
kubectl get pods
```
This command lists remaining pods, confirming the deletion.


## 6. Labels and Selectors in Kubernetes

### Labels in Kubernetes
A label is a key-value pair attached to a Kubernetes resource (such as Pods, Nodes, or Services). Labels help identify and group related objects.

#### Syntax of Labels:
```yaml
labels:
  key: value
```

#### Example: Applying Labels to a Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: web-pod
  labels:
    app: webserver
    environment: production
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
```

### Viewing Labels on a Pod
```sh
kubectl get pods --show-labels
```

### Adding or Modifying Labels
Add a Label to an Existing Pod:
```sh
kubectl label pod web-pod team=frontend
```

Remove a Label:
```sh
kubectl label pod web-pod team-
```

---

## 7. Using Selectors in Services

### Example: `service.yaml`
```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-service
spec:
  selector:
    app: webserver
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

### Explanation:
- **selector:** Ensures this Service applies only to Pods with `app: webserver`.
- **port: 80** → Exposes the service on port 80.
- **targetPort: 80** → Routes traffic to Pods running on port 80.

---

## 8. Using Selectors in Deployments

### Example: `deployment.yaml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: webserver
  template:
    metadata:
      labels:
        app: webserver
    spec:
      containers:
      - name: nginx-container
        image: nginx:latest
```

### How It Works:
- The Deployment creates 3 Pods.
- All Pods are labeled `app: webserver`.
- The selector ensures that only Pods with `app: webserver` are managed by this Deployment.
