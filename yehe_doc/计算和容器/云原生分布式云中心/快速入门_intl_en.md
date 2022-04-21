This document describes how to activate TDCC service, register a cluster, create an application and configure a distribution policy to implement multi-cloud and multi-cluster application management.

## Step 1: Signing up for a Tencent Cloud Account

If you already have a Tencent Cloud account, ignore this step.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:13px;">Sign up for a Tencent Cloud account</a></div>

## Step 2: Activating TDCC Service

For information on how to activate TDCC service, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/1144/45539).

### Service authorization

Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/), select **Tencent Cloud services** > **Tencent Kubernetes Engine Distributed Cloud Center** to enter the TDCC console. Activate TDCC service and grant permissions to it as prompted. If you have already granted permissions to TDCC service, skip this step.

>? TDCC is based on **Tencent Kubernetes Engine**. Click agree to grant permissions when requesting permissions from **Tencent Kubernetes Engine**.

<div style="background-color:#00A4FF; width: 150px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/tdcc" target="_blank"  style="color: white; font-size:13px;">Grant permissions to TDCC</a></div>

### Configure and activate the hub cluster

>? TDCC manages the registered sub-clusters by the hub cluster that is managed at the backend.

1. When you complete the authorization, you will be directed to the service activation page to configure the basic information, which will be used to configure the hub cluster.
  - **Available region**: Select the region for the hub cluster. Only Guangzhou is available currently. More regions will be available in the future.
  - **Availability zone**: Select availability zones for the hub cluster.
  - **Cluster network**: Select a subnet. An ENI is required when you access kube-apiserver of the hub cluster. Therefore, you need to set a VPC subnet. TKE will auto-create a proxy ENI in the selected subnet.
2. Click **Complete**. In a few minutes, you will enter the TDCC console automatically.

## Step 3: Registering a Cluster
1. Log in to the [TDCC console](https://console.cloud.tencent.com/tdcc). Click **Distributed Basic Infrastructure** > **Cluster** in the left sidebar.
2. Click **Register an existing cluster**. Register a cluster named "cluster1". You can register a **TKE cluster** or a **non-TKE cluster**. For details, see [Registering a Cluster](https://intl.cloud.tencent.com/document/product/1144/45543).
![](https://qcloudimg.tencent-cloud.cn/raw/adfbc815cbaaf4bdc52311ef214206e7.png)
3. Click **Complete**. To describe multi-cluster management, another cluster "cluster2" is registered.
![](https://qcloudimg.tencent-cloud.cn/raw/1b4278ee231f2910efd3fb6780f1ef32.png)


## Step 4: Creating a Namespace

1. Log in to the [TDCC console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Namespace** on the left side. Click **Create** to create a namespace, for example, "nginx-test".
3. At the bottom of the page, you need to configure a distribution policy for this resource. You can select **Create distribution policy**, **Existing distribution policy** or **Do not associate with distribution policy**. Here, we select **Create distribution policy**.
4. Click **Select an existing cluster** and select the desired clusters. Distribution policies will be auto-created for them at the backend.
![](https://qcloudimg.tencent-cloud.cn/raw/8fc50845a38454974391f9fc35d0a071.png)
5. Click **Create namespace** at the bottom of the page. On the namespace list page, you can see that the namespace is created.
![](https://qcloudimg.tencent-cloud.cn/raw/82becc070caf97144262c47faf88dc31.png)
6. Click the name of the created namespace to enter the details page, where you can view the basic information of the namespace, the associated distribution policy and the topology map. Click **Instance management**, you can see that the namespace has been deployed in multiple clusters.

 

## Step 5: Creating a Workload
>? The process of creating a workload and any K8s resource is largely the same as that of creating a namespace. You can configure a workload as needed.

1. Log in to the [TDCC console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Workload** > **Deployment** on the left side. Click **Create** to create a Deployment workload. In this sample, we will create a workload named “my-nginx”.
3. At the bottom of the page, you need to configure a distribution policy for the resource. Here, we select **Existing distribution policy**. Click the drop-down list and select the distribution policy created before.
 ![](https://qcloudimg.tencent-cloud.cn/raw/9e9dcc4261c9167dbbac52132fd3cefc.png)
4. Click **Create workload** at the bottom of the page. On the workload list page, you can see that the workload is created.
 ![](https://qcloudimg.tencent-cloud.cn/raw/b4cc6dc47d03cac2bdbc421e2fbc3681.png)
5. Click the name of the created Deployment to enter the details page, where you can view the basic information of the Deployment, the associated distribution policy and the topology map. Click **Instance management**, you can see that the Deployment has been deployed in multiple clusters.
 ![](https://qcloudimg.tencent-cloud.cn/raw/7891bfa58ff81865c8c491fbfde125c6.png)


## Step 6: Simulating a Canary Release

>? The nginx application has been released in two clusters. You can upgrade the image tag of nginx in one of the clusters and simulate the canary release.

1. Log in to the [TDCC console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click the workload “my-nginx” to enter the details page. Click **Instance management** tab, you can see that the workload has been deployed in multiple clusters.
 ![](https://qcloudimg.tencent-cloud.cn/raw/4fa34712173e524023dfc177ed17e7cb.png)
3. Select an instance in one of the clusters. Click **Create localization policy** and configure the policy in the pop-up dialog box. In this sample, we upgrade the image tag of the instance to “nginx:1.14.2”. For more information on localization policy, see [Localization Policy](https://intl.cloud.tencent.com/document/product/1144/45548).
```yaml
apiVersion: apps.clusternet.io/v1alpha1
kind: Localization
metadata:
  labels:
    f07d0bec-fac8-4ed1-b4e5-1e2f00111111: Deployment
  name: my-nginx-overrides
  namespace: clusternet-b5vgv
spec:
  priority: 300
  feed:
    apiVersion: apps/v1
    kind: Deployment
    name: my-nginx
    namespace: nginx-test
  overridePolicy: ApplyLater
  overrides:
    - name: update-image-version
      type: JSONPatch
      value: |-
              - path: "/spec/template/spec/containers/0/image"
                value: "nginx:1.14.2"
                op: replace

```
4. Click **Complete** at the bottom of the page. On the instance list page, you can see that the localization policy is created.
![](https://qcloudimg.tencent-cloud.cn/raw/a66bf2cfd8c57464693cfdf4257f2393.png)
5. Click the cluster name to enter the cluster management page. You can see that the image tag of my-nginx has been upgraded to nginx:1.14.2. This means the localization configuration of the cluster has taken effect, and the canary upgrade of my-nginx has been implemented in this cluster.
![](https://qcloudimg.tencent-cloud.cn/raw/a1312be97501302949e7ea0fd7fc722d.png)
