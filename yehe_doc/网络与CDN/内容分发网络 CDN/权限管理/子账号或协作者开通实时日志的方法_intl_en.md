To activate real-time logging as a sub-account or collaborator, you need to ask the root account or sub-account with administrator permissions to grant access to the following:

1. Preset policy: `QcloudCamSubaccountsAuthorizeRoleFullAccess`
2. Custom policy: `cdn_PassRole`

## Directions

1. Associate the preset policy `QcloudCamSubaccountsAuthorizeRoleFullAccess` to the sub-account or collaborator.
   The root account/sub-account with administrator permissions needs to log in to the CAM console, and select **Policy** on the left sidebar. Search the preset policy `QcloudCamSubaccountsAuthorizeRoleFullAccess`, and click **Associate Users/Groups** on the right of the policy. In the pop-up dialog, select a sub-account/collaborator to be associated.

2. Create a custom policy `cdn_PassRole` and associate the policy to the sub-account or collaborator.
   1. The root account/sub-account with administrator permissions needs to log in to the CAM console, select **Policy** on the left sidebar, and then click **Create Custom Policy**. In the pop-up dialog, select **Create by Policy Syntax**. 

   2. On the **Create by Policy Syntax** page, select **Blank Template**, and click **Next**. On the **Edit Policy** page, enter the policy name and content as shown below before clicking **Done**.

      The policy syntax is as follows:
```
{
 "version": "2.0",
 "statement": [
     {
         "effect": "allow",
         "action": [
                 "cam:PassRole"
         ],
            "resource": [
                "qcs::cam::uin/${OwnerUin}:roleName/CDN_QCSRole"
            ]
     }
 ]
}
```
`${OwnerUin}` should be replaced with the root account ID, which can be obtained from the CAM console.
 3. Associate the custom policy `cdn_PassRole` to the sub-account or collaborator.
On the **Policy** page, the custom policy `cdn_PassRole` created is displayed, or search the policy by its name. Click **Associate Users/Groups** on the right of the policy. In the pop-up dialog, select a sub-account/collaborator to be associated.

3. After all the policy associations are complete, the sub-account/collaborator can activate real-time logging as prompted in the console.

