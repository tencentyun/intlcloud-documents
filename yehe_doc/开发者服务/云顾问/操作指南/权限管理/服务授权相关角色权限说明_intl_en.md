
When you use Tencent Smart Advisor, in order to use Tencent Cloud resources, you will encounter a variety of scenarios that require service authorization. Each scenario usually involves preset policies for different roles. Here, the `Advisor_QCSLinkedRoleInBusinessContinuity` role and `QcloudAccessForAdvisorLinkedRoleInBusinessContinuity` preset policy are mainly involved. This document details authorization policies, scenarios, and directions.


## Role Authorization
### Role name
`Advisor_QCSLinkedRoleInBusinessContinuity`

### Permission description
After Tencent Smart Advisor is activated on the [**Service Authorization**](https://console.cloud.tencent.com/advisor/auth) page, Tencent Cloud will grant your account the `Advisor_QCSLinkedRoleInBusinessContinuity` role. By default, the role is associated with the `QcloudAccessForAdvisorLinkedRoleInBusinessContinuity` preset policy, which grants Tencent Smart Advisor access to CVM, VPC, TencentDB, and other Tencent Cloud resources under your account.


## Preset Policy

### Policy name
`QcloudAccessForAdvisorLinkedRoleInBusinessContinuity`


### Authorization scenario
When you log in to the [Tencent Smart Advisor console](https://console.cloud.tencent.com/advisor) for the first time after registering and logging in to a Tencent Cloud account, you need to go to the **Cloud Access Management** page to grant Tencent Smart Advisor permissions to manipulate CVM, VPC, TencentDB, and other Tencent Cloud resources.

### Authorization steps

1. Log in to the Tencent Smart Advisor console and select [**Authorization**](https://console.qcloud.com/advisor/auth) on the left sidebar.
2. On the **Service Authorization** page, enable **Service Authorization**.
![](https://qcloudimg.tencent-cloud.cn/raw/71ef5d776a0a1288d8f2f57c5b036a5c.png)
3. In the **Authorize** pop-up window, click **Cloud Access Management** to enter the CAM console.
4. On the **Role Management** page, click **Grant** to complete authentication.
![](https://qcloudimg.tencent-cloud.cn/raw/5489e7b652cc6a520b9b972c434876cb.png)
