## Overview
You can grant a user the permission to view and use specific resources in the ENI console by using a Cloud Access Management (CAM) policy. This document describes how to grant the permission to view and use specified resources.

## Examples
This example grants a sub-user the permission [DeleteNetworkInterface](https://intl.cloud.tencent.com/document/product/215/15822) to delete the ENI *eni-abcdefgh*.

### Solution 1. Generating a policy by policy generator
With a policy created by the policy generator, you can create policy syntax automatically by selecting a service and operations, and defining resources. This method is highly recommended for its simplicity and flexibility.
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy). Click **Create custom policy** in the upper-left corner.
   ![]()
2. In the pop-up window, click **Create by policy generator** to go to the **Edit policy** page.
<img src="" width="70%">
3. Select the service in the **Visual policy generator**, enter the following information, and edit an authorization statement. (You can also choose JSON to use the policy syntax method to edit the policy, and the authorization effect is the same as the **Visual policy generator**).
  - Effect (required): You can select "Allow" or "Deny". Select "Allow" in this example.
  - Service (required): Select the desired product. Select "VPC" in this example.
  - Action (required): Select the desired operation. Select [DeleteNetworkInterface](https://intl.cloud.tencent.com/document/product/215/15822) in this example.
  - Resource (required): Select all resources or the desired resource. In this example, we use six-piece format, that is, qcs::vpc:$region:$account:eni/$networkInterfaceId, where the "$region", "$account:eni" and "$networkInterfaceId" are set to the actual region, account and ENI instance ID respectively.
      ![]()
4. After editing the policy authorization statement, click **Next** to enter the **Associate with user/user group** page.
>?
>+ The policy name is `policygen` by default, which is generated automatically in the console. The suffix number is generated based on the creation date. This is customizable.
>+ You can also associate the policy with a user/user group after creation of the policy.
>
![]()
5. Click **Complete**.

### Solution 2: Generating policy by policy syntax
The following policy allows you to delete the ENI instance *eni-abcdefgh*. You can associate the policy with a user or user group.

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "vpc:DeleteNetworkInterface"
            ],
            "resource": [
                "qcs::vpc::uin/10000xxxxxxx:eni/eni-abcdefgh"
            ]
        }
    ]
}
```
