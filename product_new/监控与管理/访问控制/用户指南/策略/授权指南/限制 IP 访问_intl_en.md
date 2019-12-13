## Introduction
This document describes how to use custom policy to restrict sub-accounts’ access IPs. After setting the policy, the set IPs will control the sub-accounts’ access to the root account resources. 
## Prerequisites
The product must support limiting access via IP. For more information, see [FAQs](https://intl.cloud.tencent.com/document/product/598/18795).
## Directions
1. Go to the [Policies](https://console.cloud.tencent.com/cam/policy) management page and click **New Custom Policy** in the upper left corner.
3. In the selection window that pops up, click **Create by Policy Generator**.
4. In the Service and Action selection page, enter the following information:
  - Effect: Required. Select “Allow”. If you choose “Deny”, users or groups will not be able to obtain authorization.
  - Service: Required. Select the product you want to add.
  - Action: Required. Select product permissions according to your requirements.
  - Resources: Required. For more information on what to enter, see [Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606).
  - Conditions: Enter the IP address according to your needs. You can add multiple restrictions. For example, for effect, select **Allow** to only permit users or groups from this IP address to obtain authorization.

## Use Case
In the following example, the user must be in the 10.217.182.3/24 or 111.21.33.72/24 IP ranges to invoke the cos:PutObject Cloud API call. This is shown in the following figure:

![](https://main.qcloudimg.com/raw/7fa22e4797a7ca350957fafa1c8889b0.png)

The policy syntax is as follows:
```
{
 "version": "2.0",
 "statement": {
     "effect": "allow",
     "action": "cos:PutObject",
     "resource": "*",
     "condition": {
         "ip_equal": {
             "qcs:ip": [
                 "10.217.182.3/24",
                 "111.21.33.72/24"
             ]
         }
     }
 }
}
```
