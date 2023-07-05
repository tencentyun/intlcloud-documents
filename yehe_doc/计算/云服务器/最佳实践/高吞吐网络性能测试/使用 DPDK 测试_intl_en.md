## Scenarios
This document describes how to use DPDK to test CVM instances for high-throughput network performance.


## Directions

### Compiling and installing DPDK
1. Prepare two test servers. You can purchase them as instructed in [Customizing Linux CVM Configurations](https://www.tencentcloud.com/document/product/213/10517). This document uses CVM instances with CentOS 8.2 installed as an example.
2. Log in to the two CVM instances successively and run the following command to download DPDK. For more information on how to log in to the CVM instances, see [Logging in to Linux Instance Using Standard Login Method](https://www.tencentcloud.com/document/product/213/5436).
```shellsession
yum install -y sysstat wget tar automake make gcc 
```
```shellsession
wget http://git.dpdk.org/dpdk/snapshot/dpdk-17.11.tar.gz
```
```shellsession
tar -xf dpdk-17.11.tar.gz 
```
```shellsession
mv dpdk-17.11 dpdk
```
3. Modify the txonly engine to allow UDP port traffic change on the DPDK sender CPU to generate multiple data streams.
 - Run the following command to modify the `dpdk/app/test-pmd/txonly.c` file.
```shellsession
vim dpdk/app/test-pmd/txonly.c
```
Press **i** to enter the edit mode and make the following configurations:
    1. Locate `#include "testpmd.h"` and enter the following content in the next line.
```shellsession
RTE_DEFINE_PER_LCORE(struct udp_hdr, lcore_udp_hdr);
RTE_DEFINE_PER_LCORE(uint16_t, test_port);
```
   The result should be as follows:
<img src="https://qcloudimg.tencent-cloud.cn/raw/986339620a9b4d690ba89c6e23f41783.png" width="50%">

   2. Locate ` ol_flags |= PKT_TX_MACSEC;` and append the following content to the next lines.

```shellsession
/* dummy test udp port */
memcpy(&RTE_PER_LCORE(lcore_udp_hdr), &pkt_udp_hdr, sizeof(pkt_udp_hdr)); 
```
   3. Locate `for (nb_pkt = 0; nb_pkt < nb_pkt_per_burst; nb_pkt++) {`. Start a new line and add the following:
```shellsession
RTE_PER_LCORE(test_port)++;
RTE_PER_LCORE(lcore_udp_hdr).src_port = rte_cpu_to_be_16(2222);
RTE_PER_LCORE(lcore_udp_hdr).dst_port = rte_cpu_to_be_16(rte_lcore_id() * 2000 + RTE_PER_LCORE(test_port) % 64);
```
The result should be as follows:
<img src="https://qcloudimg.tencent-cloud.cn/raw/5292a45d611ad354690cfd129335b333.png" width="70%">
    4. Replace `copy_buf_to_pkt(&pkt_udp_hdr, sizeof(pkt_udp_hdr), pkt,` with the following content:
```shellsession
copy_buf_to_pkt(&RTE_PER_LCORE(lcore_udp_hdr), sizeof(RTE_PER_LCORE(lcore_udp_hdr)), pkt,
```
The result should be as follows:
![](https://main.qcloudimg.com/raw/b235e11355eb0d96d8412b3ae15cc2e9.png)
Press **Esc** and enter **:wq** to save and close the file.
 - Run the following command to modify the `dpdk/config/common_base` file.
```shellsession
vim dpdk/config/common_base
```
Press **i** to enter the edit mode, and change the value of `CONFIG_RTE_MAX_MEMSEG=256` to `1024` as shown below:
![](https://main.qcloudimg.com/raw/6dea86be41b819b3f16042630346d2e3.png)
Press **i** to enter the edit mode and locate `CONFIG_RTE_MAX_LCORE=128`. Change the value to `256` if your CPU core is over 128.
<img src="https://qcloudimg.tencent-cloud.cn/raw/4247747c42915d68ec71704df91a9672.png" width="25%"> 
Press **Esc** and enter **:wq** to save and close the file.
<dx-alert infotype="explain" title="">
Modify these configuration files on both the initiator and receiver servers. You can run the following commands to send the modified file to the peer end to avoid repeated modification.
```shellsession
scp -P 22 /root/dpdk/app/test-pmd/txonly.c root@<IP>:/root/dpdk/app/test-pmd/
scp -P 22 /root/dpdk/config/common_base root@<IP>:/root/dpdk/config
```
</dx-alert>
4. Run the following command to replace the IP address of `dpdk/app/test-pmd/txonly.c` with the test server IP.
```shellsession
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
```shellsession
yum install numactl-devel
```
:::
::: Ubuntu
```shellsession
apt-get install libnuma-dev
```
:::
</dx-tabs>
6. Run the following command in the `dpdk/` directory to close KNI.
```shellsession
sed -i  "s/\(^CONFIG_.*KNI.*\)=y/\1=n/g" ./config/*
```
7. If your OS uses a later kernel version (for example, 5.3), run the following command to shield the differences.
```shellsession
sed -i "s/\(^WERROR_FLAGS += -Wundef -Wwrite-strings$\)/\1 -Wno-address-of-packed-member/g" ./mk/toolchain/gcc/rte.vars.mk
```
```shellsession
sed -i "s/fall back/falls through -/g" ./lib/librte_eal/linuxapp/igb_uio/igb_uio.c
```
8. Run the following command to compile DPDK.
```shellsession
make defconfig
```
```shellsession
make -j
```

### Configuring huge pages
Run the following command to configure huge pages.
```shellsession
echo 4096 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
```
If an error message appears, the huge pages are insufficient. In this case, adjust the command, for example:
```shellsession
echo 2048 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
```

### Loading the kernel module and binding the interface
<dx-alert infotype="explain" title="">
You need to use Python for this step. Go to the [Python official website](https://www.python.org/doc/) to download and install an appropriate version. This document uses Python 3.6.8 as an example.
</dx-alert>


1. [Log in to the Linux instance via VNC](https://www.tencentcloud.com/document/product/213/32494). After the ENI driver is bound to igb_uio user mode driver, ENI can only be accessed via VNC or console, instead of an SSH key or IP address.
2. Run the following commands successively to load the UIO module and bind the virtio interface.
```shellsession
ifconfig eth0 0
```
```shellsession
ifconfig eth0 down
```
```shellsession
modprobe uio
```
```shellsession
insmod /root/dpdk/build/kmod/igb_uio.ko
```
```shellsession
cd /root/dpdk/usertools/
```
```shellsession
python3 dpdk-devbind.py --bind=igb_uio 00:05.0
```
<dx-alert infotype="explain" title="">
Replace `00.05.0` in the command with the actual ENI address, which can be obtained using the following command:
```shellsession
python3 dpdk-devbind.py -s
```
</dx-alert>
After completing tests, run the following commands to restore ENI.
```shellsession
cd /root/dpdk/usertools/
```
```shellsession
python3 dpdk-devbind.py --bind=virtio-pci 00:05.0
```
```shellsession
ifconfig eth0 up
```

### Testing bandwidth and throughput

<dx-alert infotype="explain" title="">
- The tests use the `txpkts` parameter to control the packet size, for example, 1430B bandwidth and 64B pps.
- The command parameters provided in this step are applicable to CentOS 8.2. You need to modify them to suit other system image versions and test again. For example, due to the performance difference between the CentOS 7.4 kernel version 3.10 and the CentOS 8.2 kernel version 4.18, change the `nb-cores` in the bandwidth test to `2`. For more information about the command parameters, see [estpmd-command-line-options](https://doc.dpdk.org/guides-17.11/testpmd_app_ug/run_app.html#testpmd-command-line-options).
</dx-alert>


1. Run the following command to start testpmd on the sender in the txonly mode, and enable the rxonly mode on the receiver.
  - Sender:
```shellsession
/root/dpdk/build/app/testpmd  -l 8-191 -w 0000:00:05.0 -- --burst=128 --nb-cores=32 --txd=512 --rxd=512 --txq=16 --rxq=16  --forward-mode=txonly --txpkts=1430 --stats-period=1
```
>? Replace  `-l 8-191 -w 0000:00:05.0` with the actual value of your test environment.
>

  - Receiver:
```shellsession
/root/dpdk/build/app/testpmd -l 8-191 -w 0000:00:05.0 -- --burst=128 --nb-cores=32 --txd=512 --rxd=512 --txq=16 --rxq=16 --forward-mode=rxonly --stats-period=1
```
2. Run the following command to test pps (UDP 64B packets).
 - Sender:
```shellsession
/root/dpdk/build/app/testpmd  -l 8-191 -w 0000:00:05.0 -- --burst=128 --nb-cores=32 --txd=512 --rxd=512 --txq=16 --rxq=16  --forward-mode=txonly --txpkts=64 --stats-period=1
```
 - Receiver:
```shellsession
/root/dpdk/build/app/testpmd -l 8-191 -w 0000:00:05.0 -- --burst=128 --nb-cores=32 --txd=512 --rxd=512 --txq=16 --rxq=16  --forward-mode=rxonly --stats-period=1
```
The test result is as shown below:
![](https://main.qcloudimg.com/raw/778c351d2b7975581bff0d7ab05b9f88.png)

### Calculating the network bandwidth
The current receiving bandwidth can be calculated according to pps and packet length on the receiver using the following formula:
PPS × packet length × 8bit/B × 10<sup>-9</sup> = Bandwidth
You can use the test result to obtain the current bandwidth:
4692725 pps × 1430B × 8 bit/B × 10<sup>-9</sup>  ≈ 53 Gbps
>?
>- The packet length is 1430B, including 14B Ethernet header, 4B CRC and 20B IP header.
>- Rx-pps in the test result is an instantaneous statistical value. You can conduct several tests and calculate the average to make the result more accurate.
>
