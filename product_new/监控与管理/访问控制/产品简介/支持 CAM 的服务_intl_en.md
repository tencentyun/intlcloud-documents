## Introduction	

Cloud Access Management (CAM) helps you securely manage permissions for most Tencent Cloud services. This document provides information on the services that support CAM. The information covers authorization granularity, console operations, using tags for authorization, reference documentation, etc.
The table below lists Tencent Cloud services that support CAM.
Definitions:

- Service: name of the CAM-enabled Tencent Cloud service. For more information on a specific service, click the name to link to the product documentation.	
- Authorization granularity: the finest authorization granularity currently supported by the service.

> Authorization granularity has three levels: service level, operation level, and resource level.	
>
> - Service level defines whether a user has the permission to access a specific service as a whole. A user either has full access to the service or has no access to it.
> - Operation level defines whether a user has the permission to call a specific API of a service. For example, granting an account read-only access to the CVM service is an authorization at the operation level.	
> - Resource level is the finest authorization granularity which defines whether a user has the permission to access specific resources. For example, granting an account Read/Write access to a specific CVM is an authorization at the resource level..

- Console: whether sub-accounts can access the service through the Console. “&#10003;” means “Yes”; “-” means “No”.	
- Using tags for authorization: whether the service supports using tags for permissions management. “&#10003;” means “Yes”; “-” means “No”.		
- [Service role](https://intl.cloud.tencent.com/document/product/598/19420): whether the service can access other services as a role entity. "&#10003;" means “Yes”; "-" means “No”.	
- Reference documentation: the link to the documentation on access control for the service. “-” means “Documentation not available yet”.

## Compute	

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |	
| ------------------------------------------------------------| ------ | -------- | ------- |  ---- |	---- |	
| [Cloud Virtual Machine (CVM)](https://intl.cloud.tencent.com/document/product/213) <sup>1</sup> | Resource level  | &#10003;      |&#10003;    |  &#10003;  | [Access Control](https://intl.cloud.tencent.com/document/product/213/10311)   |		
| [Tencent Kubernetes Engine (TKE)](https://intl.cloud.tencent.com/document/product/457) | Resource level | &#10003;       | - | &#10003;    |[Access Control](https://intl.cloud.tencent.com/document/product/457/11526)  |	
| [Auto Scaling (AS)](https://intl.cloud.tencent.com/document/product/377) | Resource level | &#10003;      | -  | &#10003;    |-    |	
| [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583)  | Resource level | &#10003;        |  -  | &#10003;   |[Access Control](https://intl.cloud.tencent.com/document/product/583/9203)  |	
| [BatchCompute](https://intl.cloud.tencent.com/document/product/599)  | Resource level | &#10003;         |  -  | -    |-    |	
><sup>1</sup> Both [GCC instances](https://intl.cloud.tencent.com/document/product/560) and [CDH instances](https://intl.cloud.tencent.com/document/product/416) support CAM.

## Storage	

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |	
| ------------------------------------------------------------ | ------ | --------  | ------- | ---- |	---- |	
| [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436) | Resource level | &#10003;       | -  | &#10003;   |[Access Control](https://intl.cloud.tencent.com/document/product/436/12473)   |
| [Cloud File Storage (CFS)](https://intl.cloud.tencent.com/document/product/582) | Resource level | &#10003;        | -  |  &#10003;    |[Access Control](https://intl.cloud.tencent.com/document/product/582/14679)   |		
| [Cloud Block Storage (CBS)](https://intl.cloud.tencent.com/document/product/362) | Resource level | &#10003;       | &#10003;  |  -    |-    |	
| [Cloud Log Service (CLS)](https://intl.cloud.tencent.com/document/product/614)  | Resource level | &#10003;        | -  | &#10003; |[Access Control](https://intl.cloud.tencent.com/document/product/614/35564)    |	

## Networking	

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |	
| ------------------------------------------------------------ | ------ | -------- | ------- | ---- |	 ---- |
| [Cloud Load Balancer (CLB)](https://intl.cloud.tencent.com/document/product/214)   | Resource level | &#10003;      | &#10003;    |    &#10003;  |[Access Control](https://intl.cloud.tencent.com/document/product/214/9777) |	
| [Virtual Private Cloud (VPC)](https://intl.cloud.tencent.com/document/product/215)<sup>1</sup>  | Resource level | &#10003;        | -     | - | - |	
| [Direct Connect (DC)](https://intl.cloud.tencent.com/document/product/216) | Resource level   | &#10003;       | -       | -  | - |	
><sup>1</sup>CAM is supported by [ENI](https://intl.cloud.tencent.com/document/product/576), [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015), [Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connection](https://intl.cloud.tencent.com/document/product/1037), [Anycast Internet acceleration (AIA)](https://intl.cloud.tencent.com/document/product/644), and [Cloud Connect Network (CCN)](https://intl.cloud.tencent.com/document/product/1003).

## Database	

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |	
| ------------------------------------------------------------ | ------ | --------| --------- | ---- |	---- |
| [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236)  | Resource level | &#10003; | -  |  &#10003; |[Access Control](https://intl.cloud.tencent.com/document/product/236/14469) |			
| [TencentDB for SQL Server](https://intl.cloud.tencent.com/document/product/238)  | Resource level | &#10003;  | -    | -     |- |	
| [TencentDB for TDSQL](https://intl.cloud.tencent.com/document/product/1042)  | Resource level | &#10003;  | -    | -    |[Access Control](https://intl.cloud.tencent.com/document/product/1042/33343) |	
| [TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239)   | Resource level | &#10003; | -  | - |[Access Control](https://intl.cloud.tencent.com/document/product/239/32845) |	
| [TencentDB for MongoDB](https://intl.cloud.tencent.com/document/product/240) | Resource level | &#10003; | -   |&#10003;|[Access Control](https://intl.cloud.tencent.com/document/product/240/32839) |			
| [Data Transfer Service](https://intl.cloud.tencent.com/document/product/571)  | Resource level |  &#10003;  | -    | &#10003;    |-|	

## CDN & Acceleration	

| Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |	
| ------------------------------------------------------------| ------ | -------- | -------- |  ---- |	---- |	
| [Global Application Acceleration Platform (GAAP)](https://intl.cloud.tencent.com/document/product/608)  | Resource level | &#10003;  |  -   |  -  |-  |
| [Enterprise Content Delivery Network (ECDN)](https://intl.cloud.tencent.com/document/product/570/10364)  | Service level | &#10003;  |  - | -  |-  |
| [Content Delivery Network (CDN)](https://intl.cloud.tencent.com/document/product/228)| Operation level<sup>1</sup> | &#10003;   |  -   | &#10003; |[Access Control](https://intl.cloud.tencent.com/document/product/228/12722)  |

><sup>1</sup> At present, CDN does not support permission management through policy syntax, and instead supports permission management through projects. For more information, see [CDN Permissions](https://intl.cloud.tencent.com/document/product/228/12722).

## Middleware	

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |
| ------------------------------------------------------------| ------ | -------- | -------- |  ---- |	 ---- |
| [Cloud Message Queue (CMQ)](https://intl.cloud.tencent.com/document/product/406) | Resource level   | &#10003;  | - |  - |- |
| [CMQ Kafka (CKafka)](https://intl.cloud.tencent.com/document/product/597) | Resource level | &#10003; | - | &#10003;   |-|
| [API Gateway](https://intl.cloud.tencent.com/document/product/628)     | Resource level | &#10003;  | -  | &#10003; | - |

## Domain Names and Websites	

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |
| ------------------------------------------------------------ | ------ | --------| ----- | ---- |	---- |	
| [Website ICP Filing](https://intl.cloud.tencent.com/document/product/1039)   | Service level | &#10003;   | -   |  - |- |	

## Network Security	

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |
| ----------------------------------------------------------- | ------ | -------- | ----- | ---- | ---- |
| [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029) | Service level | &#10003; | -   |  - | - |
| [Anti-DDoS Advanced](https://intl.cloud.tencent.com/document/product/297) | Service level  | &#10003; | -   |  - | - |

## Security Management

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |
| ------------------------------------------------------------ | ------ | -------- | ------- | ---- |  ---- | 
| [Security Operations Center](https://intl.cloud.tencent.com/document/product/1008)    | Operation level | &#10003; | -   | &#10003; |-  | 

## Application Security

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |
| ------------------------------------------------------------ | ------ | -------- | ------ |---- |	---- |	
| [Web Application Firewall (WAF)](https://intl.cloud.tencent.com/document/product/627)  | Operation level | &#10003;  | -  |  - |- |

## Video Services

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |
| ------------------------------------------------------------ | ------ | -------- | -------- | ---- |	---- |	
| [Live Video Broadcasting (LVB)](https://intl.cloud.tencent.com/document/product/267)   | Resource level | &#10003; | &#10003;  |  &#10003;  |[Access Control](https://intl.cloud.tencent.com/document/product/267/32468) |		

## Big Data Platform

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |
| ----------------------------------------------------------- | ------ | --------| ----- |  ---- |	 ---- |
| [Elastic MapReduce (EMR)](https://intl.cloud.tencent.com/document/product/1026)   | Operation level | &#10003;  | -   |  &#10003;  | [Access Control](https://intl.cloud.tencent.com/document/product/1026/31100) |
| [Tencent Sparkling Data Warehouse Suite](https://intl.cloud.tencent.com/document/product/1019)  | Resource level | &#10003; | -  | &#10003;    | - |
| [Oceanus](https://intl.cloud.tencent.com/document/product/1000)  | Service level   | &#10003;     | -  | &#10003;  | - |
| [Elasticsearch Service (ES)](https://intl.cloud.tencent.com/document/product/845)  | Operation level | &#10003; | -   |  -  | [Access Control](https://intl.cloud.tencent.com/document/product/845/19550) |

## Image Recognition

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |
| ------------------------------------------------------------ | ------ | -------- | -------- | ---- |	 ---- |		
| [Optical Character Recognition (OCR)](https://intl.cloud.tencent.com/document/product/1005) | Service level | &#10003;| -  | - | - |	

## Gaming Services

| Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |
| ----------------------------------------------------------- | ------ | -------- | ----- |  ---- |	 ---- |		
| [Game Multimedia Engine (GME)](https://intl.cloud.tencent.com/document/product/607)  | Resource level | &#10003;| -   |  -    | -   |

## Mobile Services	

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |
| ------------------------------------------------------------  | ------ | -------- | ------- | ---- |	---- |	
| [Tencent Push Notification Service (TPNS)](https://intl.cloud.tencent.com/document/product/1024)   | Operation level | &#10003; | -   |  -   |-   |

## Cloud Communication	

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |
| ------------------------------------------------------------ | ------ | -------- | ----- | ---- |	---- |
| [SMS](https://intl.cloud.tencent.com/document/product/382) | Operation level | &#10003; | -   | -  |-  |		
	
## Cloud Resource Management

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |
| ----------------------------------------------------------- | ------ | -------- | ----- | ---- |	 ---- |	
| [Tag](https://intl.cloud.tencent.com/document/product/651) | Operation level | &#10003;  | - |  - | - |	

## Management and Auditing

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |
| ------------------------------------------------------------| ------ | --------| ----- |  ---- |		 ---- |
| [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598)  | Operation level | &#10003; | -   | -    | [Access Control](https://intl.cloud.tencent.com/document/product/598/17848)   |
| [CloudAudit (CA)](https://intl.cloud.tencent.com/document/product/1021)  | Operation level | &#10003; | -   | &#10003;    | -   |
| [Tencent Cloud Organization (TCO)](https://intl.cloud.tencent.com/document/product/1031) | Operation level | &#10003; | -  |- | -   |

## Monitoring and OPS	

 | Service                                                         | Authorization Granularity | Console | Using Tags for Authorization | Service Role | Reference Documentation |
| ------------------------------------------------------------  | ------ | -------- | ----- | ---- |	---- |
| [Cloud Monitor (CM)](https://intl.cloud.tencent.com/document/product/248) | Operation level | &#10003;  | -  |  - |- |	
| [Key Management Service (KMS)](https://intl.cloud.tencent.com/document/product/1030/) | Resource level | &#10003;  | -  |  -     |[Access Control](https://intl.cloud.tencent.com/document/product/1030/31978) |	
| [Migration Service Platform (MSP)](https://intl.cloud.tencent.com/document/product/1036/)  | -   | -  | -   |&#10003;    |- |	