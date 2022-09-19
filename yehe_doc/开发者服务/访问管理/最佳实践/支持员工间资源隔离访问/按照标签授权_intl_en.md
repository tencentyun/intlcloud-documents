## Overview
This document describes how to grant permissions by tag to allow the sub-user `cvmtest01` only to manage the resource-level API permissions of `ins-duglsqg0`.
For details, see [Overview](https://intl.cloud.tencent.com/document/product/598/47825)

## Policy Content
To grant permissions by tag as needed, you can use the following policy content:
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
1. Log in to the CAM console with the admin account. On the [Policies](https://console.cloud.tencent.com/cam/policy/createV3) page, create a custom policy by tag as instructed in [Creating Custom Policy > Authorizing by tag](https://intl.cloud.tencent.com/document/product/598/35596).
	![](https://qcloudimg.tencent-cloud.cn/raw/34feadcd7fe7865521f48909b3f2ab36.png)
	- Authorized user: cvmtest01
	- Bound tag: game:webpage
	- Operation permissions: All CVM operation permissions and the `DescribeVpcEx` and `DescribeNetworkInterfaces` permissions of VPC. If you are not sure what other APIs are involved, see [Authorization by Resource ID > Step 3](https://www.tencentcloud.com/document/product/598/47826#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E4.BD.BF.E7.94.A8.E7.AE.A1.E7.90.86.E5.91.98.E8.B4.A6.E5.8F.B7.E8.B0.83.E6.95.B4.E7.AD.96.E7.95.A5.E5.86.85.E5.AE.B9).      
2. Click **Next** and enter a policy name.
3. Click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/a9175a9975d4e91bedd13855f54f6a08.png)    


### Step 2: Verify the result
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1) as the sub-user `cvmtest01` and access the instance list page.
Then the sub-user `cvmtest01` can start, shut down, restart, rename, and reset the password of the CVM instance.
<img src="https://qcloudimg.tencent-cloud.cn/raw/21d3450e703909023e6ffa18c5920f57.png" >         
