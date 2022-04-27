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
![](https://qcloudimg.tencent-cloud.cn/raw/d187faff5e3352ae63296355bcde48e0.png)
3. Click **Complete**. To describe multi-cluster management, another cluster "cluster2" is registered.
![](https://qcloudimg.tencent-cloud.cn/raw/b91dc3b0244dac683f17afd389f83cc4.png)


## Step 4: Creating a Namespace

1. Log in to the [TDCC console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Namespace** on the left side. Click **Create** to create a namespace, for example, "nginx-test".
3. At the bottom of the page, you need to configure a distribution policy for this resource. You can select **Create distribution policy**, **Existing distribution policy** or **Do not associate with distribution policy**. Here, we select **Create distribution policy**.
4. Click **Select an existing cluster** and select the desired clusters. Distribution policies will be auto-created for them at the backend.
![](https://qcloudimg.tencent-cloud.cn/raw/142396d1c2858a430511560fa59c03f3.png)
5. Click **Create namespace** at the bottom of the page. On the namespace list page, you can see that the namespace is created.
![](https://qcloudimg.tencent-cloud.cn/raw/2a29fcebb2300f66f29311b82958158a.png)
6. Click the name of the created namespace to enter the details page, where you can view the basic information of the namespace, the associated distribution policy and the topology map. Click **Instance management**, you can see that the namespace has been deployed in multiple clusters.

 

## Step 5: Creating a Workload
>? The process of creating a workload and any K8s resource is largely the same as that of creating a namespace. You can configure a workload as needed.

1. Log in to the [TDCC console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Workload** > **Deployment** on the left side. Click **Create** to create a Deployment workload. In this sample, we will create a workload named “my-nginx”.
3. At the bottom of the page, you need to configure a distribution policy for the resource. Here, we select **Existing distribution policy**. Click the drop-down list and select the distribution policy created before.
 ![](https://qcloudimg.tencent-cloud.cn/raw/289d5ed6f91e05a66778842720581f41.png)
4. Click **Create workload** at the bottom of the page. On the workload list page, you can see that the workload is created.
 ![](https://qcloudimg.tencent-cloud.cn/raw/a18e6ab04d669b66bed26fa154b56e26.png)
5. Click the name of the created Deployment to enter the details page, where you can view the basic information of the Deployment, the associated distribution policy and the topology map. Click **Instance management**, you can see that the Deployment has been deployed in multiple clusters.
 ![](https://qcloudimg.tencent-cloud.cn/raw/a7b80c5f1583daac71b85d62061eb5d1.png)


## Step 6: Simulating a Canary Release

>? The nginx application has been released in two clusters. You can upgrade the image tag of nginx in one of the clusters and simulate the canary release.

1. Log in to the [TDCC console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click the workload “my-nginx” to enter the details page. Click **Instance management** tab, you can see that the workload has been deployed in multiple clusters.
 ![](https://qcloudimg.tencent-cloud.cn/raw/6b3f35914dacf843fb4de6f9c8dd6108.png)
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
![](https://qcloudimg.tencent-cloud.cn/raw/86835dd456c1bcf2876007a1f3e27b1a.png)
5. Click the cluster name to enter the cluster management page. You can see that the image tag of my-nginx has been upgraded to nginx:1.14.2. This means the localization configuration of the cluster has taken effect, and the canary upgrade of my-nginx has been implemented in this cluster.

