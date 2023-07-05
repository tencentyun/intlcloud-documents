## Overview
Tencent Container Registry (TCR) can host Helm charts to meet users' requirements for hosting and distribution of cloud native applications. You can manage both container images and Helm charts in the same namespace so that cloud native deliverables of both container images and Helm charts can be used in a business project.

Currently, only TCR Enterprise Edition instances support Helm chart hosting and the use of the console or a Helm client to upload and download Helm charts. Helm chart repositories inherit the public or private attribute from their namespaces, and no extra configuration is needed. In terms of permission management, Helm charts and container images share the **repository** resource type. That is, the resource description <b> qcs::tcr:$region:$account:repository/tcr-xxxxxx/project-a/*</b> contains all image repositories and Helm charts in the "project-a" namespace. You can flexibly use these image repositories and Helm charts during resource permission management. 


## Prerequisites
Before uploading and managing Helm charts in a TCR Enterprise Edition instance, complete the following tasks:
- [Create an Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/39088).
- If you are using a sub-account, you must have granted the sub-account required permissions for the instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Managing Helm charts in console
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Helm Chart** on the left sidebar.
2. On the **Helm Chart** page, you can view the list of Helm charts for the current instance. To change the instance, select the desired instance name from the **Instance Name** drop-down list at the top of the page, as shown in the figure below:
![](https://main.qcloudimg.com/raw/9661ec41a9092b123498fee4a42c9685.png)
   The chart list contains the following information and operations:
   - **Name**: Helm chart name. You can click it to enter the chart details page, where you can view and manage each version of the chart. You can also view the file details of each version of the chart package in the **Basic Information** tab.
   - **Namespace**: namespace to which the Helm chart belongs.
   - **Creation Time**: time when the Helm chart is pushed to the repository for the first time.
   - **Operation**: click **Use commands** to obtain the quick commands for manipulating the current repository, or click **Delete** to delete the current repository.
3. Click the name of the specified Helm chart repository to enter the repository details page.
	- **Tag Management**: this page displays the existing chart versions in the current repository, and you can **download** or **delete** the specified versions, as shown in the figure below:
![](https://main.qcloudimg.com/raw/bfdcb7b09f1e7e575b10f110c5b54b4b.png)
	- **Basic Information**: this page allows you to browse the detailed information of the specified chart version, such as Chart.yaml, as shown in the figure below:
		![](https://main.qcloudimg.com/raw/4ee02de5f33c1ceb16d22b57997bc45a.png)

### Using the console to upload and download Helm charts
#### Uploading a local Helm chart package
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Helm Chart** on the left sidebar.
On the **Helm Chart** page, you can view the list of Helm chart repositories for the current instance. To change the instance, select the desired instance name from the **Instance Name** drop-down list at the top of the page.
2. Click **Upload**. In the **Upload Helm Chart** window, configure based on the following information, as shown in the figure below:
![](https://main.qcloudimg.com/raw/411575f7b551915ca182c439921f9df3.png)
 - **Associated Instance**: the current instance selected.
 - **Namespace**: the namespace to which the Helm chart belongs. If the list is empty, please first [create namespaces](https://intl.cloud.tencent.com/document/product/1051/35487) in the instance.
 - **Chart Package**: click to select a Helm chart package that has been downloaded to the local system.
>! Only Helm chart packages in .tgz format are supported. Please avoid uploading other types of files. Uploading a file will overwrite the existing chart with the same name; therefore, please do so with caution.
>
3. Click **Upload** to start uploading the Helm chart package. After uploading, you can view the uploaded Helm chart on the repository list page. If the uploaded package does not have a corresponding Helm chart repository, a new repository will be created automatically.

#### Downloading a Helm chart package to the local system
1. View the Helm chart repository list in the current instance on the **Helm Chart** page. Click the specified repository to enter its tag management page.
2. Select the specified version in the chart repository, click **Download** on the right of the row where the version is located, and the chart package on this version will be automatically downloaded to the local system. Depending on the browser and configuration, you can choose to specify the download path.


### Using the Helm client to upload and download Helm charts
#### Downloading the Helm client
>?
>- If you want to use Helm in Tencent Kubernetes Engine (TKE), you need to select the Helm v3.x.x version. You can run the `helm version -c` command to check the version of the installed client.
>- This document takes the installation on a Linux node as an example. For installation on other platforms, please download the corresponding installation package. 
>
Run the following commands in sequence to download and install the Helm client. For more information, see [Installing Helm](https://helm.sh/docs/intro/install/).
```
 curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
```
```
chmod 700 get_helm.sh
```
```
./get_helm.sh
```

### Adding a Helm repository
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select an instance name on the **Instance List** page to enter the instance details page.
2. [](id:Step2)Obtain the username and login password as instructed in [Obtaining an Instance Access Credential](https://intl.cloud.tencent.com/document/product/1051/37253).
3. Run the following command in the node to add the namespace used for Helm chart management to the local Helm repository.
>!The server running the command must be in the public network allowlist of the corresponding instance or in the linked VPC. For more information, see [Public Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35491) and [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492).
>
```
helm repo add $instance-$namespace https://$instance.tencentcloudcr.com/chartrepo/$namespace --username $username --password $instance-token
```
 - `$instance-$namespace`: name of the Helm repository. We recommend that you use the combination of **instance name+namespace name** for naming so as to distinguish between instances and namespaces.
 - `https://$instance.tencentcloudcr.com/chartrepo/$namespace`: remote address of the Helm repository.
    - `$username`: the username obtained in [step 2](#Step2).
    - `$instance-token`: the login password obtained in [step 2](#Step2).
If the addition is successful, the following message will be prompted.
```
"$instance-$namespace" has been added to your repositories
```

#### Pushing Helm charts
1. Install the Helm Push plugin.
>! Please install the helm-push plugin on version 0.9.0 or above so as to prevent Helm chart push exceptions caused by version incompatibility and other issues.
>
To upload chart packages on Helm CLI, you need to install the helm-push plugin. The plugin supports using the `helm push` command to push Helm charts to the specified repository, as well as uploading directories and compressed packages.
```
helm plugin install https://github.com/chartmuseum/helm-push
```
2. Run the following command on the node to create a chart.
```
helm create tcr-chart-demo
```
3. Run the following command to directly push the specified directory to the chart repository (optional).
```
helm push tcr-chart-demo $instance-$namespace
```
Here, `$instance-$namespace` is the name of the added local repository.
4. Run the following command to compress the specified directory and push it to the chart repository.
```shell
tar zcvf tcr-chart-demo-1.0.0.tgz tcr-chart-demo/
```
```
helm push tcr-chart-demo-1.0.0.tgz $instance-$namespace
```
Here, `$instance-$namespace` is the name of the added local repository.


#### Pulling Helm charts
1. Run the following command on the node to obtain the latest chart information.
```
helm repo update
```
2. Run the following command to pull the Helm chart on the specified version:
```
helm fetch <local repository name>/<chart name> --version <chart version>
```
In the following example, tcr-chart-demo 1.0.0 in the "project-a" namespace is pulled from the "tcr-demo" Enterprise Edition instance.
```
helm fetch tcr-demo-project-a/tcr-chart-demo --version 1.0.0
```
