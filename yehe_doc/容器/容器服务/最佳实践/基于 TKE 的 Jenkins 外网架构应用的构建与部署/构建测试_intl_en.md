This step describes how to publish one or more images in the TKE image repository, and how to use an image to create a Deployment in the TKE console.
<span id="buildConfiguration"></span>
### Building configuration
1. Log in to the Jenkins backend and click the task "test" created in the [Slave pod building configuration](https://intl.cloud.tencent.com/document/product/457/34868) step from the task list, as shown in the following figure:
2. Click **Build with Parameters** in the left sidebar to open the "Project test" panel and configure the following parameters:
- **mbranch**: select the branch required for building. This document uses `origin/nginx` as an example.
  - **name**: select the name of the image to be built based on your actual needs. This document uses `nginx` as an example.
  - **version**: enter a custom image tag. This document uses `v1` as an example.
3. Click **Start Building**.
After the building is successfully completed, go to the TKE console and choose **Image Repository** > **[My Images](https://console.cloud.tencent.com/tke2/registry/user)** to view the built image.


### Publishing in the Console
1. Log in to the TKE console and click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Select the target cluster ID and go to the cluster management page of the Deployment to be created.
3. Click **Create** to go to the "Create a workload" page. See [Creating a Deployment](https://intl.cloud.tencent.com/document/product/457/30662) for the configuration of key parameters.
 In "Containers in the pod", choose **Select Image** > **My Images**. Then, select the image that was successfully uploaded during the preceding building process.
4. Click **Save** to finish creating the Deployment.
On the **Pod Management** page, the nginx pod is running normally if the deployment was successful.


### Related Operations: Batch Building Configuration
1. Log in to the Jenkins backend and click **System Management** in the left sidebar. Click **System Configuration** on the "Manage Jenkins" panel that appears.
2. On the "System Configuration" page, customize the "number of executors". This document uses 10 as an example.
> The number of executors is 10, indicating that 10 jobs can be executed at the same time.
>
3. For other configuration items, ensure that they are consistent with those in the [Configuring the slave pod template](https://intl.cloud.tencent.com/document/product/457/34867#PodTemplates) step.
4. Create 10 tests by referring to the [Slave pod building configuration](https://intl.cloud.tencent.com/document/product/457/34868) step, as shown in the following figure.
5. Configure building for multiple tasks by referring to the [Building Configuration](#buildConfiguration) step.
6. After the building is completed successfully, you can log in to the node and query the job pod by running the following command.
```
kubectl get pod
```
If the result similar to the following is returned, the call was successful.
![](https://main.qcloudimg.com/raw/87e0ff0807bc66c6566523bfbca7f65a.png)
