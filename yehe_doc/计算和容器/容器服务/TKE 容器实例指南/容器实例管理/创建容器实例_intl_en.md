
## Overview

This document describes how to create and edit a container instance, and how to view events and logs.

If you are creating a container instance for the first time, we recommend that you refer to [Creating a Container Instance](https://intl.cloud.tencent.com/document/product/457/47001).
If you want to use advanced features such as container group and log collection, please refer to [Creating a Container Instance](#EKSCI2).


The configuration supported by the two modes are as follows:

| Supported Item                                 | Quick Creation | Complete Creation |
| -------------------------------------- | -------- | -------- |
| All regions                               |   &#10003;       |      &#10003;    |
| All specifications                               |   &#10003;       |   &#10003;      |
| Volume                                 |       &#10003;   |   &#10003;       |
| Container environment variables                           |   &#10003;       |       &#10003;   |
| Number of instances                               |     &#10003;     |   &#10003;       |
| Multi-container                                 |     ×    |      &#10003;    |
| Advanced configuration of a container (such as running command and init container) |    ×      |      &#10003;    |
| Restart policy (it defaults to Always)                |     ×     |    &#10003;      |
| Log collection                               |     ×     |     &#10003;     |
| Binding a role                               |     ×    |    &#10003;     |
|Binding an EIP                        |       ×   |    &#10003;      |


>! Container instances are in beta currently. To use them, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).




## Directions




### Granting permissions at the first time of use
You need to grant permissions to the current account for TKE to operate cloud resources when you use an EKSCI for the first time. For details, see [Service Authorization](https://intl.cloud.tencent.com/document/product/457/37808). If you have granted permissions to TKE, please skip this step.

<dx-alert infotype="explain" title="">
You can log in to the [CAM console](https://console.cloud.tencent.com/cam/role) to check if there is a TKE_QCSRole role.
</dx-alert>


[](id:EKSCI2)

### Creating a container instance

1. Log in to the **TKE console**.
2. On the list page of container instances, select the region where the instance is located.
3. Click **Create instance** on the top of the instance list.
4. On the **Create instance** page, configure the basic information of the instance.
<table><tr>
<th width=20%>Configuration Item</th><th>Description</th></tr>
<tr>
<td>Instance name</td>
<td>Enter the name of the instance to be created.</td>
</tr>
<tr>
<td>Region</td>
<td>Select a closest region. For example, if you are located in Shenzhen, please select "Guzhangzhou" for the region.</td>
</tr>
<tr>
<td>Container network</td>
<td>Assign an IP address within the IP range of the container network to the container instance.
<dx-alert infotype="notice" title="">
Subnet determines the availability zone. Each availability zone supports different type of resources, such as AMD, GPU-T4 and GPU-V100. Please select a subnet which supports the desired type of resources according to the prompts.
</dx-alert>
</td>
</tr>
<tr>
<td>Security group</td>
<td>Security group has the capability of a firewall and can limit the network communication of the instance. Default value is default.</td>
</tr>
<tr>
<td>Instance specification</td>
<td>For specifications supported by an instance, see <a href="https://intl.cloud.tencent.com/document/product/457/34057">Resource Specifications</a>.</td>
</tr>
<tr>
<td>Volume (optional)</td>
<td>Provides storage for the container. Currently, it supports NFS and CBS. Also, it needs to be mounted to the specified path of the container.
<table>
   <tr>
      <th>Volume type</th>
      <th>Description</th>
   </tr>
   <tr>
	 <td><a href="https://www.tencentcloud.com/document/product/362">Cloud Block Storage (CBS)</a></td>
      <td>You can mount a Tencent Cloud CBS disk to a specified path of the container. When the container is migrated, the cloud disk will be migrated along with it. CBS volumes are suitable for the persistent storage of data and can be used for stateful services such as MySQL. For a service for which a CBS volume is configured, the maximum number of Pods is 1.</td>
   </tr>
   <tr>
      <td nowrap="nowrap"><a href="https://www.tencentcloud.com/document/product/582">Network File System (NFS)</a></td>
      <td>You only need to enter the NFS path. You can use a CFS or NFS for file storage. NFS volumes are suitable for the persistent storage of data that is read and written many times. They can also be used in scenarios such as big data analysis, media processing, and content management.</td>
   </tr>
</table>
</td>
</tr>
<tr>
<td>Containers in the Pod</td>
<td>You can add multiple containers.<ul><li><b>Name</b>: (Optional) enter a custom name. If it is left empty, the image name will be used.</li><li><b>Image</b>: You can select an image from TCR Enterprise Edition, TCR Personal Edition, Dockerhub or a third-party image repository.</li><li><b>Image tag</b>: It defaults to `latest` if it is left empty.</li>
<li><b>Environment variable</b>: You can configure the environment variables for the container.</li>
<li><b>CPU limit</b>: It is left empty by default and the container can use all instance resources. You can set the maximum amount of CPU resources that the container can use.</li>
<li><b>Memory limit</b>: It is left empty by default and the container can use all instance resources. You can set the maximum amount of memory resources that the container can use.</li>
<li><b>Health check</b>: For details, see <a href="https://intl.cloud.tencent.com/document/product/457/30669">Health Check for Containers</a>.</li>
<li><b>Running commands and parameters</b>: For details, see <a href="https://intl.cloud.tencent.com/document/product/457/30670">Running Commands and Parameters for Containers</a>.</li>
<li><b>Init container</b>: You can set the container to init container. Note that there must be a business container other than the init container.</li>
</ul>
</td>
</tr>
<tr>
<td>Image repository credential</td>
<td>When you select an image from Docker Hub or a third-party image repository, you must enter the image credential, i.e., access address, username and password of the repository.</td>
</tr>
<tr>
<td>Number of instances</td>
<td>You can create multiple instances at a time. You can create only one replica if you select CBS as the volume type.</td>
</tr>
</table>
5. Click **Confirm** to go to the "Confirm configuration" page.
6. On this page, confirm the resource specification and configuration cost. Click **Create instance** to complete the creation.


You can set the advanced configuration on **Other configurations** page.
<dx-tabs>
::: Restart policy
You can select a restart policy from the following three policies. It defaults to `Always`.
- **Always**: Auto-restart the container if it is in any status other than `running`.
- **Never**: Regardless of the status, never restart the container.
- **OnFailure**: Auto-restart the container when the container terminates of the operation and the exit code is not 0.
Restart policy is actually the behavior that acts on containers in the Pod. It does not means the container instance will be restarted.

:::
::: Log collection
You can enable the log collection. For more information, see [Enabling Log Collection](https://intl.cloud.tencent.com/document/product/457/46236).
:::
::: Role authorization[](id:CAM)
You can bind a role to a container instance. For more information, see [Binding a Role to a Container Instance](https://intl.cloud.tencent.com/document/product/457/46237).
:::
::: EIP
You can bind a container instance to an EIP to access the public network. For more information, see [Accessing Public Network by Binding an EIP](https://intl.cloud.tencent.com/document/product/457/46235).
<dx-alert infotype="notice" title="">
This capability is only available to bill-by-IP accounts.
</dx-alert>

:::
</dx-tabs>


### Editing a container instance

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/eksci).
2. On the list page of container instances, select the region where the instance is located.
3. Click **More** > **Edit** on the right of the instance to be edited.
4. Modify the parameters of the instance on **Edit instance** page.
5. Click **Update instance** when you finished the modification.
>?
>- Previous configuration will be cleared when you update the container instance. You need to recreate it.
>- You cannot modify the following parameters for the container instance. Please recreate them if you want to modify.
>- Region
>- Network
>- Security group
>- Resource specification


