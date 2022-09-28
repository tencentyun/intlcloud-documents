## Overview

COS allows you to filter buckets by tag in the console, which is powered by the Tencent Cloud Tag service.

Suppose the enterprise account `CompanyExample` (OwnerUin: 100000000001, Owner_appid: 1250000000) has a sub-account `Developer`, and `CompanyExample` needs to grant the sub-account permissions to get the list of tagged objects. The following describes how to grant the permissions.



## Notes
If you want to allow the sub-account to get the list of buckets filtered by tag in the console, you need to grant it the required permissions `GetResourceTags`, `GetResourcesByTags`, and `GetTags` by creating custom policies in the [CAM console](https://console.cloud.tencent.com/cam/policy).



## Directions

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) as the enterprise account `CompanyExample` and enter the policy configuration page.
2. Grant the sub-account `Developer` permissions to pull the list of tagged objects through the **policy generator** or **policy syntax**.
<dx-tabs>
::: Policy generator
1. Go to the [Policies](https://console.cloud.tencent.com/cam/policy) page in the CAM console.
2. Click **Create Custom Policy** > **Create by Policy Generator**.
3. On the permission configuration page, configure the following:

 - **Tag**:
    - **Effect**: Use the default option **Allow**.
    - **Service**: Select **Tag**.
    - **Action**: Select actions based on your business needs. Here, select `GetResourceTags`, `GetResourcesByTags`, and `GetTags`.
    - **Resource**: Select **All resources**.
 - **Add Permissions**: Configure based on your business needs.

5. Click **Next**, enter the policy name, and associate users/user groups.
6. Click **Complete**.
:::
::: Policy syntax
1. Go to the [Policies](https://console.cloud.tencent.com/cam/policy) page in the CAM console.
2. Click **Create Custom Policy** > **Create by Policy Syntax**.
3. You can choose a blank template or an existing tag template. Here, select the **QcloudTAGFullAccess** template.

4. Click **Next**, and you can see the template policy is `tag:*` by default. Here, change `action` to `name/tag:GetResourceTags`, `name/tag:GetResourcesByTags`, and `name/tag:GetTags`. Below is the policy syntax:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/tag:GetResourceTags",
                "name/tag:GetResourcesByTags",
                "name/tag:GetTags"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```
5. Click **Complete**.
:::
</dx-tabs>
3. Associate the policy with the sub-account `Developer` by locating the policy created in step 2 on the **Policies** page and clicking **Associate Users/Groups** on the right.
4. In the **Associate Users/Groups** window, select the sub-account `Developer` and click **OK**.
![](https://main.qcloudimg.com/raw/4818cbb813fce18bc8d6fd6062e35e55.png)
5. Log in to the console with the sub-account `Developer`. On the [Bucket List](https://console.cloud.tencent.com/cos5/bucket) page, select **Tag** and enter a **tag key** to search for buckets with the specified tag:
![](https://main.qcloudimg.com/raw/3f31b5273da16e7728ab40209cfedfa9.png)

