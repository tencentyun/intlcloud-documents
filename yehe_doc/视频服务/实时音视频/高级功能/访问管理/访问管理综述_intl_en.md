>!This document describes the access management feature of **TRTC**. For more information on access management for other Tencent Cloud services, please see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

[Cloud Access Management](https://intl.cloud.tencent.com/document/product/598) (**CAM**) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

TRTC has been connected to **CAM**. You can grant appropriate TRTC access permissions to sub-accounts as needed.

## Getting Started

Before using CAM for TRTC, you need to have some knowledge of the basic concepts in CAM and TRTC, including:

- CAM: [user](https://intl.cloud.tencent.com/document/product/598/32633) and [policy](https://intl.cloud.tencent.com/document/product/598/10601) 
- TRTC: [application](https://intl.cloud.tencent.com/document/product/647/37714) and [SDKAppID](https://intl.cloud.tencent.com/document/product/647/37714)

## Use Cases

### Permission isolation at Tencent Cloud service level
Among the various departments using Tencent Cloud in an organization, department A takes charge of the TRTC service. Personnel of department A need permission to access TRTC but not other Tencent Cloud services. To this end, the organization can create a sub-account for department A through the root account, grant it only TRTC-related permissions, and then provide it to department A.

### Permission isolation at TRTC application level
When multiple businesses in an organization are using TRTC, isolation is generally needed. Isolation involves resource isolation and permission isolation, of which the former is enabled by TRTC's application system and the latter implemented by TRTC access management. In this case, sub-accounts can be created for each business and granted permission to the relevant TRTC applications, so that each business can only access the specified application.

### Permission isolation at TRTC operation level
Product operations personnel of a business using TRTC in an organization need to access the TRTC Console to get usage statistics, but they should be forbidden to perform sensitive operations (such as modifying relayed push and on-cloud recording configuration) so as to protect the business against any faulty operations. To meet such needs, you can create a custom policy that has permissions to log in to the TRTC Console and call usage statistics APIs, create a sub-account and bind it to that policy, and then provide the sub-account information to the product operations personnel.

## Authorization Granularity
The core feature of CAM is to **allow or forbid an account to perform some operations or manipulate some resources**. TRTC access management supports [resource-level authorization](https://intl.cloud.tencent.com/document/product/598/10588#.E7.AE.80.E4.BB.8B), the resource granularity is [TRTC application](https://intl.cloud.tencent.com/document/product/647/37714), and the operation granularity is [TencentCloud API](https://intl.cloud.tencent.com/product/api), including [server APIs](https://intl.cloud.tencent.com/document/product/647/34260) and APIs that may be used when the TRTC Console is accessed.



## Limits
- TRTC access management supports authorization at the [application](https://intl.cloud.tencent.com/document/product/647/37714) level but not at finer-grained resource level (such as application information and configuration information).
- TRTC access management does not support projects. We recommend you use [tags](https://intl.cloud.tencent.com/document/product/651/13335) to manage Tencent Cloud service resources.
