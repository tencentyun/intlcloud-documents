## Prerequisites
- You have created a database credential. If haven’t, see [Creating a Database Credential](https://intl.cloud.tencent.com/document/product/1078/41801).
- You have enabled rotation for the credential. If haven’t, see [Enabling a Database Credential](https://intl.cloud.tencent.com/document/product/1078/41803).



## Rotation Effect
SSM rotates accounts and passwords stored in the credential upon a periodical rotation preset by the user, so that the client can obtain the newest account and password by calling [GetSecretValue](https://intl.cloud.tencent.com/document/product/1078/38649).
The rotation does not affect the credential’s access to the corresponding database using the newest account and password, as SSM synchronizes the account and password information to the database.

## Integrating Application with SSM
Only by calling [GetSecretValue](https://intl.cloud.tencent.com/document/product/1078/38649), the application can obtain the newest account and password for database access.

## Risk Notice
### Risk
The database credential’s account password has been updated after the periodical rotation. If you access the database with the expired password, an access failure occurs.

### Solution
To prevent access failure, do not enable the client to save passwords automatically. Also, use Tencent Cloud’s SSM SDK ([Go](https://github.com/TencentCloud/ssm-rotation-sdk-golang) and [Python](https://github.com/TencentCloud/ssm-rotation-sdk-python)) recommended in **Best Practices** instead of a third-party SDK that implements database connection pooling. 
