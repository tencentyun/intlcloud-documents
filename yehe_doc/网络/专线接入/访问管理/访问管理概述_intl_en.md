If you have multiple users managing different Tencent Cloud services such as Direct Connect, VPC, CVM and other Tencent Cloud products, and they all share your Tencent Cloud account access key, you may face the following problems:
- The risk of your key being compromised is high since multiple users are sharing it.
- Your users might introduce security risks from misoperations due to the lack of user access control.

You can avoid the above problems by CAM, which allows different users to manage different services through sub-accounts. The dedicated tunnel of Direct Connect supports the resource-level permissions. By default, a sub-account does not have permissions to use dedicated tunnel or its resources. Therefore, you need to create a policy to grant different permissions to the sub-accounts.

>?You can skip this section if you do not need to manage permissions to dedicated tunnel resources for sub-accounts. This will not affect your understanding and use of the other sections of the document.
>

## Supported Permissions
The Direct Connect service consists of connection, dedicated tunnel and direct connect gateway resources. The following table specifies the supported access permissions to resources:
<table>
<tr>
<th>Resource</th>
<th>Permission</th>
<th>Authorization Granularity</th>
</tr>
<tr>
<td>Connection</td>
<td>Supported</td>
<td>API-level</td>
</tr>
<tr>
<td>Dedicated tunnel</td>
<td>Supported</td>
<td>Resource-level</td>
</tr>
<tr>
<td>Direct connect gateway</td>
<td>Supported</td>
<td>Resource-level</td>
</tr>
</table>

## CAM
Cloud Access Management (CAM) is a Tencent Cloud web service that helps you securely manage and control access to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users and user groups. You can manage identities and policies to allow specific users to access your Tencent Cloud resources.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, see [Syntax Logic](https://intl.cloud.tencent.com/document/product/598/33415). For more information on the use of CAM policies, see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).

The root account can associate policies with sub-accounts to implement permissions. The policies support multiple dimensions, such as API, resource, user, user group, allowing, forbidding, and condition.
- **Account**
  - **Root account**: the owner of Tencent Cloud resources and the fundamental entity for resource usage, usage calculation, and billing. It can be used to log in to Tencent Cloud services.
  **Sub-account**: an account created by the root account. It has a specific ID and identity credential that can be used to log in to the Tencent Cloud console. A root account can create multiple sub-accounts (users). **By default, a sub-account does not own any resources and must be authorized by its root account.**
  - **Identity credential**: includes login credentials and access certificates. **Login credential** refers to a user’s login name and password. **Access certificate** refers to Tencent Cloud API keys (SecretId and SecretKey).
- **Resource and permission**
  - **Resource**: an object that is operated in Tencent Cloud services, such as a CVM instance, a COS bucket, or a VPC instance.
  - **Permission**: an authorization that allows or forbids users to perform certain operations. **By default, the root account has full access to all resources under the account**, while **a sub-account does not have access to any resources under its root account**.
  - **Policy**: syntax rule that defines and describes one or more permissions. The **root account** performs authorization by **associating policies** with users/user groups.
>?For more information, please see [CAM Overview](https://intl.cloud.tencent.com/document/product/598/10583).


## Documentation

| Task | Link |
| :----------------------- | :----------------------------------------------------------- |
| Understand the relationship between policies and users | [Policy](https://intl.cloud.tencent.com/document/product/598/10601) |
| Understand the basic structure of policies | [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603)|
| Check CAM-enabled products | [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588)|

