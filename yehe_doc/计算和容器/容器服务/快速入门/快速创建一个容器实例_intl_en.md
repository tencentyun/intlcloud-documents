





## Step 1. Sign up and top up
1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/register) and complete identity verification.
If you already have a Tencent Cloud account, ignore this step.
2. [Top up online](https://console.cloud.tencent.com/expense/recharge).
EKS provides two billing modes: Pay-as-you-go and reservation. Before purchasing a container instance, you need to top up your account as instructed in [Payment Methods](https://intl.cloud.tencent.com/zh/document/product/555/7425).





## Step 2. Authorize the service
1. Container instance is in beta test. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category?level1_id=6&level2_id=2028&source=0&data_title=%E5%BC%B9%E6%80%A7%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1%20EKS&step=1) for application.
2. After your account is added to the allowlist, authorize the container instance as prompted in the TKE console. (If you have already authorized the container instance, skip this step.)





## Step 3. Create a container instance


Log in to the TKE console and configure the container instance on the **Quick create** page.

<table><tr>
<th width=20%>Configuration Item</th><th>Description</th></tr>
<tr>
<td>Region</td>
<td>Select a closest region. For example, if you are located in Shenzhen, select "Guangzhou" for the region.</td>
</tr>
<tr>
<td>Container network</td>
<td>Assign an IP address within the IP range of the container network to the container instance.
<dx-alert infotype="notice" title="">
Subnet determines the availability zone. Each availability zone supports different type of resources, such as AMD, GPU-T4 and GPU-V100. Select a subnet which supports the desired type of resources according to the prompts.
</dx-alert>
</td>
</tr>
<tr>
<td>Security Group</td>
<td>Security group has the capability of a firewall and can limit the network communication of the instance. Default value is default.</td>
</tr>
<tr>
<td>Instance specification</td>
<td>For specifications supported by an instance, see <a href="https://intl.cloud.tencent.com/document/product/457/34057">Resource Specifications</a>.</td>
</tr>
<tr>
<td>Image</td>
<td>You can select an image from TCR Enterprise Edition, TCR Personal Edition, Docker Hub, or other third-party image repositories.</td>
</tr>
<tr>
<td>Image Tag</td>
<td>If this parameter is left empty, `latest` will be used by default.</td>
</tr>
<tr>
<td>Image Repository Credential</td>
<td>If you select an image from a third-party image repository other than Dockerhub, you must enter the image credential, i.e., access address, username and password of the image repository.</td>
</tr>
<tr>
<td>Volume (optional)</td>
<td>Provides storage for the container. Currently, it supports NFS and CBS. Also, it needs to be mounted to the specified path of the container.
<table>
   <tr>
      <th>Volume Type</th>
      <th>Description</th>
   </tr>
   <tr>
	 <td><a href="https://intl.cloud.tencent.com/zh/document/product/362">Cloud Block Storage (CBS)</a></td>
      <td>You can mount a Tencent Cloud CBS disk to a specified path of the container. When the container is migrated, the cloud disk will be migrated along with it. CBS volumes are suitable for the persistent storage of data and can be used for stateful services such as MySQL. For a service for which a CBS volume is configured, the maximum number of Pods is 1.</td>
   </tr>
   <tr>
      <td nowrap="nowrap"><a href="https://intl.cloud.tencent.com/zh/document/product/582">Network File System (NFS)</a></td>
      <td>You only need to enter the NFS path. You can use a CFS or NFS for file storage. NFS volumes are suitable for the persistent storage of data that is read and written many times. They can also be used in scenarios such as big data analysis, media processing, and content management.</td>
   </tr>
</table>
</td>
</tr>
<tr>
<td>Environment Variable (optional)</td>
<td>You can configure environment variables for containers.</td>
</tr>
<tr>
<td>Number of Instances (optional)</td>
<td>You can create multiple instances at a time. You can create only one copy if you select CBS as the volume type.</td>
</tr>
</table>
After configuring the required fields, confirm the resource specification and configuration fees, and click **Create Instance**. Then, you can view the created container instance.


## Step 4. View container instance events
<dx-tabs>
::: Method 1
1. Log in to the TKE console. 
2. On the container instance list page, click **More** > **View events** on the right of the instance for which you want to view the events.

:::
::: Method 2
1. Log in to the TKE console. 
2. On the container instance list page, click the name of the instance for which you want to view the events.
3. On the container instance details page, click **Events** to view them.

:::
</dx-tabs>




## Step 5. View container logs

<dx-tabs>
::: Method 1
1. Log in to the TKE console. 
2. On the container instance list page, click **Logs** on the right of the instance for which you want to view the events.

:::
::: Method 2
1. Log in to the TKE console. 
2. On the container instance list page, click the name of the instance for which you want to view the events.
3. On the container instance details page, click **Logs** to view them.

:::
</dx-tabs>



Only the standard output logs of the container can be viewed here. For more information on the collection of standard output logs and container file logs, see [Enabling Log Collection](https://intl.cloud.tencent.com/document/product/457/46236).
