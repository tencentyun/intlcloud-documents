## Step 1. Log in to the CAM console

After creating a sub-user/collaborator, you can click **Username** on the **User List** management page in the [CAM console](https://console.cloud.tencent.com/cam) to disable or enable the console access for the current user in **User Details**.

>! The sub-user/collaborator denied access to the console will not be able to log in to the Tencent Cloud console with the current account, but they can still log in to the Tencent Cloud console with their own accounts; in other words, access grant/revocation by the current account does not affect their use of their own Tencent Cloud account.

## Step 2. Grant API access (programming access)

You can configure and manage API access keys as instructed in [Root Account Access Key Management](https://intl.cloud.tencent.com/document/product/598/34228) and [Access Key](https://intl.cloud.tencent.com/document/product/598/32675).

>! Your API key represents your account identity and granted permissions, **which is equivalent to your login password**. Do not disclose it to others.

## Step 3. Authorize a sub-user/collaborator

### Grant access to CMS services

CAM allows you to grant sub-users/collaborators the access permissions of specific CMS services. It can be combined with access method authorization (console/API access) for refined permission management.

#### Policy authorization process

1. Log in to the [console](https://console.cloud.tencent.com/cam) with the root account or a sub-user/collaborator with admin permissions and enter the **User List** page.

2. On the **User List** page, select the target sub-user/collaborator and click **Authorize** to pop up the **Associate Policy** page.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/bc7396527b4c5d4d0ad9c2678ad49015.png)

3. On the **Associate Policy** page, configure the access permissions of CMS services for the sub-user/collaborator as needed.

   >? Currently, you can configure **full access/read-only access** to the AMS, VM, IMS, and TMS services under CMS.

   ![img](https://qcloudimg.tencent-cloud.cn/raw/c9bebcd69e9d65cbdd6d01d21875199e.png)

4. Click **OK**.

#### Description of CAM policies for CMS services

The preset policies for CMS services are as listed below:

<table>
  <tr>
     <td colspan="1" width=150>Service</td>
     <td colspan="1" width=250>Preset Policies</td>
     <td colspan="1">Permission Description</td>
  </tr>
  <tr>
     <td rowspan="2">TMS</td>
     <td colspan="1">QcloudTMSFullAccess</td>
     <td colspan="1">Full access</td>
  </tr>
  <tr>
     <td colspan="1">QcloudTMSReadOnlyAccess</td>
     <td colspan="1">Read-Only access</td>
  </tr>
  <tr>
     <td rowspan="2">IMS</td>
     <td colspan="1">QcloudIMSFullAccess</td>
     <td colspan="1">Full access</td>
  </tr>
  <tr>
     <td colspan="1">QcloudIMSFullAccess</td>
     <td colspan="1">Read-Only access</td>
  </tr>
  <tr>
     <td rowspan="2">AMS</td>
     <td colspan="1">QcloudAMSFullAccess</td>
     <td colspan="1">Full access</td>
  </tr>
  <tr>
     <td colspan="1">QcloudAMSReadOnlyAccess</td>
     <td colspan="1">Read-Only access</td>
  </tr>
  <tr>
     <td rowspan="2">VM</td>
     <td colspan="1">QcloudVMFullAccess</td>
     <td colspan="1">Full access</td>
  </tr>
  <tr>
     <td colspan="1">QcloudVMReadOnlyAccess</td>
     <td colspan="1">Read-Only access</td>
  </tr>
</table>

>? The above preset policies can be used to associate different access permissions of the corresponding CMS services with a sub-user/collaborator. After you assign a preset policy to a sub-user/collaborator as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602), the sub-user/collaborator can access or use the corresponding service according to the permissions granted by the policy.

### Notes

By default, a root account is the resource owner and has full access to all resources under it, while a sub-user/collaborator does not have access to any resources. **A resource creator does not automatically possess the access to the created resource** and should be authorized by the resource owner instead.

A policy is a syntax rule that defines and describes one or more permissions. There are two policy types: **preset policy** and **custom policy**.

>?
>- A preset policy is a set of common permissions that are frequently used by users, such as super admin and full resource access. Preset policies cover a wide range of operation objects at a coarse operation granularity. They are preset by the system and cannot be edited by users.
>- A custom policy is a set of user-defined permissions that describes resource management in a more refined way. It allows fine-grained permission division and can flexibly meet your differentiated permission management needs.

You can set user permissions by selecting a policy in the policy list for association, reusing the existing user policy, or adding the user to a group to get the permissions of the group.

- For how to create a custom policy, see [Creating Custom Policy](https://intl.cloud.tencent.com/document/product/598/35596).
- For how to configure a policy for a user/user group, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

## Step 4. Configure and manage CAM

CAM needs to be properly configured and continuously managed to maximize its value. For the security suggestions on the configuration and management of CAM, see [Security Setting Policy](https://intl.cloud.tencent.com/document/product/598/10592).