## Overview

On the domain management and configuration page in COS, you can configure the default accelerated domain name, the custom CDN accelerated domain name, and the custom origin server domain name. Among them, the configuration of the default accelerated domain name and the custom CDN accelerated domain name is logically related to the CDN service. Therefore, if you want a sub-account to be able to configure them, in addition to the COS management permission, you must also grant the sub-account relevant permissions to the **CDN service**.

To ensure resource security, if you do not grant the **sub-account** relevant permissions to the CDN service, the **sub-account** will not have the permission to configure the default accelerated domain name for a COS bucket and the CDN accelerated domain name by default. If an unauthorized sub-account logs in to the [COS Console](https://console.cloud.tencent.com/cos5) and navigates to the domain management configuration page, an access denied error will be displayed as shown below:
![](https://main.qcloudimg.com/raw/77d9f257ac7c5a87b7542de66977c94d.png)

If the sub-account needs to configure such domain names, you need to authorize it in the [CAM Console](https://console.cloud.tencent.com/cam/overview) by following the steps below:

## Directions

1. As there is no corresponding policy template in the [CAM Console](https://console.cloud.tencent.com/cam/overview), you need to create a custom policy. Go to the [Policies](https://console.cloud.tencent.com/cam/policy) page in the CAM Console and select **Create Custom Policy** > **Create by Product Feature or Project Permission** to enter the service type configuration page.
>? The permissions can be configured by a **root account** by default. If you are using a sub-account and want to configure the permissions here, please confirm that the root account has granted you permissions to do so. The user policy that should be authorized by the root account in this case is QcloudCamFullAccess. 
2. On the service type configuration page, enter your policy name (e.g., COS_DomainAccess) and select the service type as **CDN** as shown below:
   ![](https://main.qcloudimg.com/raw/b6bcf4015e618cec4e01a75df70c7231.png)
3. Click **Next**. You can grant the user permissions to the corresponding feature APIs based on your business needs. Access to and configuration of the default accelerated domain name and CDN accelerated domain name for a COS bucket involve five features, i.e., **querying domain name information, adding domain names, enabling/disabling domain names, deleting domain names, and modifying domain name configuration**. If you want the sub-account to have full access to the configurations of all domain names on the domain name configuration page, please toggle on all of the above features.
   ![](https://main.qcloudimg.com/raw/566e7b03d1577297f9a45b111de9f3a9.png)
4. After selecting the corresponding features, click **Next** to associate objects.
5. Associate the features with objects. Select **Associate an Object** > **All objects (including new resource objects purchased in the future)**, which has to be selected to make the policy configuration fully effective.
   ![](https://main.qcloudimg.com/raw/5c756b375a5bee9408666f789489d1dc.png)
6. Confirm that the permissions are correctly configured and click **Finish** to create the custom policy.
7. After the custom policy is created, switch to the [User List](https://console.cloud.tencent.com/cam) page and associate the sub-account with the policy.
![](https://main.qcloudimg.com/raw/40b12ae2795abc818d21d2fbf801e19a.png)
8. In the **Associate a Policy** pop-up window, search for and select the custom policy you just created and click **OK**.
   ![](https://main.qcloudimg.com/raw/e52e64404ba209d89ca7017cda332d1f.png)
9. After the policy is associated, the sub-account is authorized and can log in to the [COS Console](https://console.cloud.tencent.com/cos5) to access and configure the default accelerated domain name and CDN accelerated domain name for a COS bucket as shown below:
![](https://main.qcloudimg.com/raw/acea9bfb4a09091df7f14c1d6bd2ac9e.png)
