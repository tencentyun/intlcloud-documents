
## Overview  
Sub-users generally don't have financial permissions. When they purchase a monthly subscribed DTS instance, the system will prompt that only the root account can pay the order. After the root account grants financial permissions to them, they can purchase such instances by themselves and use the account balance of the root account to make payments.

## Prerequisites
You have created and authorized a sub-user as instructed in [Creating and Authorizing Sub-user](https://intl.cloud.tencent.com/document/product/571/47358).

## Directions
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) as the root account.
2. Click **Policies** on the left sidebar. Then, click **Create Custom Policy** on the right and select **Create by Policy Syntax**.      
3. Select **Blank Template** and click **Next**.  
4. Create a policy, enter the policy name and description as needed, and copy the sample code to the **Policy Content**. <br>
   <br>Sample policy syntax: 
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": "finance:*",
            "resource": "qcs::dts:::*"
        }
    ]
}
```
5. Click **Complete**, return to the **Policy List** page, and click **Associate Users/Groups**.   
6. Select the sub-user to be authorized (i.e., the sub-user created above) and click **OK**.


