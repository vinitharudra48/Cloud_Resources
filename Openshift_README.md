jumpserver
Cluster
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


# Pods - have one/more containers
