This document lists the limits of certain metrics and performance in CKafka. Please be careful not to exceed the corresponding limits during use so as to avoid exceptions.


| Limit | Description |
|---------|---------|
| Total number of topics | The upper limit varies by product specification. More topics can be added on the Pro Edition. | 
| Number of partitions | <li>Standard Edition: one topic supports up to 24 partitions. </li><li>Pro Edition: one topic supports up to 500 partitions. </li><li>The instance-level partition quantity limit applies to the number of replicas, which is generally 2 or 3. </li><li>The number of partitions cannot be reduced. </li>| 
| Number of consumer groups |<li>Standard Edition: the upper limit for the number of instance-level consumer groups is 50 by default. </li><li>Pro Edition: the initial limit for the number of instance-level consumer groups is 50. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=消息服务%20CKafKa&level3_id=955&radio_title=配额提升申请&queue=81&scene_code=18356&step=2) to increase the limit to 500.</li>| 
| Instance | <li>The region attribute of instances cannot be changed.</li><li>The maximum number of client connections to an instance is 5000.</li>| 
| Version | <li>Standard Edition: it is compatible with open-source versions 0.9, 0.10, and 1.1. v1.1 is installed by default. Custom versions are not supported.</li><li>Pro Edition: it is compatible with open-source versions 0.9, 0.10, 1.1, and 2.4, which can be freely selected upon purchase.</li> |
| Multi-route | You can create up to 5 routes for one instance, and only one route can be public network route. |
| ZooKeeper exposure | Not supported. |
| Underlying resource exposure | This is not supported, helping avoid risks caused by maloperations. |
| Message size | A message can be up to 8 MB; if larger, it will fail to be sent. |
| Tag | One Tencent Cloud resource can have up to 50 tags. |
