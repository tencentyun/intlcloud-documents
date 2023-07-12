## Overview

You can filter buckets by tag and get a buckets list in the COS Console. This feature relies on the Tencent Cloud tagging service.

Assume that the enterprise account CompanyExample (OwnerUin: 100000000001, Owner_appid: 1250000000) has a sub-account jason.read, and CompanyExample needs to grant the sub-account permissions to get a list of tagged objects. The following provides details on how to grant the permissions.



## Notes
If you want to enable the sub-account to get a list of buckets filtered by tag in the console, you need to grant it the necessary permissions GetResourceTags, GetResourcesByTags and GetTags by creating custom policies in the [CAM](https://console.cloud.tencent.com/cam/policy) Console.



## Directions

1. Log in to the [CAM](https://console.cloud.tencent.com/cam/policy) console using the enterprise account CompanyExample and enter the policy configuration page.
2. Grant the sub-account jason.read permissions to pull a list of tagged objects using **policy generator** or **policy syntax**.
 - **Using policy generator**
(1). Go to the [CAM](https://console.cloud.tencent.com/cam/policy) policies list page.
(2) Click **Create Custom Policy** > **Create by policy generator**.
(3) Enter the creation details page, and configure the following:
    - **Effect**: use the default option Allow.
    - **Service**: select Tag.
    - **Action**: check actions as needed for your business. Check GetResourceTags, GetResourcesByTags and GetTags here.
    - **Resource**: enter `*` here, or a description that you see fill your environment. See [Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606).
![](https://main.qcloudimg.com/raw/6ef8573a92f3c59b7c0f633b935273da.png)
(4) Click **Add Statement**, and you can see the configured permission right below.
(5) Click **Next**, enter the policy name, and click **Done** to complete the creation.
 - **Using policy syntax**
(1) Go to the [CAM](https://console.cloud.tencent.com/cam/policy) policies list page.
(2) Click **Create Custom Policy** > **Create by Policy Syntax**.
(3) You can choose to create the policy using Blank Template or an existing tag template. Here we choose **QcloudTAGFullAccess**.
![](https://main.qcloudimg.com/raw/b5117e831228f59427f03d91a6fdf646.png)
(4) Click **Next**, and you can see the policy template is defaulted as `tag:*`. Here we change `action` to `name/tag:GetResourceTags`, `name/tag:GetResourcesByTags` and `name/tag:GetTags` with policy syntax as shown below:
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
(5) Click **Done** to complete the creation.
3. Associate the policy with the sub-account jason.read by locating the policy created in step 2 in the policies page and clicking **Bind User/Group** on the right side.
4. In the **Bind User/User Group** window, select sub-account jason.read and click **OK**.
![](https://main.qcloudimg.com/raw/4818cbb813fce18bc8d6fd6062e35e55.png)
5. Log in to the console using the sub-account jason.read. In the [Bucket List](https://console.cloud.tencent.com/cos5/bucket) page, select **Tag** and enter **Tag Key** to search for a list of buckets all with the specified tag as shown below:
![](https://main.qcloudimg.com/raw/3f31b5273da16e7728ab40209cfedfa9.png)
