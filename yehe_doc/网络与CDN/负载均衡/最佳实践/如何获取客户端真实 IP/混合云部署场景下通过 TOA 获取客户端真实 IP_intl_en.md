This document describes how the layer-4 (only TCP) CLB service obtains the real client IP through TOA in hybrid cloud deployment and NAT64 CLB scenarios.
<dx-steps>
- [Enable TOA in the console](#loadopentoa)
- [Load TOA](#load-toa)
- [Adapt the real server](#adapt-rs)
- [(Optional) Monitor TOA status](#monitor-toa)
</dx-steps>

>?
>- Only the Beijing region supports obtaining the real client source IP via TOA.
>- Layer-4 (TCP) CLB can obtain the real client source IP via TOA, while Layer-4 (UDP) and layer-7 (HTTP/HTTPS) CLB cannot.
>- This feature is in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20CLB&level3_id=1068&radio_title=%E9%85%8D%E9%A2%9D/%E7%99%BD%E5%90%8D%E5%8D%95&queue=96&scene_code=41669&step=2).
>


## Use Cases
### Hybrid cloud deployment
In [hybrid cloud deployment](https://intl.cloud.tencent.com/document/product/214/38442) scenarios, IPs of the IDC and VPC may overlap with each other, so an SNAT IP is required. For the server, the real client IP is invisible, and it needs to be obtained through TOA.

### NAT64 CLB
In NAT64 CLB scenarios, the real IPv6 client IP is translated to an IPv4 public IP, which is invisible to the real server.
In this case, the real client IP can be obtained through TOA, that is, the TCP packets transmit the real client IP information to the server after you insert the real client IP into the field `TCP option`, and the client can obtain the real client IP by calling the API of the TOA kernel module.


## Restrictions
<dx-accordion>
::: Resource limits
- The kernel version of the TOA compilation environment must be consistent with that of the service environment.
- In a container environment, the TOA kernel module needs to be loaded in the host.
- To load the TOA kernel module, the root permission is required.
:::
::: Compatibility limits
 - UDP listeners cannot get the real client IP through TOA.
 - If there are already TOA-related operations between the client and the real server, the real server may fail to obtain the real client IP.
 - After TOA is inserted, it takes effect only on new connections.
 - TOA may degrade the server performance as it needs to perform additional processing such as extracting the address from the field `TCP option`.
 - Compatibility issues may come up when Tencent Cloud TOA is used with other TOA modules.
 - Tencent Cloud TOA is embedded in TencentOS and can be used to obtain the real source IP in hybrid cloud deployment scenarios. If the server is run on TencentOS and deployed in a hybrid cloud, you can directly execute the command `modprobe toa` to load TOA. If the server is run on Linux, Linux TOA should be used instead.
:::
</dx-accordion>

## Enable TOA in the console[](id:loadopentoa)
1. Create a NAT64 CLB instance. For more information, see [Creating IPv6 NAT64 CLB Instances](https://intl.cloud.tencent.com/document/product/214/34556).
2. Log in to the [CLB console](https://console.cloud.tencent.com/clb) to create a TCP listener. For more information, see [Configuring TCP Listener](https://intl.cloud.tencent.com/document/product/214/32517).
3. Enable TOA in the "Create listener " window.
![]()




## [Load TOA](id:load-toa)
1. Download and decompress the TOA package corresponding to the version of Linux OS on Tencent Cloud.
<dx-accordion>
::: CentOS
[CentOS 8.0 64](https://clb-toa-1255852779.file.myqcloud.com/CentOS%208.0.1905.zip)
[CentOS 7.6 64](https://clb-toa-1255852779.file.myqcloud.com/CentOS%207.6.1810.zip)
[CentOS 7.2 64](https://clb-toa-1255852779.file.myqcloud.com/CentOS%207.2.1511.zip)

:::
::: Debian
[Debian 9.0 64](https://clb-toa-1255852779.file.myqcloud.com/Debian%209.zip)
:::
::: SUSE Linux
[SUSE 12 64](https://clb-toa-1255852779.file.myqcloud.com/SUSE%2012.zip)
[SUSE 11 64](https://clb-toa-1255852779.file.myqcloud.com/SUSE%2011.zip)
:::
::: Ubuntu
[Ubuntu 18.04.4 LTS 64](https://clb-toa-1255852779.file.myqcloud.com/Ubuntu%2018.04.4%20LTS.zip)
[Ubuntu 16.04.7 LTS 64](https://clb-toa-1255852779.file.myqcloud.com/Ubuntu%2016.04.7%20LTS.zip)
:::
</dx-accordion>

2. [](id:step2)After it is decompressed, run the `cd` command to access the decompressed folder and run the module loading command:
```
insmod toa.ko
```
3. Run the following command to check whether TOA has been loaded. If you see the message "toa load success", the loading is successful.
```
dmesg -T | grep TOA
```
4. After it is loaded, load the `toa.ko` file in the startup script (the `toa.ko` file needs to be reloaded if the server is restarted).
5. (Optional) If TOA is no longer needed, run the following command to uninstall it.
```
rmmod toa
```
6. (Optional) Run the following command to check whether the module is uninstalled. If you see the message "TOA unloaded", the uninstallation is successful.
```
dmesg -T
```

If you cannot find an installation package above for your OS version, you can download the general source package for Linux OS and compile it to obtain the `toa.ko` file. This general version supports most Linux distributions (e.g., CentOS 7, CentOS 8, Ubuntu 16.04, and Ubuntu 18.04).
>? Linux kernels and Linux distributions are varied, and that may cause compatibility issues. We recommend compiling the TOA source package on your OS before using it.
>
1. Download the source package.
>!If your OS is Linux, download the Linux TOA source package; if it is TencentOS, download the TLinux TOA source package.
>
  - Linux
```
wget "https://clb-toa-1255852779.file.myqcloud.com/tgw_toa_linux_ver.tar.gz"
```
  - TLinux
```
wget "https://clb-toa-1255852779.file.myqcloud.com/tgw_toa_tlinux_ver.tar.gz"
```
2. To compile the Linux environment for TOA, you need to install the GCC compiler, Make tool and kernel development package first.
<dx-accordion>
::: Procedure to install on CentOS

```
yum install gcc
yum install make
//Install the kernel development package. The version of the package header file and library must be consistent with the kernel version.
yum install kernel-devel-`uname -r`
```
:::
::: Procedure to install on Ubuntu and Debian

```
apt-get install gcc
apt-get install make
//Install the kernel development package. The version of the package header file and library must be consistent with the kernel version.
apt-get install linux-headers-`uname -r`
```
:::
::: Procedure to install on SUSE
```
zypper install gcc
zypper install make
//Install the kernel development package. The version of the package header file and library must be consistent with the kernel version.
zypper install kernel-default-devel
```
:::
</dx-accordion>

3. Compile the source package to generate the `toa.ko` file. If `warning` and `error` are not prompted during the compilation process, the compilation is successful. Take the source package for Linux OS as an example:
```
tar zxvf tgw_toa_linux_ver.tar.gz
cd tgw_toa_linux_ver//Enter the decompressed directory tgw_toa
make
```
4. After the compilation is successful, take [the second step](#step2) to load TOA.


## [Adapt the Real Sever](id:adapt-rs)
<dx-accordion>
::: Hybrid cloud deployment
When adapting the real server in a hybrid cloud, you only need to call the standard Linux network programming API to get the real client IP without code changes. The following shows a code sample.
```
struct sockaddr v4addr;  
len = sizeof(struct sockaddr);  
//`get_peer_name` is the standard Linux network programming API.
if (get_peer_name(client_fd, &v4addr, &len) == 0) {  
	inet_ntop(AF_INET, &(((struct sockaddr_in *)&v4addr)->sin_addr), from, sizeof(from));  
	printf("real client v4 [%s]:%d\n", from, ntohs(((struct sockaddr_in *)&v4addr)->sin_port));   
}
```
:::
::: NAT64 CLB
To get the real source IP in the NAT64 CLB scenario, you need to modify the source code after the `toa.ko` kernel module is inserted into the real server and TOA will pass the IP address to the real server.
1. Define a data structure to store the IP address.
```
struct toa_nat64_peer {  
	struct in6_addr saddr;  
	uint16_t sport;  
};  
....  
struct toa_nat64_peer client_addr;  
....  
```
2. Define TOA variables and make calls to get the real source IPv6 address.
```
enum {  
	TOA_BASE_CTL            = 4096,  
	TOA_SO_SET_MAX          = TOA_BASE_CTL,  
	TOA_SO_GET_LOOKUP       = TOA_BASE_CTL,  
	TOA_SO_GET_MAX          = TOA_SO_GET_LOOKUP,  
};  
getsockopt(client_fd, IPPROTO_IP, TOA_SO_GET_LOOKUP, &client_addr, &len);  
```
3. Obtain the source IP address.
```
real_ipv6_saddr = client_addr.saddr;  
real_ipv6_sport = client_addr.sport;
```

A complete configuration sample is as follows:
```
//Define TOA variables. Set `TOA_BASE_CTL` to 4096.
enum {  
	TOA_BASE_CTL            = 4096,  
	TOA_SO_SET_MAX          = TOA_BASE_CTL,  
	TOA_SO_GET_LOOKUP       = TOA_BASE_CTL,  
	TOA_SO_GET_MAX          = TOA_SO_GET_LOOKUP,  
};  
//Define a data structure to store the IP address.
struct toa_nat64_peer {  
	struct in6_addr saddr;  
	uint16_t sport;  
};  
//Declare the variable that is used to store the address.  
struct toa_nat64_peer client_addr;  
.……  
//Get the file descriptor of the client, where `listenfd` is the listening file descriptor of the server.  
client_fd = accept(listenfd, (struct sockaddr*)&caddr, &length);  
//Make calls to get the real source IP of the user in the NAT64 scenario.  
char from[40];  
int len = sizeof(struct toa_nat64_peer);  
if (getsockopt(client_fd, IPPROTO_IP, TOA_SO_GET_LOOKUP, &client_addr, &len) == 0) {  
	inet_ntop(AF_INET6, &client_addr.saddr, from, sizeof(from));  
	//Obtain the source IP and source port  
	printf("real client [%s]:%d\n", from, ntohs(client_addr.sport));  
}  
```
:::
::: NAT64 CLB used in a hybrid cloud
To get the real source IP in the scenario where NAT64 CLB is used in a hybrid cloud, you need to modify the source code after the `toa.ko` kernel module is inserted into the real server and TOA will pass the IP address to the real server.

A complete configuration sample is as follows:
```
//Define TOA variables. Set `TOA_BASE_CTL` to 4096.  
enum {  
	TOA_BASE_CTL = 4096,  
	TOA_SO_SET_MAX = TOA_BASE_CTL,  
	TOA_SO_GET_LOOKUP = TOA_BASE_CTL,  
	TOA_SO_GET_MAX = TOA_SO_GET_LOOKUP,   
};  

//Define a data structure to store the IP address.    
struct toa_nat64_peer {    
	struct in6_addr saddr;    
	uint16_t sport;    
};    

//Declare the variable that is used to store the address.    
struct toa_nat64_peer client_addr_nat64;    
.......  
//Get the file descriptor of the client, where `listenfd` is the listening file descriptor of the server.  
//Make calls to get the real client IP in the NAT64 scenario.   
char from[40];    
int len = sizeof(struct toa_nat64_peer);  
int ret;  
ret = getsockopt(client_fd, IPPROTO_IP, TOA_SO_GET_LOOKUP, &client_addr_nat64, &len);  
if (ret == 0) {  
	inet_ntop(AF_INET6, &(client_addr_nat64.saddr), from, sizeof(from));    
	//Obtain the source IP and source port.   
	printf("real client v6 [%s]:%d\n", from, ntohs(client_addr_nat64.sport));   
} else if (ret != 0) {  
	struct sockaddr v4addr;  
	len = sizeof(struct sockaddr);  
	//Obtain the source IP and source port:  
	//In the hybrid cloud deployment scenario, the source IP address is the IP address after SNAT;  
	//In the non-hybrid cloud deployment scenario, the source IP address is the client IP address without SNAT and NAT64.  
	//The semantics of this function is to get the real client address and port.  
	if (get_peer_name(client_fd, &v4addr, &len) == 0) {  
		inet_ntop(AF_INET, &(((struct sockaddr_in *)&v4addr)->sin_addr), from, sizeof(from));  
		printf("real client v4 [%s]:%d\n", from, ntohs(((struct sockaddr_in *)&v4addr)->sin_port));   
	}  
}  
```
:::
</dx-accordion>


## [(Optional) Monitor TOA Status](id:monitor-toa)
To ensure execution stability, this kernel module allows you to monitor status. After inserting the `toa.ko` kernel module, you can monitor the TOA working status on the host of the container in either of the following ways.
<dx-accordion>
::: Method 1: Check the IPv6 address stored in TOA
Run the following command to check the IPv6 address stored in TOA.
>!Executing this command may degrade performance. Please proceed with caution.

```
cat /proc/net/toa_table
```
:::
::: Method 2: Check TOA metrics
Run the following command to check the TOA metrics.
```
cat /proc/net/toa_stats
```
![](https://qcloudimg.tencent-cloud.cn/raw/0dcbd6a263316481f50d99c2e4fbab7a.png)
The monitoring metrics are described as follows:
<table>
<thead>
<tr>
<th>Metric</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>syn_recv_sock_toa</td>
<td>Receives connections with TOA information.</td>
</tr>
<tr>
<td>syn_recv_sock_no_toa</td>
<td>Receives connections without TOA information.</td>
</tr>
<tr>
<td>getname_toa_ok</td>
<td>This count increases when you call `getsockopt` and get the source IP successfully or when you call `accept` to receive client requests.</td>
</tr>
<tr>
<td>getname_toa_mismatch</td>
<td>This count increases when you call `getsockopt` and get the source IP that does not matched the required type. For example, a client connection contains an IPv4 source IP address whereas you get an IPv6 address, the count will increase.</td>
</tr>
<tr>
<td>getname_toa_empty</td>
<td>This count increases when the `getsockopt` function is called in a client file descriptor that does not contain TOA.</td>
</tr>
<tr>
<td>ip6_address_alloc</td>
<td>Allocates space to store the information when TOA gets the source IP and source port saved in the TCP data packet.</td>
</tr>
<tr>
<td>ip6_address_free</td>
<td>When the connection is released, TOA will release the memory previously used to save the source IP and source port. If all connections are closed, the total count of `ip6_address_alloc` for each CPU should be equal to the count of this metric.</td>
</tr>
</tbody>
</table>

:::
</dx-accordion>


## FAQs
<dx-accordion>
::: Why do I need to modify the server program after TOA is inserted for NAT64 CLB?
This is because that the client IP (IPv4) is converted to an IPv6 address in the hybrid cloud deployment scenario, which is different from the NAT64 CLB scenario where the client IP type remains unchanged. Therefore, you need to modify the server program so that the server can understand the IPv6 address.
:::
::: How do I know my OS is based on the Linux distribution or TLinux kernel?
- Run the following command to check my kernel version. If you see `tlinux` in the command output, you are using TLinux OS, while `linux` indicates you are using Linux OS.
```
uname -a
```
![](https://qcloudimg.tencent-cloud.cn/raw/3f266a4c245030173564cff0d3c77f73.png)

- You can also check the version using the following command. If `tlinux` or `tlinux` is returned, you are using TLinux OS.
```
rpm -qa | grep kernel
```
<img src="https://qcloudimg.tencent-cloud.cn/raw/4559818bd61436d7a752bcd9caf1b53d.png" width="70%">
:::
::: How do I perform preliminary checks when I failed to get the source IP?
1. Run the following command to check whether TOA has been loaded.
```
lsmod | grep toa
```
<img src="https://qcloudimg.tencent-cloud.cn/raw/5b92aa9de0db3e43e91316c4363886f1.png" width="70%">
2. Check whether the server program has made correct calls to get the source IP. You can refer to [Adapt the Real Sever](#adapt-rs).
3. Capture TCP packets on the server and check whether the packets contain the source IP information.
 - if `unknown-200` is displayed in the `tcp option` output, it indicates that the real source IP after SNAT is inserted into the field `tcp option`.
 - If `unknown-253` is displayed, it indicates that the real source IPv6 address is inserted in the NAT64 scenario.
![](https://qcloudimg.tencent-cloud.cn/raw/e8fed1ab42370a97889c7dcdce660b72.png)
4. If the packets containing the TOA address has been sent to the server, compile `toa.ko` to a DEBUG version, and further locate the problem through the kernel log. In the downloaded TOA source directory, add the DEBUG compilation option to the make file.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e89cf9fd3d96a760485fb04c966ef6b0.png"width="60%">
5. Run the following command to compile again.
```
make clean
make
```
6. Run the following commands to uninstall the original `toa.ko` and install the latest one.
```
rmmod toa 
insmod ./toa.ko
```
7. Run the following command to observe the kernel log.
```
dmesg -Tw
```
If you see the following message, TOA is working normally. You can further check whether the server program has made calls to get the real source IP, or whether the API is used incorrectly.
![](https://qcloudimg.tencent-cloud.cn/raw/9a958fc2b0ae9d185cd228c6668c7162.png)
8. If you failed to find out the problem with the preceding steps, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
:::
</dx-accordion>
