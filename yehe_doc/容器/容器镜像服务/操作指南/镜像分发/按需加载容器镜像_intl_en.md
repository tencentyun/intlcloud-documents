## Overview

When using container images to deploy and update business applications, the traditional scheme is to download and decompress the full amount of container image data. On the one hand, it takes a long time to start the container. On the other hand, it may also cause large network and disk read and write pressure due to the large scale of the cluster and the download and decompression process, which leads to large-scale container startup, failing to meet deployment expectations. In fact, container startup may use only part of the data inside the container image.
TCR Enterprise supports on-demand loading of container images. During business deployment, you can use converted accelerated image tags to download image data without full loading and decompress the data online, greatly improving application distribution efficiency for ultimate elastic experience. This document introduces how to load container images on demand.

## Prerequisites
- You have [created a container cluster](https://intl.cloud.tencent.com/document/product/457/30637). Currently, the on-demand loading feature is available only to Tencent Cloud TKE clusters that meet the following requirements:

  - The cluster Kubernetes version is 1.16 or later.

  - The cluster runtime add-on is Containerd v1.4.3. You can modify the runtime configuration of an existing cluster to Containerd v1.4.3, so that the nodes added after the modification will default to this version.

  - The cluster OS is Ubuntu, TencentOS, or CentOS. If the cluster OS is CentOS, you need to run the `yum install -y fuse` command on the cluster nodes to install FUSE.

- You have [purchased a TCR Enterprise instance](https://intl.cloud.tencent.com/document/product/1051/35486) with premium specification. The feature of loading container images on demand can be enabled only for a **premium instance**.

- The VPC of the container cluster is connected to the TCR Enterprise instance, and the cluster nodes can access the images in the instance via the private network. For the configuration details, see [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492).


## Preparing accelerated images

### Enabling image acceleration
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Image Acceleration** in the left sidebar.

2. On the **Image Acceleration** page, select the region and name of the instance for which image acceleration is to be enabled, and you can view the status of the current instance image acceleration and the list of image acceleration rules.

3. Click **Enable Image Acceleration**. In the **Activate Image Acceleration** window that pops up, read the notes carefully. 
 - Once image acceleration is enabled, a new OCI format compatible accelerated image is generated after you upload a container image that complies with the acceleration rules.
   
 - Note that after this feature is enabled and used, storing both general and accelerated images will incur additional image storage costs.
   
4. Click **Conform**.


### Adding an image acceleration rule
1. Click **Add Image Acceleration Rule**. In the **Create Image Acceleration Rule** window that pops up, configure a rule as prompted. 

  - **Name**: Rule name.

  - **Description**: Rule description.

  - **Triggering Rule**:

    - **Triggered Instance**: The currently selected instance is the triggered instance.

    - **Namespace**: Namespace whose distribution needs to be accelerated within the current instance. Currently, you cannot select all namespaces.

    - **Repository Name**: Accelerated repository. You can use a regular expression to filter repositories. If this parameter is not specified, all repositories in the namespace are selected by default.

    - **Tag**: Accelerated tag. You can use a regular expression to filter tags. If this parameter is not specified, all tags in the repositories that meet the requirements are selected by default.

  - **Validate Rule**: Enter the address of the image to be accelerated to check whether the image under the current triggering rule meets the acceleration rule.

2. Click **OK**.


### Pushing the image and automatically converting it

Check the added image acceleration rule on the **Image Acceleration** page. If the rule is enabled, push the new container image to the image repository that meets the rule. This will automatically trigger the image format conversion, and an accelerated image with the -apparate suffix will be generated. The default image artifact type is Docker-Image. After the conversion, the image artifact type is OCI-Image-v1.


## Deploying an Acceleration Image

Tencent Kubernetes Engine (TKE) is a Kubernetes managed service that works closely with TCR. You can install the TCR acceleration application in a TKE cluster and deploy an acceleration image to increase the business startup speed.

### Configuring cluster nodes

Cluster nodes do not support acceleration images by default. To enable a cluster node to use an acceleration image with priority, add the image acceleration label to the cluster node via CLI or TKE console.

<dx-tabs>
::: Adding the Image Acceleration Label via CLI
Run the following command to add the image acceleration label to a cluster node:
``` bash
kubectl label node xxx cloud.tencent.com/apparate=true
```
:::
::: Adding the Image Acceleration Label via TKE Console
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the cluster that requires image acceleration for distribution to go to the cluster details page.
3. Select the ID/name of the cluster for which to set the node label to go to the cluster details page.
4. In the left sidebar, select **Node Management** > **Nodes** to go to the **Node List** page.
5. Click **More** > **Edit Label** on the right of the target node.
6. In the **Edit Label** window that pops up, edit the label as `cloud.tencent.com/apparate=true` and click **Submit**.
:::
</dx-tabs>

### Installing the acceleration application

A cluster does not support the use of acceleration images by default, so you need to install the TCR acceleration suite application on the cluster. After the TCR acceleration suite application is installed, the nodes that have been labeled as supporting the deployment of acceleration images will automatically deploy the DaemonSet process and can load the acceleration images normally.
After the TCR acceleration suite application is installed, if you add a node and label it `cloud.tencent.com/apparate=true`, the node will also automatically deploy the DaemonSet process and can load acceleration images normally.

#### Installing the TCR acceleration suite application via CLI
1. Install the Helm V3 CLI tool. For details, see [Using the Helm client to upload and download Helm Charts](https://intl.cloud.tencent.com/document/product/1051/35493).

2. Add the Helm repository and pull the TCR acceleration application Chart package.

   ``` bash
   helm repo add tcr-helm-public https://helmhub.tencentcloudcr.com/chartrepo/public
   helm pull tcr-helm-public/apparate --version 1.0.0
   ```
3. Decompress the downloaded Chart package and modify `values.yaml`.

   ``` bash
   tar -xzvf apparate-1.0.0.tgz  
   vim apparate/values.yaml
   ```

   Configure the following parameters:

  1. `imagePullSecretsCrs`: This configuration is used for pulling acceleration images. You need to set `dockerUsername`, `dockerPassword`, and `dockerServer` to specify the TCR Enterprise instance username, password, and access domain respectively.

  2. `image`: Retain the default value. This configuration is used for pulling basic images during application installation on a cluster. If the cluster is not deployed in the Chinese mainland, change the value to the access domain name of the TCR Individual image repository in the corresponding region.

4. Build the Chart package again and install it to the specified cluster.

   ``` bash
   helm package apparate/
   helm install apparate apparate-1.0.0.tgz
   ```

   Before running the `helm install` command, you need to configure the cluster access credentials locally in advance. For details, see [Connecting to a Cluster Using the Local Helm Client](https://intl.cloud.tencent.com/document/product/457/30684).

5. Go to the [cluster application](https://console.cloud.tencent.com/tke2/helm) page and confirm the application's installation status and configuration.


### Deploying an acceleration image

When creating a workload, select an image within the current instance. Only when the following conditions are met, the cluster loads the image on demand to quickly start the container:
- The container image specified for the workload is a converted acceleration image, such as `nginx:latest-apparate`, and its artifact type is OCI-Image-v1.

- The image acceleration label `cloud.tencent.com/apparate=true` is added to the node to which the workload Pod is scheduled.


   Therefore, when creating a workload, select an accelerated image tag, add nodeSelector, and set `cloud.tencent.com/apparate=true` so that the workload will be scheduled to a node that supports accelerated images to implement accelerated startup.


## FAQs

#### Can I delete regular and accelerated images?

Yes. When both regular and accelerated images exist in the repository, deleting one will not affect the pull and deployment of the other.

#### What should I do if no accelerated image is generated automatically after image push?

Check if the image matches the existing acceleration rules. If you are sure that the image meets the acceleration rules in the enabled state, you can [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for help.