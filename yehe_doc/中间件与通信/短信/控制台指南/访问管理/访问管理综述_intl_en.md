>!This document describes the access management feature of **SMS**. For more information on access management for other Tencent Cloud services, please see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/zh/document/product/598) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

SMS has been connected to **CAM**. You can grant appropriate SMS access permissions to sub-accounts as needed.

## Getting Started
Before using CAM for SMS, you need to have some knowledge of the basic concepts in CAM and SMS, including:
- CAM: [user](https://intl.cloud.tencent.com/document/product/598/32633) and [policy](https://intl.cloud.tencent.com/document/product/598/10601)
- SMS: [application](https://intl.cloud.tencent.com/document/product/382/35468)

## Use Cases
### Permission isolation at the Tencent Cloud service level
Among the various departments using Tencent Cloud in an organization, department A is in charge of the SMS service. Personnel of department A need permission to access SMS, but not to access other Tencent Cloud services. To this end, the organization can create a sub-account for department A through the root account, grant it only SMS-related permissions, and then provide it to department A.
### Permission isolation at the SMS application level
When multiple businesses in an organization are using SMS, isolation is needed. Isolation involves resource isolation and permission isolation, of which the former is enabled by the [SMS application]() system and the latter is implemented by SMS access management. In this case, sub-accounts can be created for each business and granted permission to the relevant SMS applications so that each business can only access the specified applications.
### Permission isolation at the SMS action level
Product operations personnel of a business using SMS in an organization need to access the SMS console to get delivery statistics, but they should be forbidden to perform sensitive operations (such as modifying an over-limit delivery notification or a delivery rate limit) so as to protect the business against any faulty operations. To do this, you can create a custom policy that has permissions to log in to the SMS console but no permissions to call the APIs for over-limit delivery notification and delivery rate limit, create a sub-account and bind it to that policy, and then provide the sub-account information to the product operations personnel.

## Authorization Granularity
The core feature of CAM is to **allow or forbid an account to perform some operations or manipulate some resources**. SMS access management supports [resource-level authorization](https://intl.cloud.tencent.com/document/product/598/10588#.E7.AE.80.E4.BB.8B). The resource granularity is the SMS application, and the operation granularity is the [TencentCloud API](https://intl.cloud.tencent.com/product/api), including server APIs and APIs that may be used when the SMS console is accessed. For more information, please see [Authorizable Resources and Actions](https://intl.cloud.tencent.com/document/product/382/38454).

## Limitations
- SMS access management supports authorization at the application level but not at the finer-grained resource level (such as the application information and the configuration information).
- SMS access management does not support projects and tags.

