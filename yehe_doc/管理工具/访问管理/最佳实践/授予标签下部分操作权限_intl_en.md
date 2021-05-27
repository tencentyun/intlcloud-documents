## Overview

If you have purchased multiple types of Tencent Cloud resources which are grouped and managed by tag, you can grant employees of different teams permissions to use corresponding APIs by tag on an as-needed basis. This document uses a typical case to describe how to grant sub-accounts certain operation permissions of resources through tags. 

Suppose that:
- The company account `CompanyExample` has a sub-account `DevA`.
- The company account `CompanyExample` has a tag key-value pair `test1&test1`.
- The company account `CompanyExample` wants to grant the sub-account `DevA` the permission to restart CVM instances (cvm:RebootInstances) under the tag `test1&test1`.


## Directions

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) with the company account `CompanyExample`.
2. On the **Policy** page, click **Create Policy** > **[Create by Policy Syntax](https://console.cloud.tencent.com/cam/policy/createV2)**.
3. Select **Blank Template** under **Select a template type** and click **Next** to enter the **Edit Policy** page
![](https://main.qcloudimg.com/raw/f36f86fedfa5f25576232c9bdcd29b60.png)
4. On the **Edit Policy** page, fill out the following form:
	- Policy Name: the default value is `policygen-current date`. We recommend you define a unique and meaningful policy name, such as `cvm-RebootInstances`.
	- Description: write a description, which is optional. 
	- Policy Content: copy and paste the following content. Here, `cvm:RebootInstances` is the name of the API that needs to be authorized, and `tes1t&test1` is the tag key-value pair that needs to be authorized.
<dx-codeblock>
::: plaintext
{
"version": "2.0",
"statement": [
    {
        "effect": "allow",
        "action": [
            "cvm:RebootInstances"
        ],
        "resource": "*",
        "condition": {
            "for_any_value:string_equal": {
                "qcs:tag": [
                    "tes1t&test1"
                ]
            }
        }
    }
]
}
:::
</dx-codeblock>
5. Click **Complete** to create the policy, which will be displayed on the **Policy List** page.
6. Find the just created policy in the [Policy List](https://console.cloud.tencent.com/cam/policy) and click **Associate** in the **Operation** column on the right.
![](https://main.qcloudimg.com/raw/22a6b170266073a245cdeab0b0aba40d.png)
7. In the **Associate with User/User Group** window that pops up, search for and select the sub-account `DevA` and click **OK** to complete the authorization.
The sub-account `DevA` will have the permission to restart CVM instances under the `test1&test1` tag.
![](https://main.qcloudimg.com/raw/274cd63688f690065fb272191f5a8c5e.png)


## Related Documents

If you want to know how to associate resources with tags, please see [Managing Tags](https://intl.cloud.tencent.com/document/product/651/32583).
If you want to know how to grant all operation permissions of the resources under a tag, please see [Authorizing Different Sub-accounts Separate Permissions to Manage Tencent Cloud Resources](https://intl.cloud.tencent.com/document/product/598/36300).
