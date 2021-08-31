Welcome to Cloud Virtual Machine (CVM).

CVM runs at the Tencent IDC and provides scalable computing services. It can be used to build and host software systems based on your business needs.

CVM provides elastic computing, storage, and network resources. This API documentation describes APIs used in CVM, and provides samples about how to operate on CVMs, such as create, terminate, and restart CVM instances and adjust their bandwidth. For more information about supported operations, see [API Overview](https://intl.cloud.tencent.com/document/product/213/15689).

Before you use CVM APIs, make sure that you fully understand the [CVM overview](https://intl.cloud.tencent.com/document/product/213/495).


> ?
> All CVM APIs described in this chapter have been upgraded to API 3.0. All new CVM features will be updated in this chapter. It is recommended that you use API 3.0.


## Glossary
The following table introduces the common terms used in the CVM API documentation.

| Term | Full Name | Description |
|---------|---------|---------|
| [Instance](https://intl.cloud.tencent.com/document/product/213/4939) | Instance | A CVM.|
| [Region](https://intl.cloud.tencent.com/document/product/213/6091) | Region | A region where resources are located. Each region contains one or more availability zones. |
| [AZ](https://intl.cloud.tencent.com/document/product/213/6091) | Availability Zone | A physical IDC of Tencent Cloud with independent power supply and network resources within a [region](https://intl.cloud.tencent.com/document/product/213/6091). Availability zones are designed to ensure business stability because failures within an availability zone are isolated without affecting other availability zones within the same region. |
| [Image](https://intl.cloud.tencent.com/document/product/213/4940) | Image | A copy of the software environment on a CVM instance, which generally includes the operating system and installed software. Images are used to create instances. |
| [Security Group](https://intl.cloud.tencent.com/document/product/213/12452) | Security Group | A stateful virtual firewall with the packet filtering feature. As a critical network security isolation method, security groups are used to control the network access to CVM instances. |
| [EIP](https://intl.cloud.tencent.com/document/product/213/5733) | Elastic IP | A type of public IP. Unlike an ordinary public IP, an EIP is bound to a user account rather than an instance. The mapping relationship between an instance and a public IP can be changed at any time. |
| Pay-as-you-go | Pay-as-you-go | A billing mode. For more information, see [Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180#2.-.E6.8C.89.E9.87.8F.E8.AE.A1.E8.B4.B9). |

#### Description of input and output parameters

* `Limit` and `Offset`
>?
>These parameters are used for paging control. `Limit` indicates the maximum number of entries returned at a time, and `Offset` indicates the offset value. If the number of results exceeds the value of `Limit`, the number of returned results is equal to the value of `Limit`.
>
>For example, if `Offset` is set to 0 and `Limit` is set to 20, the 0th to 19th entries are returned; if `Offset` is set to 20 and `Limit` is set to 20, the 20th to 39th entries are returned; if `Offset` is set to 40 and `Limit` is set to 20, the 40th to 59th entries are returned.

* `Ids.N`
>?
>Format for inputting multiple parameters at a time. If a parameter is in such a format, you can specify multiple values for the parameter. For example:
>
>GET request or POST x-www-form-urlencoded request: `Ids.0=ins-r8hr2upy&Ids.1=ins-5d8a23rs&Ids.2=ins--dcs9x3gz`
>
>`N` starts from 0.
>
>POST JSON request: `{"Ids": ["ins-r8hr2upy", "ins-5d8a23rs", "ins--dcs9x3gz"]}`


## Getting Started with APIs
The following section describes how to call CVM APIs in some typical use cases:
1. To create a pay-as-you-go instance, call the [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237) API by providing the availability zone ID, image ID, model, and other required request parameters.

2. To upgrade the configuration of an instance, call the [ResetInstancesType](https://intl.cloud.tencent.com/document/product/213/33239) API. You can change the instance model to change its CPU and memory.

3. To shut down the instance, call the [StopInstances](https://intl.cloud.tencent.com/document/product/213/33235) API.

4. If the instance is no longer required, call the [TerminateInstances](https://intl.cloud.tencent.com/document/product/213/33234) API to terminate the instance. A terminated instance is no longer billed.

## Use Limits

* CVMs created through the API are subject to the quantity limit (quota) described in [CVM Purchase Limits](https://intl.cloud.tencent.com/document/product/213/2664). They share the quota with CVMs created at the official website.

* For more information, see related API documents or product documents.

