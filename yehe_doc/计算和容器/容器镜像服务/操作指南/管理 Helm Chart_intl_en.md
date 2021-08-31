## Overview
Tencent Container Registry (TCR) can host Helm charts to meet users' requirements for hosting and distributing cloud-native applications. You can manage both container images and Helm charts in the same namespace so that cloud-native deliverables of both container images and Helm charts can be used in a business project.

Currently, only TCR Enterprise Edition instances support Helm chart hosting and uploading and downloading Helm charts in the console or a Helm client. Helm chart repositories inherit the public or private attribute from their namespaces, and no extra configuration is required. For permission management, Helm charts and container images share the **repository** resource type. This means the resource description <b> qcs::tcr:$region:$account:repository/tcr-xxxxxx/project-a/*</b> contains all image repositories and Helm charts in the "project-a" namespace. You can use these image repositories and Helm charts as needed during resource permission management. 


## Prerequisites
Before uploading and managing Helm charts in a TCR Enterprise Edition instance, complete the following tasks:
- [Purchasing Instances](https://intl.cloud.tencent.com/document/product/1051/39088).
- If you are using a sub-account, you must grant the sub-account required permissions for the instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Managing Helm charts in the console
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Helm Chart** in the left sidebar.
2. On the "Helm Chart" page, you can view the list of Helm charts in the current instance. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the page, as shown in the figure below:
![](https://main.qcloudimg.com/raw/9661ec41a9092b123498fee4a42c9685.png)
   The chart list contains the following information and operations:
   - **Name**: indicates the Helm chart name. You can click it to go to the chart details page, where you can view and manage chart versions. You can also view the details of files for each chart version on the "Basic Information" tab page.
   - **Namespace**: indicates the namespace to which a Helm chart belongs.
   - **Create Time**: indicates the time when the Helm chart is pushed to the repository for the first time.
   - **Operation**: you can click **Delete** to delete the current repository.
3. Click the specified Helm chart repository name to go to the details page of the repository.
	- **Version Management**: this page displays existing chart versions in the current repository. You can **Download** or **Delete** a specific version, as shown in the figure below:
![](https://main.qcloudimg.com/raw/bfdcb7b09f1e7e575b10f110c5b54b4b.png)
	- **Basic Information**: on this page, you can view the details of a specific chart version, such as Chart.yaml, as shown in the figure below:
	![](https://main.qcloudimg.com/raw/4ee02de5f33c1ceb16d22b57997bc45a.png)

### Using the console to upload and download Helm charts
#### Uploading a local Helm chart package
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Helm Chart** in the left sidebar.
On the "Helm Chart" page, you can view the list of Helm chart repositories in the current instance. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the page.
2. Click **Upload**. In the "Upload Helm Chart" window that appears, refer to the information shown in the figure below to configure the parameters:
![](https://main.qcloudimg.com/raw/411575f7b551915ca182c439921f9df3.png)
 - **Instance**: indicates the selected instance.
 - **Namespace**: indicates the namespace to which the Helm chart belongs. If the list is empty, [create a namespace](https://intl.cloud.tencent.com/document/product/1051/35487) in the instance.
 - **Chart package**: click and select a local Helm chart package that has been downloaded.
>! Only Helm chart packages in the .tgz format are supported. Do not upload other types of files. Note that uploading a file with the same name as an existing chart overwrites the existing chart. Therefore, exercise caution when uploading a file.

3. Click **Upload** to start uploading the Helm chart package. After the upload is completed, you can view the uploaded Helm chart package on the repository list page. If the uploaded Helm chart package does not have a corresponding Helm chart repository, a chart repository will be automatically created.

#### Downloading a Helm chart package to a local directory
1. On the "Helm Chart" page, view the list of Helm chart repositories in the current instance. Click a repository to go to the version management page of the Helm repository.
2. Select a version in the chart repository and click **Download** for the version to automatically download a chart package of this version to a local directory. For different browsers and configurations, you can select a download path as needed.


### Using a Helm client to upload and download Helm charts
#### Downloading a Helm client
>?
>- Note that, if you wish to use Helm in Tencent Kubernetes Engine (TKE), you must select version v3.x.x. You can run the `helm version -c` command to check the version of the installed client.
>- This document describes the installation process on a node in the Linux operating system. If you install the client on another platform, download the installation package for the platform. 

Run the following commands in sequence to download and install the Helm client. For more information on installing Helm, see [Installing Helm](https://helm.sh/docs/intro/install/).
```
 curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
```
```
chmod 700 get_helm.sh
```
```
./get_helm.sh
```

#### Adding a Helm repository
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select an instance name on the "Instance List" page to go to the instance details page.
<span id="Step2"></span>
2. Obtain the username and password for logging in to the instance. For more information, see [Obtaining an Instance Access Credential](https://intl.cloud.tencent.com/document/product/1051/37253).
3. Run the following command on the node to add the namespace for managing Helm charts to the local Helm repository.
>! Ensure that the server where this command is run is in the Internet allowlist or connected VPC of the instance. For more information, see [Public Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35491) and [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492).
>
```
helm repo add $instance-$namespace https://$instance.tencentcloudcr.com/chartrepo/$namespace --username $username --password $instance-token
```
 - `$instance-$namespace`: indicates the name of the Helm repository. We recommend that you name this Helm repository in the following format to differentiate instances and namespaces: **<Instance name> + <Namespace name>**.
 - `https://$instance.tencentcloudcr.com/chartrepo/$namespace`: indicates the remote address of the Helm repository.
    - `$username`: indicates the username obtained in [Step 2](#Step2).
    - `$instance-token`: indicates the login password obtained in [Step 2](#Step2).
The following information appears if the namespace has been added successfully.
```
"$instance-$namespace" has been added to your repositories
```

#### Pushing Helm charts
1. Installing the Helm Push plug-in
>! Please install the helm-push plug-in v0.9.0 or later to avoid push failure because of version incompatibility.

To use Helm CLI to upload a chart package, you must install the helm-push plug-in. This plug-in supports using the `helm push` command to push Helm charts to a specified repository. Both directories and compressed packages can be uploaded.
```
helm plugin install https://github.com/chartmuseum/helm-push
```
2. Run the following command on the node to create a chart.
```
helm create tcr-chart-demo
```
3. (Optional) Run the following command to push the specified directory to the chart repository.
```
helm push tcr-chart-demo $instance-$namespace
```
In the preceding commands, `$instance-$namespace` indicates the name of the local repository that has been added.
4. Run the following commands to compress the specified directory and push it to the chart repository.
```shell
tar zcvf tcr-chart-demo-1.0.0.tgz tcr-chart-demo/
```
```
helm push tcr-chart-demo-1.0.0.tgz $instance-$namespace
```
In the preceding commands, `$instance-$namespace` indicates the name of the local repository that has been added.


#### Pulling Helm charts
1. Run the following command on the node to obtain the latest chart information.
```
helm repo update
```
2. Run the following command to pull a Helm chart of the specified version.
```
helm fetch <Local repository name>/<Chart name> --version <Chart version>
```
In the following example, tcr-chart-demo 1.0.0 in the "project-a" namespace is pulled from the "tcr-demo" Enterprise Edition instance.
```
helm fetch tcr-demo-project-a/tcr-chart-demo --version 1.0.0
```
