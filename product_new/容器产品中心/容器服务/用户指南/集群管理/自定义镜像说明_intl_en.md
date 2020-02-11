## Introduction
This document describes how to use the basic images provided by TKE to create custom images.

## Notes
- The OS is configured at the cluster level. Clusters will use the configured OS when creating a node, creating a scaling group, adding an existing node, and upgrading a node.
- Changes to the OS only apply to new nodes and reinstalled nodes, but not existing nodes.
- Currently, you can only create an image of the same type of OS. For example, you can use the CentOS basic image to create a CentOS custom image.
> If you use the custom image feature, please use the basic images provided by TKE to create custom images.
- Whenever TKE plans to adjust the image logic, we will notify you at least one week in advance via Message Center, SMS, and email. 
Once the image logic changes, creation of new nodes with existing custom images will fail. You will need to create new custom images. If your cluster uses a scaling group, you will need to modify the image ID in its launch configurations.
- If you need to use the custom image feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category/?level1_id=6&level2_id=350&source=undefined&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1).


## Directions

### Creating CVM with Basic Images

#### TKE Basic Images

TKE provides you with the following basic images which are divided into **marketplace images** and **public images**. Please choose based on your needs.
 >  
 >- We will keep optimizing the basic images and generating new versions. This list will be updated as we make changes to the basic images.
 >- New versions of basic images will not affect the custom images you created with the old versions. We recommend that you use the newer versions for better experience.

<table>
	<tr>
	<th>Image ID </th><th>Name on the console</th><th>Image type</th><th>OS type</th><th>Release time</th><th>GPU</th><th>State in TKE</th><th>OS name</th><th>Description</th>
	</tr>
	<tr>
	<td><a href="https://market.cloud.tencent.com/products/15271">img-4wpaazux</a></td>
	<td>Ubuntu 16.04</td><td>Marketplace image</td><td>Ubuntu</td><td>2019.08.14</td><td>No</td><td>Active</td>
	<td>Ubuntu 16.04.1 LTSx86_64</td>
	<td>Ubuntu 16.04 with DNS nameserver modified</td>
</tr>
	<td><a href="https://market.cloud.tencent.com/products/15711">img-h1qos5y5</a></td>
	<td>Ubuntu 16.04 GPU</td><td>Marketplace image</td><td>Ubuntu</td><td>2019.08.14</td><td>Yes</td><td>Active</td>
	<td>Ubuntu16.04.1 LTSx86_64 GPU</td>
	<td>-</td>
</tr>
	<tr>
	<td><a href="https://console.cloud.tencent.com/cvm/image/detail/8/PUBLIC_IMAGE/img-pi0ii46r"> img-pi0ii46r </a></td>
	<td>Ubuntu 18.04</td><td>Public image</td><td>Ubuntu</td><td>2019.09.27</td><td>No</td><td>Active</td>
	<td>Ubuntu 18.04.1x86_64</td>
	<td>Ubuntu 18.04.1 public kernel</td>
</tr>
	<tr>
	<td><a href="https://market.cloud.tencent.com/products/15873">img-mk7tthq3</a></td>
	<td>Ubuntu 18.04 GPU</td><td>Marketplace image</td><td>Ubuntu</td><td>2019.09.27</td><td>Yes</td><td>Active</td>
	<td>Ubuntu 18.04.1x86_64 GPU</td>
	<td>Ubuntu 18.04.1 public kernel GPU nvidia:418.67 cuda:10.1.168</td>
</tr>
	<tr>
	<td><a href="https://market.cloud.tencent.com/products/17217">img-0amm1ukz</a></td>
	<td>Ubuntu 18.04 TKE Optimized</td><td>Marketplace image</td><td>Ubuntu</td><td>2019.11.18</td><td>No</td> <td>Active</td>
	<td>Ubuntu18.04.1x86_64</td>
	<td>Kernel 4.14.105-19-0008</td>
</tr>
	<tr>
	<td><a href="https://market.cloud.tencent.com/products/17237">img-fmdi67gb</a></td>
	<td>Ubuntu 18.04 TKE Optimized GPU</td><td>Marketplace image</td><td>Ubuntu</td><td>2019.11.18</td><td>Yes</td><td>Active</td>
	<td> Ubuntu 18.04.1x86_64 GPU</td>
	<td>Kernel 4.14.105-19-0008</td>
</tr>
	<tr>
	<td><a href="https://market.cloud.tencent.com/products/17175">img-rkiynh11</a></td>
	<td>CentOS 7.2</td><td>Marketplace image</td><td>CentOS</td><td>2019.11.14</td><td>No</td><td>Active</td>
	<td>CentOS7.2x86_64</td>
	<td>Kernel 3.10.0-1062.1.2.el7.x86_64</td>
</tr>
	<tr>
	<td><a href="https://market.cloud.tencent.com/products/14798">img-idtyzihp</a></td>
	<td>CentOS 7.2 GPU</td><td>Marketplace image</td><td>CentOS</td><td>2019.01.01</td><td>Yes</td><td>Active</td>
	<td>CentOS7.2x86_64 GPU</td>
	<td>CentOS 7.2 (actually 7.5) GPU; kernel 3.10.0-862.9.1.el7.x86_64</td>
</tr>
	<tr>
	<td><a href="https://console.cloud.tencent.com/cvm/image/detail/8/PUBLIC_IMAGE/img-9qabwvbn">img-9qabwvbn</a></td>
	<td> CentOS 7.6 </td><td>Public image</td><td>CentOS</td><td>2019.09.27</td><td>No</td><td>Active</td>
	<td>CentOS7.6.0_x64</td>
	<td>CentOS 7.6 public kernel 3.10.0-957.21.3.el7.x86_64</td>
</tr>
<tr>
	<td><a href="https://market.cloud.tencent.com/products/15706">img-8trzkv6h</a></td>
	<td>CentOS 7.6 GPU</td><td>Marketplace image</td><td>CentOS</td><td>2019.09.27</td><td>Yes</td><td>Active</td>
	<td>CentOS7.6.0_x64 GPU</td>
	<td>CentOS 7.6 public kernel 3.10.0-957.21.3.el7.x86_64 GPU nvidia:418.67 cuda:10.1.168</td>
</tr>
	<tr>
	<td><a href="https://market.cloud.tencent.com/products/17219">img-3kkoodwh</a></td>
	<td>CentOS 7.6 TKE Optimized</td><td>Marketplace image</td><td>CentOS</td><td>2019.11.18</td><td>No</td><td>Active</td>
	<td>CentOS 7.6.0_x64</td>
	<td>Kernel 4.14.105-19-0008</td>
</tr>
<tr>
	<td><a href="https://market.cloud.tencent.com/products/17238">img-es1i6ihl</a></td>
	<td> CentOS 7.6 TKE Optimized GPU</td><td>Marketplace image</td><td>CentOS</td><td>2019.11.18</td><td>Yes</td><td>Active</td>
	<td>CentOS 7.6.0_x64 GPU</td>
	<td>Kernel 4.14.105-19-0008</td>
</tr>
<tr>
	<td><a href="https://console.cloud.tencent.com/cvm/image/detail/16/PUBLIC_IMAGE/img-bh86p0sv">img-bh86p0sv</a></td>
	<td>tlinux 2.2</td><td>Public image</td><td>tlinux</td><td>2019.01.01</td><td>No</td><td>Active</td>
	<td>Tencent tlinux release 2.2（Final）</td>
	<td><ul class="params"><li> tlinux public image，2019/11 kernel is 0050</li><li>Currently this basic image is only available to internal users</li></ul></td>
</tr>
<tr>
	<td><a href="https://market.cloud.tencent.com/products/15369">img-9lmndrar</a></td>
	<td>tlinux 2.2 GPU</td><td>Marketplace image</td><td>tlinux</td><td>2019.08.01</td><td>Yes</td><td>Active</td>
	<td>Tencent tlinux release 2.2（Final）GPU</td>	<td>-</td>
</tr>
</table>

#### Creating a CVM
1. Log in to the [CVM Console](https://cloud.tencent.com/product/cvm), and select **Create** to go to the CVM purchase page.
2. Select a TKE basic image in **Image**. This document uses TKE image CentOS 7.2 64 bit (3.10.0-862 kernel) 1.0 as an example as shown below:
![](https://main.qcloudimg.com/raw/a53ae34dfe64d4fa30d70d960ab817e6.png)
3. For information on other configurations, see [Creating an Instance](https://intl.cloud.tencent.com/document/product/213/4855).


### Creating a Custom Image
1. Please log in to the CVM as instructed in [Log into Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute the following command to create a `test.txt` file.
```
vi test.txt
```
3. Press **i** to enter the insert mode, and enter the following.
```
this is customer cvm images test
```
4. Press **Esc** and enter **:wq** to exit and save.
5. Complete the creation as instructed in [Create Custom Images](https://intl.cloud.tencent.com/document/product/213/4942).


### Using a Custom Image
> After creating a custom image, you can use the image to create TKE clusters.
>
Select **Custom Image** in **Image Provider** on the **Create Cluster** page, and select a previously-created custom image in **Operating System** as shown below:
![](https://main.qcloudimg.com/raw/53151b87f9b23443e3ef7ba527d3eda2.png)
For other configurations, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).


### Verifying a Custom Image
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Select the ID of the cluster that is created using the custom image to go to the cluster details page.
3. Select **Node Management** > **Nodes** in the left sidebar and record the ID of the node to be verified.
4. Log in to the [CVM Console](https://cloud.tencent.com/product/cvm), enter the node ID in the search box, and click <img src="https://main.qcloudimg.com/raw/5244c9e564aa8ae65717a9eb33f94291.png" style="margin:-3px 0px">. You will see the existing nodes as shown below:
![](https://main.qcloudimg.com/raw/610b5fcd57067bfee6aa37c359c716ee.png)
5. Log in to the node as instructed in [Log into Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
6. Execute the following command to verify the custom image.
```
cat test.txt
```
If the results are as shown below, it means that the node is already using the custom image.
![](https://main.qcloudimg.com/raw/a3c1abdddf1d9b2990b787c849226348.png)

## Tips
- When creating a custom image, you must use the basic images provided by TKE. A fully custom image cannot be recognized in the TKE Console.
- If file protection (`chattr +i /etc/resolv.conf`) is configured for the `/etc/resolv.conf` file in the custom image, `cloud-init` will fail. Since TKE requires `cloud-init` in the successful state, such file protection will cause failure to add the node to the cluster.
- Since the order in which `rc.local` and `container_cluster_agent` are executed cannot be ensured, user’s data copied by `start_init.sh` script may be lost. It is recommended to execute `start_init.sh` in `user-data` instead of `rc.local`.
- If the `/var/lib/cloud` directory is saved on a node that has been used to create an image, the `config_scripts_user` file under the `/var/lib/cloud/instances/ins-1cgoe1y9/sem` directory will lead to errors in the `cloud-init` service. In such a case, the modified node hostname will be be invalid when the node is added to the TKE cluster.
- When a private yum source is added to a custom image, if it is placed in a wrong place, such as `/etc/yum.repo.d/`, it will cause `container-cluster-agent` to report an error when executing the `yum install` operation. In such a case, the operation will be skipped and the installation of the yum source by the agent will fail.


<style>
	.params{margin-bottom:0px !important;}
</style>

