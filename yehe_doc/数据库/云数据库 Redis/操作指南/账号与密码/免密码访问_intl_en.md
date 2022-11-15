TencentDB for Redis supports password-enabled and password-free access.
>?
>- For the sake of data security, you are not recommended to enable password-free access.
>- After password-free access is enabled, you are recommended to limit the number of accessing servers using a security group.

## Setting Password-Free Access
#### Select password-free access when creating an instance
 1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), and click **Create Instance** in the instance list.
 2. In the **Set Password** section on the purchase page, select **Password-Free Authentication**. After the instance is created successfully, it can be accessed without password. 
![](https://qcloudimg.tencent-cloud.cn/raw/c6b59ca29aca31786e4c9b84c0ffd36b.png)

#### Enable password-free access for existing instances
In the instance list, click an instance name to enter the **Instance Details** page, and click **Password-Free Access** in **Configuration Info** > **Connection Password**.

## Viewing Password-Free Access Status
In the instance list, click an instance name to enter the **Instance Details** page, and check whether **Password-Free Access** is enabled in **Configuration Info** > **Connection Password**.
![](https://qcloudimg.tencent-cloud.cn/raw/859076f9404d65817437ce32bb7aa4ec.png)

## Disabling Password-Free Access
In **Configuration Info** > **Connection Password**, you can disable **Password-Free Access** by resetting your password in **Reset Password**.

## Related APIs

| API | Description |
|---------|---------|
| [ResetPassword](https://www.tencentcloud.com/document/product/239/32054) | Resets password. If you leave the `Password` parameter empty, password-free access will be enabled.

