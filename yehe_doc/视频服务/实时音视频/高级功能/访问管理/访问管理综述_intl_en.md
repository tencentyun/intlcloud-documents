>!This document mainly describes the access management of **TRTC**. For more access managements of other Tencent Cloud services, please see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

[Cloud Access Management](https://intl.cloud.tencent.com/document/product/598) (Cloud Access Management **CAM**) is a web service provided by Tencent Cloud that helps customers securely manage access to their Tencent Cloud account resources. CAM allows you to create, manage, or terminate users (groups) and provides identity management and policy management to control who is allowed to access and use your Tencent Cloud resources.

TRTC has been connected to **CAM**. You can grant appropriate TRTC access permissions to sub-accounts as needed.

## Getting Started

Before using CAM for TRTC, you need to have some knowledge of the basic concepts in CAM and TRTC, including:

- CAM: [User Types](https://intl.cloud.tencent.com/document/product/598/32633) and [Policy](https://intl.cloud.tencent.com/document/product/598/10601) 
- TRTC: [Application](https://intl.cloud.tencent.com/document/product/647/37714) and [SDKAppID](https://intl.cloud.tencent.com/document/product/647/37714)

## Use Cases

### Permission isolation at Tencent Cloud service level
Among the various departments using Tencent Cloud in an organization, department A takes charge of the TRTC service. Staff of department A need permission to access TRTC but not to other Tencent Cloud products. To this end, the root account can create a sub-account and only grant it TRTC-related permissions, and then provide it to department A.

### Permission isolation at TRTC application level
When multiple businesses in an organization are using TRTC, isolation is generally needed. Isolation involves resource isolation and permission isolation, of which the former is enabled by TRTC's application system and the latter implemented by TRTC access management. In this case, sub-accounts can be created for each business and granted permission to the relevant TRTC applications, so that each business can only access the specified application.

### Permission isolation at TRTC operation level
Product operations staff of a business using TRTC in an organization need to access the TRTC Console to get usage statistics, but they should be forbidden to perform sensitive operations (such as modifying relayed push and on-cloud recording configuration) so as to protect the business against any faulty operations. To meet such needs, you can create a custom policy that has permissions to log in to the TRTC Console and call usage statistics APIs, create a sub-account and bind it to that policy, and then deliver the sub-account information to the product operations staff.

## Authorization Granularity
The core feature of CAM is to **allow or forbid the execution of certain operations to certain resources by certain accounts**. TRTC access management supports [resource-level authorization](https://intl.cloud.tencent.com/document/product/598/10588#.E7.AE.80.E4.BB.8B), the resource granularity is [Application](https://intl.cloud.tencent.com/document/product/647/37714), and the operation granularity is [TencentCloud API](https://intl.cloud.tencent.com/product/api), including [server APIs](https://intl.cloud.tencent.com/document/product/647/34260) and APIs that you may use to access the TRTC Console.



## Limits
- The resource granularity of TRTC access management is [Application](https://intl.cloud.tencent.com/document/product/647/37714), which cannot implement more refined access control (such as application information and configuration information).
- Projects management is not available in TRTC access management. We recommend you use [tags](https://intl.cloud.tencent.com/document/product/651/13335) to manage cloud service resources.
