
## Prerequisites

- You have logged in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=1).
- You have deployed [Nginx-ingress Addon](https://intl.cloud.tencent.com/document/product/457/38981) in the cluster.
- You have installed and created the Nginx-ingress instance required for the business.

## How to Use

### Nginx-ingress usage on console

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. Click the cluster ID that has installed the Nginx-ingress addon to go to the cluster details page.
3. Select **Services and Route** > **Ingress** to go to the Ingress information page.
4. Click **Create** to go to the **Create an Ingress** page.
5. Set the Ingress parameters based on actual needs, as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/b43a14d57bab7b87d99f843ca8d30743.png)
 - Ingress type: select **Nginx Ingress Controller**.
 - Forwarding configuration: configure forwarding rules as needed.
6. Click **Create Ingress**.

### Managing Nginx-ingress using Kubectl


Before importing the IngressClass resource and the ingressClassName field in Kubernetes, the Ingress class was specified by the `kubernetes.io/ingress.class` annotation in Ingress.
Sample:

```
metadata:
  name: 
  annotations:
    kubernetes.io/ingress.class: "nginx-pulic". ## The corresponding Nginx-ingress instance name of the Nginx-ingress addon in the TKE cluster.
```


## Relevant Operations[](id:annotation)

You can configure annotations for Nginx Ingress objects. For details, see [Official Document](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/).

### Usage model of Nginx-ingress object

When multiple Ingress objects apply to one Nginx entity:
- Sort the Ingress rules by the CreationTimestamp field, that is, the previous rules shall prevail.
- If the same path is defined for the same host in multiple Ingresses, the most previous rules shall prevail.
- If multiple Ingresses contain the TLS part of the same host, the most previous rules shall prevail.
- If multiple Ingresses define an annotation that affects the configuration of the Server block, the most previous rules shall prevail.
- Create NGINX Server based on each hostname.
- If multiple Ingresses define different paths for the same host, the ingress-controller merges these definitions.
- Multiple Ingresses can define different annotations. These definitions are not shared among Ingresses.
- Ingress annotations will be applied to all paths in Ingress.

### Triggering nginx.conf update mechanism

The following describes the situation where nginx.conf needs to be reloaded:
- Create an Ingress object.
- Add a new TLS for Ingress.
- The modification of Ingress annotation not only affects the upstream configuration, but also has a greater impact. For example, the load-balance annotation does not need to be reloaded.
- Add/delete paths for Ingress.
- Delete Ingress and the Service and Secret of Ingress.
- The status of the object associated with the Ingress is unknown, such as Service or Secret.
- Update a Secret.
