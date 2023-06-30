### Demo Application Overview
The demo application is an ecommerce website based on the Istio sample [Bookinfo](https://raw.githubusercontent.com/istio/istio/release-1.12/samples/bookinfo/platform/kube/bookinfo.yaml). It consists of six services:

- **frontend**: It is the website frontend that calls the user, product, cart, and order services.
- **product**: It is the product service that provides product information and has two editions with and without an advertising banner at the top.
- **user**: It is the user login service.
- **cart**: It is the cart service that allows adding items to the cart and viewing the cart and reports stock alarms after calling the stock service. An order can be placed after login.
- **order**: It is the order checkout service that has two editions with and without freight deduction based on points. After logging in, click **CHECKOUT** to start the checkout process, which needs to call the stock service to query the stock. An order cannot be placed if the stock is insufficient.
- **stock**. It is the stock service that provides stock information for stock alarming of the cart service and stock querying of the order checkout service.

#### Demo application architecture
![](https://qcloudimg.tencent-cloud.cn/raw/02031d18dc786306d8c1771493a09c9b.png)

#### Demo application homepage
![](https://qcloudimg.tencent-cloud.cn/raw/0e2a71adac0f270e5a92662b676e8c0a.png)


### Demo Application Installation
You can go to the Tencent Cloud Mesh demo repository at [GitHub](https://github.com/Tencent-Cloud-Mesh/mesh-demo) to get the demo application. As Tencent Cloud Mesh's automatic sidecar injection requires labeling the Istio version, you need to select a branch on the same version as Istio or modify the master branch, specifically, the version label of the base namespace in the `mesh-demo/yamls/step01-apps-zone-a.yaml` path:
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: base
  labels:
    istio.io/rev: 1-10-3
spec:
  finalizers:
    - kubernetes
```
For example, if your Istio version is 1.8.1, you need to change `istio.io/rev: 1-10-3` to `istio.io/rev: 1-8-1`; otherwise, sidecar injection will fail.

You can use the following command to quickly deploy the demo application:
```
kubectl apply -f yamls/step01-apps-zone-a.yaml
```


You can also go to the [TKE console](https://console.cloud.tencent.com/tke2/cluster), select **Cluster Details** > **Workload** > **Deployment**, select **Create Via YAML**, and copy the above YAML content to quickly create demo application resources.