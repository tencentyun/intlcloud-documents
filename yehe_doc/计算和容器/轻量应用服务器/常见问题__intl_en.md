### What is Lighthouse?

TencentCloud Lighthouse (Lighthouse) is a new-gen, out-of-the-box cloud server service developed for lightweight business scenarios to help small and medium-sized enterprises (SMEs) and developers conveniently and efficiently build small websites, blogs, forums, storage services, and various development, testing, and learning environments in the cloud. It is easier to use than traditional cloud server services and delivers applications at one stop by integrating and packaging basic cloud resources and popular open-source software, offering you the best way to get started with Tencent Cloud.

### What are the differences between Lighthouse and CVM?
Lighthouse is easier to use than CVM. It integrates multiple Tencent Cloud services and application service capabilities and simplifies the advanced concepts and features of CVM, allowing you to focus more on business logic and innovation. For more information, please see [Product Comparison](https://intl.cloud.tencent.com/document/product/1103/41521).

### How do I use Lighthouse?

For more information on Lighthouse and how to quickly get started with it, please see the following documents:
- [Quickly Creating Application with Lighthouse](https://intl.cloud.tencent.com/document/product/1103/41399)
- [Quickly Creating Lighthouse Instance](https://intl.cloud.tencent.com/document/product/1103/41400)

### What are the use limits of Lighthouse?
There are certain limits on the quota, ICP filing, and private network connectivity. For more information, please see [Use Limits](https://intl.cloud.tencent.com/document/product/1103/41265).

### Which operating systems does Lighthouse support?

Currently, Lighthouse supports CentOS, Ubuntu, and Windows Server operating systems. It also supports application images that encapsulate operating systems and software (such as LAMP, WordPress, ASP.NET, Node.js, and BT-Panel).

### Can I log in to a Lighthouse instance remotely from a local SSH terminal?

For instances on Linux, you can log in remotely from a local SSH terminal. For instances on Windows, you can log in from a remote desktop over the RDP protocol.

### Can I install applications or software programs on a Lighthouse instance?

Yes. After a Lighthouse instance is created, you can install applications or software programs as needed on it. The installation methods are the same as those on general servers, such as using the apt-get tool on Ubuntu or using the yum tool on CentOS.

### Why can't I add a sound card or graphics card to a Lighthouse instance?

Lighthouse is a conventional server service rather than a multimedia server service, and it doesn't provide sound card and graphics card components by default. Therefore, you cannot add a sound card or graphics card to the system.

### Are there any limits on creating a website on a Lighthouse instance?
You can host different websites on a Lighthouse instance, but if you already have a domain name or want to access your website at a domain name, you should determine whether you need to perform operations such as website ICP filing application according to the Lighthouse instance and domain name conditions .

### How do I upload local files to a Lighthouse instance?
You can copy local files to a Lighthouse instance or download the files on it to your local file system. 

### What is a region?

Tencent Cloud regions are completely isolated. This guarantees the maximum cross-region stability and fault tolerance. We will gradually deploy nodes in more regions for a wider coverage. We recommend you select the region closest to your end users to minimize the access latency and improve the download speed.

### Can Lighthouse connect to or access other Tencent Cloud services over the private network?
- There are certain limits on private network connectivity between Lighthouse and other Tencent Cloud services. For more information, please see [Region and Network Connectivity](https://intl.cloud.tencent.com/document/product/1103/41266).
- - By default, Lighthouse instances cannot interconnect with other Tencent Cloud resources in VPCs such as CVM and TencentDB over the private network, and their interconnection needs to be implemented by associating a CCN instance. 

### Can different Lighthouse instances access each other over the private network?
There are certain limits on private network connectivity between different Lighthouse instances. For more information, please see [Region and Network Connectivity](https://intl.cloud.tencent.com/document/product/1103/41266).

### How do I verify whether Lighthouse accesses COS over the private network?
>? By default, Lighthouse accesses COS over the private network if they are in the same region and over the public network if they are in different regions. You can perform a verification in the following steps.

You can run the `nslookup` command on the Lighthouse instance to resolve the COS domain name. If a private IP is returned, the access is over the private network; otherwise, it is over the public network.

If `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com` is the destination bucket address, the `Address: 169.254.x.xx` in the following returned result indicates that the access is over the private network:
>?Generally, a private IP address is in the format of `10.*.*.*` or `100.*.*.*`, while a VPC IP address `169.254.*.*`. Both IP formats are on the private network.
>
```shell
nslookup examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Server:         xxx.xx.xx.xx
Address:        xxx.xx.xx.xx  #53


Name:   examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 169.254.x.xx
```

### Does Lighthouse support changing the IP or binding an EIP?
No. After a Lighthouse instance is created successfully, you cannot change its private or public IP or bind an EIP to it.

### Does Lighthouse support IPv6?
No. If you need IPv6, please use CVM.

### Does Lighthouse support CAM?
Yes. Lighthouse is connected to Cloud Access Management (CAM) and supports resource-level authorization. CAM can help you securely manage and control the access permissions, resources, and use permissions of your Tencent Cloud account. For more information, please see [Overview](https://intl.cloud.tencent.com/document/product/1103/41527).

### Does Lighthouse support CloudAudit? Does it have CloudAudit operation records?
Yes. You can view CloudAudit operation records in the following steps:
1. Log in to the CloudAudit console and select **[Operation Record](https://console.cloud.tencent.com/cloudaudit)** on the left sidebar.
2. Select **LIGHTHOUSE** as the **Resource Event Name** and click **Query** to view the CloudAudit operation records.


### How is Lighthouse billed?

Lighthouse is billed in a prepaid (monthly subscription) manner. The purchase duration of a package can range from 1 month to 5 years. You can terminate an instance before it expires, and after it is terminated, you will get a refund on the remaining purchase duration. For more information, please see [Refund Description](https://intl.cloud.tencent.com/document/product/1103/41406).

### Can I purchase a separate traffic package for a Lighthouse instance?
No. The basic package you select at the time of purchase already includes a traffic package. After the actually used traffic exceeds the monthly traffic package limit in the selected basic package, the Lighthouse instance will be billed by instance outbound traffic. For more information on the basic package and excessive traffic, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/1103/41403).

### Can I get a refund on the remaining traffic in the traffic package after a Lighthouse instance expires?
No. A Lighthouse instance is billed by the basic package in the monthly subscription billing mode, which includes resources such as traffic package. After the instance expires, you cannot get a refund on the remaining traffic in the traffic package or carry the remaining traffic of the current month over to the next month. You can select a [basic package](https://intl.cloud.tencent.com/document/product/1103/41403) based on your actual needs at the time of purchase.

### What is a Lighthouse image?

A Lighthouse image is a preconfigured template started and executed by Lighthouse, which contains preinstalled operating systems and software applications. You can use an image to create one or multiple instances. Lighthouse provides images on multiple operating systems such as Linux and Windows Server as well as images of applications such as LAMP and WordPress. Simply put, you can consider an image as an "installation disk" for Lighthouse.

### What image types does Lighthouse support?

Lighthouse supports the following image types:
- **System image**: it contains only the initial operating system (such as Linux or Windows Server) without applications or relevant runtime environment and configuration information.
- **Application image**: in addition to the underlying operating system, it also encapsulates applications, their runtime environments, and relevant initialization configuration information, allowing you to deploy applications quickly.
- **Custom image**: it is an image created by using the image creation feature and can only be used by the creator.

### Does Lighthouse supports reinstalling the operating system?

You can use the application resetting feature to reinstall the operating system on the instance. This operation can restore the instance to the initial state upon startup, and it is an important way to restore the instance in case of system failures.

### How do I log in to an instance as the root user on Ubuntu?

The default username on Ubuntu is `ubuntu`, and the root account and password are not set in the installation process by default. If needed, you can enable root login in the settings in the following steps:
1. Log in to the Lighthouse instance with your Ubuntu account.
2. <span id="Step2"></span>Run the following command to set the root password.
```
sudo passwd root
```
3. Enter the root password and press **Enter**.
4. Enter the root password again and press **Enter**. 
If the following information is returned, the root password is set successfully.
```
passwd: password updated successfully
```
5. Run the following command to open the `sshd_config` configuration file.
```
sudo vi /etc/ssh/sshd_config 
```
6. Press **i** to switch to the editing mode, find `#Authentication`, and change the value of the `PermitRootLogin` parameter to `yes`. If the `PermitRootLogin` parameter is commented, remove the comment symbol (`#`) from the first line as shown below:
![](https://main.qcloudimg.com/raw/e3d9dd2e362616a8bc25f8793a403cba.png)
7. Find `#Authentication` and change the value of the `PasswordAuthentication` parameter to `yes` as shown below:
>?If the `sshd_config` configuration file doesn't contain this configuration item, add `PasswordAuthentication yes`.
>
![](https://main.qcloudimg.com/raw/29ebeedf5f50279aa67974784d6140af.png)
8. Press **Esc**, enter **:wq**, save the file, and return. 
9. Run the following command to restart the SSH service.
```
sudo service ssh restart
```
10. Log in to the Lighthouse instance on Ubuntu as instructed in Logging in to Linux Instance from Remote Login Software:
 - **Username**: root
 - **Login password**: the password set in [step 2](#Step2)


### Why is the instance memory size returned by the `free` command different from the actual memory size?
After an instance is created successfully with the instance package of 1 GB memory, when you run the `free -m` command to view the instance memory size, you will find that it is not the same as the actual memory, which is normal. The cause is as follows:
>?This problem will also occur when you run the `free -m` command to view the instance memory size on a physical machine.
>



#### Error description
1. Run the `free` command to query the memory size.
```
free -m
```
The returned information is as follows, indicating that the memory size is 990 MB, which is lower than the actual 1 GB.
```
              total        used        free      shared  buff/cache   available
Mem:            990         258          69           0         662         573
Swap:             0           0           0
```
2. Run the following command to view the actual hardware memory size.
```
sudo dmidecode -t memory
```
The returned information is as follows, indicating that the memory size is 1024 MB, which is the same as the actual configuration.
```
# dmidecode 3.2
Getting SMBIOS data from sysfs.
SMBIOS 2.8 present.
Handle 0x1000, DMI type 16, 23 bytes
Physical Memory Array
        Location: Other
        Use: System Memory
        Error Correction Type: Multi-bit ECC
        Maximum Capacity: 1 GB
        Error Information Handle: Not Provided
        Number Of Devices: 1
Handle 0x1100, DMI type 17, 40 bytes
Memory Device
        Array Handle: 0x1000
        Error Information Handle: Not Provided
        Total Width: Unknown
        Data Width: Unknown
        Size: 1024 MB
        Form Factor: DIMM
        Set: None
        Locator: DIMM 0
        Bank Locator: Not Specified
        Type: RAM
        Type Detail: Other
        Speed: Unknown
        Manufacturer: Smdbmds
        Serial Number: Not Specified
        Asset Tag: Not Specified
        Part Number: Not Specified
        Rank: Unknown
        Configured Memory Speed: Unknown
        Minimum Voltage: Unknown
        Maximum Voltage: Unknown
        Configured Voltage: Unknown
```

#### Cause
- Relevant devices will be initialized at system startup, and this process uses a certain amount of memory.
- The kernel also uses a certain amount of memory at startup. The amount of memory used by kdump can be set, but do not change the amount of memory used by kdump unless necessary.
- `free -m` command queries the available memory of the instance, while `dmidecode -t memory` queries the actual hardware memory size of the instance.


### Which ports does Tencent Cloud not support?

- By default, Tencent Cloud restricts TCP port 25, which is the default mailbox service port. For security reasons, port 25 on Lighthouse instances is restricted by default.
- Certain ports have security risks, and although they are not restricted by Tencent Cloud, they will still be blocked by ISPs and thus become inaccessible. In order to avoid this situation, we recommend you change the ports and not listen on the following ports:
<table>
<tr><th>Protocol</th><th>Ports That May Be Blocked</th></tr>
<tr><td>TCP</td><td>42, 135, 137, 138, 139, 445, 593, 1025, 1434, 1068, 3127, 3128, 3129, 3130, 4444, 5554, 5800, 5900, and 9996</td></tr>
<tr><td>UDP</td><td>1026, 1027, 1434, 1068, 5554, 9996, 1028, 1433, and 135–139</td></tr>
</table>

### How do I unblock the public IP of my Lighthouse instance manually after it suffers DDoS attacks?
You can unblock it as instructed in [Manual Unblocking](https://console.cloud.tencent.com/ddos/unblock/list) in the Anti-DDoS console.



