## Glossary

- Role: different from a role in Tencent Cloud, a role in TDMQ is a proprietary concept. It is the smallest unit of permission division performed by you in TDMQ. You can add multiple roles and assign them the production/consumption permissions of different namespaces.
- Token: it is an authentication tool in TDMQ. You can add a token in a client to access TDMQ for message production/consumption. Tokens correspond to roles one by one, and each role has its own unique token.

TDMQ for RocketMQ inherits these concepts. In TDMQ for RocketMQ, the `ACL_ACCESS_KEY` defined in the open-source client corresponds to the TDMQ token.

## Use Cases

- You need to securely use TDMQ to produce/consume messages.
- You need to set production/consumption permissions of different namespaces for different roles.

For example, your company has departments A and B, and department A's system produces transaction data and department B's system performs transaction data analysis and display. In line with the principle of least privilege, two roles can be configured to grant department A only the permission to produce messages to the transaction system namespace and grant department B only the permission to consume messages. This helps greatly avoid problems caused by unclear division of permissions, such as data disorder and dirty business data.

## Directions

### Creating role

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq) and click **[Role Management](https://console.cloud.tencent.com/tdmq/role?rid=4&protocol=RocketMQ&clusterId=)** on the left sidebar to enter the **Role Management** page.
2. On the **Role Management** page, select the target cluster and click **Create** to enter the **Create Role** page.
3. On the **Create Role** page, enter the role name and remarks:
   - Role Name: it can contain up to 32 digits, letters, and delimiters (underscore or hyphen).
   - Remarks (optional): enter remarks of up to 100 characters.
4. Click **Submit**.
    ![](https://qcloudimg.tencent-cloud.cn/raw/c3a86cd8ab8e808166e880a423178f10.png)

### Granting permission to role

1. Find the newly created role in **[Role Management](https://console.cloud.tencent.com/tdmq/role?rid=4&protocol=RocketMQ&clusterId=)** in the TDMQ console and copy the role token in the following methods:
   <dx-tabs>
     ::: Method\s1.\sCopy\sin\sthe\s<b>Token</b>\scolumn
     Click **Copy** in the **Token** column.
    ![](https://qcloudimg.tencent-cloud.cn/raw/10afef255c4577473b0426af8cc9e7cf.png)
     :::
     ::: Method\s2.\sView\sand\scopy\sin\sthe\s<b>Operation</b>\scolumn
     Click **View Token** in the **Operation** column and click **Copy** in the pop-up window.
     ![](https://qcloudimg.tencent-cloud.cn/raw/5778445dc839d99bff8755d5813a1201.png)
     :::
     </dx-tabs>

> !Token leakage may lead to data leakage; therefore, you should keep your token confidential.

2. Add the copied role token to the client parameters. For directions on how to add the token parameter to the client code, see the [sample code](https://github.com/streamnative/rop/blob/master/examples/src/main/java/org/streamnative/rocketmq/example/simple/AclClient.java) of RocketMQ.

   A recommended way is given below:
   1. Declare two fields `ACL_SECRET_KEY` and `ACL_SECRET_ACCESS`. If you use various frameworks, we recommend you read them from the configuration file. **Here, `ACL_SECRET_KEY` uses "rop" directly**.

      ```java
      private static final String ACL_ACCESS_KEY = "eyJr****";
      private static final String ACL_SECRET_KEY = "rop"; // Use "rop" directly
      ```
   2. Declare a static function to load a `RPCHook` object of the RocketMQ client.
      ```java
      static RPCHook getAclRPCHook() {
          return new AclClientRPCHook(new SessionCredentials(ACL_ACCESS_KEY, ACL_SECRET_KEY));
      }
      ```
   3. When creating RocketMQ's `producer`, `pushConsumer`, or `pullConsumer`, import the `RPCHook` object.
      Below is the sample code for creating a `producer`:

      ```java
      DefaultMQProducer producer = new DefaultMQProducer("rocketmq-mw***|namespace", "ProducerGroupName", getAclRPCHook());
      ```
3. After selecting the cluster with the previously set role in the TDMQ for RocketMQ console, switch to the **Namespace** page, select a namespace for which to configure production and consumption permissions, and click **Configure Permissions** in the **Operation** column.
	![](https://qcloudimg.tencent-cloud.cn/raw/5cd676d675dd1442f89b1f616c5fdd80.png)
4. Click **Add Role**, find the role just created in the drop-down list, select the required permission, and click **Save**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/05914b652c631220caf865e008823b9b.png)
5. Check whether the permission has taken effect.
   You can run the configured client to access the topic resources in the namespace and produce/consume messages according to the configured permission. Check whether a no permission error is reported, and if not, the permission has been configured successfully.

### Editing permission

1. In **Namespace** in the TDMQ for RocketMQ console, find the target namespace and click **Configure Permission** in the **Operation** column to enter the permission configuration list.
2. In the permission configuration list, click **Edit** in the **Operation** column of the target role.
3. In the pop-up window, modify the permission information and click **Save**.



### Deleting permission

> !
> - Before deleting a permission, make sure that the current business no longer uses the role to produce/consume messages; otherwise, a client exception may occur due to the failure to produce/consume messages.
> - A role cannot be deleted if it has permissions configured in namespaces.

1. In **Namespace** in the TDMQ for RocketMQ console, find the target namespace and click **Configure Permission** in the **Operation** column to enter the permission configuration list.
2. In the permission configuration list, click **Delete** in the **Operation** column of the target role.
3. In the pop-up window, click **OK**.
