This document lists the limits of certain metrics and performance in CKafka. Please be careful not to exceed the corresponding limits during use so as to avoid exceptions.


| Limit items              | Description                                       |
| ------------------- | ------------------------------------------------------------ |
| Number of topics        | The number of topics varies with product specification. For details, please visit https://intl.cloud.tencent.com/document/product/597/11745. |
| Number of partitions | <li>Standard Edition: one topic supports up to 24 partitions. </li><li>Pro Edition: one topic supports up to 500 partitions. </li><li>The number of instance-level partitions is the partition limit per topic * the number of topics (generally 2 or 3). </li><li>The number of partitions cannot be reduced. </li> |
| Number of consumer groups | <li>Standard Edition: The instance-level number of consumer groups is limited to 50 by default. </li><li>Pro Edition: The number of instance-level consumer groups is initially limited to 50. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to increase to a maximum of 500.</li> |
| Instance | <li>The region attribute of instances cannot be changed. </li><li>The maximum number of client connections to an instance is 5,000. When the number of instance connections has reached the limit, the client cannot create more connections. If this maximum value is unreasonable in your actual business, you can [submit a ticket] (https://console.cloud.tencent.com/workorder/category) to increase it. </li> |
| Version | <li>Standard Edition: it is compatible with open-source versions 0.9, 0.10, and 1.1. v1.1 is installed by default. Customized versions are not supported.</li><li>Pro Edition: it is compatible with open-source versions 0.9, 0.10, 1.1, 2.4, and 2.8.</li> |
| Multiple Routing              | An instance can create up to 5 routes, with only one of them being a public network route.               |
| Public network Bandwidth               | It currently supports up to 1 MB/s.               |
| Opening Zookeeper      | It is not supported.                                                     |
| Opening underlying resource        | It is not supported so as to avoid risks caused by user’s operation.                       |
| Message size            | It cannot exceed 8 MB, otherwise message will fail to be sent.                         |
| Tag                | Each cloud resource can only support up to 50 tags. |

