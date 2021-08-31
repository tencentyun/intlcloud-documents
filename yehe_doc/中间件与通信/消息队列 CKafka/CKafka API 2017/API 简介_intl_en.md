>?
>- The APIs listed on this page are on legacy versions and may be disused in the future. [CKafka APIs v3.0](https://intl.cloud.tencent.com/document/product/597/35332) have more standardized definitions and much lower access latency and thus are recommended.
>- If you need to access the legacy APIs of CKafka, please see [API Overview](https://intl.cloud.tencent.com/document/product/597/10076).

Welcome to Cloud Kafka (CKafka).

CKafka runs in Tencent IDCs and provides elastically scalable message queuing services.

CKafka provides scalable storage and network resources. You can refer to the APIs described in this document and related samples to create, terminate, and upgrade CKafka instances. For the full list of supported operations, please see [API Overview](https://intl.cloud.tencent.com/document/product/597/10076).

You need to fully understand the [CKafka overview](https://intl.cloud.tencent.com/document/product/597/10066) before using these APIs.

## Glossary
The following describes the common terms used in the documentation.

| Term | Full Name | Description |
|---------|---------|---------|
| Instance | Server instance | A CKafka server, which is a logical concept and consists of many physical machines that provide services. |
| [Region](https://intl.cloud.tencent.com/document/product/213/6091) | Region | A region where resources are located. Each region contains one or more availability zones. |
| [AZ](https://intl.cloud.tencent.com/document/product/213/6091) | Availability zone | A physical IDC of Tencent Cloud with independent power supply and network resources within a [region](https://intl.cloud.tencent.com/document/product/213/6091). Availability zones are designed to ensure business stability because failures within an availability zone are isolated without affecting other availability zones within the same region. |
| Monthly subscription | Monthly subscription |	A billing mode. For more information, please see [Instance Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180). |
| Pay-as-you-go | Pay-as-you-go |	A billing mode. For more information, please see [Instance Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180). |

#### Input and output parameter description
* `Limit` and `Offset`
These parameters are used for paging control. `Limit` indicates the maximum number of entries returned at a time, and `Offset` is the offset value. If the number of results exceeds the `Limit`, the number of returned results equals to the value of `Limit`.
For example, if Offset=0 and Limit=20, the 0th to 19th entries are returned; if Offset=20 and Limit=20, the 20th to 39th entries are returned; if Offset=40 and Limit=20, the 40th to 59th entries are returned, and so on.
	
* topic.N (array parameter) [](id:topic)
Format for inputting multiple parameters at a time. The format below indicates an array parameter (String Array), which means multiple parameters can be input at the same time. The inputting format is:
topic.0=test1&topic.1=test2&topic.2=test3, and so on (start with the subscript 0).


## Getting Started with APIs
The following describes some typical use cases of CKafka APIs:
- Create a topic by using the [CreateTopic](https://intl.cloud.tencent.com/document/product/597/10096) API and providing required information such as instance ID, topic name, number of partitions, and number of replicas.
- To modify the configuration of a topic, use the [SetTopicAttributes](https://intl.cloud.tencent.com/document/product/597/10098) API.

## Use Limits 
* CKafka allows up to 100 API calls per minute and no more than 100 calls per minute for a single API.
* For more information on specific limits, please see the documents of corresponding APIs or services.
