#API Server
-Every communication is done through API server. (Heart)
-The API Server is the heart of Kubernetes, coordinating all cluster operations and maintaining the link between components and etcd.(All communication between components goes through it: Kubelet, Controller Manager, Scheduler, and CLI tools like kubectl.)
#Control Manager
-is responsible for maintaining the cluster’s desired state by continuously comparing:
•	Desired State (DS) – what you want (e.g., number of pods, container specs)
•	Actual State (AS) – what is currently running in the cluster
If DS ≠ AS, the Controller Manager takes action to reconcile the difference.
It contains multiple controllers, for example:
•	ReplicaSet Controller – ensures the specified number of replicas/pods are running
•	StatefulSet Controller – manages stateful applications with stable network IDs
•	DaemonSet Controller – ensures a copy of a pod runs on each node
