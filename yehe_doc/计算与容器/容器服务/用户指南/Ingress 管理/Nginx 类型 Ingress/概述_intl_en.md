

## Nginx Ingress Introduction

Nginx can be used as a reverse proxy, load balancer, and for HTTP caching.

Nginx-ingress is an Ingress controller for Kubernetes that uses NGINX as a reverse proxy and load balancer. You can deploy and use Nginx-ingress addon in the cluster. TKE provides productized capabilities to help you install and use Nginx-ingress in the cluster.

## Nginx-ingress Concepts

- **Nginx-ingress Addon**: you can use Nginx-ingress in TKE through Nginx-ingress addon. Install and deploy Nginx-ingress addon with one click on the **Addon Management** page.
- **Nginx-ingress Instance**: you can deploy multiple Nginx-ingress instances in a cluster (for example, one for the public network and one for the private network). Each instance corresponds to a CRD resource in Kubernetes. When an Nginx-ingress instance is created, Nginx-ingress-controller, service, configmap and other Kubernetes resources will be automatically created in the cluster.
- **Nginx-ingress-controller**: the actual Nginx load. The controller will watch the kubernetes ingress object and update the changes in the cluster. The forwarding configuration of Nginx load is the `nginx.conf` file.



## Nginx-ingress Relevant Operations

For details of Nginx-Ingress relevant operations and features, see the documents below:
- [Installing Nginx Ingress Instance](https://intl.cloud.tencent.com/document/product/457/38981)
- [Using Nginx-ingress Object to Access External Traffic of the Cluster](https://intl.cloud.tencent.com/document/product/457/38982)
- [Nginx-ingress Monitoring Configuration](https://intl.cloud.tencent.com/document/product/457/38984)
- [Nginx-ingress Log Configuration](https://intl.cloud.tencent.com/document/product/457/38983)

