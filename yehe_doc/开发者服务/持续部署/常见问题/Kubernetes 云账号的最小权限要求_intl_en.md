This document describes how to configure the minimum permissions required for Kubernetes cloud accounts in CODING.

## Prerequisites

You must activate the CODING DevOps service for your Tencent Cloud account before you can use Coding Continuous Deployment (CD). 

## Open Project

1. Log in to the [CODING console](https://console.cloud.tencent.com/coding) and click the team domain name to enter the CODING page.
2. On the Workspace homepage, click <img src ="https://main.qcloudimg.com/raw/12230547b45d5eae85ad1c4fa86fba68.png" style ="margin:0" data-nonescope="true"> on the left to go to the Continuous Deployment console.

### Feature description

If you want to release apps in a Kubernetes scenario (using a K8s account), CODING-CD must be able to call Kubernetes APIs. We do not recommend you grant all permissions for the Kubernetes cluster to CODING-CD. Using Kubernetes' Role Based Access Control (RBAC), you can grant CODING-CD the minimum permissions required to release apps. The following describes how to configure mini permissions.

#### Role

We recommend you create a `Role` in the namespace for which you will grant permissions and bind a `ServiceAccount` to the `Role`.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
 name: coding-cd-role
rules:
- apiGroups: [""]
  resources: ["namespaces", "configmaps", "events", "replicationcontrollers", "serviceaccounts", "pods/logs"]
  verbs: ["get", "list"]
- apiGroups: [""]
  resources: ["pods", "pods/portforward", "services", "services/proxy", "secrets"]
  verbs: ["*"]
- apiGroups: ["autoscaling"]
  resources: ["horizontalpodautoscalers"]
  verbs: ["list", "get"]
- apiGroups: ["apps"]
  resources: ["controllerrevisions", "statefulsets"]
  verbs: ["list"]
- apiGroups: ["extensions", "app", "apps"]
  resources: ["deployments", "replicasets", "ingresses", "daemonsets"]
  verbs: ["*"]
```

### Service Account

Next, create a `Service Account` for CODING-CD. The Continuous Deployment console uses the `Service Account` to interact with the Kubernetes cluster. You can use the following manifest to create a `Service Account`.

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
 name: coding-cd-service-account
 namespace: default
```

### Role Binding

Finally, create a `RoleBinding` to bind the above `coding-cd-role` to `coding-cd-service-account`.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
 name: coding-cd-role-
 namespace: webapp
roleRef:
 apiGroup: rbac.authorization.k8s.io
 kind: Role
 name: coding-cd-role
subjects:
- namespace: default
 kind: ServiceAccount
 name: coding-cd-service-account
```

