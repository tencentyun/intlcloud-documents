You can use cross-region data migration to move data on a CVM in an availability zone in a region to a destination CVM in an availability zone of another region, or move data between CVMs in different availability zones within the same region.

## 1. Obtaining the Migration Tool  
 [Click here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to obtain the compressed migration tool package.

## 2. Choosing a Migration Mode Based on the Network Environment
Choose the appropriate migration mode according to the network environments of your source servers and destination CVMs.
Currently, the migration tool supports the default mode and the private network mode. The private network mode applies to three scenarios. Each migration mode or scenario has different network requirements for source servers and destination CVMs. If both source servers and destination CVMs can access the public network, you can use the default mode for migration. If source servers or destination CVMs cannot directly access the public network, you need to establish a connection between them through [VPC peering connections](https://intl.cloud.tencent.com/document/product/553), [VPN connections](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003), or [Direct Connect](https://intl.cloud.tencent.com/document/product/216) before using the private network mode for migration.

## 3. Backing up Data
You can [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) or use other methods to back up data.

## 4. Checking Before the Migration
Before migration, check the following items of the source server and destination CVM:
<table>
	<tr><th style="width: 15%;">Destination CVM</th><td><ol style="margin: 0;"><li>Storage: cloud disks (including system disks and data disks) of the destination CVM must have sufficient storage capacity to store data from the source server.</li><li>Security group: 443 and 80 ports must be open to the Internet in a security group.</li><li>Bandwidth: we recommend that you increase inbound and outbound bandwidth for faster migration. The traffic consumed during migration will be approximately equal to the data volume. If needed, change your network billing method in advance.</li><li>Operating system: we recommend that you use the same operating system on both the source server and the destination CVM. Different operating systems will result in inconsistency between the image to be created and the actual operating system. For example, when migrating a source server with the CentOS 7 system installed, choose a CVM with the CentOS 7 system installed as the destination.</li></ol></td></tr>
	<tr><th>Linux source server</th><td><ol  style="margin: 0;"><li>Check and install Virtio. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/9929">Checking Virtio Drivers in Linux</a>.</li><li>Check whether rsync is installed by running <code>which rsync</code> for verification.</li><li>Check whether SELinux is enabled. If yes, disable it.</li><li>Ensure the current system time is correct, because the Tencent Cloud API will use the UNIX timestamp to check the generated token after receiving a migration request.</li></ol></td></tr>
</table>

>? 
> - You can use tool commands to automatically check the source server, for example, `sudo ./go2tencentcloud_x64 --check`.
> - By default, the go2tencentcloud migration tool automatically performs checks upon launch. To skip checks and perform forced migration, configure `Client.Extra.IgnoreCheck` to `true` in the client.json file.
> - For more information on the go2tencentcloud migration tool, see [Migration Tool](https://intl.cloud.tencent.com/document/product/213/35640).
 > 

## 5. Starting the Migration

1. (Optional) Establish a connection between the source server and the destination CVM. 
 - If you are using the private network mode, establish a connection between the source server and the destination CVM through [VPC peering connections](https://intl.cloud.tencent.com/document/product/553), [VPN connections](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003), or [Direct Connect](https://intl.cloud.tencent.com/document/product/216).
 - Skip to the next step if you are using the default mode.
2. Configure the “user.json” file.
The “user.json” file is used to configure the source server and the destination CVM. It contains the following configuration items:
 - The API keys of your account, that is, `SecretId` and `SecretKey`. For more information, see [Access Key](https://intl.cloud.tencent.com/document/product/598/32675).
 - The region and instance ID of the destination CVM. For more information on supported regions, see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091). The instance ID can be checked on the [Instances](https://console.cloud.tencent.com/cvm/instance/index?rid=1) page.
 - (Optional) The data disk configuration of the source server.  
3. Configure the “client.json” file.
The “client.json” file is used to configure the migration scenario and other parameters. You need to configure the `Client.Net.Mode` parameter in the “client.json” file, regardless of which migration modes or scenarios you select.
4. (Optional) Exclude files and directories on the source server that do not need to be migrated.  
 Edit the “rsync\_excludes\_linux.txt” file on the Linux source server to remove files and directories that do not need to be migrated.
5. Run the tool.
For example, on a 64-bit Linux source server, execute the following command as the root user to run the tool.
```
sudo ./go2tencentcloud_x64
```
For example, if you are using the [private network mode: scenario 2](https://intl.cloud.tencent.com/document/product/213/35640#Scenario2) for migration and the following appears on the console, the migration has been successful.
 ![](https://main.qcloudimg.com/raw/3d5c45ccb9f5350bb30cf3d3fce29590/console-cross-region.png)
