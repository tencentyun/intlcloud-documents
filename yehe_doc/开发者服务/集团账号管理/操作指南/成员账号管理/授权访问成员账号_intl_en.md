## Overview
This document describes how to grant a sub-user an organization management policy created by the organization creator, so that the sub-user can log in with member accounts created by the organization.

## Prerequisites
You have created a member successfully as instructed in [Adding Organization Member](https://www.tencentcloud.com/document/product/1031/51865).

## Directions

### Adding an authorization
1. Log in to the TCO console and click **[Member account management](https://console.cloud.tencent.com/organization/member)** on the left sidebar.
2. On the **Member account management** page, click **Log in** on the right of the target member.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/DFiY033_%E6%8E%88%E6%9D%83%E8%AE%BF%E9%97%AE%E6%88%90%E5%91%98%E8%B4%A6%E5%8F%B7-%E6%B7%BB%E5%8A%A0%E6%8E%88%E6%9D%83.png)
3. In the **Log in** pop-up window, click **Create authorization policy**.
<dx-alert infotype="explain" title="">
The policy created in this step is an organization management policy.
</dx-alert>
4. In the **Create authorization policy** window, configure the options as follows:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/cz24304_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226180956.png)
   - **Authorization policy name**: Enter a custom name.
   - **Access permission**: Grant a specific permission.
   - **Associate sub-account**: Select the target sub-account to grant the sub-account the member management permission.
5. Click **OK**.


### Logging in to the console as the sub-account[](id:membersLogConsole)
After completing authorization, you can log in to the console as the sub-account to perform management operations as follows:
1. Log in to the TCO console as the authorized sub-account and click **[Member account management](https://console.cloud.tencent.com/organization/member)** on the left sidebar.
2. On the **Member account management** page, click **Log in** on the right of the target member account.
In the **Log in** pop-up window, you can perform management operations.

