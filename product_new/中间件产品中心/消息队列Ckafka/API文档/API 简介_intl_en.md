Welcome to CKafka.

CKafka runs in Tencent IDC and provides scalable message queuing services.

CKafka provides scalable storage and network resources. Users can refer to the APIs described in this document and related samples to create, terminate and upgrade CKafka instances. For the full list of supported operations, see [API Overview](https://intl.cloud.tencent.com/document/api/597/10076).

You need to fully understand the [CKafka Overview] before using these APIs (https://intl.cloud.tencent.com/document/product/597/10066).

## Glossary
Below is the list of common terms used in this document:

| Term | Full Name | Description |
|---------|---------|---------|---------|
| Instance | Server instance | Message queue server is a logical concept and consists of many physical machines that provide services |
| Region | [Region] (https://intl.cloud.tencent.com/doc/product/213/6091) | The region where resources are located. Each region contains multiple availability zones |
| Zone | [Availability Zone](https://intl.cloud.tencent.com/doc/product/213/6091) | Physical IDCs of Tencent Cloud with independent power and network resources within the same region (https://intl.cloud.tencent.com/doc/product/213/6091). They are designed to ensure business stability as failures within an availability zone can be isolated without affecting other zones |
| Monthly subscription | Monthly subscription |A billing method. For more information, see [Billing Methods](https://intl.cloud.tencent.com/doc/product/213/2180#1.-.E5.8C.85.E5.B9.B4.E5.8C.85.E6.9C.88) |
| Pay-as-you-go | Pay-as-you-go |A billing method. For more information, see [Billing Methods](https://intl.cloud.tencent.com/doc/product/213/2180#2.-.E6.8C.89.E9.87.8F.E8.AE.A1.E8.B4.B9) |

#### Definitions of Input and Response Parameters
* Limit and Offset
These parameters are used for paging control. "Limit" indicates the maximum number of entries returned at a time, and "Offset" is the offset value. If the number of results exceeds the Limit, the number of returned results equals to the value of Limit.
For example, if Offset=0 and Limit=20, the 0th to 19th entries are returned; if Offset=20 and Limit=20, the 20th to 39th entries are returned; if Offset=40 and Limit=20, the 40th to 59th entries are returned and so on.
	
* topic.N
Format for inputting multiple parameters at a time. The format below indicates an array parameter, which means multiple parameters can be input at the same time. The inputting format is: 
topic.0=test1&topic.1=test2&topic.2=test3, and so on (start with the subscript 0).


## Getting Started with APIs
The following describes some typical use cases for CKafka APIs:
- Create a topic by using the [CreateTopic](https://intl.cloud.tencent.com/document/product/597/10096) API and providing required information such as instance ID, topic name, number of partitions, and number of replicas.
- To modify the configuration of a topic, use the [SetTopicAttributes] (https://intl.cloud.tencent.com/document/product/597/10098) API.

## Use Limits 
* CKafka allows up to 100 API calls per minute, and not more than 100 calls per minute for a single API.
* For information on specific limits, see documents for corresponding APIs or products.
