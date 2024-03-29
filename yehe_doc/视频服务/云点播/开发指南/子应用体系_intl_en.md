## Overview
VOD provides a **subapplication** feature to enable you to isolate resources in it. This feature is an internal concept in VOD with respect to how resources are divided. A subapplication is similar to an independent VOD account. After a subapplication is created, the ownership of VOD resources will be as shown below:
<img src="https://main.qcloudimg.com/raw/58880e642525a040fc3bcd5e5c6d12b9.png" width="595">

>?**Resources** mentioned in this document include media files in VOD and their attributes, derivative files, configurations, CDN domain names, and statistics of VOD service usage.

### Use cases
Below are some typical use cases for VOD subapplication:

- **Multi-department/multi-business isolation**: a company intends to develop its own products based on Tencent Cloud. Department A plans to use VOD to develop a UGSV application, and department B a movie and television website. These two VOD businesses need to be isolated from each other. However, out of financial considerations, the company cannot create an independent Tencent Cloud account for each department. In this case, the subapplication feature of VOD can be used to assign a subapplication to each department.
- **Permission control**: in the above multi-department/multi-business isolation scenario, developers may have further permission control needs, such as granting each department access only to subapplications associated with its own business but not other subapplications. In this case, the account manager can assign a sub-user to each department (A and B) and grant the corresponding VOD subapplication access permissions. For detailed directions, please see [Access Management](https://intl.cloud.tencent.com/document/product/266/33970).
- **Separation between production and test environments**: if you want to test some VOD features (e.g., modifying the method of [event notification](https://intl.cloud.tencent.com/document/product/266/33948) or enabling [hotlink protection](https://intl.cloud.tencent.com/document/product/266/33984)) without affecting the operations of the production environment, you can create two subapplications, one for the production environment and one for the test environment. New features can be tested in the test environment first and then made available in the production environment after successful validation.

### Role definition and identification
Roles in the VOD subapplication system include **admin**, **primary application**, and **subapplication**. Their definitions are as shown below.
<img src="https://main.qcloudimg.com/raw/c873e8cdb0eb762df5d899efc13aa7cc.png" width="724" >

1. After you activate the VOD service, you are in the default role of **primary application**, to which all VOD resources belong. The primary application ID is your Tencent Cloud `APPID`, which can be viewed in [**Account Info**](https://console.cloud.tencent.com/developer) in the console.
2. After you enable the VOD subapplication feature, an **admin** role will be generated, which does not own any VOD resources, and all resources still belong to the primary application.
3. If you create a **subapplication** in the "admin" role, the new subapplication will have separate VOD resources. It is equivalent to and isolated from the primary application (which can be viewed as a special subapplication). When you create a subapplication, VOD will assign a globally unique ID to it, which is called subapplication ID. For more information on how to view the ID, please see [Console Use Instructions - Application Management](#p1).
4. If you create another **subapplication** in the "admin" role, the new subapplication will also have separate VOD resources; the new subapplication, the primary application, and all other subapplications will be equal to and isolated from one another, and so on.

>?Unless otherwise specified, the primary application and subapplications will not be distinguished in the following sections and will be collectively referred to as **subapplication**.

### Capabilities
The VOD subapplication system provides the following capabilities:

- Creating and setting subapplications: after you enable the VOD subapplication feature, you can create subapplications in the console as the admin and set the name and description for each subapplication.
- Disabling subapplications: all subapplications except the primary application can be disabled. When a subapplication is disabled, its VOD resources will not be cleared and other features such as video upload and transcoding will not be affected; instead, only its domain name will be disabled.
- Isolating resources: VOD resources of different subapplications are isolated from one another.
- You can manipulate VOD resources of any subapplications through the console or server APIs.
- Independent statistics are generated for each subapplication, such as storage usage, bandwidth/traffic, transcoding duration, intelligent video recognition duration, and playback data.
- Aggregated statistics for all subapplications are provided.

### Limits<span id ="p4"></span>
The VOD subapplication system has the following limits:

- The name and description of the primary application cannot be modified.
- Subapplications cannot be deleted.
- Up to 50 subapplications can be created under one VOD account.
- No separate billing logic (such as billing mode and separate bill generation) can be set for subapplications. All subapplications under a VOD account belong to the same account, and all VOD usage data (including but not limited to VOD billable items such as storage, traffic, transcoding duration, and intelligent video recognition duration) is aggregated for fee calculation and unified billing.

## Console Use Instructions<span id="p3"></span>

### Enabling subapplication feature

1. Log in to the [VOD console](https://console.cloud.tencent.com/vod).
2. Click **Enable Subapplication** on the left sidebar to enter the subapplication enablement page.
3. Click **Get Started** to enable the subapplication feature of VOD.

>?If the subapplication feature has already been enabled, **Enable Subapplication** on the left sidebar will be invisible.

### Selecting role
After the subapplication feature is enabled, a drop-down list will be displayed in the top-left corner of the [VOD console](https://console.cloud.tencent.com/vod) where you can select a role. If you have just enabled the subapplication feature, there are only two roles in the drop-down list: **admin** and **primary application**. After you create a subapplication, it will be displayed as a role in the drop-down list.
![](https://qcloudimg.tencent-cloud.cn/raw/0dc90b954520c36cddac7a9d78c24cf8.png)

### Admin
Under the admin role, the left sidebar displays the following entries: **Service Overview**, **Application Management**, and **UGSV License**.

- Service Overview: this page displays the VOD billing mode, aggregated key business data of all subapplications, and key business data of each subapplication.
- <span id = "p1"></span>Application Management: on this page, you can view, create, edit, or disable subapplications. Subapplication IDs are also displayed on this page.

### Subapplication
Under the subapplication role, usage of the VOD console is basically the same as that before the subapplication feature is enabled, and you can view and manipulate the subapplication's VOD resources. The main difference lies in that the subapplication itself has no separate billing configuration.

## Server API Use Instructions
After enabling the subapplication feature, you must specify the subapplication whose resources you want to access when using VOD server APIs.

### Specifying subapplication in server API<span id = "p2"></span>
VOD server API has been upgraded to [TencentCloud API 3.0](https://intl.cloud.tencent.com/product/api). You can use the `SubAppId` parameter in each API to specify the subapplication you want to access. If you want to access the primary application, you can enter the primary application ID or leave this parameter empty.

### Specifying subapplication in server API 2017
Server API 2017 also supports subapplications. When using it, you need to add the `SubAppId` parameter (case-sensitive) to the request. This parameter is at the same level as common request parameters of server API 2017, and its value is the subapplication ID. If you want to access the primary application, you can enter the primary application ID or leave this parameter empty.

>?
>- Server API 2017 documentation does not disclose the `SubAppId` parameter, which will not affect the use of it though.
>- The `SubAppId` parameter is also involved in signature calculation for server APIs in the same calculation rule.

## File Upload Description
After enabling the VOD subapplication feature, you must specify the subapplication to which you want to upload your media files.

### LVB recording
[LVB recording](https://intl.cloud.tencent.com/document/product/267/31563) allows you to generate recording files in the specified subapplication by adding `vod_sub_app_id=xxx` (`xxx` refers to the subapplication ID) to the LVB push parameters. If you want to generate recording files in the primary application, simply leave this parameter empty.

### Upload from server
[Upload from server](https://intl.cloud.tencent.com/document/product/266/33912) supports file upload to the specified subapplication. For more information on how to set the parameters, please visit the link below. If you want to upload files to the primary application, you can enter the primary application ID or leave the corresponding parameter empty.

#### Through SDK
* [SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914)
* [SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916)
* [SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917)
* [SDK for Node.js](https://intl.cloud.tencent.com/document/product/266/33918)
* [SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919)

#### Through server API
The [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120) and [CommitUpload](https://intl.cloud.tencent.com/document/product/266/34119) APIs will be used for upload. For more information, please see [Specifying a Subapplication in a Server API](#p2).
We strongly recommend you use the SDK for upload.

### Upload from client
[Upload from client](https://intl.cloud.tencent.com/document/product/266/33921) allows you to upload files to the specified subapplication by adding `vodSubAppId=xxx` (`xxx` refers to the subapplication ID) to the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922). If you want to upload files to the primary application, you can enter the primary application ID or leave this parameter empty.

>?The `vodSubAppId` parameter is also involved in calculation of the signature for upload from client in the same calculation rule.

### Upload from URL
Upload from URL allows you to upload files to the specified subapplication.

* Through the console: for more information, please see [Console Use Instructions](#p3).
* Through server API: use the [PullUpload](https://intl.cloud.tencent.com/document/product/266/34118) API. For more information, please see [Specifying Subapplication in Server API](#p2).

## Permission Management
VOD has been connected to CAM and supports authorization at subapplication level. For more information, please see [Access Management](https://intl.cloud.tencent.com/document/product/266/33970).

## FAQs
#### After the subapplication feature is enabled, will it affect existing business logic in the production environment?
No. The subapplication system is designed with compatibility in mind. If the subapplication ID is not specified, all server APIs will manipulate the primary application by default.

#### Will fees be charged for enabling the subapplication feature?
The subapplication feature itself is free of charge; however, resources consumed by each subapplication will be billed under the VOD account according to the VOD [billing rules](https://intl.cloud.tencent.com/document/product/266/2838).

#### My company uses the subapplication feature to implement business isolation. How can the internal settlement/cost allocation be implemented for each business?
As described in [Limits](#p4) above, VOD only generates one aggregated bill for the entire account. If you have multiple businesses that require cost allocation, you can define and calculate the allocated costs based on the subapplication-level statistics provided by VOD.

#### What will happen to a subapplication if my VOD service is suspended?
If your VOD service is suspended due to overdue payment, all subapplications under your account will be disabled.

#### Can I migrate videos from one subapplication to another?
Resources of different subapplications are isolated, so resources of one subapplication cannot be migrated to another.
