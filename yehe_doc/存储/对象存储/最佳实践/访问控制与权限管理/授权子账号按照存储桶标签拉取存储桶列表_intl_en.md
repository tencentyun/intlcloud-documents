## Overview

COS allows you to filter buckets by tag in the console, which is powered by the Tencent Cloud Tag service.

Assume that the enterprise account CompanyExample (OwnerUin: 100000000001, Owner_appid: 1250000000) has a sub-account Developer, and CompanyExample needs to grant the sub-account permissions to get a list of tagged objects. The following provides details on how to grant the permissions.



## Notes
If you want to enable the sub-account to get a list of buckets filtered by tag in the console, you need to grant it the necessary permissions GetResourceTags, GetResourcesByTags and GetTags by creating custom policies in the [CAM](https://console.cloud.tencent.com/cam/policy) Console.



## Directions

1. Log in to the [CAM](https://console.cloud.tencent.com/cam/policy) console using the enterprise account CompanyExample and enter the policy configuration page.
2. Grant the sub-account Developer permissions to pull a list of tagged objects using **policy generator** or **policy syntax**.
<dx-tabs>
::: Policy generator
1. Go to the [CAM policy configuration](https://console.cloud.tencent.com/cam/policy) page.
2. Click **Create Custom Policy** > **Create by Policy Generator**.
3. On the permission configuration page, configure the following:
 - **Tag**:
    - **Effect**: use the default option Allow.
    - **Service**: select Tag.
    - **Action**: check actions as needed for your business. Check GetResourceTags, GetResourcesByTags and GetTags here.
    - **Resource**: Select **All resources**.
 - **Add Permissions**: Configure based on your business needs.
5. Click **Next** and enter the policy name.
6. Click **Complete**.
:::
::: Policy syntax
1. Go to the [CAM policy configuration](https://console.cloud.tencent.com/cam/policy) page.
2. Click **Create Custom Policy** > **Create by Policy Syntax**.
3. You can choose a blank template or an existing tag template. Here, select the **QcloudTAGFullAccess** template.
4. Click **Next**, and you can see the template policy is `tag:*` by default. Here, change `action` to `name/tag:GetResourceTags`, `name/tag:GetResourcesByTags`, and `name/tag:GetTags`. Below is the policy syntax:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action":[
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
5. Click **OK** to complete the process.
:::
</dx-tabs>
3. Associate the policy with the sub-account `Developer` by locating the policy created in step 2 on the **Policies** page and clicking **Associate User/Group/Role** on the right.
4. In the pop-up window, select the sub-account `Developer` and click **OK**.
5. Log in to the console with the sub-account `Developer`. On the [Bucket List](https://console.cloud.tencent.com/cos5/bucket) page, select **Tag** and enter a **tag key** to search for buckets with the specified tag:

