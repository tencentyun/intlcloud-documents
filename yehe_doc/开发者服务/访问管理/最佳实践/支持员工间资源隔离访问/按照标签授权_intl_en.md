## Overview
This document describes how to grant permissions by tag to allow the sub-user `cvmtest01` only to manage the resource-level APIs of `ins-duglsqg0`.


## Policy Content
To grant permissions by tag to implement the above need, use the following policy content:
```json
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cvm:*",
                "vpc:DescribeVpcEx",
                "vpc:DescribeNetworkInterfaces"
            ],
            "resource": "*",
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "game&webpage"
                    ]
                }
            }
        }
    ]
}
```


## Directions
### Step 1. Create a policy and configure permissions
1. Log in to the CAM console with the admin account. On the [Policy](https://console.cloud.tencent.com/cam/policy/createV3) page, create a custom policy with tag as instructed in [Creating Custom Policy > Authorizing by tag](https://intl.cloud.tencent.com/document/product/598/35596).
	![](https://qcloudimg.tencent-cloud.cn/raw/34feadcd7fe7865521f48909b3f2ab36.png)
	- Authorized user: cvmtest01
	- Bound tag: game:webpage
	- Operation permissions: All CVM operation permissions and VPC permissions of `DescribeVpcEx` and `DescribeNetworkInterfaces`      
2. Click **Next** and enter a policy name.
3. Click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/a9175a9975d4e91bedd13855f54f6a08.png)    


### Step 2. Verify the result
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1) with the sub-user account `cvmtest01` and enter the instance list page. You can see that the expected effect is achieved.
At this point, the sub-user `cvmtest01` can start, shut down, restart, rename, and reset the password of the CVM instance.
<img src="https://qcloudimg.tencent-cloud.cn/raw/21d3450e703909023e6ffa18c5920f57.png" >         
