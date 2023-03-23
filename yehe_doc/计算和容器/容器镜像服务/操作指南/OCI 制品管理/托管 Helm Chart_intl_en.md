## Overview
Tencent Container Registry (TCR) can host Helm Charts to meet users' requirements for hosting and distribution of cloud native applications. You can manage both container images and Helm Charts in the same namespace so that cloud native deliverables of both container images and Helm Charts can be used in a business project.

Currently, only TCR Enterprise Edition instances support Helm Chart hosting and the use of the console or a Helm client to upload and download Helm Charts. Helm Chart repositories inherit the public or private attribute from their namespaces, and no extra configuration is needed. In terms of permission management, Helm Charts and container images share the **repository** resource type. This means the resource description <b> qcs::tcr:$region:$account:repository/tcr-xxxxxx/project-a/*</b> contains all image repositories and Helm Charts in the "project-a" namespace. You can flexibly use these image repositories and Helm Charts during resource permission management. 


## Prerequisite
Before uploading and managing Helm Charts in a TCR Enterprise Edition instance, complete the following tasks:
- [Purchasing Instances](https://intl.cloud.tencent.com/document/product/1051/39088).
- If you are using a sub-account, you must have granted the sub-account required permissions for the instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Managing Helm Charts in the console
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Helm Chart** in the left sidebar.
2. On the "Helm Chart" page, you can view the list of Helm Charts in the current instance. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the page, as shown in the figure below.
   ![](https://main.qcloudimg.com/raw/9661ec41a9092b123498fee4a42c9685.png)
   The Chart list contains the following information and operations:
   - **Name**: Helm Chart name. You can click it to enter the Chart details page, where you can view and manage each version of the Chart. You can also view the file details of each version of the Chart package in the **Basic Information** tab.
   - **Namespace**: namespace to which a Helm Chart belongs.
   - **Create Time**: time when the Helm Chart is pushed to the repository for the first time.
   - **Operation**: click **Use commands** to obtain the commands for operating the current repository. For more information, see [Using the Helm client to upload and download Helm Charts](https://intl.cloud.tencent.com/document/product/1051/35493). Click **Delete** to delete the current repository.
3. Click the name of the specified Helm Chart repository to enter the repository details page.
	- **Version Management**: this page displays the existing Chart versions in the current repository, and you can **download** or **delete** the specified versions, as shown in the figure below:
	![](https://main.qcloudimg.com/raw/bfdcb7b09f1e7e575b10f110c5b54b4b.png)
	- **Basic Information**: this page allows you to browse the detailed information of the specified Chart version, such as Chart.yaml, as shown in the figure below:
	![](https://main.qcloudimg.com/raw/245e50656e42d1a17d380889feeeda7d.png)

### Using the console to upload and download Helm Charts
#### Uploading a local Helm Chart package
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Helm Chart** in the left sidebar.
On the "Helm Chart" page, you can view the list of Helm Chart repositories in the current instance. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the page.
2. Click **Upload**. In the **Upload Helm Chart** window, configure based on the following information, as shown in the figure below:
![](https://main.qcloudimg.com/raw/411575f7b551915ca182c439921f9df3.png)
 - **Associated Instance**: the current instance selected.
 - **Namespace**: the namespace to which the Helm Chart belongs. If the list is empty, please first [create a namespace](https://intl.cloud.tencent.com/document/product/1051/35487) in the instance.
 - **Chart Package**: click to select a Helm Chart package that has been downloaded to the local system.
>! Only Helm Chart packages in .tgz format are supported. Please avoid uploading other types of files. Note that uploading a file will overwrite the existing Chart with the same name.
>
3. Click **Upload** to start uploading the Helm Chart package. After uploading, you can view the uploaded Helm Chart on the repository list page. If the uploaded package does not have a corresponding Helm Chart repository, a new repository will be created automatically.

#### Downloading a Helm Chart package to the local system
1. View the Helm Chart repository list in the current instance on the **Helm Chart** page. Click the specified repository to enter its version management page.
2. Select the specified version in the Chart repository, click **Download** on the right of the row where the version is located, and the Chart package on this version will be automatically downloaded to the local system. Depending on the browser and configuration, you can choose to specify the download path.


### Using the Helm client to upload and download Helm Charts
#### Installing a Helm client
>?
>- Note that, if you wish to use Helm in Tencent Kubernetes Engine (TKE), you need to select the v3.x.x version. You can run the `helm version -c` command to check the version of the installed client.
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

#### Adding a Helm repository
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select an instance name on the "Instance List" page to go to the instance details page.
2. [](id:Step2)Obtain the username and password used to log in to the instance. For more information, see [Obtaining an Instance Access Credential](https://intl.cloud.tencent.com/document/product/1051/37253).
3. Run the following command on the node to add the namespace, which is used to manage Helm Charts, to the local Helm repository.
>!The server running the command must be in the public network allowlist of the corresponding instance or in the linked VPC. For more information, see [Public Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35491) and [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492).
>
```
helm repo add $instance-$namespace https://$instance.tencentcloudcr.com/chartrepo/$namespace --username $username --password $instance-token
```
 - `$instance-$namespace`: name of the Helm repository. We recommend that you use the combination of **instance name+namespace name** for naming so as to distinguish between instances and namespaces.
 - `https://$instance.tencentcloudcr.com/chartrepo/$namespace`: remote address of the Helm repository.
    - `$username`: the username obtained in [step 2](#Step2).
    - `$instance-token`: the login password obtained in [step 2](#Step2).
    If it is added successfully, the following message will be prompted.
```
"$instance-$namespace" has been added to your repositories
```

#### Pushing Helm Charts
1. Install the helm cm-push plugin.
>! Please install the helm-push plugin on version 0.9.0 or above so as to prevent Helm Chart push exceptions caused by version incompatibility and other issues.
>
To upload Chart packages on Helm CLI, you need to install the helm-push plugin. The plugin supports using the `helm cm-push` command to push Helm Charts to the specified repository, as well as uploading directories and compressed packages.
```
helm plugin install https://github.com/chartmuseum/helm-push
```
2. Run the following command on the node to create a Chart.
```
helm create tcr-chart-demo
```
3. Run the following command to directly push the specified directory to the Chart repository (optional).
```
helm cm-push tcr-chart-demo $instance-$namespace
```
Here, `$instance-$namespace` is the name of the added local repository.
4. Run the following command to compress the specified directory and push it to the Chart repository.
```shell
tar zcvf tcr-chart-demo-1.0.0.tgz tcr-chart-demo/
```
```
helm cm-push tcr-chart-demo-1.0.0.tgz $instance-$namespace
```
Here, `$instance-$namespace` is the name of the added local repository.


#### Pulling Helm Charts
1. Run the following command on the node to obtain the latest Chart information.
```
helm repo update
```
2. Run the following command to pull the Helm Chart on the specified version:
```
helm fetch <Local repository name>/<Chart name> --version <Chart version>
```
In the following example, tcr-chart-demo 1.0.0 in the "project-a" namespace is pulled from the "tcr-demo" enterprise edition instance.
```
helm fetch tcr-demo-project-a/tcr-chart-demo --version 1.0.0
```
