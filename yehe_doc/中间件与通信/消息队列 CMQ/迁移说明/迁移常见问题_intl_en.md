This document provides solutions to common problems during migration from CMQ to TDMQ for CMQ.

### Basic Data Migration

#### Problem
The numbers of subscribers displayed on the basic information pages in the TDMQ for CMQ and CMQ consoles are different.

#### Cause
The difference lies in the queues manually deleted in CMQ. CMQ doesn't strictly filter out deleted queues when you view subscribers, although these "extra" subscribers have already lost their consumption logic. By contrast, in the subscription logic of TDMQ for CMQ, once a queue is deleted, subscriptions to it will also be deleted, and relevant subscribers won't be displayed.

#### Solution
To check this problem, search for the subscribed queues that are "not migrated" in the queue list in the CMQ console. If no results are returned, the above reason can explain the problem of missing subscriptions in TDMQ for CMQ.


### Longer Consumption Latency

#### Problem
After switching to TDMQ for CMQ, you find that it takes more time (10–20s) to pull messages. This is a known problem that usually occurs in scenarios with a small number of messages and consumers. In the distributed architecture of TDMQ for CMQ, the randomness of polling nodes to pull messages is more obvious when the number of messages is small, so the underlying layer may poll repeatedly, which increases the latency.

#### Solution

1. Decrease the value of the **Long Polling Wait Time for Message Receipt** parameter in queue attributes. We recommend you set it to 3 seconds.
2. Clusters specially optimized for this scenario are provided to reduce the polling time. **You can switch the client access points to such clusters to pull messages more quickly**, with no need to create queues again.

Currently, such clusters are available in the following regions:

| Region | Access Point |
|-|-|
|Guangzhou| <li>http://gz.mqadapter.cmq.tencentyun.com:8080 (private network)</li><li>https://cmq-gz.public.tencenttdmq.com:9443</li>|
| Shanghai | <li>http://sh.mqadapter.cmq.tencentyun.com:8080 (private network)</li><li>https://cmq-sh.public.tencenttdmq.com:9443 (public network)</li>|
| Beijing | <li>http://bj.mqadapter.cmq.tencentyun.com:8080 (private network)</li><li>https://cmq-bj.public.tencenttdmq.com:8443 (public network)</li>|
| Hong Kong (China) | <li>http://hk.mqadapter.cmq.tencentyun.com:8080 (private network)</li><li>https://cmq-hk.public.tencenttdmq.com:8443 (public network)</li>|


### Incompatibility of Control APIs (for Adding and Viewing Queues)
#### Problem
Control methods such as `createQueue` in the SDK report errors after the switch.

#### Cause
TDMQ for CMQ is incompatible with the control operations in the CMQ SDK, such as creating queues and viewing the queue list. We have upgraded TencentCloud APIs from v2 to v3 in the console and no longer provide APIs over the v2 protocol. Therefore, TDMQ for CMQ control APIs need to be transformed based on the latest TencentCloud API protocol. After the transformation, the performance and developer-friendliness will be higher. For more information, see [API Documentation](https://intl.cloud.tencent.com/document/product/1111/43018).

TDMQ for CMQ separates control flows and data flows for better service. In principle, they have different call scenarios and characteristics. Therefore, their call domain names are also different.
You can get the call addresses of data flows in the console. For the call addresses of control flows, refer to the specific TencentCloud API documentation, such as [CreateCmqQueue](https://intl.cloud.tencent.com/document/api/1110/44169).

### Error with SDK Using TCP Protocol in TDMQ for CMQ

TDMQ for CMQ supports the HTTP protocol only by default. If you use an SDK over the TCP protocol in CMQ and want to seamlessly migrate it, use the following TCP-specific access points:

| Region | Access Point |
|-|-|
| Guangzhou | <li>http://gz.mqadapter.cmq.tencentyun.com:12000 (private network)</li><li>https://cmq-gz.public.tencenttdmq.com:12000 (public network)</li>|
| Shanghai | <li>http://sh.mqadapter.cmq.tencentyun.com:12000 (private network)</li><li>https://cmq-sh.public.tencenttdmq.com:12000 (public network)</li>|
| Beijing | <li>http://bj.mqadapter.cmq.tencentyun.com:12000 (private network)</li><li>https://cmq.bj.public.tencenttdmq.com:12000 (public network)</li>|

To solve this problem, configure the TCP client to use the above access points.


### Difficult Migration of Complicated System

If your system using CMQ is complicated or is hard to maintain and migrate for various reasons, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=947&source=14&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20CMQ&step=1) for assistance, and we will provide a backend switch scheme for migration.


<dx-alert infotype="notice" title="">
<li>The backend switch will increase the latency.</li>
<li>After the backend switch is completed, do not add or edit items in CMQ.</li>
</dx-alert>



