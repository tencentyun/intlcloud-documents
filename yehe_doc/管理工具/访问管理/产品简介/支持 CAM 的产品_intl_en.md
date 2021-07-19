<style>
table th:nth-of-type(1) {
width: 27%;        
}
table th:nth-of-type(2) {
width: 15%;        
}
table th:nth-of-type(3) {
width:12%;        
}
table th:nth-of-type(4) {
width: 13%;        
}
table th:nth-of-type(5) {
width: 15%;        
}
table th:nth-of-type(6) {
width: 18%;        
}
</style>

## Overview	

Cloud Access Management (CAM) helps you securely manage permissions for most Tencent Cloud services. This document provides information on the products and services that support CAM in multiple dimensions, such as authorization granularity, console operation, authorization by tag, and reference documentation.
The table below lists Tencent Cloud services that support CAM.
Definitions:

- Service: name of a CAM-enabled Tencent Cloud service. For more information on a specific service, click the link to the reference document.	
- Authorization granularity: the finest authorization granularity currently supported by the service.

>? Three authorization granularity levels are supported: service level, operation level, and resource level.	
>
> - Service level: it defines whether a user has the permission to access the service as a whole. A user can have either full access or no access to the service.
> - Operation level: it defines whether a user has the permission to call a specific API of the service. For example, granting an account read-only access to the CVM service is an authorization at the operation level.	
> - Resource level: it is the finest authorization granularity which defines whether a user has the permission to access specific resources. For example, granting an account read/write access to a specific CVM instance is an authorization at the resource level.

- Console: whether sub-accounts can access the service through the console. `&#10003;` means yes, while `-` means no.	
- Authorization by tag: whether the service supports using tags for permission management. `&#10003;` means yes, while `-` means no.		
- [Service role](https://intl.cloud.tencent.com/document/product/598/19420): whether the service can access other services as a role entity. `&#10003;` means yes, while `-` means no.	
- Reference document: link to the document on CAM-based access control for the service. `-` means no documentation available yet.

## Computation	

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role | 	Reference Document |	
| ------------------------------------------------------------| ------ | -------- | ------- |  ---- |	---- |	
| [Cloud Virtual Machine (CVM)](https://intl.cloud.tencent.com/document/product/213) <sup>1</sup> | Resource level  | &#10003;      |&#10003;    |  &#10003;  |	[CAM Guide](https://intl.cloud.tencent.com/document/product/213/10315)   |
| [Auto Scaling (AS)](https://intl.cloud.tencent.com/document/product/377) | Resource level   | &#10003;      | &#10003;  | &#10003;    |	-    |	
| [BatchCompute](https://intl.cloud.tencent.com/document/product/599)  | Resource level | &#10003;         |  &#10003;  | -    |[CAM Guide](https://intl.cloud.tencent.com/document/product/599/33471)   |		

>?<sup>1</sup> In CVM, [GPU Cloud Computing (GCC)](https://intl.cloud.tencent.com/document/product/560) and [CVM Dedicated Host (CDH)](https://intl.cloud.tencent.com/document/product/416) support CAM.


## Container
| [Tencent Kubernetes Engine (TKE)](https://intl.cloud.tencent.com/document/product/457) | Resource level | &#10003;       | &#10003; | &#10003;    |	[CAM Guide](https://intl.cloud.tencent.com/document/product/457/11542)  |	
| [Tencent Container Registry (TCR)](https://intl.cloud.tencent.com/document/product/1051) | Resource level  | Resource level | &#10003; | - | &#10003; |	[CAM Guide](https://intl.cloud.tencent.com/document/product/1051/37246)  |	

## Storage	

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role | 	Reference Document |	
| ------------------------------------------------------------ | ------ | --------  | ------- | ---- |	---- |	
| [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436) | Resource level | &#10003;       | &#10003; <sup>1</sup>  | &#10003;   |	[CAM Guide](https://intl.cloud.tencent.com/document/product/436/12470)   |
| [Cloud File Storage (CFS)](https://intl.cloud.tencent.com/document/product/582) | Resource level | &#10003;        | &#10003;  |  &#10003;    |[CAM Guide](https://intl.cloud.tencent.com/document/product/582/14679)   |			
| [Cloud Block Storage (CBS)](https://intl.cloud.tencent.com/document/product/362) | Resource level | &#10003;       | &#10003;  |  -    |-    |	
| [Cloud Data Migration (CDM)](https://intl.cloud.tencent.com/document/product/623)  | Service level | &#10003;        | -  |  - | - |	
| [Cloud Log Service (CLS)](https://intl.cloud.tencent.com/document/product/614)  | Resource level | &#10003;        | -  | &#10003; |[CAM Guide](https://intl.cloud.tencent.com/document/product/614/32854)    |	

> ?<sup>1</sup> In COS, `GetService` and `PutBucket` do not support authorization by tag for the time being; therefore, they need to be authorized with a separate custom policy.

## Networking	

| Service | Authorization Granularity | Console | Authorization by Tag | Service Role | 	Reference Document |	
| ------------------------------------------------------------ | ------ | -------- | ------- | ---- |	 ---- |
| [Cloud Load Balancer (CLB)](https://intl.cloud.tencent.com/document/product/214)   | Resource level | &#10003;      | &#10003;    |    &#10003;  |	[CAM Guide](https://intl.cloud.tencent.com/document/product/214/9777) |	
| [Virtual Private Cloud (VPC)](https://intl.cloud.tencent.com/document/product/215)<sup>1</sup>  | Resource level | &#10003;        | &#10003;     | - |	 - |	
| [Direct Connect (DC)](https://intl.cloud.tencent.com/document/product/216) | Resource level   | &#10003;       | &#10003;       | -  |	 - |	

>?<sup>1</sup> In VPC, [Elastic Network Interface (ENI)](https://intl.cloud.tencent.com/document/product/576), [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015), [Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), [Flow Logs (FL)](https://intl.cloud.tencent.com/document/product/682), [Anycast Internet Acceleration (AIA)](https://intl.cloud.tencent.com/document/product/644), [Cloud Connect Network (CCN)](https://intl.cloud.tencent.com/document/product/1003), and [Bandwidth Package (BWP)](https://intl.cloud.tencent.com/document/product/684) support CAM.

## CDN and Acceleration	

| Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |	
| ------------------------------------------------------------| ------ | -------- | -------- |  ---- |	---- |	
| [Global Application Acceleration Platform (GAAP)](https://intl.cloud.tencent.com/document/product/608)  | Resource level | &#10003;  | &#10003;   |  -  |-  |
| [Enterprise Content Delivery Network (ECDN)](https://intl.cloud.tencent.com/document/product/570)  | Resource level | &#10003;  |  &#10003; | -  | -  |
| [Content Delivery Network (CDN)](https://intl.cloud.tencent.com/document/product/228)<sup>1</sup>| Resource level | &#10003;   |  &#10003;   | &#10003; |[CAM Guide](https://intl.cloud.tencent.com/document/product/228/35229)  |


## Database	

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |	
| ------------------------------------------------------------ | ------ | --------| --------- | ---- |	---- |
| [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236)  | Resource level | &#10003; | &#10003;  |  &#10003; |	[CAM Guide](https://intl.cloud.tencent.com/document/product/236/14469) |		
| [TencentDB for MariaDB](https://intl.cloud.tencent.com/document/product/237)  | Resource level | &#10003;  | &#10003;    | &#10003;    |[CAM Guide](https://intl.cloud.tencent.com/document/product/237/35441) |	
| [TencentDB for SQL Server](https://intl.cloud.tencent.com/document/product/238)  | Resource level | &#10003;  | &#10003;    | -     |[CAM Guide](https://intl.cloud.tencent.com/document/product/238/34583) |	
| [TencentDB for PostgreSQL](https://intl.cloud.tencent.com/document/product/409)  | Resource level | &#10003;  | &#10003;   | -     | - |
| [TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/1042)  | Resource level | &#10003;  |  &#10003;    | -    |[CAM Guide](https://intl.cloud.tencent.com/document/product/1042/33343) |	
| [TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239)   | Resource level | &#10003; | -  | - |[CAM Guide](https://intl.cloud.tencent.com/document/product/239/32845) |	
| [TencentDB for MongoDB](https://intl.cloud.tencent.com/document/product/240) | Resource level | &#10003; | &#10003;   |&#10003;|[CAM Guide](https://intl.cloud.tencent.com/document/product/240/32839) |			
| [Data Transmission Service (DTS)](https://intl.cloud.tencent.com/document/product/571)  | Resource level |  &#10003;  | &#10003;   | &#10003;    | - |
| [TcaplusDB](https://intl.cloud.tencent.com/document/product/1016)  | Resource level |  &#10003;  | &#10003;    | -    | - |		
| [TencentDB for DBbrain](https://intl.cloud.tencent.com/document/product/1035) | Resource | &#10003;  | -    | -    |[CAM Guide](https://intl.cloud.tencent.com/document/product/1035/36050)|	
| [TDSQL-A for PostgreSQL](https://cloud.tencent.com/document/product/1378) | Resource level | &#10003; | &#10003; | &#10003; | [CAM Guide](https://cloud.tencent.com/document/product/1378/54476) |


## Serverless	

| Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |	
| ------------------------------------------------------------| ------ | -------- | -------- |  ---- |	---- |	
| [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583)  | Resource level | &#10003;        |  &#10003;  | &#10003;   |[CAM Guide](https://intl.cloud.tencent.com/document/product/583/18014)  |	
| [Serverless Application Center](https://intl.cloud.tencent.com/document/product/1040)  | Resource level | - |  -   |  &#10003;   | -   |
| Serverless Framework | -    | -    | -    | &#10003; | -    |



## Middleware	

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |
| ------------------------------------------------------------| ------ | -------- | -------- |  ---- |	 ---- |
| [Cloud Message Queue (CMQ)](https://intl.cloud.tencent.com/document/product/406) | Resource level   | &#10003;  | &#10003; |  - |	[CAM Guide](https://intl.cloud.tencent.com/document/product/406/34257) |
| [Cloud Kafka (CKafka)](https://intl.cloud.tencent.com/document/product/597) | Resource level | &#10003; | &#10003; | &#10003;   | - |
| [API Gateway](https://intl.cloud.tencent.com/document/product/628)     | Resource level | &#10003;  | &#10003;  | &#10003; |[CAM Guide](https://intl.cloud.tencent.com/document/product/628/34064)|

## Data Processing	

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |
| ------------------------------------------------------------ | ------ | --------| ----- | ---- |	 ---- |	
| [Cloud Infinite (CI)](https://intl.cloud.tencent.com/document/product/1045)   | Resource level    | &#10003;   | -   | &#10003; |	[CAM Guide](https://intl.cloud.tencent.com/document/product/1045/33449) |

## Domain Names and Websites	

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |
| ------------------------------------------------------------ | ------ | --------| ----- | ---- |	---- |	
| [Website ICP Filing](https://intl.cloud.tencent.com/document/product/1022)   | Service level | &#10003;   | -   |  - |	- |	
| [SSL Certificates Service](https://intl.cloud.tencent.com/document/product/1007)   | Resource level    | &#10003;   | -   |  - |	- |	



## Data Security

| Service | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------------------------------ | ------ | -------- | ------- | ---- |  ---- |
| [Key Management Service (KMS)](https://intl.cloud.tencent.com/document/product/1030) | Resource level   | &#10003;  | &#10003;  |  -     |[CAM Guide](https://intl.cloud.tencent.com/document/product/1030/31978) |


## Security Management

| Service | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------------------------------ | ------ | -------- | ------- | ---- |  ---- |
| [Security Operations Center](https://intl.cloud.tencent.com/document/product/1008)    | Operation level | &#10003; | -   | &#10003; |-  |

## Application Security

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |
| ------------------------------------------------------------ | ------ | -------- | ------ |---- |	---- |	
| [Web Application Firewall (WAF)](https://intl.cloud.tencent.com/document/product/627)  | Operation level | &#10003;  | -  |  - |- |

## Video Services

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |
| ------------------------------------------------------------ | ------ | -------- | -------- | ---- |	---- |	
| [Tencent Real-Time Communication (TRTC)](https://intl.cloud.tencent.com/document/product/647)   | Resource level | &#10003; | &#10003;  |  - |	-|	
| [Cloud Streaming Services (CSS)](https://intl.cloud.tencent.com/document/product/267)   | Resource level | &#10003; | &#10003;  |  &#10003;  |	[CAM Guide](https://intl.cloud.tencent.com/document/product/267/32468) |	
| [Video on Demand (VOD)](https://intl.cloud.tencent.com/document/product/266)    | Resource level   | &#10003;  | &#10003;    |  &#10003;  |	[CAM Guide](https://intl.cloud.tencent.com/document/product/266/33970)  |	
| [Media Processing Service (MPS)](https://intl.cloud.tencent.com/document/product/1041)    | Service level   | &#10003;  | -    |   &#10003;   |	-  |		
| [StreamLive](https://intl.cloud.tencent.com/document/product/1048)    | Operation level   | &#10003;  | -    |   -   |	-  |	
| [StreamPackage](https://intl.cloud.tencent.com/document/product/1063)    | Operation level   | &#10003;  | -    |   -   |	-  |	

## Big Data Platform

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |
| ----------------------------------------------------------- | ------ | --------| ----- |  ---- |	 ---- |
| [Elastic MapReduce (EMR)](https://intl.cloud.tencent.com/document/product/1026)   | Resource level | &#10003;  | &#10003;   |  &#10003;  |	 [CAM Guide](https://intl.cloud.tencent.com/document/product/1026/31100) |
| [Elasticsearch Service (ES)](https://intl.cloud.tencent.com/document/product/845)  | Resource level | &#10003; | &#10003;   |  -  | 	[CAM Guide](https://intl.cloud.tencent.com/document/product/845/19550) |

## Image Recognition

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |
| ------------------------------------------------------------ | ------ | -------- | -------- | ---- |	 ---- |		
| [Optical Character Recognition (OCR)](https://intl.cloud.tencent.com/document/product/1005) | Service level | &#10003;| -  | - |	 - |	

## Gaming Services

| Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |
| ----------------------------------------------------------- | ------ | -------- | ----- |  ---- |	 ---- |		
| [Game Multimedia Engine (GME)](https://intl.cloud.tencent.com/document/product/607)  | Resource level | &#10003;| &#10003;   |  -    |	 -   |
| [Game Server Elastic-scaling (GSE)](https://intl.cloud.tencent.com/document/product/1055)  | Resource level | &#10003;| &#10003;   |  &#10003;    |  [CAM Guide](https://intl.cloud.tencent.com/zh/document/product/1055/37776)   |
| [Game Player Matchmaking (GPM)](https://intl.cloud.tencent.com/document/product/1072) | Resource level   | &#10003; | &#10003;         | &#10003; | - |


## Mobile Services	

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |
| ------------------------------------------------------------  | ------ | -------- | ------- | ---- |	---- |	
| [Tencent Push Notification Service (TPNS)](https://intl.cloud.tencent.com/document/product/1024)   | Resource level  | &#10003; | -   |  -   |	[CAM Guide](https://intl.cloud.tencent.com/document/product/1024/35288)   |

## Cloud Communication	

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |
| ------------------------------------------------------------ | ------ | -------- | ----- | ---- |	---- |
| [Instant Messaging (IM)](https://intl.cloud.tencent.com/document/product/1047)   | Resource level | &#10003;   | -  |  - | - |
| [Short Message Service (SMS)](https://intl.cloud.tencent.com/document/product/382) | Resource level | &#10003; | &#10003;   | -  |	-  |	

## Cloud Resource Management

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |
| ----------------------------------------------------------- | ------ | -------- | ----- | ---- |	 ---- |	
| [Tag](https://intl.cloud.tencent.com/document/product/651) | Operation level | &#10003;  | - |  - |	 - |	
| [Tencent Infrastructure as Code (TIC)](https://intl.cloud.tencent.com/document/product/1043) | Service level | -  | - | &#10003; |	 - |	

## Management and Auditing

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |
| ------------------------------------------------------------| ------ | --------| ----- |  ---- |		 ---- |
| [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598)  | Operation level | &#10003; | -   | -    | [CAM Guide](https://intl.cloud.tencent.com/document/product/598/17848)   |
| [CloudAudit](https://intl.cloud.tencent.com/document/product/1021)  | Operation level | &#10003; | -   | &#10003;    | -   |
| [Tencent Cloud Organization (TCO)](https://intl.cloud.tencent.com/document/product/1031) | Operation level | &#10003; | -  |- | -   |

## Monitoring and OPS	

 | Service | Authorization Granularity | Console | Authorization by Tag | Service Role |	Reference Document |
| ------------------------------------------------------------  | ------ | -------- | ----- | ---- |	---- |
| [Cloud Monitor (CM)](https://intl.cloud.tencent.com/document/product/248) | Resource level | &#10003;  | &#10003;  |  &#10003; |	- |		
| [Migration Service Platform (MSP)](https://intl.cloud.tencent.com/document/product/1036)  | Service level   | &#10003; | -   |&#10003;    |	- |	









