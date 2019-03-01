[//]: # (chinagitpath:XXXXX)

[Creating a Sub-account](https://cloud.tencent.com/document/product/634/14453) describes how to grant a sub-account the full-access control permissions in IoT Hub. This document describes how to grant a sub-account the product-level access control permissions. The product-level access control permissions allow the sub-account to access and control the products created by itself or created for it by the primary account.

In order to do so, you need to configure according to the steps below.
## Creating a Policy
1. Go to Tencent Cloud [Policy Management Console](https://console.cloud.tencent.com/cam/policy), click **Create Custom Policy** and select "Create by Policy Syntax".
![](https://mc.qcloudimg.com/static/img/21ec61d96a985398d58f6c478d011cca/celue1.png)

2. Select "Blank Template" and click **Next**.
![](https://mc.qcloudimg.com/static/img/c922969864266ee02b6ea21fbbe026ad/celue2.png)

3. Enter the custom policy name and edit the policy content based on the policy template.
```
{
        "version": "2.0",
        "statement": [
            {
                "action": [
                    "iotcloud:CreateProduct"
                ],
                "resource": "*",
                "effect": "deny"
            },
            {
                "action": [
                    "iotcloud:*"
                ],
                "resource": "*",
                "effect": "allow",
                "condition": {
                    "string_equal_if_exist": {
                        "product": [
                            "${productID1}",
                            "${productID2}",
                            "${productID3}"
                        ]
                    }
                }
            }
        ]
}
```
![](https://mc.qcloudimg.com/static/img/28e8be65466cbe88cc60fba80fb1f0cb/celue3.png)

## Associating a Policy
1. After the custom policy is created, go to "User Management", select the sub-account to which to grant the permissions and click **Associate Policy**.
![](https://mc.qcloudimg.com/static/img/ec344b63e0855b58db762bcc32198b07/image.png)

2. Search for the name of the policy just created, click **OK** after selecting it, and the permissions defined in the policy will be granted.
![](https://mc.qcloudimg.com/static/img/46da94e36d9f29a7a7c206a6dd031d78/guanliancelue2.png)

## Policy Notes
- The policy template below indicates that the sub-account is not allowed to create products. To disable other permissions for the sub-account, you can write the permission API names in "action". For example, writing "iotcloud::DeleteDevice" there prohibits the deletion of devices.
```
{
         "action": [
              "iotcloud:CreateProduct"
         ],
         "resource": "*",
         "effect": "deny"
 }
```

- The policy template below indicates that other permissions (such as device creation and deletion) are granted. However, these operations can only be performed under the specified product, subject to the PID entered in the product list (you can replace ${productID\*} with the product ID of the IoT product to which to grant the permissions).
```
{
       "action": [
            "iotcloud:*"
        ],
        "resource": "*",
        "effect": "allow",
        "condition": {
             "string_equal_if_exist": {
                  "product": [
                       "${productID1}",
                       "${productID2}",
                       "${productID3}"
                  ]
             }
       }
}
```
The product ID can be obtained from the basic product information in the console shown in the figure below.
![](https://main.qcloudimg.com/raw/d6d45dcaf556d9a4a5487b6bbdf3db0d.png)

