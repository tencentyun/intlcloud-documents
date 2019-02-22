[//]: # (chinagitpath:XXXXX)

## Using Non-website Traffic Forwarding Rules
When Anti-DDoS Advanced uses non-website traffic forwarding rules, the real server needs to obtain the real client IP using the TOA module.

### Basic principle
Anti-DDoS Advanced is accessed through public network proxy, so the source and destination addresses of data packets will be modified. The source address of the data packet shown on the real server is the intermediate IP of the Anti-DDoS Advanced instance instead of the real client IP. To pass the client IP to the real server, the protective IP records the client's IP and Port in a custom tcp option field when forwarding the request. As shown below:
```
#define TCPOPT_ADDR  200
#define TCPOLEN_ADDR 8      /* |opcode|size|ip+port| = 1 + 1 + 6 */

/*
 * insert client ip in tcp option, now only support IPV4,
 * must be 4 bytes alignment.
 */
struct ip_vs_tcpo_addr {
    __u8 opcode;
    __u8 opsize;
    __u16 port;
    __u32 addr;
};
```

### Supported operating systems
•	CentOS 6.x
•	CentOS 7.x
>!
- Windows operating systems do not support using the TOA module to obtain the real client IP.
- To find out whether other operating systems of Linux are supported, contact [Tencent Cloud support team](https://cloud.tencent.com/about/connect).

### Notes
- It is recommended to install and test the TOA module in a test environment, and then deploy it to the official environment after confirming that the product is available and stable.
- If you need to upgrade the kernel, it is recommended that you save the original kernel before upgrade, in case of upgrade failure and other accidents.
-  TOA only supports IPv4. If the environment acquires IPv6 by default, the client IP cannot be obtained correctly.

### How to obtain the real client IP
1. Install the compiling environment by executing the following command with root user:
`yum install gcc kernel-headers kernel-devel -y `
2. [Download](https://daaa-1254383475.cos.ap-shanghai.myqcloud.com/TOA_CentOS_v1.zip) the installation package and decompress it.
 ```
wget  https://daaa-1254383475.cos.ap-shanghai.myqcloud.com/TOA_CentOS_v1.zip
unzip TOA_CentOS_v1.zip
 ```
 <span id="step3"></span>
3. Execute the `uname -r` command to view the kernel version.
 Example:
```
[root@VM_0_2_centos toa]# uname -r
3.10.0-514.26.2.el7.x86_64
```
4. Modify the path parameter KERNEL_DIR in the Makefile configuration file according to the query result from [step 3](#step3).
Example:
```
[root@VM_0_2_centos toa]# vim Makefile 
obj-m := toa.o
KERNEL_DIR := /usr/src/kernels/3.10.0-514.26.2.el7.x86_64/
PWD := $(shell pwd)
#EXTRA_CFLAGS+=-D__GENKSYMS__
all:
        make -C $(KERNEL_DIR) M=$(PWD) modules
clean:    
        rm *.o *.ko *.mod.c  Module.symvers modules.order
```
5. Execute the `make` command for compilation.
6. Move the module and load it.
```
mv toa.ko /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
insmod /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
```
 - The real client IP can be obtained normally if the module is loaded successfully.
 - If the real client IP cannot be obtained, you can check whether the TOA module is loaded successfully by executing the `lsmod | grep toa` command.

### Remove the TOA module
Remove the TOA module by executing the following command with root user:
```
rmmod /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
```

## Using Website Traffic Forwarding Rules
When Anti-DDoS Advanced uses website traffic forwarding rules, the X-Forwarded-For field in the HTTP header can be used to obtain the real client IP.
X-Forwarded-For is an extended field in the HTTP header used to enable the server to identify the real IP of the clients accessing the server through proxies.
The format is:
`X-Forwarded-For: Client, proxy1, proxy2, proxy3……`
When forwarding the user's access request to the real server, the protective IP will record the real IP of the requesting user at the head of the X-Forwarded-For field. Therefore, the application on the real server only needs to get the content of the X-Forwarded-For field in the HTTP header.
For more information, see [How to Obtain the Real Client IP Based on Layer-7 Forwarding Rules](https://cloud.tencent.com/document/product/214/3728).

