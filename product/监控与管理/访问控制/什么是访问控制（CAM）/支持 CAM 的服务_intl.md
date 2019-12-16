## Overview
CAM (Cloud Access Management) helps you securely manage access to many Tencent Cloud resources and services.
This article contains information about CAM-enabled services, including detailed policy syntax, cloud APIs, console, authorization granularity and temporary certificates.
 CAM currently is integrated with the following Tencent Cloud services and resources. Please note that products marked with an asterisk (*) has not yet been released on the international console.
 
 Definitions:
- Service: Name of the CAM-enabled Tencent Cloud services. For more information about specific service or product, tap the link to go to the product documentation.
- Policy syntax: Whether the service enables you to use policy syntax to manage access. “✔” means “Yes”; “-” means “No”.
- Cloud API: Whether sub-account users can use Tencent Cloud API to access the service. “✔” means “Yes”; “-” means “No”.
- Console: Whether sub-account users can access the service via console. “✔” means “Yes”; “-” means “No”.
- Authorization granularity: Level of detail used to define authorization rules for controlling the access to resources and services under a Tencent Cloud account.
> Authorization granularity has three levels: Service level, operation level and resource level.
> - Service level: Whether a user can be permitted to access all of the Tencent Cloud services the Tencent Cloud account has purchased.
> - Operation level: Whether a user can be permitted to call the API of a specified Tencent Cloud service the Tencent Cloud account has purchased. For example, a user has read-only access to the Tencent Cloud account's CVM.
> - Resource level: Whether a user can be permitted to access specific resource under the Tencent Cloud account. For example: a user has read-only access to a CVM owned by the Tencent Cloud account. Resource level presents the finest authorization granularity. 
- Temporary key (STS): Whether a user can be permitted to access the service via temporary security credentials. “✔” means “Yes”; “-” means “No”.
- [Role](https://intl.cloud.tencent.com/document/product/598/19420): Whether the service can access other services as a role entity. "✔" means “Yes”; "-" means “No”.

## Compute	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [CVM](https://intl.cloud.tencent.com/document/product/213/10314) | ✔        | ✔      | ✔      | Resource level   | ✔        |   ✔  |
| CPM* | ✔        | ✔      | ✔      | Resource level   | ✔        | -    |
| [TKE](https://intl.cloud.tencent.com/document/product/457) | ✔        | ✔      | ✔      | Resource level   | ✔        | ✔    |
| [AS](https://intl.cloud.tencent.com/document/product/377)   | ✔        | ✔      | ✔      | Resource level   | ✔        | -    |
| [SCF](https://intl.cloud.tencent.com/document/product/583) | ✔        | ✔      | ✔      | Resource level   | ✔        | ✔   |
| [BatchCompute](https://intl.cloud.tencent.com/document/product/599)   | ✔        | ✔      | ✔      | Resource level   | ✔        | -    |


## Storage	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [COS](https://intl.cloud.tencent.com/document/product/436) | ✔        | ✔      | ✔      | Resource level   | ✔        | ✔   |
| [CFS](https://intl.cloud.tencent.com/document/product/582) | ✔        | ✔      | -      | Service Level   | ✔        | -    |
| CSG*  | ✔        | -      | ✔      | Service level   | -        | -    |
| [CBS](https://intl.cloud.tencent.com/document/product/362)     | ✔        | ✔      | ✔      | Resource level   | ✔        | -    |
| [CLS](https://intl.cloud.tencent.com/document/product/614)   | ✔        | -      | ✔      | Service level   | -        |  ✔ |

## Networking	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [CLB](https://intl.cloud.tencent.com/document/product/214) | ✔        | ✔      | ✔      | Resource level   | ✔        |    -  |
| [VPC](https://intl.cloud.tencent.com/document/product/215) | ✔        | ✔      | ✔      | Resource level   | ✔        | - |

## Database	
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236) | ✔        | ✔      | ✔      | Resource level   | ✔        | ✔ |
| TencentDB for CTSDB* | ✔        | ✔      | -      | Operation level   | ✔        | - |
| [TencentDB for MongoDB](https://intl.cloud.tencent.com/document/product/240)         |-        | -      | -      | -   | -        |✔    |


## CDN & Acceleration	
| Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [CDN](https://intl.cloud.tencent.com/document/product/228) | -        | ✔      | ✔      | Operation level   | ✔        | - |
| [DSA](https://intl.cloud.tencent.com/document/product/570) | ✔        | ✔      | ✔      | Service level   | ✔        |   -   |

## Middleware	
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [CMQ](https://intl.cloud.tencent.com/document/product/406) | ✔        | ✔      | ✔      | Resource level   | ✔        | - |
| [CKafka](https://intl.cloud.tencent.com/document/product/597) | ✔        | ✔      | ✔      | Resource level   | ✔        | ✔   |
| [API Gateway](https://intl.cloud.tencent.com/document/product/628)         | ✔       | ✔      | ✔      | Resource level   | -        | ✔    |
| TSF*         |-        | -      | -      | -   | -        | ✔    |


## Domains & Websites	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| Domain Service*   | ✔        | -      | ✔      | Service level   | -        |    -  |
| ICP Filing Registration*   | ✔        | -      | ✔      | Service level   | -        | - |
| HttpDNS* | ✔        | -      | ✔      | Service level   | -        | - |

## Network Security	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| Anti-DDoS Basic* | ✔        | ✔      | ✔      | Service level   | -        | - |

## Host Security	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [Host Security](https://intl.cloud.tencent.com/document/product/296) | ✔        | ✔      | ✔      | Operation level   | ✔        | - |

## Security Management
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [SSA](https://intl.cloud.tencent.com/document/product/1008)   | ✔        | ✔      | ✔      | Service level   | -        | - |

## Application Security
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [WAF](https://intl.cloud.tencent.com/document/product/627)         |✔       | ✔      | ✔      | Operation level   | ✔      | - |

## Video Services

 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [LVB](https://intl.cloud.tencent.com/document/product/267)       | ✔        | ✔      | ✔      | Operation level   | ✔        |  -    |
| VOD      | ✔        | -      | ✔      | Service level   | -        |  -  |
| ILVB*   | ✔        | -      | ✔      | Service level   | -        | -     |

## Big Data Platform 
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| EMR* | ✔        | ✔      | ✔      | Operation level   | ✔        | ✔  |
| [Sparkling Data Warehouse Suite](https://intl.cloud.tencent.com/document/product/1019)         |✔       | -      | ✔      | Resource level   | -        | ✔    |
| Snova Data Warehouse* | ✔        | ✔      | ✔      | Operation level   | ✔        | - |
| [SCS](https://intl.cloud.tencent.com/document/product/1000) | ✔        | ✔      | ✔      | Service level   | ✔        |✔       |
| [Elasticsearch Service](https://intl.cloud.tencent.com/document/product/845)         |✔       | ✔      | ✔      | Operation level   | ✔        | -    |

## Big Data Application
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| TIR* | ✔        | -      | ✔      | Service level   | ✔        | - |
| DM* | ✔        | -      | ✔      | Service level   | ✔        | - |
| TCS*       | ✔        | -      | ✔      | Service level   | -        | - |

## Face Recognition
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| FaceID* | ✔        |✔     | ✔      | Service level   | ✔        | - |

## Speech Technology	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| Artificial Audio Intelligence* | ✔        | -      | ✔      | Service level   | -        | - |

## Natural Language Processing	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| NLP*| ✔        | -      | ✔      | Service level   | -      | -|
| TMT*   | ✔        | -      | ✔      | Service level   | -        | - |

## Intelligent Robot	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| Xiaowei Customer Service* | ✔        | -      | ✔      | Service level   | -        | - |


## AI Platform Services	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| TI-ML* | ✔        | -      | ✔      | Service level   | -        |   ✔   |

## Game Services

| Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [GME](https://intl.cloud.tencent.com/document/product/607)         |✔        | -      | ✔      | Resource level   | ✔       | -    |

## Retail

| Service                                                        | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| YouMall       |-        | -      | -      | -   | -        |✔    |

## Mobile	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| TCB*   |-        | -      | -      | -   | -        | ✔    	

## Basic Communication	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| IM*    | ✔        | -      | ✔      | Service level   | -        | - |
| [SMS](https://intl.cloud.tencent.com/document/product/382)       | ✔        | -      | ✔      | Service level   | -        |  -    |

## Internet of Things	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| IoT Hub* | ✔        | ✔      | ✔      | Service level   | ✔   | ✔    |

## Blockchain	
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| TBaaS*      | ✔        | ✔      | ✔      | Operation level   | ✔        | - |

## Cloud Resource Management
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [Tag](https://intl.cloud.tencent.com/document/product/651)       | ✔        | ✔      | ✔      | Operation level   | ✔        | - |

## Management & Audit
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |		
| [CloudAudit](https://intl.cloud.tencent.com/document/product/1021)     | ✔        | ✔      | ✔      | Operation level   | ✔        |✔    |

## Monitoring & OPS	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [CM](https://intl.cloud.tencent.com/document/product/248)     | ✔        | ✔      | ✔      | Operation level  | ✔        | - |
| CAT*     | ✔        | -      | ✔      | Service level   | -        | - |
| KMS* | ✔        | ✔      | ✔      | Resource level   | ✔        | -     |
| MSP*         |-        | -      | -      | -   | -        |✔    |
	

## Developer Tools
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| BlueKing*        |-        | -      | -      | -   | -        |✔    |

## Data Processing	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| CI*   | ✔        | -      | ✔      | Service level   | -        | ✔ |
| VC*               |-        | -      | -      | -   | -        |✔    |

## Solution	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| CPay* | ✔        | -      | ✔      | Service level   | -        | - |

## Management & Support

 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- |----|
| Channel Partner | ✔       | -      | ✔      | Operation level | -        | -    |
| Laboratory       | -      | -     | -    | -   | -      |✔   |

## Third-party Services	
 
 | Service                                                          | Role|
| ---------------------- | ------ | 	
| TrustSQL            | ✔    |
