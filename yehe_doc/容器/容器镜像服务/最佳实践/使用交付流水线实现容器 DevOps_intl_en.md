## Overview

The cloud-native era has witnessed the popularity of the DevOps concept and its implementation thanks to the rise and wide spread of container technologies. Continuous integration and continuous deployment based on container DevOps can significantly speed up application creation and delivery, thereby enhancing enterprise competitiveness.

This document describes how to coordinate the TCR delivery pipeline feature, TKE, and CODING DevOps to offer easy-to-use container DevOps capabilities and enable [automatic triggering of image build and application deployment after code push](https://www.tencentcloud.com/document/product/1051/53613) or [automatic triggering of deployment after local image push](https://www.tencentcloud.com/document/product/1051/53613).

## Prerequisites
- You have purchased a TCR Enterprise Edition instance and created an image repository as instructed in [Creating an Enterprise Edition Instance](https://intl.cloud.tencent.com/document/product/1051/35486) and [Basic Image Repository Operations](https://intl.cloud.tencent.com/document/product/1051/35488).

- You have created a TKE cluster and deployed a container application. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).

- You have activated the CODING DevOps service.
  

   > ?
   > Currently, you can use a TCR Enterprise image to create a workload in the TKE console. In addition, you can install TCR-dedicated add-ons for general TKE clusters to pull images from TCR Enterprise over the private network without a secret. For more information, see [Using a Container Image in a TCR Enterprise Instance to Create a Workload](https://intl.cloud.tencent.com/document/product/457/36838).


## Directions

### Use case 1. Automatic triggering of image build and application deployment after code push

You can configure the pipeline to automatically build the image and trigger automatic deployment to the container platform after code changes.

#### Configuring delivery pipeline
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **[Delivery Pipeline](https://console.cloud.tencent.com/tcr/pipeline)** in the left sidebar.

2. On the **Delivery Pipeline** page, click **Create**.

3. In **Basic Info**, configure the following parameters and click **Next: Image Configuration**.
 - **Pipeline Name**: Set the delivery pipeline name.
   
 - **Pipeline Description**: Add description information for the delivery pipeline, which can be modified later.
   
4. In **Image Configuration**, configure the following parameters and click **Next: Application Deployment**.

  - **Image Repository**: Select the image repository associated with the delivery pipeline to automatically configure and push the image build for hosting application deployment.

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

 - **Platform**: The delivery pipeline supports TKE, EKS, and TKE Edge. In this use case, TKE is used as an example.
   
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
![](https://qcloudimg.tencent-cloud.cn/image/document/818ac8b896e6ba1f371a850dd7b66b39.png)

2. Execute the pipeline.
After the source code is pushed, the pipeline execution will be triggered if the image build trigger conditions in the image configuration are met. You can click a pipeline to view its execution history and progress.

 - **Checkout**: Check out the code.
   
 - **Docker Build**: Build the image based on the image build configuration and tag the generated image with the specified rule, for example, `v-{tag}-{date}-{commit}`.
   
 - **Docker Push**: The system automatically pushes the image to the associated image repository.
   
 - **Deploy to TKE**: Use the latest pushed image to update the associated workload and the image with the same name in the Pod.
   
3. Check the application update status.

   3.1 Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster?rid=1)** in the left sidebar.

   3.2 Click the ID of the target cluster to enter the **Workload** page.

   3.3 On the **Deployment** tab, click the **Instance Name** to enter the instance details page.

   3.4 On the **Update History** tab, view the statuses of application updates. 
   You can also access the application service to check whether the update is completed, specifically, over the public network address exposed by the Service.


### Use case 2. Automatic triggering of deployment after local image push

In some use cases, if you don't need to have an image automatically built, you can still use TCR to have the locally pushed image automatically deployed to a container platform via a trigger.

#### Configuring delivery pipeline
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **[Delivery Pipeline](https://console.cloud.tencent.com/tcr/pipeline)** in the left sidebar.

2. On the **Delivery Pipeline** page, click **Create**.

3. In **Basic Info**, configure the following parameters and click **Next: Image Configuration**.

 - **Pipeline Name**: Set the delivery pipeline name.
   
 - **Pipeline Description**: Add description information for the delivery pipeline, which can be modified later.
   
4. In **Image Configuration**, configure the following parameters and click **Next: Application Deployment**.

  - **Image Repository**: Select the image repository associated with the delivery pipeline to automatically configure and push the image build for hosting application deployment.

  - **Image Version Filtering**: Impose limitations on the version of images in the execution delivery pipeline to filter out unnecessary ones for execution deployment.

    - **Deploy any version**: Any version of the image pushed to the image repository will be deployed.

    - **Deploy specified version only**: Specify the image tag and separate multiple versions with commas. Versions not specified will not be deployed.

    - **Deploy specified rule version only**: You need to enter a regular expression.

    - **Image Source**: Supports images built on the platform and locally pushed. Here, the second kind is used as an example.

    - **Image built on the platform**: Allows you to associate code repositories from different code hosting platforms and automatically triggers the delivery pipeline when code changes for the automatic build, image push, and application deployment.

    - **Image pushed locally**: When images are manually pushed, application deployment is triggered.

5. In **Application Deployment**, configure the following parameters and click **OK**.

  - **Platform**: The delivery pipeline supports TKE, EKS, and TKE Edge. In this use case, TKE is used as an example.

  - **Region**: Region of the target cluster. Select the region of the created general TKE cluster.

  - **Cluster**: Target cluster. Select the created general TKE cluster.

  - **Deployment Method**: Currently, only **Update existing workloads** is supported.

  - **Namespace**: Namespace of the deployed application.

  - **Workload**: The workload associated with the deployed application.

  - **Pod Container**: Pod container within the workload of the deployed application. It uses the image from the image repository associated in the previous step.


#### Updating container application

After completing the above configuration, you can push the image locally by running commands to trigger automatic deployment.
1. Push the image locally.

1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Image Repository** in the left sidebar.
On the "Image Repository" page, you can view the image repository list of the current instance. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the page.    

2. Click **Shortcuts** on the right of the instance to view the shortcuts in the pop-up window.

3. Execute the pipeline.
After the image is pushed locally, the pipeline execution will be triggered if the image build trigger conditions in the image configuration are met. As the image is ready, the pipeline only needs to perform automatic deployment.

4. Check the application update status.

   4.1 Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster?rid=1)** in the left sidebar.

   4.2 Click the ID of the target cluster to enter the **Workload** page.

   4.3 On the **Deployment** tab, click the **Instance Name** to enter the instance details page.

   4.4 On the **Update History** tab, you can view the application update status.
 You can also access the application service to check whether the update is completed, specifically, over the public network address exposed by the Service, as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/df27041_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230106155749.png)
