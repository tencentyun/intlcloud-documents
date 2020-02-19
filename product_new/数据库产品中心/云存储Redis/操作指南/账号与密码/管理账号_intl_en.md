## Operation Scenarios
TencentDB for Redis provides read/write permission control and routing policy control through the account mechanism, which helps meet the needs of business permission management in complex scenarios. Currently, only the 4.0 Standard Edition and 4.0 Cluster Edition support account settings.
- **Account category**
  - Default account: an account with password only.
  - Custom account: an account with an account name. The authentication method of a custom account is `account name@password`, which is used as the password parameter for accessing Redis, such as `redis-cli -h 1.1.1.1 -p 6379 -a readonlyuser@password`.
- **Account match priority**
  - When there is a default account with the @ separator, it will be matched first before a custom account. Custom accounts will be matched with the first @ symbol as the separator.
  - TencentDB for Redis uses a password-free authentication method different from that of Redis Community Edition. Specifically, after password-free access is enabled for an instance, if the password in the access parameter is not empty, authentication will fail in the former but will succeed in the latter.
- **Permission settings**
  - Read-only permission: the account has the permission to read but not modify data.
  - Read/write permission: the account has the permission to read and write data.
- **Read-only routing policy**
  - By configuring a read-only routing policy, you can distribute **read requests** from the specified account to the specified (master or replica) node.
  - If **read-only replica** is not enabled for an instance, the instance will not support routing to replica nodes. This feature can be enabled on the **Manage Node** page.
  - If an instance has an account accessing a replica node, the **read-only replica** feature cannot be disabled. To disable it, you need to delete the account first.
  
## Directions
1. In the instance list, click an instance name to enter the instance management page.
2. Go to the **Manage Database** > **Manage Account** page, on which you can perform operations such as creating accounts, modifying permissions, resetting passwords, and deleting accounts.
![](https://main.qcloudimg.com/raw/286bfb48c760d737c4b34fffb44fe1ad.png)
 - "Create Account" dialog box:
![](https://main.qcloudimg.com/raw/5d55447bbeb0c6bb2ccb31effa900bf5.png)
 - "Modify Permissions" dialog box:
![](https://main.qcloudimg.com/raw/eee29009f9b33b66b89b4f9fb564a60c.png)
