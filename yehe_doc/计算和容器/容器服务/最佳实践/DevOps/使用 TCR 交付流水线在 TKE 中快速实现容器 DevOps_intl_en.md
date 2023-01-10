## Overview 
The cloud-native era has witnessed the popularity of the DevOps concept and its implementation thanks to the rise and wide spread of container technologies. Continuous integration and continuous deployment based on container DevOps can significantly speed up application creation and delivery, thereby enhancing enterprise competitiveness.

This document describes how to coordinate the TCR delivery pipeline feature, TKE, and CODING DevOps to offer easy-to-use container DevOps capabilities and enable [automatic triggering of image build and application deployment after code push](#scene1) or [automatic triggering of deployment after local image push](#scene2).
![](https://qcloudimg.tencent-cloud.cn/raw/00b24d8903d89887afab9f49f6c0822c.png)

## Prerequisites 

- You have purchased a TCR Enterprise Edition instance and created an image repository as instructed in [Creating an Enterprise Edition Instance](https://intl.cloud.tencent.com/document/product/1051/35486) and [Basic Image Repository Operations](https://intl.cloud.tencent.com/document/product/1051/35488).
- You have created a TKE cluster and deployed the container application as instructed in [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- You have activated the CODING DevOps service.


<dx-alert infotype="explain" title="">
Currently, you can use a TCR Enterprise Edition image to create a workload in the TKE console. In addition, you can install TCR-dedicated add-ons for general TKE clusters to pull images from TCR Enterprise Edition over the private network without a secret. For more information, see [Using a Container Image in a TCR Enterprise Instance to Create a Workload](https://intl.cloud.tencent.com/document/product/457/36838).
</dx-alert>





## Directions
### Use case 1. Automatic triggering of image build and application deployment after code push[](id:scene1)
You can configure the pipeline to automatically build the image and trigger automatic deployment to the container platform after code changes.


#### Configuring delivery pipeline
1. Log in to the TCR console and select **[Delivery Pipeline](https://console.cloud.tencent.com/tcr/pipeline)** on the left sidebar.
2. On the **Delivery Pipeline** page, click **Create**.
3. In **Basic Info**, configure the following parameters and click **Next: Image Configuration** as shown below: 
![](https://qcloudimg.tencent-cloud.cn/raw/095cc8c8c58fba3d2ecf588908e95498.png)
 - **Pipeline Name**: Set the delivery pipeline name.
 - **Pipeline Description**: Add description information for the delivery pipeline, which can be modified later.
4. In **Image Configuration**, configure the following parameters and click **Next: Application Deployment** as shown below: 
![](https://qcloudimg.tencent-cloud.cn/raw/b0525906ba564b79a5a685798ddacf56.png)
 - **Image Repository**: Select the image repository associated with the delivery pipeline to automatically configure and push the image build.
 - **Image Version Filtering**: Impose limitations on the version of images in the execution delivery pipeline to filter out unnecessary ones for execution deployment.
    - **Deploy any version**: Any version of the image pushed to the image repository will be deployed.
    - **Deploy specified version only**: Specify the image tag and separate multiple versions with commas. Versions not specified will not be deployed.
    - **Deploy specified rule version only**: You need to enter a regular expression.
   - **Image Source**: Supports images built on the platform and locally pushed. Here, the first kind is used as an example.
    - **Image built on the platform**: Allows you to associate code repositories from different code hosting platforms and automatically triggers the delivery pipeline when code changes for the automatic build, image push, and application deployment.
    - **Image pushed locally**: When images are manually pushed, application deployment is triggered.
   - **Code Source and Code Repository**: Select the code repository used to build the image, and the pipeline will pull the source code of the repository for compilation and build. Authorization is required during first use. Currently, GitHub, public GitLab, private GitLab, Gitee, and TGit code hosting platforms are supported.
   - **Trigger Rule**: Rule for triggering automatic image build. Currently, four rules are supported:
     - **Upon pushing to a specified branch**: You need to specify a branch.
     - **Upon pushing a new tag**: The build is triggered when a tag is created and pushed.
     - **Upon pushing to a branch**: You don't need to specify a branch, as the build is triggered upon push to any branch.
     - **Upon matching branch or tag rules**: You need to enter a regular expression, for example, `^refs/heads/master$`, to match the master branch for triggering.
   - **Dockerfile Path**: The image build is based on a Dockerfile in the code repository, and you need to specify the path to this file. If it is not specified, the file named `Dockerfile` in the root directory of the code repository is used by default.
   - **Build Directory**: The working directory where the image build is executed, that is, the context. By default, it is the root directory of the code repository.
   - **Version Rule**: Define the name of the image generated by the build, that is, the image tag. You can use custom prefixes and add `branch/tag`, `update time`, and `commit number` environment variables. Here, `update time` is the system time to build the service by running the `docker tag` command.
5. In **Application Deployment**, configure the following parameters and click **OK**.
 - **Platform**: In this use case, TKE is used as an example.
 - **Region**: Region of the target cluster. Select the region of the created general TKE cluster.
 - **Cluster**: Target cluster. Select the created general TKE cluster.
 - **Deployment Method**: Currently, only **Update existing workloads** is supported.
 - **Namespace**: Namespace of the deployed application.
 - **Workload**: The workload associated with the deployed application.
 - **Pod Container**: Pod container within the workload of the deployed application. It uses the image from the image repository associated in the previous step.
6. After completing the above configuration, you can view the created pipeline on the **Delivery Pipeline** list page.

#### Updating container application
After completing the above configuration, the system can automatically trigger the image build, push, and application update after the application code is updated.
1. Update the source code.
   Update the source code and commit it to the remote code repository as shown below: 
   ![image-20201208195919986](https://main.qcloudimg.com/raw/00d42c83c07c15d48c090e5ec71107b9.png)
2. Execute the pipeline.
   After the source code is pushed, the pipeline execution will be triggered if the image build trigger conditions in the image configuration are met. You can click a pipeline to view its execution history and progress.
   - **Checkout**: Check out the code.
   - **Docker Build**: Build the image based on the image build configuration and tag the generated image with the specified rule, for example, `v-{tag}-{date}-{commit}`.
   - **Docker Push**: The system automatically pushes the image to the associated image repository.
   - **Deploy to TKE**: Use the latest pushed image to update the associated workload and the image with the same name in the Pod.
3. Check the application update status.
 1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster?rid=1)** on the left sidebar.
 2. Click the ID of the target cluster to enter the **Workload** page.
 3. On the **Deployment** tab, click the **Instance Name** to enter the instance details page.
 4. On the **Update History** tab, view the statuses of application updates. As shown below, v1 is the manually deployed Nginx image, which was updated to v2, a new image that was automatically built after the pipeline execution.
![](https://qcloudimg.tencent-cloud.cn/raw/2ac81cf5f0b39c44e2fdda1f11a75323.png)
      You can also access the application service to check whether the update is completed, specifically, over the public network address exposed by the Service, as shown below: 
![](https://qcloudimg.tencent-cloud.cn/raw/a65464c77876eb81f2c7b6e721971edf.png)
![](https://qcloudimg.tencent-cloud.cn/raw/77bad8339f4cc43f2e5a6a5bac51d002.png)


### Use case 2. Automatic triggering of deployment after local image push[](id:scene2)
In some use cases, if you don't need to have an image automatically built, you can still use TCR to have the locally pushed image automatically deployed to a container platform via a trigger.

#### Configuring delivery pipeline
1. Log in to the TCR console and select **[Delivery Pipeline](https://console.cloud.tencent.com/tcr/pipeline)** on the left sidebar.
2. On the **Delivery Pipeline** page, click **Create** as shown below: 
![](https://qcloudimg.tencent-cloud.cn/raw/f10c1b70a850780e59ce7f4de1ba1ab9.png)
3. In **Basic Info**, configure the following parameters and click **Next: Image Configuration** as shown below: 
![](https://qcloudimg.tencent-cloud.cn/raw/095cc8c8c58fba3d2ecf588908e95498.png)
 - **Pipeline Name**: Set the delivery pipeline name.
 - **Pipeline Description**: Add description information for the delivery pipeline, which can be modified later.
4. In **Image Configuration**, configure the following parameters and click **Next: Application Deployment** as shown below: 
![](https://qcloudimg.tencent-cloud.cn/raw/3e9bf49c97a34f99ea37ccf0a2e8faf7.png)
 - **Image Repository**: Select the image repository associated with the delivery pipeline to automatically configure and push the image build for hosting application deployment.
 - **Image Version Filtering**: Impose limitations on the version of images in the execution delivery pipeline to filter out unnecessary ones for execution deployment.
    - **Deploy any version**: Any version of the image pushed to the image repository will be deployed.
    - **Deploy specified version only**: Specify the image tag and separate multiple versions with commas. Versions not specified will not be deployed.
    - **Deploy specified rule version only**: You need to enter a regular expression.
   - **Image Source**: Supports images built on the platform and locally pushed. Here, the second kind is used as an example.
    - **Image built on the platform**: Allows you to associate code repositories from different code hosting platforms and automatically triggers the delivery pipeline when code changes for the automatic build, image push, and application deployment.
    - **Image pushed locally**: When images are manually pushed, application deployment is triggered.
5. In **Application Deployment**, configure the following parameters and click **OK**.
 - **Platform**: In this use case, TKE is used as an example.
 - **Region**: Region of the target cluster. Select the region of the created general TKE cluster.
 - **Cluster**: Target cluster. Select the created general TKE cluster.
 - **Deployment Method**: Currently, only **Update existing workloads** is supported.
 - **Namespace**: Namespace of the deployed application.
 - **Workload**: The workload associated with the deployed application.
 - **Pod Container**: Pod container within the workload of the deployed application. It uses the image from the image repository associated in the previous step.



#### Updating container application
After completing the above configuration, you can push the image locally by running commands to trigger automatic deployment.

1. Push the image locally.
  1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Image Repository** on the left sidebar.
On the **Image Repository** page, you can view the list of image repositories in the current instance. To switch the instance, select the target instance from the **Instance Name** drop-down list at the top of the page.    
  3. Click **Shortcuts** on the right of the instance to view the shortcuts in the pop-up window.
2. Execute the pipeline.
   After the image is pushed locally, the pipeline execution will be triggered if the image build trigger conditions in the image configuration are met. As the image is ready, the pipeline only needs to perform automatic deployment.
3. Check the application update status.
  1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster?rid=1)** on the left sidebar.
  2. Click the ID of the target cluster to enter the **Workload** page.
  3. On the **Deployment** tab, click the **Instance Name** to enter the instance details page.
  4. On the **Update History** tab, you can view the application update status.
      You can also access the application service to check whether the update is completed, specifically, over the public network address exposed by the Service, as shown below: 
      ![](https://qcloudimg.tencent-cloud.cn/raw/d4da6f593f14129c67cd1fcb727b2733.png)

   
