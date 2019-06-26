## Overview

You can filter the bucket list by bucket tag in the COS Console. This feature relies on the Tencent Cloud tagging service.
Assume that the enterprise account CompanyExample (OwnerUin: 100000000001, Owner_appid: 1250000000) has a sub-account Developer, and CompanyExample needs to grant the sub-account permissions to pull the tag list.
The following section will guide you through how to grant the permissions.



## Notes
If you want the sub-account to be able to pull the tag list in the console, you need to grant it the permissions `GetResourceTags` and `GetResourceByTags`, which should be implemented by creating a custom policy. The policy can be created by policy builder or policy syntax based on your business needs.


## Steps

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/policy) using the enterprise account CompanyExample and enter the policy configuration page.
2. Grant the sub-account Developer permissions to pull the tag list in two ways:


#### Creating by Policy Builder

1. Go to the [CAM policy configuration](https://console.cloud.tencent.com/cam/policy) page.
2. Click **Create a Custom Policy** > **Create by Policy Builder**.
3. You can select the corresponding items to grant the sub-account the permissions `GetResourceTags` and `GetResourceByTags` based on your business needs and associate the policy with the sub-account. See the figure below:
![](https://main.qcloudimg.com/raw/6ef8573a92f3c59b7c0f633b935273da.png)

#### Creating by Policy Syntax

1. Go to the [CAM policy configuration](https://console.cloud.tencent.com/cam/policy) page.
2. Click **Create a Custom Policy** > **Create by Policy Syntax**.
3. You can select a blank or existing tag template for creation.
![](https://main.qcloudimg.com/raw/b5117e831228f59427f03d91a6fdf646.png)
4. Click **Next**, enter the policy name, and modify the policy syntax in the template by changing `action` to the `action` name of the specified tag. The policy syntax is as shown below:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/tag:GetResourceTags",
                "name/tag:GetResourcesByTags"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```
