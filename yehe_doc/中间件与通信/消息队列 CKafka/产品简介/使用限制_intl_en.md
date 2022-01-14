This document lists the limits of certain metrics and performance in CKafka. Be careful not to exceed the corresponding limits during use so as to avoid exceptions.


| Limit | Description |
| ------------------- | ------------------------------------------------------------ |
| Number of topics        | The number of topics varies with product specification. For details, please refer to [Billing Overview](https://intl.cloud.tencent.com/document/product/597/11745). |
| Number of partitions | <li>One topic supports up to 2,500 partitions. </li><li>The number of instance-level partitions is the partition limit per topic * the number of topics (generally 2 or 3). </li><li>The number of partitions cannot be reduced. </li> |
| Number of consumer groups | The instance-level number of consumer groups should be below 200. For Pro Edition instances, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to increase the limit to 500. |
| Instance | <li>The region attribute of instances cannot be changed. </li><li>The maximum number of client connections to an instance is 5,000. When the number of instance connections has reached the limit, the client cannot create more connections. If this maximum value is unreasonable in your actual business, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to increase it. </li> |
| Version | <li>Standard Edition: it is compatible with open-source versions 0.9, 0.10, and 1.1. v1.1 is installed by default. Customized versions are not supported.</li><li>Pro Edition: it is compatible with open-source versions 0.9, 0.10, 1.1, 2.4, and 2.8.</li> |
| Multiple routing              | An instance can create up to 5 routes, with only one of them being a public network route.               |
| Public network bandwidth            | CKafka provides 3 Mbps public network bandwidth for free by default. Pro Edition instances can upgrade public network bandwidth to 198 Mbps additionally. |
| Opening ZooKeeper      | It is not supported.                                                     |
| Opening underlying resource        | It is not supported so as to avoid risks caused by user's operation.                       |
| Message size            | It cannot exceed 12 MB; otherwise, messages will fail to be sent.                         |
| Tag                | Each cloud resource can only support up to 50 tags. |
