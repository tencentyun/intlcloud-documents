This document describes the cluster assets feature and how to view the details of clusters, Pods, Services, and Ingresses.
![](https://qcloudimg.tencent-cloud.cn/raw/924b5267259984da67c46c43d0551c1c.png)

## Viewing the Cluster Module
The cluster module displays the total number of clusters and the number of clusters of each type.

### Viewing the list of clusters
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Asset Management** on the left sidebar.
2. On the **Asset Management** page, click **Clusters** to enter the **Security Check** page and view all clusters.
![](https://qcloudimg.tencent-cloud.cn/raw/5fb66207dc0d1d99a596cac9e99436b1.png)
3. On the **Security Check** page, click the search box and search for clusters by keyword such as cluster name, ID, type, and region.
![](https://qcloudimg.tencent-cloud.cn/raw/6dc4430d80be2bd18fafc01d211eaf70.png)

### Custom list management
1. On the **Security Check** page, click ![](https://qcloudimg.tencent-cloud.cn/raw/131751ce4e643d8bc382f8b0bb316beb.png) to pop up the **Custom List Management** window.
2. In the pop-up window, select the target type and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/cb76f083f243b760442eb5311fd9e71f.png)

## Viewing the Pod Module
The Pod module displays the total number of cluster Pods and the numbers of running and pending Pods.

### Viewing the list of Pods
1. On the **Asset Management** page, click **Pods** to enter the Pod list page and view all Pods.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7293bb60448a089708a62d6ebd05578a.png" style="zoom:80%;" />
2. On the Pod list page, filter Pods by cluster name, namespace, or region; click **More filters** to filter them by Pod status, workload type, workload name, cluster ID, Pod IP, node IP, container name, container ID, or image name; or click the search box and search for Pods by Pod name.
![](https://qcloudimg.tencent-cloud.cn/raw/ec1218e09f2c650b8ffe913db6daccc3.png)
3. Find the target Pod and click the **Pod name** to pop up the drawer on the right, which displays the Pod details, including the basic Pod information, Service information, and container information.
![](https://qcloudimg.tencent-cloud.cn/raw/91636c57327aa64ac379ae67c45f5ebb.png)

### Custom list management
1. On the Pod list page, click ![](https://qcloudimg.tencent-cloud.cn/raw/131751ce4e643d8bc382f8b0bb316beb.png) to pop up the **Custom List Management** window.
2. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/751087386ce5677bea89a6558e1a9803.png" style="zoom:80%;" />

## Viewing the Service Module
The Service module displays the total number of cluster Services and the numbers of Services of the ClusterIP and NodePort types.

### Viewing the list of Services
1. On the **Asset Management** page, click **Services** to enter the Service list page and view all Services.
<img src="https://qcloudimg.tencent-cloud.cn/raw/5eabffc28ba9427a82f80b423a8c8410.png" style="zoom:80%;" />
2. On the Service list page, filter Services by cluster name, namespace, or region; click **More filters** to filter them by cluster ID, Service type, load balancer IP, Service IP, label, or port; or click the search box and search for Services by Service name.
![](https://qcloudimg.tencent-cloud.cn/raw/cc0baecfb0d27d6a37c2bb9272fed4a1.png)
3. Find the target Service and click the **Service name** to pop up the drawer on the right, which displays the Service details, including the basic Service information, Pod information, YAML information, and port mapping rules.
![](https://qcloudimg.tencent-cloud.cn/raw/3af7e3324dd3a4f4a5d174b5ce828d9a.png)

### Custom list management
1. On the Service list page, click ![](https://qcloudimg.tencent-cloud.cn/raw/131751ce4e643d8bc382f8b0bb316beb.png) to pop up the **Custom List Management** window.
2. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/5558fd9a87c2b7d099380f1a8f9cebb9.png" style="zoom:80%;" />

## Viewing the Ingress Module
The Ingress module displays the total number of cluster Ingresses.

### Viewing the list of Ingresses
1. On the **Asset Management** page, click **Ingresses** to enter the Ingress list page and view all Ingresses.
<img src="https://qcloudimg.tencent-cloud.cn/raw/4de8c84beb002b7f0052650a5e50f3f3.png" style="zoom:80%;" />
2. On the Ingress list page, filter Ingresses by cluster name, namespace, or region; click **More filters** to filter them by Ingress name, VIP, label, or backend service, or click the search box and search for Ingresses by Ingress name.
![](https://qcloudimg.tencent-cloud.cn/raw/349d3d3ab0343023feb6b50ba1e41987.png)
3. Find the target Ingress and click the **Ingress name** to pop up the drawer on the right, which displays the Ingress details, including the basic Ingress information, forwarding configuration, and YAML information.
![](https://qcloudimg.tencent-cloud.cn/raw/3229161beba3f95b003e5dee6a7e907f.png)


### Custom list management
1. On the Ingress list page, click ![](https://qcloudimg.tencent-cloud.cn/raw/131751ce4e643d8bc382f8b0bb316beb.png) to pop up the **Custom List Management** window.
2. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/336f38bdb675f2e8113d7621216d1bf8.png" style="zoom:80%;" />
