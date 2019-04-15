## Overview
CAM(Cloud Access Management) helps you manage access to most of Tencent Cloud resources and services securely.
This article describes detailed policy syntax, cloud APIs, console, authorization granularity, temporary certificate in CAM.
 CAM currently is integrated with the following Tencent Cloud services and resources.
 Definitions:
- Service: Name of the CAM-enabled Tencent Cloud services. For more information about specific service or product, see product documentation.
- Policy syntax: Whether the service enables you to use policy syntax to manage access. “✔” means “Yes”; “-” means “No”.
- Cloud API: Whether sub-account users can use Tencent Cloud API to access the service. “✔” means “Yes”; “-” means “No”.
Console: Whether sub-account users can access the service via console. “✔” means “Yes”; “-” means “No”.
- Authorization granularity: Level of detail used to define authorization rules for controlling the access to resources and servies under a Tencent Cloud account.
>? Authorization granularity has three levels: Service level, operation level and resource level.
> - Service level: Whether a user can be permitted to access all of the Tencent Cloud services the Tencent Cloud account has purchased.
> - Operation level: Whether a user can be permitted to call the API of a specified Tencent Cloud service the Tencent Cloud account has purchased. For example, a user has read-only access to the Tencent Cloud account CVM.
> - Resource level: Whether a user can be permitted to access specific resource under your Tencent Cloud account. For example: a user has read-only access to a CVM owned by the Tencent Cloud account. Resource level presents the finest authorization granularity. 
- Temporary key (STS): Whether a user can be permitted to access the service via temporary security credentials. “✔” means “Yes”; “-” means “No”.
- [Role](https://cloud.tencent.com/document/product/598/19420): Whether the service can access other services as the principal of a role. "✔" means “Yes”; "-" means “No”.

## Compute	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [CVM](https://cloud.tencent.com/document/product/213/10314) | ✔        | ✔      | ✔      | Resource level   | ✔        |   ✔  |
| [CPM](https://cloud.tencent.com/document/product/386/13245) | ✔        | ✔      | ✔      | Resource level   | ✔        | -    |
| [TKE](https://cloud.tencent.com/document/product/457) | ✔        | ✔      | ✔      | Resource level   | ✔        | ✔    |
| [AS](https://cloud.tencent.com/document/product/377)   | ✔        | ✔      | ✔      | Resource level   | ✔        | -    |
| [SCF](https://cloud.tencent.com/document/product/583/18014) | ✔        | ✔      | ✔      | Resource level   | ✔        | ✔   |
| [BatchCompute](https://cloud.tencent.com/document/product/599)   | ✔        | ✔      | ✔      | Resource level   | ✔        | -    |


## Storage	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [COS](https://cloud.tencent.com/document/product/436/12469) | ✔        | ✔      | ✔      | Resource level   | ✔        | ✔   |
| [CFS](https://cloud.tencent.com/document/product/582/14679) | ✔        | ✔      | -      | Service Level   | ✔        | -    |
| [CAS](https://cloud.tencent.com/document/product/572)   | ✔        | ✔      | -      | Resource level   | ✔        | -    |
| [CSG](https://cloud.tencent.com/document/product/581)   | ✔        | -      | ✔      | Service level   | -        | -    |
| [CBS](https://cloud.tencent.com/document/product/362)     | ✔        | ✔      | ✔      | Resource level   | ✔        | -    |
| [CLS](https://cloud.tencent.com/document/product/614)   | ✔        | -      | ✔      | Service level   | -        |  ✔ |

## Networking	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [CLB](https://cloud.tencent.com/document/product/214/9779) | ✔        | ✔      | ✔      | Resource level   | ✔        |    -  |
| [VPC](https://cloud.tencent.com/document/product/215/20171) | ✔        | ✔      | ✔      | Resource level   | ✔        | - |

## Database	
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [TencentDB for MySQL](https://cloud.tencent.com/document/product/236/14469) | ✔        | ✔      | ✔      | Resource level   | ✔        | ✔ |
| [TencentDB for CTSDB](https://cloud.tencent.com/document/product/652) | ✔        | ✔      | -      | Operation level   | ✔        | - |
| [TencentDB for MongoDB](https://cloud.tencent.com/document/product/240)         |-        | -      | -      | -   | -        |✔    |


## CDN & Acceleration	
| Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [CDN](https://cloud.tencent.com/document/product/228/12722) | -        | ✔      | ✔      | Operation level   | ✔        | - |
| [DSA](https://cloud.tencent.com/document/product/570) | ✔        | ✔      | ✔      | Service level   | ✔        |   -   |

## Middleware	
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [CMQ](https://cloud.tencent.com/document/product/406/8621) | ✔        | ✔      | ✔      | Resource level   | ✔        | - |
| [CKafka](https://cloud.tencent.com/document/product/597/17989) | ✔        | ✔      | ✔      | Resource level   | ✔        | ✔   |
| [API Gateway](https://cloud.tencent.com/document/product/628)         | ✔       | ✔      | ✔      | Resource level   | -        | ✔    |
| [TSF](https://cloud.tencent.com/document/product/649)         |-        | -      | -      | -   | -        | ✔    |


## Domains & Websites	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [Domain Service](https://cloud.tencent.com/document/product/242)   | ✔        | -      | ✔      | Service level   | -        |    -  |
| [ICP Filing Registration](https://cloud.tencent.com/document/product/243)   | ✔        | -      | ✔      | Service level   | -        | - |
| [HttpDNS](https://cloud.tencent.com/document/product/379) | ✔        | -      | ✔      | Service level   | -        | - |

## Network Security	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [Anti-DDoS Basic](https://cloud.tencent.com/document/product/1020) | ✔        | ✔      | ✔      | Service level   | -        | - |

## Host Security	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [Host Security](https://cloud.tencent.com/document/product/296) | ✔        | ✔      | ✔      | Operation level   | ✔        | - |

## Security Management
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [SSA](https://cloud.tencent.com/document/product/664)   | ✔        | ✔      | ✔      | Service level   | -        | - |

## Application Security
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [WAF](https://cloud.tencent.com/document/product/627)         |✔       | ✔      | ✔      | Operation level   | ✔      | - |

## Video Services

 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [LVB](https://cloud.tencent.com/document/product/267)       | ✔        | ✔      | ✔      | Operation level   | ✔        |  -    |
| [VOD](https://cloud.tencent.com/document/product/266)       | ✔        | -      | ✔      | Service level   | -        |  -  |
| [ILVB](https://cloud.tencent.com/document/product/268)   | ✔        | -      | ✔      | Service level   | -        | -     |

## Big Data Platform 
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [EMR](https://cloud.tencent.com/document/product/589/14625) | ✔        | ✔      | ✔      | Operation level   | ✔        | ✔  |
| [Sparkling Data Warehouse Suite](https://cloud.tencent.com/document/product/1002)         |✔       | -      | ✔      | Resource level   | -        | ✔    |
| [Snova Data Warehouse](https://cloud.tencent.com/document/product/878) | ✔        | ✔      | ✔      | Operation level   | ✔        | - |
| [SCS](https://cloud.tencent.com/document/product/849) | ✔        | ✔      | ✔      | Service level   | ✔        |✔       |
| [Elasticsearch Service](https://cloud.tencent.com/document/product/845)         |✔       | ✔      | ✔      | Operation level   | ✔        | -    |

## Big Data Application
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [TIR](https://cloud.tencent.com/document/product/587) | ✔        | -      | ✔      | Service level   | ✔        | - |
| [DM](https://cloud.tencent.com/document/product/588) | ✔        | -      | ✔      | Service level   | ✔        | - |
| [TCS](https://cloud.tencent.com/document/product/270)       | ✔        | -      | ✔      | Service level   | -        | - |

## Face Recognition
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [FaceID](https://cloud.tencent.com/document/product/1007) | ✔        |✔     | ✔      | Service level   | ✔        | - |

## Speech Technology	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [Artificial Audio Intelligence](https://cloud.tencent.com/document/product/441) | ✔        | -      | ✔      | Service level   | -        | - |

## Natural Language Processing	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [NLP](https://cloud.tencent.com/document/product/271) | ✔        | -      | ✔      | Service level   | -      | -|
| [TMT](https://cloud.tencent.com/document/product/551)   | ✔        | -      | ✔      | Service level   | -        | - |

## Intelligent Robot	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [Xiaowei Customer Service](https://cloud.tencent.com/document/product/645) | ✔        | -      | ✔      | Service level   | -        | - |


## AI Platform Services	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [TI-ML](https://cloud.tencent.com/document/product/851) | ✔        | -      | ✔      | Service level   | -        |   ✔   |

## Game Services

| Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [GME](https://cloud.tencent.com/document/product/607)         |✔        | -      | ✔      | Resource level   | ✔       | -    |

## Retail

| Service                                                        | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [YouMall](https://cloud.tencent.com/document/product/860)         |-        | -      | -      | -   | -        |✔    |

## Mobile	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [TCB](https://cloud.tencent.com/document/product/876)     |-        | -      | -      | -   | -        | ✔    	

## Basic Communication	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [IM](https://cloud.tencent.com/document/product/269)     | ✔        | -      | ✔      | Service level   | -        | - |
| [SMS](https://cloud.tencent.com/document/product/382)       | ✔        | -      | ✔      | Service level   | -        |  -    |

## Internet of Things	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [IoT Hub](https://cloud.tencent.com/document/product/634) | ✔        | ✔      | ✔      | Service level   | ✔   | ✔    |

## Blockchain	
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [TBaaS](https://cloud.tencent.com/document/product/663)      | ✔        | ✔      | ✔      | Operation level   | ✔        | - |

## Cloud Resource Management
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [Tag](https://cloud.tencent.com/document/product/651)       | ✔        | ✔      | ✔      | Operation level   | ✔        | - |

## Management & Audit
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |		
| [CloudAudit](https://cloud.tencent.com/document/product/629)     | ✔        | ✔      | ✔      | Operation level   | ✔        |✔    |

## Monitoring & OPS	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |
| [CM](https://cloud.tencent.com/document/product/248)     | ✔        | ✔      | ✔      | Operation level  | ✔        | - |
| [CAT](https://cloud.tencent.com/document/product/280)     | ✔        | -      | ✔      | Service level   | -        | - |
| [KMS](https://cloud.tencent.com/document/product/573) | ✔        | ✔      | ✔      | Resource level   | ✔        | -     |
| [MSP](https://cloud.tencent.com/document/product/659)         |-        | -      | -      | -   | -        |✔    |
	

## Developer Tools
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [BlueKing](https://cloud.tencent.com/document/product/274)         |-        | -      | -      | -   | -        |✔    |

## Data Processing	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [CI](https://cloud.tencent.com/document/product/460)   | ✔        | -      | ✔      | Service level   | -        | ✔ |
| [VC](https://cloud.tencent.com/document/product/314)                |-        | -      | -      | -   | -        |✔    |

## Solution	
 
 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- | ---- |	
| [CPay](https://cloud.tencent.com/document/product/569) | ✔        | -      | ✔      | Service level   | -        | - |

## Management & Support

 | Service                                                         | Policy Syntax | Cloud API | Console | Authorization Granularity | Temporary Key | Role |
| ------------------------------------------------------ | -------- | ------ | ------ | -------- | -------- |
| [Channel Partner](https://cloud.tencent.com/document/product/563) | ✔       | -      | ✔      | Operation level | -        | -    |
| [Laboratory](https://cloud.tencent.com/document/product/658/13897)       | -      | -     | -    | -   | -      |✔   |

## Third-party Services	
 
 | Service                                                          | Role|
| ---------------------- | ------ | 	
| [TrustSQL](https://trustsql.qq.com/)               | ✔    |
