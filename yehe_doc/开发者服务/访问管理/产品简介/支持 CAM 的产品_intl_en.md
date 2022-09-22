## Overview 

Cloud Access Management (CAM) helps you securely manage permissions for most Tencent Cloud services. This document provides information on the products and services that support CAM in multiple dimensions, such as authorization granularity, console operation, authorization by tag, and reference documentation.
The table below lists Tencent Cloud services that support CAM.
Definitions:

- Service: Name of a CAM-enabled Tencent Cloud service. For more information on a specific service, click the link to the reference document.  
- Authorization granularity: The finest authorization granularity currently supported by the service.

> ? Three authorization granularity levels are supported: service level, operation level, and resource level.  
>
> - Service level: It defines whether a user has the permission to access the service as a whole. A user can have either full access or no access to the service.
> - Operation level: It defines whether a user has the permission to call a specific API of the service. For example, granting an account read-only access to the CVM service is an authorization at the operation level.  
> - Resource level: It is the finest authorization granularity which defines whether a user has the permission to access specific resources. For example, granting an account read/write access to a specific CVM instance is an authorization at the resource level.

- Console: Whether sub-accounts can access the service through the console. "&#10003;" means yes, while "-" means no.  
- Authorization by tag: Whether the service supports using tags for permission management. "&#10003;" means yes, while "-" means no.   
- [Service role](https://intl.cloud.tencent.com/document/product/598/19420): Whether the service can access other services as a role entity. "&#10003;" means yes, while "-" means no.  
- Reference document: Link to the document on CAM-based access control for the service. `-` means no documentation available yet.

## Compute 

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [Cloud Virtual Machine (CVM)](https://intl.cloud.tencent.com/document/product/213) <sup>1</sup> | cvm | Resource level  | &#10003;      |&#10003;    |  &#10003;  |[Access Management](https://intl.cloud.tencent.com/document/product/213/10311)   |
| [Auto Scaling (AS)](https://intl.cloud.tencent.com/document/product/377) | as | Resource level   | &#10003;      | &#10003;  | &#10003;    |-    |
| [BatchCompute](https://intl.cloud.tencent.com/document/product/599)  | batch | Resource level | &#10003;         |  &#10003;  | -    |[Cloud Access Management](https://intl.cloud.tencent.com/document/product/599/33471)   |
| [Edge Computing Machine (ECM)](https://intl.cloud.tencent.com/document/product/1119) | ecm | Resource level   | &#10003; | &#10003;         | -        | -                                                            |
| [Tencent Cloud Lighthouse (Lighthouse)](https://intl.cloud.tencent.com/document/product/1103) | lighthouse | Resource level   | &#10003; | &#10003;         | -        | -                                                            |
| [Tencent Cloud Automation Tools (TAT)](https://intl.cloud.tencent.com/document/product/1147) | tat |Resource level   | &#10003; | -                | -        | [Cloud Access Management](https://intl.cloud.tencent.com/document/product/1147/46037) |

> ?<sup>1</sup> In CVM, [GPU Cloud Computing (GCC)](https://intl.cloud.tencent.com/document/product/560), [CVM Dedicated Host (CDH)](https://intl.cloud.tencent.com/document/product/416), and [Cloud Block Storage (CBS)](https://intl.cloud.tencent.com/document/product/362) support CAM.



## Container

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [Tencent Kubernetes Engine (TKE)](https://intl.cloud.tencent.com/document/product/457)   | tke | Resource level   | &#10003; | &#10003;         | &#10003; | [Permission Management](https://intl.cloud.tencent.com/document/product/457/37361) |
| [Tencent Container Registry (TCR)](https://intl.cloud.tencent.com/document/product/1051) | tcr  | Resource level | &#10003; | - | &#10003; |[Overview](https://intl.cloud.tencent.com/document/product/1051/37246)  |
|Tencent Cloud Mesh (TCM)                                                     | tcm |Resource level   | &#10003; | -                | &#10003; | -                                                            |



## Storage 

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436) <sup>1</sup>  | cos | Resource level   | &#10003; | &#10003;  | &#10003; | [Access Control and Permission Management](https://intl.cloud.tencent.com/document/product/436/12473) |
| [Cloud File Storage (CFS)](https://intl.cloud.tencent.com/document/product/582)   | cfs | Resource level   | &#10003; | &#10003;              | &#10003; | [Access Management](https://intl.cloud.tencent.com/document/product/582/14679) |
| [Cloud HDFS (CHDFS)](https://intl.cloud.tencent.com/document/product/1106)   | chdfs | Resource level   | &#10003; | &#10003;              | -        | [Authorizing Access with CAM](https://intl.cloud.tencent.com/document/product/1106/41966) |
| [Cloud Log Service (CLS)](https://intl.cloud.tencent.com/document/product/614)   | cls | Resource level   | &#10003; | &#10003;                   | &#10003; | [Permission Management](https://intl.cloud.tencent.com/document/product/614/32853) |

> ?<sup>1</sup> In COS, `GetService` and `PutBucket` do not support authorization by tag for the time being; therefore, they need to be authorized with a separate custom policy.



## Network 

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [Cloud Load Balancer (CLB)](https://intl.cloud.tencent.com/document/product/214)   | clb | Resource level   | &#10003; | &#10003;         | &#10003; | [Cloud Access Management](https://intl.cloud.tencent.com/document/product/214/9776) |
| [Virtual Private Cloud (VPC)](https://intl.cloud.tencent.com/document/product/215) <sup>1</sup> | vpc | Resource level   | &#10003; | &#10003;         | -        | [Access Management](https://intl.cloud.tencent.com/document/product/215/31859) |
| [Direct Connect (DC)](https://intl.cloud.tencent.com/document/product/216)   | dc | Resource level   | &#10003; | &#10003;         | -        | [Access Policy Types](https://intl.cloud.tencent.com/document/product/216/39512) |

> ?<sup>1</sup> In VPC, [Elastic Network Interface (ENI)](https://intl.cloud.tencent.com/document/product/576), [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015), [Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), [Flow Logs (FL)](https://intl.cloud.tencent.com/document/product/682), [Anycast Internet Acceleration (AIA)](https://intl.cloud.tencent.com/document/product/644), [Cloud Connect Network (CCN)](https://intl.cloud.tencent.com/document/product/1003), and [Bandwidth Package (BWP)](https://intl.cloud.tencent.com/document/product/684) support CAM.

## CDN and Acceleration  

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [Global Application Acceleration Platform (GAAP)](https://intl.cloud.tencent.com/document/product/608) | gaap | Resource level   | &#10003; | &#10003;         | -        | -                                                            |
| [Enterprise Content Delivery Network (ECDN)](https://intl.cloud.tencent.com/document/product/570) | ecdn | Resource level   | &#10003; | &#10003;         | -        | [Console Permission Description](https://intl.cloud.tencent.com/document/product/570/35819) |
| [Content Delivery Network (CDN)](https://intl.cloud.tencent.com/document/product/228) <sup>1</sup> | cdn | Resource level   | &#10003; | &#10003;         | &#10003; | [Console Permissions](https://intl.cloud.tencent.com/document/product/228/35229) |

> ?<sup>1</sup> In CDN, [Secure Content Delivery Network (SCDN)](https://intl.cloud.tencent.com/products/scdn) supports CAM.

## Database  

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236) | cdb | Resource level   | &#10003; | &#10003;         | &#10003; | [Access Management](https://intl.cloud.tencent.com/document/product/236/14465) |
| [TDSQL-C](https://intl.cloud.tencent.com/document/product/1098) | cynosdb | Resource level   | &#10003; | &#10003;         | -        | [Access Management](https://intl.cloud.tencent.com/document/product/1098/40639) |
| [TencentDB for MariaDB](https://intl.cloud.tencent.com/document/product/237) | mariadb | Resource level   | &#10003; | &#10003;         | &#10003; | [CAM](https://intl.cloud.tencent.com/document/product/237/35439) |
| [TencentDB for SQL Server](https://intl.cloud.tencent.com/document/product/238) | sqlserver | Resource level   | &#10003; | &#10003;         | -        | [CAM](https://intl.cloud.tencent.com/document/product/238/34582) |
| [TencentDB for PostgreSQL](https://intl.cloud.tencent.com/document/product/409) | postgres | Resource level   | &#10003; | &#10003;         | -        | [Overview](https://intl.cloud.tencent.com/document/product/409/38834) |
| [TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/1042) | tdmysql | Resource level   | &#10003; | &#10003;         | -        | [Access Management](https://intl.cloud.tencent.com/document/product/1042/33342) |
| [TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239) | redis | Resource level   | &#10003; | &#10003;               | -        | [Access Management](https://intl.cloud.tencent.com/document/product/239/32844) |
| [TencentDB for MongoDB](https://intl.cloud.tencent.com/document/product/240) | mongodb | Resource level   | &#10003; | &#10003;         | &#10003; | [Access Management](https://intl.cloud.tencent.com/document/product/240/32838) |
| [TencentDB for CTSDB](https://intl.cloud.tencent.com/document/product/1100) | ctsdb | Resource level   | &#10003; | &#10003;         | -        | [Overview](https://intl.cloud.tencent.com/document/product/1100/40913) |
| [TcaplusDB](https://intl.cloud.tencent.com/document/product/1016) | tcaplusdb | Resource level   | &#10003; | &#10003;         | -        | [Overview](https://intl.cloud.tencent.com/document/product/1016/35749) |
| [TencentDB for DBbrain](https://intl.cloud.tencent.com/document/product/1035) | dbbrain | Resource level   | &#10003; | -                | -        | - |
| [Data Transmission Service (DTS)](https://intl.cloud.tencent.com/document/product/236) | dts | Resource level   | &#10003; | &#10003;         | &#10003; | - |


## Serverless 

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583)     | scf | Resource level   | &#10003; | &#10003;         | &#10003; | [Permission Management](https://intl.cloud.tencent.com/document/product/583/9203) |
| [Serverless Application Center (SAC)](https://intl.cloud.tencent.com/document/product/1040) | sls | Resource level   | &#10003; | -                | &#10003; | [Access Management Configuration](https://intl.cloud.tencent.com/document/product/1040/36859) |
| [EventBridge](https://intl.cloud.tencent.com/document/product/1108)  | eb | Resource level   | &#10003; | -                | &#10003; | -                                                            |




## Middleware  

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [Cloud Message Queue (CMQ) - queue model](https://intl.cloud.tencent.com/zh/document/product/406) | cmqqueue | Resource level   | &#10003; | &#10003;         | -        | [Users and Permissions](https://intl.cloud.tencent.com/zh/document/product/406/34253) |
| [Cloud Message Queue (CMQ) - topic model](https://intl.cloud.tencent.com/zh/document/product/406) | cmqtopic | Resource level   | &#10003; | &#10003;         | -        | [Users and Permissions](https://intl.cloud.tencent.com/zh/document/product/406/34253) |
| [CKafka](https://intl.cloud.tencent.com/document/product/597) | ckafka | Resource level   | &#10003; |-        | &#10003; | [Configuring ACL Policy](https://intl.cloud.tencent.com/document/product/597/39084) |
| [API Gateway](https://intl.cloud.tencent.com/document/product/628)   | apigw | Resource level   | &#10003; | &#10003;         | &#10003; | [Permission Management](https://intl.cloud.tencent.com/document/product/628/34064) |
| [TDMQ for Pulsar](https://intl.cloud.tencent.com/document/product/1110) | tdmq | Resource level   | &#10003; | &#10003;            | -        | [Access Management](https://intl.cloud.tencent.com/document/product/1110/42935) |


## Microservice 

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [Tencent Cloud Elastic Microservice (TEM)](https://intl.cloud.tencent.com/document/product/1094) | tem | Operation level   | &#10003; | -                | &#10003; | -                                                            |




## Data Processing 

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [Cloud Infinite (CI)](https://intl.cloud.tencent.com/zh/document/product/1045) | ci | Resource level   | &#10003; | -                | &#10003; | [Access Management](https://intl.cloud.tencent.com/zh/document/product/1045/33448) |

## Domain Name and Website  

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [SSL Certificate Service](https://intl.cloud.tencent.com/document/product/1007)    | ssl |Resource level   | &#10003; |  &#10003;                | &#10003; | - |
| [HTTPDNS](https://intl.cloud.tencent.com/document/product/1130) | httpdns | Operation level   | &#10003; | -                | -        | [Overview](https://intl.cloud.tencent.com/document/product/1130/44478) |
| [Private DNS](https://intl.cloud.tencent.com/document/product/1097) | privatedns | Resource level   | &#10003; | -                | -        | [Access Control Overview](https://intl.cloud.tencent.com/document/product/1097/40575) |




## Terminal Security

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [Cloud Workload Protection Platform (CWPP)](https://intl.cloud.tencent.com/document/product/296) | cwpp | Operation level   | &#10003; | -                | &#10003; | -        |



## Data Security


| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [Data Security Center](https://intl.cloud.tencent.com/document/product/1126) | dsgc       | Operation level   | ✓      | -                | ✓        | -                                                            |
| [Key Management Service (KMS)](https://intl.cloud.tencent.com/document/product/1030) | kms        | Resource level   | ✓      | ✓                | -        | [Access Control](https://intl.cloud.tencent.com/document/product/1030/31977) |
| [Secrets Manager  (SSM)](https://intl.cloud.tencent.com/document/product/1078) | ssm        | Resource level   | ✓      | ✓                | ✓        | [Overview](https://intl.cloud.tencent.com/document/product/1078/38610) |


## Security Management

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [Security Operations Center (SOC)](https://intl.cloud.tencent.com/zh/document/product/1008) | ssa | Operation level   | &#10003; | -                | &#10003; | -        |

## Application Security

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | -------- |
| [Web Application Firewall (WAF)](https://intl.cloud.tencent.com/document/product/627) | waf       | Operation level   | ✓      | ✓                | -        | -        |
| [Vulnerability Scan Service (VSS)](https://intl.cloud.tencent.com/document/product/1142) | cws        | Operation level   | ✓      | -                | ✓        | -        |


## Video Services

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------------------------------ | ----------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [Tencent Real-Time Communication (TRTC)](https://intl.cloud.tencent.com/document/product/647) | trtc        | Resource level   | ✓      | ✓                | -        | [Overview](https://intl.cloud.tencent.com/document/product/647/38319) |
| [Cloud Streaming Services (CSS)](https://intl.cloud.tencent.com/document/product/267)     | consolelive | Resource level   | ✓      | ✓                | ✓        | [CAM-Based Access Control](https://intl.cloud.tencent.com/document/product/267/32468) |
| [Video on Demand (VOD)](https://intl.cloud.tencent.com/document/product/266)     | consolevod  | Resource level   | ✓      | ✓                | ✓        | [Overview](https://intl.cloud.tencent.com/document/product/266/33970) |
| [Media Processing Service (MPS)](https://intl.cloud.tencent.com/document/product/1041)   | mps         | Service level   | ✓      | -                | ✓        | -                                                            |



## Data Analysis

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [Elastic MapReduce (EMR)](https://intl.cloud.tencent.com/document/product/1026) | emr        | Resource level   | ✓      | ✓                | ✓        | [Collaborator/Sub-account Permissions](https://intl.cloud.tencent.com/document/product/1026/31100) |
| [Elasticsearch Service (ES)](https://intl.cloud.tencent.com/document/product/845) | es         | Resource level   | ✓      | ✓                | -        | [CAM-based Access Control Configuration](https://intl.cloud.tencent.com/document/product/845/19550) |
| [Cloud Data Warehouse for ClickHouse (CDWCH)](https://intl.cloud.tencent.com/document/product/1129) | cdwch      | Resource level   | ✓      | ✓                | -        | -                                                            |



## OCR

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [Optical Character Recognition (OCR)](https://intl.cloud.tencent.com/document/product/1005) | ocr | Service level   | &#10003; | -                | -        | -        |



## Face Recognition

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [Face Recognition](https://intl.cloud.tencent.com/document/product/1059)  | iai | Resource level   | &#10003; | -                | &#10003; | - |
| [FaceID](https://intl.cloud.tencent.com/document/product/1061) | faceid | Service level   | &#10003; | -                | &#10003; | -                                                            |


## Speech Technology 

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [Automatic Speech Recognition (ASR)](https://intl.cloud.tencent.com/document/product/1118) | asr | Resource level   | &#10003; | &#10003;         | -        | [Overview](https://intl.cloud.tencent.com/document/product/1118/43349) |


## Gaming Services

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [Game Multimedia Engine (GME)](https://intl.cloud.tencent.com/document/product/607) | gme        | Resource level   | ✓      | ✓                | -        | -                                                            |


## Mobile Services 

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [Tencent Push Notification Service (TPNS)](https://intl.cloud.tencent.com/document/product/1024) | tpns       | Resource level   | ✓      | ✓                | -        | [Advanced Custom Configuration](https://intl.cloud.tencent.com/document/product/1024/35288) |


## Cloud Communication  

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [Instant Messaging (IM)](https://intl.cloud.tencent.com/document/product/1047) | im         | Resource level   | ✓      | ✓                | -        | - |
| [Short Message Service (SMS)](https://intl.cloud.tencent.com/document/product/382)       | consolesms | Resource level   | ✓      | ✓                | -        | [Cloud Access Management](https://intl.cloud.tencent.com/document/product/382/38453) |
| [Simple Email Service (SES)](https://intl.cloud.tencent.com/document/product/1084)  | ses        | Service level   | ✓      | -                | -        | -                                                            |



## Internet of Things  

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------------------------------ | ---------------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [IoT Hub](https://intl.cloud.tencent.com/document/product/1105) | iotcloud         | Resource level   | ✓      | ✓                | ✓        | [Sub-account Access to IoT Hub](https://intl.cloud.tencent.com/document/product/1105/41473) |




## Cloud Resource Management

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | -------- |
| [Tag](https://intl.cloud.tencent.com/document/product/651)       | tag        | Operation level   | ✓      | -                | -        | -        |
| [Tencent Infrastructure as Code (TIC)](https://intl.cloud.tencent.com/document/product/1043) | tic        | Service level   | ✓      | -                | ✓        | -        |
| [Tencent Smart Advisor (TSA)](https://intl.cloud.tencent.com/document/product/1079)    | advisor    | Service level   | ✓      | -                | ✓        | -        |


## Management and Audit

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------------------------------ | ------------ | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598)   | cam          | Operation level   | ✓      | -                | -        | [User Guide](https://intl.cloud.tencent.com/document/product/598/10590) |
| [CloudAudit](https://intl.cloud.tencent.com/document/product/1021)     | cloudaudit   | Operation level   | ✓      | -                | ✓        | -                                                            |

## Monitoring and Ops  

| Product | Abbreviation in CAM | Authorization Granularity | Console | Authorization by Tag | Service Role |Reference Document |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [Tencent Managed Service for Prometheus (TMP)](https://intl.cloud.tencent.com/document/product/1116)     | monitor    | Resource level   | ✓      | ✓                | ✓        | [Overview](https://intl.cloud.tencent.com/document/product/1116/43206) |
| [Migration Service Platform (MSP)](https://intl.cloud.tencent.com/document/product/1036) | msp        | Service level   | ✓      | -                | ✓        | -                                                            |
| [Real User Monitoring (RUM)](https://intl.cloud.tencent.com/document/product/1131) | rum        | Resource level   | ✓      | ✓                | -        | [Overview](https://intl.cloud.tencent.com/document/product/1131/44510) |


