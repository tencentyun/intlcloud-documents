You can associate Tencent Cloud Mesh-related preset policies in CAM with sub-accounts to rapidly complete CAM authorization for Tencent Cloud Mesh. 

## Tencent Cloud Mesh-related Preset Policies

You can grant your sub-account the necessary permissions by using the following preset policies:

|Policy | Description|
|------- |--------|
|`QcloudTCMFullAccess` | Full access to Tencent Cloud Mesh (All operations such as creation and deletion are allowed.) |
|`QcloudTCMReadOnlyAccess`| Read-only access to Tencent Cloud Mesh (Viewing all resources in Tencent Cloud Mesh is allowed, but creating, updating, and deleting them are not allowed.) |

### Preset Policy for Full Access to Tencent Cloud Mesh

Policy name: QcloudTCMFullAccess; policy content:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "tcm:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

### Preset Policy for Read-Only Access to Tencent Cloud Mesh

Policy name: QcloudTCMReadOnlyAccess; policy content:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "tcm:List*",
                "tcm:Describe*",
                "tcm:ForwardRequestRead"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

## CAM Permissions of Tencent Cloud Mesh-related Products

The use of Tencent Cloud Mesh also involves CAM permissions of related products such as VPC, CCN, CLB, and TKE. You can grant appropriate permissions to sub-accounts by referring to the CAM authorization document of the corresponding product.

| Tencent Cloud Mesh-related Product | Authorization Guide |
|------- |--------|
| VPC | [Cloud Access Management Overview](https://intl.cloud.tencent.com/document/product/215/35498) |
| CLB | [Overview](https://intl.cloud.tencent.com/document/product/214/9777) |
| TKE | [Overview](https://intl.cloud.tencent.com/document/product/457/11542) |

## Associating Sub-accounts with Preset Policies

In the step for setting user permissions when creating a sub-account, you can associate preset policies with the sub-account by [direct association](#direct) or [association via group](#byGroup).

### Direct Association[](id:direct)

You can directly associate your sub-account with a policy to obtain the permissions contained in the policy.

1. Log in to the CAM console and choose **Users** > **[User list](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. On the **User list** page, find the target sub-account and click **Grant permission** in the **Operation** column.
3. On the **Associate policies** page, select the policies that you want to associate.
4. Click **OK**.

### Association via Group[](id:byGroup)

You can add your sub-account to a user group. Then, the sub-account automatically obtains the permissions that are associated with this user group. To disassociate the sub-account from the policies of the group, you simply need to remove the sub-account from the user group.

1. Log in to the CAM console and choose **Users** > **[User list](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. On the **User list** page, find the target sub-account and choose **More** > **Add to group** in the **Operation** column.
3. On the **Add to group** page, select the target user group.
4. Click **OK**.

### Logging In to the Sub-account for Verification

Log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh) to verify that the features corresponding to the associated policies can be used. If they can be used, the sub-account was successfully authorized.
   
