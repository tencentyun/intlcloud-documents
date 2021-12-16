When you use TMP, in order to use related Tencent Cloud resources, you will encounter a variety of scenarios that require service authorization. The `CM_QCSRole` service role is mainly involved in the process of using TMP. This document describes the details, scenarios, and steps of each authorization policy by role.

The preset policies associated with the `CM_QCSRole` role by default include the following:

QcloudAccessForCMRoleInPromHostingService: TKE permission required by TMP.

## Use Cases

After you successfully create a TMP instance, you need to monitor the services running on TKE. In order to integrate the TKE service more conveniently, you need to access TKE-related APIs. In this case, your authorization is required before TKE can be normally accessed to install basic monitoring components and get their running status information.

This role doesn't need to actively look for configuration. If its permission hasn't been granted, after you successfully create a TMP instance, the authorization page will automatically pop up when you enter the **Integrate with TKE** page for instance management.

## Authorization Steps

#### Authorizing by root account

1. After you successfully create a TMP instance, an authorization window will pop up when you access the **Integrate with TKE** page, and you need to authorize Cloud Monitor permissions as shown below:
2. Click **Authorize Now** in the window.
3. On the **CAM** > **Role Management** page, click **Grant**, and the system will prompt that the authorization is successful.
>?This authorization window will appear only once. If you have already authorized, it will not appear again.

#### Granting permissions to sub-account

After the root account completes the above authorization operations and successfully creates the `CM_QCSRole` role, the sub-account doesn't have permission to access it. The sub-account must be granted the `PassRole` permission by the root account before it can normally access TKE in TMP; otherwise, an error will be displayed when it accesses the TKE cluster list.

When granting the `PassRole` permission to your sub-account, please make sure that your sub-account has the following permissions:

| Permission Description | Granted Policy |
|---------|---------|
| The sub-account needs to be granted access to CAM before granting the `PassRole` permission to the sub-account by the root account can take effect | `QcloudCamReadOnlyAccess` <br> or `QcloudCamFullAcces` |
| The Cloud Monitor policy depends on the Tencent Cloud service policy; therefore, before granting the `PassRole` permission to the sub-account, you need to make sure that the sub-account can normally access TKE resources | For more information, please see <a href="https://cloud.tencent.com/document/product/457/11526">Permission Management |

To ensure that the above permissions are granted successfully, please grant the `cam:PassRole` permission to the sub-account in the following steps.

1. Use the root account or a sub-account with administrative permissions to create the following custom policy:
```json
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": "cam:PassRole",
            "resource": "qcs::cam::uin/${OwnerUin}:roleName/CM_QCSRole"
        }
    ]
}
```
2. After creation, associate the sub-account with the custom policy as instructed in [CAM - Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
 After granting the sub-account the `cam:PassRole` permission, access the **Integrate with TKE** page of the corresponding TMP instance, and an authorization window will pop up.
