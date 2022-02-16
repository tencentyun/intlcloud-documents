## Overview

This document describes how to authorize API Gateway to access the API server of a TKE cluster, offers solutions to authorization issues, and lists the permissions obtained by API Gateway in an YAML file.

## Prerequisites

1. You have logged in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index).
2. You have an TKE cluster and have obtained its admin role.

## Directions

- In the TKE tunnel configuration of API Gateway, if you reference a TKE cluster for the first time, you need to grant API Gateway the access to the cluster's API server and ensure that the cluster has private network access enabled.

 When the TKE tunnel is configured, the API Gateway system will automatically check whether the cluster has been authorized, and if not, it will prompt you for authorization.
![](https://qcloudimg.tencent-cloud.cn/raw/2a5a13b6626f9975394c3a83b27d2d71.png)        

- If the cluster access has already been granted to API Gateway, the system will display **Authorized API Gateway**. Each cluster only needs to be authorized for API Gateway once and doesn't require repeated authorizations for subsequent operations.                 
<img src="https://qcloudimg.tencent-cloud.cn/raw/51688fa680387191c838fcf6dbe0ba23.png" width="450px">      

## How It Works

The process for API Gateway to get the authorization is as follows:

1. Under the `kube-system` namespace, create a ServiceAccount named `apigw-ingress` and a ClusterRole named `apigw-ingress-clusterrole`.

2. Bind `apigw-ingress` and `apigw-ingress-clusterrole` through ClusterRoleBinding. Then, the permission of the `apigw-ingress` ServiceAccount is obtained by API Gateway to access the API server of the cluster.

   The permission of the `apigw-ingress` ServiceAccount is stored in the Secret prefixed with `apigw-ingress-token-`.

For more information on the permissions obtained by API Gateway and the specific method, see the YAML used to create resources:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: apigw-ingress-clusterrole
rules:
  - apiGroups:
      - ""
    resources:
      - services
      - namespaces
      - endpoints
      - nodes
      - pods
    verbs:
      - get
      - list
      - watch
  - apiGroups:
      - apps
    resources:
      - deployments
      - replicasets
    verbs:
      - get
      - list
      - watch
  - apiGroups:
      - ""
    resources:
      - configmaps
      - secrets
    verbs:
      - "*"
  - apiGroups:
      - extensions
    resources:
      - ingresses
      - ingresses/status
    verbs:
      - "*"
  - apiGroups:
      - ""
    resources:
      - events
    verbs:
      - create
      - patch
      - list
      - update
  - apiGroups:
      - apiextensions.k8s.io
    resources:
      - customresourcedefinitions
    verbs:
      - "*"
  - apiGroups:
      - cloud.tencent.com
    resources:
      - tkeserviceconfigs
    verbs:
      - "*"
---
apiVersion: v1
kind: ServiceAccount
metadata:
  namespace: kube-system
  name: apigw-ingress
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: apigw-ingress-clusterrole-binding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: apigw-ingress-clusterrole
subjects:
  - kind: ServiceAccount
    name: apigw-ingress
    namespace: kube-system
```

## Notes

After you successfully grant API Gateway the access to the TKE cluster, you cannot modify the resources reserved by API Gateway, including:

- The ServiceAccount named `apigw-ingress` under the `kube-system` namespace.
- The ClusterRole named `apigw-ingress-clusterrole` under the `kube-system` namespace.
- The ClusterRoleBinding named `apigw-ingress-clusterrole-binding` under the `kube-system` namespace.
- The Secret prefixed with `apigw-ingress-token-` in the `kube-system` namespace.



## FAQs

**Problem**: during authorization, it is found that the private network access feature is not enabled for the TKE cluster.
<img src="https://qcloudimg.tencent-cloud.cn/raw/5f87b05a0ceb35b43cb881634687ba55.png" width="450px">              

**Solution**: [enable the TKE cluster's private network access feature](https://intl.cloud.tencent.com/document/product/628/44309) and then click **Retry**.
