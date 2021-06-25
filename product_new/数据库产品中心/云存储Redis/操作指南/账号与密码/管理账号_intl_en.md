## Operation Scenarios
TencentDB for Redis provides read/write permission control and routing policy control through the account mechanism, which helps meet the needs of business permission management in complex scenarios. Currently, only the TencentDB for Redis Memory Edition (excluding v2.8) supports account settings.
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
1. Log in to the [Redis Console](https://console.cloud.tencent.com/redis) and click an instance ID in the instance list to enter the instance management page.
2. Select the **Manage Account** tab, on which you can create accounts, modify permissions, reset passwords, and delete accounts.
![](https://main.qcloudimg.com/raw/276fb5f3092f46c57d675b19d1a14962.png)
