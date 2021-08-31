>!This document describes the management of access to **TRTC**. For access management of other Tencent Cloud services, see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

[Cloud Access Management](https://intl.cloud.tencent.com/document/product/598) (Cloud Access Management **CAM**) is a web service provided by Tencent Cloud that helps customers securely manage access to their Tencent Cloud account resources. CAM allows you to create, manage, or terminate users or user groups and control who is allowed to access and use your Tencent Cloud resources through identity and policy management.

TRTC has supported **CAM**. You can grant TRTC permissions to sub-accounts as needed. 

## Getting Started

Before you start, make sure that you understand the basic concepts of CAM and TRTC, including:

- CAM: [User Types](https://intl.cloud.tencent.com/document/product/598/32633) and [Policy](https://intl.cloud.tencent.com/document/product/598/10601) 
- TRTC: [Application](https://intl.cloud.tencent.com/document/product/647/37714) and [SDKAppID](https://intl.cloud.tencent.com/document/product/647/37714)

## Use Cases

### Granting product-level permissions
A company has multiple departments that are using Tencent Cloud’s products. Department A is solely responsible for TRTC-related business, and the company needs to grant the department access to TRTC but not to other Tencent Cloud products. To achieve this, the company can create a sub-account for department A under its root account and grant the sub-account only TRTC-related permissions.

### Granting application-level permissions
A company has multiple businesses that are using TRTC and needs to isolate them from each other. There are two dimensions to isolation: resource isolation and permission isolation. The former is enabled by TRTC’s application system, and the latter by CAM. The company can create a sub-account for each of the businesses and grant them access only to the TRTC applications they are responsible for.

### Granting action-level permissions
A company has a business that is using TRTC. It needs to grant the business’ operational staff access to the TRTC console so that they can obtain usage statistics, and at the same time deny them access to critical operations such as modifying relayed push and on-cloud recording configurations. To achieve this, the company can create a custom policy that has the permissions to use relevant APIs to log in to the TRTC console and view usage statistics, and associate the policy with the sub-account created for the operational staff.

## Authorization Granularity
In essence, CAM enables you to **allow or forbid specified accounts to access certain resources**. TRTC access management supports [resource-level authorization](https://intl.cloud.tencent.com/document/product/598/10588#.E7.AE.80.E4.BB.8B). The granularity of manageable resources is [TRTC applications](https://intl.cloud.tencent.com/document/product/647/37714), and the granularity of manageable actions is [TencentCloud APIs](https://intl.cloud.tencent.com/product/api), including [server APIs](https://intl.cloud.tencent.com/document/product/647/34260) and the APIs used to access the TRTC console. For more information, please see [Manageable Resources and Actions](https://intl.cloud.tencent.com/document/product/647/39549).



## Limitations
- The granularity of manageable resources for TRTC access management is [applications](https://intl.cloud.tencent.com/document/product/647/37714). Access control of finer granularity (e.g., application information or configuration information) is not supported.
- TRTC does not support project-level access management. We recommend that you use [tags](https://intl.cloud.tencent.com/document/product/651/13335) to manage your cloud service resources.
