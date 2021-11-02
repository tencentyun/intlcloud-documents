## Overview
This document describes how to use DPDK to test CVM instances for high-throughput network performance.


## Directions

### Compiling and installing DPDK
1. Two test servers are required. You can purchase them as instructed in [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517). This document uses CVM instances with CentOS 8.2 installed as an example.
2. Log in to the two CVM instances and run the following command to download DPDK. For more information on how to log in to the CVM instances, see [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
```
yum install -y sysstat wget tar automake make gcc 
```
```
wget http://git.dpdk.org/dpdk/snapshot/dpdk-17.11.tar.gz
```
```
tar -xf dpdk-17.11.tar.gz 
```
```
mv dpdk-17.11 dpdk
```
3. Modify the txonly engine to allow UDP port traffic change on the DPDK sender CPU to generate multiple data streams.
 - Run the following command to modify the `dpdk/app/test-pmd/txonly.c` file.
```
vim dpdk/app/test-pmd/txonly.c
``` 
Press **i** to enter the edit mode and make the following configurations:
    1. Locate `#include "testpmd.h"` and enter the following content in the next line.
```
RTE_DEFINE_PER_LCORE(struct udp_hdr, lcore_udp_hdr);
```
		The result should be as follows:
![](https://main.qcloudimg.com/raw/69d640ddccd5e24538d51249e0fd0d6a.png)
    2. Locate ` ol_flags |= PKT_TX_MACSEC;` and append the following content to the next lines.
```
/* dummy test udp port */
static uint16_t test_port = 0;
test_port++;
memcpy(&RTE_PER_LCORE(lcore_udp_hdr), &pkt_udp_hdr, sizeof(pkt_udp_hdr));
RTE_PER_LCORE(lcore_udp_hdr).src_port = rte_cpu_to_be_16(rte_lcore_id() * 199 + test_port % 16);
RTE_PER_LCORE(lcore_udp_hdr).dst_port = rte_cpu_to_be_16(rte_lcore_id() * 1999 + test_port % 16);
```
The result should be as follows:
![](https://main.qcloudimg.com/raw/f3d08bb74601e96fbc59025906ee294d.png)
    3. Replace `copy_buf_to_pkt(&pkt_udp_hdr, sizeof(pkt_udp_hdr), pkt,` with the following content:
```
copy_buf_to_pkt(&RTE_PER_LCORE(lcore_udp_hdr), sizeof(RTE_PER_LCORE(lcore_udp_hdr)), pkt,
```
The result should be as follows:
![](https://main.qcloudimg.com/raw/b235e11355eb0d96d8412b3ae15cc2e9.png)
Press **Esc** and enter **:wq** to save and close the file.
 - Run the following command to modify the `dpdk/config/common_base` file.
```
vim dpdk/config/common_base
```
Press **i** to enter the edit mode, and change the value of `CONFIG_RTE_MAX_MEMSEG=256` to `1024` as shown below:
![](https://main.qcloudimg.com/raw/6dea86be41b819b3f16042630346d2e3.png)
Press **Esc** and enter **:wq** to save and close the file.
>?Modify these configuration files on both the receiving and sending CVM instances. You can run the following commands to send the modified file to the opposite end to avoid repeated modification.
>```
scp -P 22 /root/dpdk/app/test-pmd/txonly.c root@<IP>:/root/dpdk/app/test-pmd/
scp -P 22 /root/dpdk/config/common_base root@<IP>:/root/dpdk/config
```
>
4. Run the following command to replace the IP address of `dpdk/app/test-pmd/txonly.c` with the test server IP.
```
vim dpdk/app/test-pmd/txonly.c
``` 
Press **i** to enter the edit mode.
```
#define IP_SRC_ADDR (198U << 24) | (18 << 16) | (0 << 8) | 1;
#define IP_DST_ADDR (198U << 24) | (18 << 16) | (0 << 8) | 2;   
```
Replace `198`, `18`, `0`, and `1` in the above contents with the server IP, `SRC_ADDR` with the sender IP, and `DST_ADDR` with the receiver IP.
5. Run the OS-specific commands to install the numa library.
<dx-tabs>
::: CentOS
```
yum install numactl-devel
```
:::
::: Ubuntu
```
apt-get install libnuma-dev
```
:::
</dx-tabs>
6. Run the following command in the `dpdk/` directory to close KNI.
```
sed -i  "s/\(^CONFIG_.*KNI.*\)=y/\1=n/g" ./config/*
```
7. If your OS uses a later kernel version (for example, 5.3), run the following command to shield the differences.
```
sed -i "s/\(^WERROR_FLAGS += -Wundef -Wwrite-strings$\)/\1 -Wno-address-of-packed-member/g" ./mk/toolchain/gcc/rte.vars.mk
```
```
sed -i "s/fall back/falls through -/g" ./lib/librte_eal/linuxapp/igb_uio/igb_uio.c
```
8. Run the following command to compile DPDK.
```
make defconfig
```
```
make -j
```

### Configuring huge pages
Run the following command to configure huge pages.
```
echo 2048 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
```
If an error message appears, the huge pages are insufficient. In this case, adjust the command, for example:
```
echo 4096 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
```

### Loading the kernel module and binding the interface
>?The procedure requires Python. Go to the [Python official website](https://www.python.org/doc/) to download and install an appropriate version. This document uses Python 3.6.8 as an example.
>
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494). After the ENI driver is bound to igb_uio user mode driver, ENI can only be accessed via VNC or console, instead of an SSH key or IP address.
2. Run the following commands successively to load the UIO module and bind the virtio interface.
```
ifconfig eth0 0
```
```
ifconfig eth0 down
```
```
modprobe uio
```
```
insmod /root/dpdk/build/kmod/igb_uio.ko
```
```
cd /root/dpdk/usertools/
```
```
python3 dpdk-devbind.py --bind=igb_uio 00:05.0
```
>?Replace `00.05.0` in the command with the actual ENI address, which can be obtained using the following command:
> ```
python3 dpdk-devbind.py -s
```
>
After completing tests, run the following commands to restore ENI.
```
cd /root/dpdk/usertools/
```
```
python3 dpdk-devbind.py --bind=virtio-pci 00:05.0
```
```
ifconfig eth0 up
```

### Testing bandwidth and throughput
>?
>- The tests use the `txpkts` parameter to control the packet size, for example, b'andwidth of 1430B and pps of 64B.
>- The command parameters provided in the procedure are applicable to CentOS 8.2. You need to modify them to suit other system image versions and test again. For example, due to the performance difference between the CentOS 7.4 kernel version 3.10 and the CentOS 8.2 kernel version 4.18, change the `nb-cores` in the bandwidth test to `2`. For more information about the command parameters, see [estpmd-command-line-options](https://doc.dpdk.org/guides-17.11/testpmd_app_ug/run_app.html#testpmd-command-line-options).
> 
1. Run the following command to start testpmd on the sender in the txonly mode, and enable the rxonly mode on the receiver.
 - Sender:
```
/root/dpdk/build/app/testpmd -- --txd=128 --rxd=128 --txq=16 --rxq=16 --nb-cores=1 --forward-mode=txonly --txpkts=1430 --stats-period=1
```
 - Receiver:
```
/root/dpdk/build/app/testpmd -- --txd=128 --rxd=128 --txq=48 --rxq=48 --nb-cores=16 --forward-mode=rxonly --stats-period=1
```
2. Run the following command to test pps (UDP 64B packets).
 - Sender:
```
/root/dpdk/build/app/testpmd -- --txd=128 --rxd=128 --txq=16 --rxq=16 --nb-cores=3 --forward-mode=txonly --txpkts=64 --stats-period=1
```
 - Receiver:
```
 /root/dpdk/build/app/testpmd -- --txd=128 --rxd=128 --txq=48 --rxq=48 --nb-cores=16 --forward-mode=rxonly --stats-period=1
```
The test result is as shown below:
![](https://main.qcloudimg.com/raw/778c351d2b7975581bff0d7ab05b9f88.png)

### Calculating the network bandwidth
The current receiving bandwidth can be calculated according to pps and packet length on the receiver using the following formula:
PPS × packet length × 8bit/B × 10<sup>-9</sup> = Bandwidth
You can use the test result to obtain the current bandwidth:
4692725 pps × 1430B × 8 bit/B × 10<sup>-9</sup>  ≈ 53 Gbps
>?
>- The packet length is 1430B, including 14B Ethernet header, 8B CRC and 20B IP header.
>- Rx-pps in the test result is an instantaneous statistical value. You can conduct several tests and calculate the average to make the result more accurate.
