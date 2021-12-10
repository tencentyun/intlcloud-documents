## Glossary

- Role: different from a role in Tencent Cloud, a role in TDMQ for Pulsar is a proprietary concept. It is the smallest unit of permission division performed by you in TDMQ. You can add multiple roles and assign them the production/consumption permissions of different namespaces.
- Token: it is an authentication tool in TDMQ for Pulsar. You can add a token in a client to access TDMQ for Pulsar for message production/consumption. Tokens correspond to roles one by one, and each role has its own unique token.

## Use Cases

- You need to securely use TDMQ for Pulsar to produce/consume messages.
- You need to set production/consumption permissions of different namespaces for different roles.

For example, your company has departments A and B, and department A's system produces transaction data and department B's system performs transaction data analysis and display. In line with the principle of least privilege, two roles can be configured to grant department A only the permission to produce messages to the transaction system namespace and grant department B only the permission to consume messages. This helps greatly avoid problems caused by unclear division of permissions, such as data disorder and dirty business data.

## Directions

### Creating role

1. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq) and click **Role Management** on the left sidebar to enter the **Role Management** page.
2. On the **Role Management** page, select the region and cluster and click **Create** to enter the **Create Role** page.
3. On the **Create Role** page, enter the role name and remarks:
   - Role Name: it can contain up to 32 digits, letters, and delimiters (underscore or hyphen).
   - Remarks (optional): enter remarks of up to 100 characters.
4. Click **Submit**.
  ![](https://qcloudimg.tencent-cloud.cn/raw/57082bf925e3b78732f71afdbe29ea76.png)

### Granting permission to role

1. Find the newly created role in **[Role Management](https://console.cloud.tencent.com/tdmq/role)** in the TDMQ for Pulsar console and copy the role token in the following methods:
   <dx-tabs>
   ::: Method\s1.\sCopy\sin\sthe\s<b>Token</b>\scolumn
   Click **Copy** in the **Token** column.
   ![](https://qcloudimg.tencent-cloud.cn/raw/8c80626460740e87e734b27d783256a9.png)
   :::
   ::: Method\s2.\sView\sand\scopy\sin\sthe\s<b>Operation</b>\scolumn
   Click **View Token** in the **Operation** column and click **Copy** in the pop-up window.
   ![](https://qcloudimg.tencent-cloud.cn/raw/df39efabf4803bc97d2f5f07b7376f2a.png)
   :::
   </dx-tabs>
2. Add the copied role token to the client parameters. For directions on how to add the token parameter to the client code, see [JWT Authentication Configuration](https://intl.cloud.tencent.com/document/product/1110/42933).
> !Token leakage may lead to data leakage; therefore, you should keep your token confidential.

3. In **[Namespace](https://console.cloud.tencent.com/tdmq/env)** in the TDMQ for Pulsar console, select the target namespace and click **Configure Permission** in the **Operation** column.
   ![](https://qcloudimg.tencent-cloud.cn/raw/4d230e64c7eec774668ec1aed09a9ee2.png)
4. Click **Add Role**, find the role just created in the drop-down list, select the required permission, and click **Save**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/8787a1fd4967a5230d61c272c46850d7.png)
5. Check whether the permission has taken effect.
   You can run the configured client to access the topic resources in the namespace and produce/consume messages according to the configured permission. Check whether a no permission error is reported, and if not, the permission has been configured successfully.

### Editing permission

1. In **[Namespace](https://console.cloud.tencent.com/tdmq/env)** in the TDMQ for Pulsar console, find the target namespace and click **Configure Permission** in the **Operation** column to enter the permission configuration list.
2. In the permission configuration list, click **Edit** in the **Operation** column of the target role.
3. In the pop-up window, modify the permission information and click **Save**.



### Deleting permission

> !
>
> - Before deleting a permission, make sure that the current business no longer uses the role to produce/consume messages; otherwise, a client exception may occur due to the failure to produce/consume messages.
> - A role cannot be deleted if it has permissions configured in namespaces.

1. In **[Namespace](https://console.cloud.tencent.com/tdmq/env)** in the TDMQ for Pulsar console, find the target namespace and click **Configure Permission** in the **Operation** column to enter the permission configuration list.
2. In the permission configuration list, click **Delete** in the **Operation** column of the target role.
3. In the pop-up window, click **OK**.
