## Glossary

- Role: Different from a role in Tencent Cloud, a role in TDMQ is a proprietary concept. It is the smallest unit of permission division performed by you in TDMQ. You can add multiple roles and assign them the production/consumption permissions of different vhosts.
- Key: It is an authentication tool in TDMQ. You can add a key in a client to access TDMQ for message production/consumption. Keys correspond to roles one by one, and each role has its own unique key.

## Use Cases

- You need to securely use TDMQ to produce/consume messages.
- You need to set production/consumption permissions of different vhosts for different roles.

For example, your company has departments A and B, and department A's system produces transaction data and department B's system performs transaction data analysis and display. In line with the principle of least privilege, two roles can be configured to grant department A only the permission to produce messages to the transaction system vhost and grant department B only the permission to consume messages. This helps greatly avoid problems caused by unclear division of permissions, such as data disorder and dirty business data.

## Directions

### Creating role

1. Log in to the [TDMQ console](https://console.intl.cloud.tencent.com/tdmq) and click **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role?rid=4&protocol=AMQP&clusterId=)** on the left sidebar to enter the **Role Management** page.
2. On the **Role Management** page, select the target cluster and click **Create** to enter the **Create Role** page.
3. On the **Create Role** page, enter the role name and remarks:
   - Role Name: It can contain up to 32 digits, letters, and delimiters (underscore or hyphen).
   - Remarks (optional): Enter remarks of up to 100 characters.
4. Click **Submit**.
   ![img](https://main.qcloudimg.com/raw/030444db462129f54a35ce19f7a92e41.png)

### Granting permission to role

1. Find the newly created role in **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role?rid=4&protocol=AMQP&clusterId=)** in the TDMQ console and copy the role key in the following methods:

   <dx-tabs>
       ::: Option 1. Copy in the <b>Key</b> column
       Click **Copy** in the **Key** column.
       ![](https://main.qcloudimg.com/raw/bbb512dd0255b2fca33706dafd4c8b9a.png)
       :::
       ::: Option 2. View and copy in the <b>Operation</b> column
       Click **View Key** in the **Operation** column and click **Copy** in the pop-up window.
       ![](https://main.qcloudimg.com/raw/97acb6323c59344f7193c736786472e0.png)
       :::
       </dx-tabs>
>!Key leakage may lead to data leakage; therefore, you should keep your key confidential.

2. Add the copied role key to the client parameters. For directions on how to add the key parameters to the client code, see [here](https://intl.cloud.tencent.com/document/product/1112/46550) (the key parameters in this document are the username and password).

3. Select the cluster with the previously set role in the TDMQ for RabbitMQ console and click the cluster ID to enter the cluster's basic information page. Switch to the **Vhost** tab, select a vhost for which to configure production and consumption permissions, and click **Configure Permission** in the **Operation** column.
   ![](https://qcloudimg.tencent-cloud.cn/raw/0932393badf8b852dbfcb251f1af1df3.png)

4. Click **Add Role**, find the role just created in the drop-down list, select the required permission, and click **Save**.
   ![img](https://main.qcloudimg.com/raw/7afe9cdf20fb2db9a06079b1f261493e.png)

5. Check whether the permission has taken effect.
   You can run the configured client to access the exchange and queue resources in the vhost and produce/consume messages according to the configured permission. Check whether a no permission error is reported, and if not, the permission has been configured successfully.

### Editing permission

1. In **Vhost** in the TDMQ for RabbitMQ console, find the target vhost and click **Configure Permission** in the **Operation** column to enter the permission configuration list.
2. In the permission configuration list, click **Edit** in the **Operation** column of the target role.
3. In the pop-up window, modify the permission information and click **Save**.

### Deleting permission

>!
> - Before deleting a permission, make sure that the current business no longer uses the role to produce/consume messages; otherwise, a client exception may occur due to the failure to produce/consume messages.
> - A role cannot be deleted if it has permissions configured in vhosts.

1. In **Vhost** in the TDMQ for RabbitMQ console, find the target vhost and click **Configure Permission** in the **Operation** column to enter the permission configuration list.
2. In the permission configuration list, click **Delete** in the **Operation** column of the target role.
3. In the pop-up window, click **OK**.
