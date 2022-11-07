TDMQ for RocketMQ is available in forms of exclusive cluster and virtual cluster as compared below:

| Feature | Exclusive Cluster | Virtual Cluster |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Version compatibility | Compatible with open-source version 4.9 and earlier | Compatible with open-source version 4.9 and earlier |
| Instance type | Physical isolation of resources | Logical isolation of resources, where underlying physical resources are shared. |
| Billing mode | **Monthly subscription** as priced on the [purchase page](https://buy.tencentcloud.com/tdmq?protocol=RocketMQ&rid=1&clusterType=profession) | **Pay-as-you-go** as priced on the [purchase page](https://buy.tencentcloud.com/tdmq?protocol=RocketMQ&rid=1&clusterType=profession) |
| TPS range | On-demand purchase based on different node specifications | Suitable for below 4000 TPS |
| Scaling | Flexible scaling, where the number of nodes, node specifications (coming soon), and storage space can be expanded separately. | Not supported |
| Broker repair and upgrade time | Quick upgrade | Subject to virtual cluster resources, it takes a long time to upgrade. |
| Availability | 99.99% | 99.95% |
| High availability | Custom multi-AZ deployment in the same region is supported to improve the disaster recovery capabilities. | Multi-AZ deployment in the same region is not supported. |
| Technical support | Parameter optimization consulting services are supported, helping you customize parameter configurations for certain special business scenarios. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application. | Basic troubleshooting and problem fixing |
| Event support | Event support is provided for major events such as product upgrade, business launch, and promotion campaign to ensure smooth business operations. | Not supported |

