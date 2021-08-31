## Introduction
### Add-on description
Nginx can be used as a reverse proxy, load balancer, and HTTP buffer. The Nginx-ingress add-on is an Ingress controller for Kubernetes that uses Nginx as a reverse proxy and load balancer. You can deploy and use the Nginx-ingress add-on in your cluster.

### Kubernetes objects deployed in a cluster
Deploying the Nginx-ingress add-on in a cluster will deploy the following Kubernetes objects in the cluster:

| Kubernetes Object Name | Type | Default Resource Occupation | Namespaces |
| --------------------- | ---------- | ------ | ------------ |
| nginx-ingress | Service | - | Custom |
| nginx-ingress | Configmap | - | Custom |
| tke-ingress-nginx-controller-operator | Deployment | 0.13-core CPU, 128 MB memory | kube-system |
| ingress-nginx-controller | Deployment/DaementSet | 0.1-core CPU | kube-system |
| ingress-nginx-controller-hpa | HPA | - | kube-system |

## Prerequisites
- We recommend that you use Kubernetes 1.12 or later.
- We recommend that you use the TKE [node pool feature](https://intl.cloud.tencent.com/document/product/457/35900).
- We recommend that you use TKE cloud native monitoring.
- We recommend that you use [Tencent Cloud CLS](https://intl.cloud.tencent.com/document/product/614).





## Usage
- [Nginx-ingress Overview](https://intl.cloud.tencent.com/document/product/457/38980)
- [Installing Nginx-ingress](https://intl.cloud.tencent.com/document/product/457/38981)
- [Using Nginx-ingress Object to Access External Traffic of the Cluster](https://intl.cloud.tencent.com/document/product/457/38982)
- [Nginx-ingress Monitoring Configuration](https://intl.cloud.tencent.com/document/product/457/38984)
- [Nginx-ingress Log Configuration](https://intl.cloud.tencent.com/document/product/457/38983)
