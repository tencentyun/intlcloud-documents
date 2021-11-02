The new-generation Tencent Cloud CVM instances (including SA3, S6, C6, etc.) come with ultra-high network performance as detailed in [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518). This document provides two high-throughput network performance test methods for CVM instances: netperf and DPDK.

The netperf test is recommended for most use cases. However, if the CVM’s network throughput is larger than 10 million pps and the network bandwidth is higher than 50 Gbps, the kernel protocol stack of netperf consumes a lot of network resources. To obtain the actual network performance of the CVM ENI, use the DPDK method to shield the difference caused by the kernel protocol stack. 
 - [Using netperf](https://intl.cloud.tencent.com/document/product/213/42166)
 - [Using DPDK](https://intl.cloud.tencent.com/document/product/213/42167)

 
