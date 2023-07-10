## Overview

COS allows you to filter buckets by tag in the console or via the API, which is implemented based on authorization by tag.

## Authorization steps


1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) with the root account `Owner` and enter the policy configuration page.
2. Grant sub-account `SubUser` access to buckets with the specified tag through the **policy generator** or **policy syntax** as follows:
<dx-tabs>
::: Policy generator
1. Go to the [CAM policy configuration](https://console.cloud.tencent.com/cam/policy) page.
2. Click **Create Custom Policy** > **Create by Policy Generator**.
3. On the permission configuration page, configure the following:
	- **Effect**: use the default option Allow.
	- **Service**: Select COS.
	- **Operation**: Select **Read** > **GetService** (pulling the bucket list).
	- **Resource**: Select **All resources**.
	- **Condition**: Click **Add other conditions**. On the panel, configure the following:
		- **Condition Key**: Select `qcs:resource_tag`.
		- **Operator**: Select `string_equal`.
		- **Condition Value**: Enter a tag in the format of `key&val`. Here, replace `key` and `value` with the tag key and value respectively.
4. Click **Next** and enter the policy name.
5. Click **OK** to complete the process.
:::
::: Policy syntax
1. Go to the [CAM policy configuration](https://console.cloud.tencent.com/cam/policy) page.
2. Click **Create Custom Policy** > **Create by Policy Syntax**.
3. Select **Blank Template** and click **Next**.
4. Enter a policy in the following format. Here, replace `key` and `value` with the specified tag key and value respectively.
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action":[
                "name/cos:GetService"
            ],
            "resource": "*",
            "condition":{
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "key&value"
                    ]
                }
            }
        }
    ]
}
```
5. Click **OK** to complete the process.
:::
</dx-tabs>
3. Associate the policy with the sub-account `SubUser` by locating the policy created in step 2 on the **Policies** page and clicking **Associate User/User Group/Role** on the right.
4. In the pop-up window, select the sub-account `SubUser` and click **OK**.


## Viewing in the console


1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) with the sub-account `SubUser`.
2. The **Bucket List** page **automatically displays the list of buckets to which the sub-account has access**.

At this point, you have granted the sub-account access to buckets with the specified tag (key and value).


## Calling the API


>!
> - Unlike the console, the `GetService` API cannot automatically display the list of buckets to which the sub-account has access and requires you to pass in tag parameters.
> - The `GetService` API currently allows you to pass in only one tag.


1. Initiate a request with the key of the sub-account `SubUser`.
2. Call the `GetService` API to pass in the tag filtering parameters such as `(key,value)`. Below is a sample request. For more information, see [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291).

```
GET /?tagkey=key1&tagvalue=value1 HTTP/1.1
Date: Fri, 24 May 2019 11:59:51 GMT
Authorization: Auth String
```


