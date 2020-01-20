VOD has been connected to Tencent Cloud [Cloud Access Management (CAM)](/document/product/598). You can grant specified VOD permissions to subaccounts as needed. The VOD access control feature can be used directly once the VOD service is activated.
This document assumes that you already have some knowledge of Tencent Cloud CAM and VOD's subapplication system. The main concepts involved in this document include:

- CAM: [user type](https://intl.cloud.tencent.com/document/product/598/32633), [API key](/document/product/598/37140), [policy](/document/product/598/10601), and [policy syntax](https://intl.cloud.tencent.com/document/product/598/10603)
- VOD: [subapplication](https://intl.cloud.tencent.com/document/product/266/33987)

## Use Cases
The typical use cases of VOD access control are as follows:

- **Permission isolation at Tencent Cloud product level**
Among the various departments using Tencent Cloud in an organization, department A takes charge of the VOD service. Staff of department A need permission to access VOD but not other Tencent Cloud products. To this end, you can create a subuser and only grant it VOD-related permissions, and then provide it to department A.
- **Permission isolation at VOD subapplication level**
When multiple businesses in an organization are using VOD, isolation is generally needed. Isolation involves resource isolation and permission isolation, of which the former is enabled by VOD's subapplication system and the latter implemented by VOD access control. In this case, subusers can be created for each business and granted permission to the corresponding subapplications, so that each business can only access the specified subapplication.
- **Permission isolation at VOD operation level**
Product operations staff of a business using VOD in an organization need to access the VOD Console to get statistics (e.g., geographical distribution of traffic and number of playbacks), but they should be forbidden to perform sensitive operations (e.g., deleting files or disabling domain names) so as to protect the business against any faulty operations. To meet such needs, you can create a custom policy that has permissions to log in to the VOD Console and call statistics APIs, create a subuser and bind it to that policy, and then deliver the subuser information to the product operations staff.

## Resource Granularity and Operation Granularity
The core feature of CAM is to **allow or forbid an account to perform some operations or manipulate some resources**. For VOD, the resource granularity is subapplication, and the operation granularity is server API.

## Limits
- VOD access control supports authorization at subapplication level but not at finer-grained resource level (e.g., media files and domain names).
<!--doc - VOD access control does not support [projects and tags](/document/product/598/32738). -->

## APIs Supporting Authorization at Resource Level

VOD access control supports [authorization at resource level](https://intl.cloud.tencent.com/document/product/598/10588). All its APIs, except those with special limits, support authorization at resource level. Please see below for details.

### List of APIs not supporting authorization at resource level

| API Name | Description | Description |
| :---------------------------------------------- | -------------- | ------------------------------------------------------------ |
| [DescribeSubAppIds](/document/api/266/36304)    | Queries the list of subapplications | All subusers have permission to call this API with no authorization required, and subapplications do not need to be specified.  |
| [ModifySubAppIdStatus](/document/api/266/36302) | Modifies the status of a subapplication | This API can disable specified subapplications, which is highly risky. Therefore, it is available to only subusers with full VOD permissions (i.e., `QcloudVODFullAccess` as described in [Preset Policies](https://intl.cloud.tencent.com/document/product/266/33971#.E9.A2.84.E8.AE.BE.E7.AD.96.E7.95.A5.E5.88.97.E8.A1.A8)). Subusers that are granted write permissions to certain subapplications but not `QcloudVODFullAccess` cannot call this API. |

<!--api
### List of APIs supporting authorization at resource level

Except those in the above list, all APIs outlined in [API Overview](#apihttps://intl.cloud.tencent.com/document/product/266/31753) support authorization at resource level. In policy syntax, resource descriptions for these APIs are all in the format of `qcs::vod::uin/$uin:subAppId/$subAppId`.
-->