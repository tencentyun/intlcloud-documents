## Overview
On the **Application Management** page, users can disable and terminate the resources in an application, which allows users to manage their applications more flexibly. The life cycle phases (normal, disabled, and terminated) and descriptions of applications are detailed as below:
![](https://qcloudimg.tencent-cloud.cn/raw/5d453fecd052b987f8219a2fe4e331a2.png)



| Status | Meaning |
|---------|---------|
| Normal | You can change the configurations, perform video processing, media management, and other operations on applications under this status.  |
|Disabled| The application is disabled. Its resources and configuration files are retained, and its resources are billed according to the corresponding billable items, but you cannot change the configurations of a disabled application and cannot use it to access the public network. |
|Terminated| For an application in this status, its resources are completely terminated, and all its resources and configuration files are cleared and cannot be recovered. This is suitable for service suspension. |

>!
>- If you re-enable a terminated application, its application ID (`appid`/`subappid`) will not change.
>- It’s normal that there may be delay in data reporting after application termination and will not affect the user's billing.
>- As it takes 5-10 minutes to change the status of an application, you’re advised not to make frequent changes.

As resource management permissions are required for disabling, terminating, and performing other operations on applications, you’re required to finish identity verification before performing such operations. After that, identity verification will not be required again within half an hour.
The operations on the **Application Management** page differ for accounts with and without subapplications enabled.

## Account without subapplications
If the account has no subapplications, go to **Common Tools** for subapplication management. You can also add subapplications to the account and view the details.
![](https://qcloudimg.tencent-cloud.cn/raw/6f80829605ee04ce07b6414f2fc2c405.png)


## Account with multiple subapplications
If the account has multiple subapplications, go to **Admin** > **Application Management** to manage them. You can view the status of subapplications, and you can also use the **Status** button to enable or disable a subapplication.
![](https://qcloudimg.tencent-cloud.cn/raw/279d7be223412490b95bb0d73e2ed55d.png)


## Notes:
1. Without subapplications enabled:
	- Terminating the primary application will clear all resources and configurations in the VOD account.
	- You can enable the application after termination. But you cannot use it if there is overdue payment. To use it, you need to top up the account.

2. With subapplications enabled:
	- To terminate the primary application, you must disable it and all its subapplications first.
	- To enable a subapplication after you terminate the primary application, you must enable the primary application first.

