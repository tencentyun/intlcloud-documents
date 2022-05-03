## Overview

On the domain management and configuration page in COS, you can configure the default acceleration domain name, the custom CDN acceleration domain name, and the custom origin server domain name. Among them, the configuration of the default acceleration domain name and the custom CDN acceleration domain name is logically related to the CDN service. Therefore, if you want a sub-account to be able to configure them, in addition to the COS management permissions (such as basic configuration permissions on buckets), you must also grant the sub-account relevant permissions to the **CDN service**.

To ensure resource security, if you do not grant the **sub-account** relevant permissions to the CDN service, the **sub-account** will not have the permission to configure the default acceleration domain name for a COS bucket and the CDN acceleration domain name by default. If an unauthorized sub-account logs in to the [COS Console](https://console.cloud.tencent.com/cos5) and navigates to the domain management configuration page, an access denied error will be displayed as shown below:
![](https://main.qcloudimg.com/raw/88c11a1973f03c83831cf87845ee7a01.png)


If the sub-account needs to configure such domain names, you need to authorize it in the [CAM Console](https://console.cloud.tencent.com/cam/overview) by following the steps below:

## Directions

1. As there is no corresponding policy template in the [CAM Console](https://console.cloud.tencent.com/cam/overview), you need to create a custom policy. Go to the [Policies](https://console.cloud.tencent.com/cam/policy) page in the CAM Console and select **Create Custom Policy** > **Create by Product Feature or Project Permission** to enter the service type configuration page.
> The permissions can be configured by a **root account** by default. If you are using a sub-account and want to configure the permissions here, please confirm that the root account has granted you permissions to do so. The user policy that should be authorized by the root account in this case is QcloudCamFullAccess.
2. On the service type configuration page, enter your policy name (e.g., COS_DomainAccess) and select the service type as **CDN**.
   
3. Click **Next**. You can grant the user permissions to the corresponding feature APIs based on your business needs. Access to and configuration of the default acceleration domain name and CDN acceleration domain name for a COS bucket involve five features, i.e., **querying domain name information, adding domain names, enabling/disabling domain names, deleting domain names, and modifying domain name configuration**. If you want the sub-account to have full access to the configurations of all domain names on the domain name configuration page, please toggle on all of the above features.
4. After selecting the corresponding features, click **Next** to associate objects.
5. Associate the features with objects. Select **Associate an Object** > **All objects (including new resource objects purchased in the future)**, which has to be selected to make the policy configuration fully effective.
6. Confirm that the permissions are correctly configured and click **Finish** to create the custom policy.
7. After the custom policy is created, switch to the [User List](https://console.cloud.tencent.com/cam) page, and associate the sub-account with the policy by clicking **Authorize** on the right.
![](https://main.qcloudimg.com/raw/f394425f8997d39d339e6327a2c94fd5.png)
8. In the **Associate Policies** pop-up window, search for and select the custom policy you just created and click **OK**.
   ![](https://main.qcloudimg.com/raw/c5dc62d62250a19ceac131b637ef513f.png)
9. After the policy is associated, the sub-account is authorized and can log in to the [COS Console](https://console.cloud.tencent.com/cos5) to access and configure the default acceleration domain name and CDN acceleration domain name for a COS bucket as shown below:
![](https://main.qcloudimg.com/raw/5ff57238dbe3685b020c746bf10573ba.png)

