jumpserver
# Cluster

An OpenShift cluster is a group of master and worker nodes that work together to run containerized applications. The control plane manages the cluster, while worker nodes run the workloads (pods). A cluster provides scalability, high availability, networking, storage, and security for all workloads.

<img width="259" height="188" alt="image" src="https://github.com/user-attachments/assets/b9a5c30a-1d8e-4cca-887d-143a1e72dd49" />

In OpenShift, the load balancer (LB) sits in front of the control plane and routes traffic to the master nodes.

Each worker has:

kubelet

kube-proxy

CRI-O (container runtime)

# Projects and Namespaces 

namespace = Kubernetes term (technical, basic)

Project = OpenShift term (namespace + extras)


A Namespace is a logical isolation boundary in Kubernetes used to group and isolate resources.

Key Technical Points:

Core Kubernetes resource (apiVersion: v1, kind: Namespace)

Provides resource isolation and scoping

Supports ResourceQuotas and LimitRanges

Applies NetworkPolicies per namespace

RBAC operates at namespace scope

Names must be unique within a cluster

Does not contain extra metadata like display names

#oc get ns

Shows raw Kubernetes namespaces

Includes system namespaces (openshift-, kube-, etc.)

A Project is an OpenShift-specific wrapper around a Kubernetes Namespace that adds additional metadata, RBAC defaults, and UI-friendly attributes.

Key Technical Points:

OpenShift API resource (project.openshift.io)

Automatically creates an underlying Namespace

Adds:

Display name

Description

Annotations & labels

Default RBAC bindings (admin, edit, view roles)

Integrates with OpenShift OAuth and user permissions

Shown in OpenShift Console as a “Project”

#oc get projects

Shows OpenShift projects

May hide some system namespaces depending on RBAC


# Nodes

node in OpenShift is basically a machine (server or VM) in the cluster where OpenShift runs workloads and system components.

👉 Think of a node as a worker in a factory.The cluster is the entire factory.

Each node has a role:

Some nodes manage the cluster → control‑plane/master nodes

Some nodes run applications → worker nodes

oc get nodes -o wide

oc describe node <node-name>

oc adm top nodes  # gives cpu and memory usage of nodes

# Pods - have one/more containers

A Pod is the smallest deployable unit in Kubernetes/OCP.
👉 Think of a Pod as a box that contains one or more containers that always run together.

✔ Pod has its own IP

Each Pod gets an IP from the cluster network.

✔ Pod is ephemeral

If a pod crashes, Kubernetes creates a new one with a different IP.

So pod IPs are NOT permanent.

✔ Pod run inside a Node

Scheduler decides which node.

✔ Pod is controlled by higher-level objects:

Deployment

StatefulSet

DaemonSet

ReplicaSet

You should NOT create pods manually for apps in production.

oc get pods -A

oc get pods -A -o wide

oc describe pod <pod-name>

oc get pod <pod-name> -o yaml

oc exec -it <pod-name> -- bash

oc logs -f <pod-name>

Pods cannot be restarted directly.

You restart the deployment:  oc rollout restart deployment <deployment-name>

You restart the statefulset:    oc rollout restart statefulset <sts-name>

oc delete pod <pod-name>

oc debug pod/<pod-name>


# Pod lifecycle events:

Pending → Pod accepted, waiting for scheduling

Scheduled → Assigned to a node

ContainerCreating → Images pulled, volumes attached

Running → Pod is healthy and serving

CrashLoopBackOff → Container keeps crashing

ImagePullBackOff / Error → Image issues

Terminating → Pod shutting down

Succeeded → Completed and exited 0

Failed → Pod finished with errors






