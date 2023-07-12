## Overview

On the **Domain Management Configuration** page of a COS bucket, you can configure the default CDN acceleration domain name, custom CDN acceleration domain name, and custom endpoint. Among them, the configurations of the first two are logically related to the CDN service. Therefore, if you want a sub-account to configure them, in addition to COS management permissions (to configure buckets, for example), you must also grant the sub-account relevant permissions of the **CDN service**.

To ensure the resource security, if you don't grant the **sub-account** relevant permissions of the CDN service, the **sub-account** will not be able to configure the default and custom CDN acceleration domain names for a COS bucket by default. If an unauthorized sub-account logs in to the [COS console](https://console.cloud.tencent.com/cos5) and navigates to the **Domain Management Configuration** page, an access denied error will be displayed.
![](https://main.qcloudimg.com/raw/88c11a1973f03c83831cf87845ee7a01.png)


If you want the sub-account to properly configure such domain names, you need to authorize it in the [CAM console](https://console.cloud.tencent.com/cam/overview) by following the steps below:

## Directions

1. Log in to the CAM console and go to the [Policies](https://console.cloud.tencent.com/cam/policy) page.
2. Click **Create Custom Policy** > **Create by Product Feature or Project Permission** to enter the **Configure Service Types** page.
>? The permissions can be configured by the **root account** by default. If you are using a sub-account and want to configure the permissions here, make sure that the root account has granted you permissions to do so. The user policy that should be authorized by the root account in this case is `QcloudCamFullAccess`.
>
3. Enter your policy name (e.g., COS_DomainAccess), select **CDN** as the **Service Type**, and click **Next**.

4. Grant corresponding feature APIs to the sub-account based on your business needs.
Access to and configuration of the default and custom CDN acceleration domain names for a COS bucket involve five features: **querying domain name information, adding domain names, enabling/disabling domain names, deleting domain names, and modifying domain name configurations**. If you want the sub-account to have full access to the configurations of all domain names on the **Domain Management Configuration** page, toggle on all these features.

5. After selecting the corresponding features, click **Next** to associate objects.
6. Associate features with objects. Select **Associate Objects** > **All (including resource objects purchased in the future)**, which **must** be selected to make the policy configuration fully effective.

7. Confirm that the permissions are correctly configured and click **Complete** to create the custom policy.
8. After the custom policy is created, switch to the [User List](https://console.cloud.tencent.com/cam) page, and then associate the sub-account with the policy by clicking **Authorize** on the right.
![](https://main.qcloudimg.com/raw/f394425f8997d39d339e6327a2c94fd5.png)
9. In the **Associate Policy** pop-up window, search for and select the custom policy you just created and click **OK**.
![](https://main.qcloudimg.com/raw/c5dc62d62250a19ceac131b637ef513f.png)
10. After the policy is associated, the sub-account is authorized and can log in to the [COS console](https://console.cloud.tencent.com/cos5) to access and configure the default and custom CDN acceleration domain names for a COS bucket.
![](https://main.qcloudimg.com/raw/5ff57238dbe3685b020c746bf10573ba.png)
