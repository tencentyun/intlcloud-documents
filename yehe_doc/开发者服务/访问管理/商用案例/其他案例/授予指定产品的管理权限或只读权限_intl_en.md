
CAM provides default (or preset) authorization policies to help you use it for your Tencent Cloud services, with at least preset management and read-only policies available for each service category. You can use these preset policies to associates CAM sub-accounts or user groups to control the access permissions for a service.

Step 1:
In the **CAM** console, select [**Policies**](https://console.cloud.tencent.com/cam/policy) on the left sidebar. Enter a Tencent Cloud service name (such as CVM) in the search box, and you can view a list of preset policies for this service.
![](https://qcloudimg.tencent-cloud.cn/raw/14537fb157c22fa3105756026d309519.png)
`QcloudCVMFullAccess` is a management policy, and `QcloudCVMInnerReadOnlyAccess` is a read-only policy.

>!The management policies of some services do not include payment permissions. You can associate a default payment management policy (such as `QcloudCVMFullAccess`) with the CAM sub-user/user group you want to authorize.

Step 2:
Authorize policies in the above list to the CAM sub-account as needed. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

- If you want to grant all the management permissions of a Tencent Cloud account to a sub-user, you can use the preset policy `AdministratorAccess`.
`AdministratorAccess`: This policy allows you to manage all users and their permissions, related financial information, and cloud service assets under this account.</td>
- If you want to grant the read-only permissions of a Tencent Cloud account to a sub-user, you can use the preset policy `ReadOnlyAccess`.
`ReadOnlyAccess`” This policy allows you to access all the cloud service assets that support API-level or resource-level authentication under a Tencent Cloud account in a read-only manner.

