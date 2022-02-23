This document describes the basic operations in CODING Continuous Deployment.

## Prerequisites
You must activate the CODING DevOps service for your Tencent Cloud account before you can use Coding project management. 


## Open Project
1. Log in to the [CODING console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to the CODING page.
2. On the Workspace homepage, click <img src ="https://main.qcloudimg.com/raw/12230547b45d5eae85ad1c4fa86fba68.png" width="15"style ="margin:0" data-nonescope="true"> on the left to go to the Continuous Deployment console.

## Function Overview[](id:intro)
CODING-CD is used to manage the project release, deployment, and delivery processes after build. It can seamlessly connect to upstream Git repositories and downstream artifact repositories to achieve automated deployment. Based on a stable technical architecture and Ops tools, it enables blue/green deployment, grayscale release (canary release), rolling release, and fast rollback.
The following Demo project shows how to use the CODING-CD console to release an application to a Tencent Cloud cluster.

## Preparation[](id:prepare)
-   Configure the permissions required for operations in CODING-CD.
-   Prepare a Kubernetes cluster that is accessible to CODING-CD. Learn how to apply for [Tencent Cloud Standard Clusters](https://intl.cloud.tencent.com/document/product/457/40029).
-   Import the [sample code repository](https://codingtest-cd.coding.net/public/k8sdemo/k8sDemo/git/files).
-   Prepare a Docker artifact repository. Learn how to use [Docker Artifact Repositories](https://intl.cloud.tencent.com/document/product/1136/44806) in a project.

## Procedure
### Step 1. Obtain and associate a cloud account[](id:1)
Because Tencent Kubernetes Engine (TKE) is used, a deployed application is released to the cluster. The team account used in the example has been associated with the Tencent Cloud account in **Team Management** > **Service Integration**.
1. Click **Deployment Console** on the left of the homepage, and bind the Tencent Cloud account in **Cloud Accounts**. You can customize your cloud account name. After selecting a region, you will automatically get the corresponding cluster.
![](https://qcloudimg.tencent-cloud.cn/raw/764a28af113f4691251467f6efbfd7ad.png)
2. Automatically generated artifact repository access credentials are stored in **Namespace**. You can create new credentials in the Tencent Cloud console.
![](https://qcloudimg.tencent-cloud.cn/raw/da95fb2b4079fa3495b5776cb1224154.png)

### Step 2. Configure an application[](id:2)
1. After adding a cloud account, go to the deployment console and click **Create Application**. Then, enter the application name and select a deployment method.
![](https://qcloudimg.tencent-cloud.cn/raw/28707631e7fdbcf3ff51aa88ce576ee3.png)
2. Select **Deploy to Kubernetes Cluster** template, and then enter the name and description to create the application.
![](https://qcloudimg.tencent-cloud.cn/raw/c67591415744e58508062badd7a321da.png)

### Step 3. Initialize project[](id:3)

1. This step configures the code and artifact repositories involved in continuous deployment. In the **Code Repository** field, choose to import an external repository. Go to the [sample repository](https://codingtest-cd.coding.net/public/k8sdemo/k8sDemo/git/files) and clone the repository address.
![](https://qcloudimg.tencent-cloud.cn/raw/2b431e19fc2c44be9f6830052ed364fe.png)
2. After the import, start to manage artifacts. Host the to-be-released Docker artifacts in the CODING artifact repository. For more information, see [Docker Artifacts](https://intl.cloud.tencent.com/document/product/1136/44806).
![](https://qcloudimg.tencent-cloud.cn/raw/ce33728700f2a7a808a48c773f631a75.png)
3. After pushing the artifacts to the artifact repository, get the artifact pulling address and enter it as the `image` address in the code repository's `/k8s/deployment.yaml` file.
![](https://qcloudimg.tencent-cloud.cn/raw/7dcdefc706453b3df42f4dfd62947922.png)
4. Next, import the cloud account's `imagePullSecrets` to the code repository. Go to **Deployment Console** > **Cloud Account**, click "View Details", and copy the name.![](https://qcloudimg.tencent-cloud.cn/raw/cca9133d508235f849ea682b8546ddae.png)
5. Paste the name in the `deployment.yaml` file of the code repository. Make sure that the `namespace` matches the **Namespace** specified above.
![](https://qcloudimg.tencent-cloud.cn/raw/9dfe5113d33b4f20966ad0272ea72c31.png)
6. It must also match the `namespace` in the `service.yaml` file at the same level.
![](https://qcloudimg.tencent-cloud.cn/raw/aa04ad06c0cc6d052a1d834e0e3b407f.png)

### Step 4. Configure deployment pipeline[](id:4)

Go to the Deployment Pipeline Configuration page to set:
-   Pipeline execution options (in this demo, all the default values are retained).
-   Artifacts needed in the deployment and service deployment stages.
-   Manual or automatic trigger.


1. Configure the deployment (Manifest) stage. For basic settings, select the cloud account bound, select **CODING Code Repository** for "Manifest Source", enter the relevant path, and choose to automatically get the image version configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/459a73afc64c300907372044a9823007.png)
2. Configure the service deployment stage by following the same steps as above. You also need to select the file path of the `k8s/service.yaml` file.

### Step 5. Configure the trigger[](id:5)
1. After configuring the deployment stage, you can select "Auto Trigger" or "Manually Submit Release Order" as the deployment method.
<dx-tabs>
::: Auto Trigger
Click the trigger type in **Basic Configuration** and select Docker repository trigger. When a developer updates the code repository and uses CI to package and push the image to the artifact repository, the updates of the Docker image version will automatically trigger the deployment process and release the application to the Kubernetes (TKE) cluster. Then, you can check whether the application has been successfully released in the infrastructure page.
![](https://qcloudimg.tencent-cloud.cn/raw/459a73afc64c300907372044a9823007.png)
:::
::: Manually Submit Release Order
To trigger the deployment process by manually submitting a release order, associate the **application** (such as flaskapp in this example) with a project. Search for the project to be associated in the **App List** in the deployment console.
![](https://qcloudimg.tencent-cloud.cn/raw/5c22157dfe7c90516aae9b949b7194ea.png)
:::
</dx-tabs>

2. After association, click **Continuous Deployment** > **Kubernetes** in the project to manually submit a release order.
![](https://qcloudimg.tencent-cloud.cn/raw/4f2483a7e0bc58b15012d60ca5559f02.png)

### Step 6. Complete the release[](id:6)
1. After a successful release, you can view the released artifacts, launch parameters, and stage execution details.
![](https://qcloudimg.tencent-cloud.cn/raw/29f95fba22e096ae5b5e9258a21f6caf.png)
2. To view the operating status of a resource in the cluster, click the workload under **Cluster** to view details (such as workload's pod instances and logs).
![](https://qcloudimg.tencent-cloud.cn/raw/cee587b1f8a590293a340231647720d8.png)
3. View workload in Tencent Kubernetes Engine.
![](https://qcloudimg.tencent-cloud.cn/raw/a9f12cee9a5f9b615d981ca5dc50a0a0.png)
