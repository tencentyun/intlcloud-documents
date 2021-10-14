## Scenarios
You want to enable rotation and encryption for database credential created in the [SSM](https://console.cloud.tencent.com/ssm) console, securing your data while reducing disclosure risks and security threats to your account.

## Prerequisites
Before using database credentials, please note the following prerequisites:
- You have [enabled KMS services](https://console.cloud.tencent.com/ssm/cloud), as SSM encrypts data based on keys managed in KMS.
- You have created a TencentDB for MySQL instance or TDSQL for MySQL instance. For details, see [Creating MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37785), and [Creating TDSQL Instance](https://intl.cloud.tencent.com/document/product/1042/33336).

## Directions
1. Log in to the [SSM Console](https://console.cloud.tencent.com/ssm) and click **Database Credential** on the left sidebar.
![](https://main.qcloudimg.com/raw/ec2c0aa7f77ae3a7e511feaffdbdece8.png)
2. Click the drop-down button in the top left corner of the credential list to modify the region.
![](https://main.qcloudimg.com/raw/095961780f5aa89c12a05dc66138bd69.png)
3. Click **Create** in the top left corner of the credential list.
4. Enter the information required to create a credential and click **OK**. The credential will be displayed at the top of the credential list.
![](https://main.qcloudimg.com/raw/36af2d4711cd3b141b3cd137894cb3ee.png)

### Fields
#### Basic settings
- **Secret Name**: supports 1–128 bytes of letters, digits, hyphens (-), and underscores (_). **It must start with a letter or digit**.
- **Description**: contains information of a credential using up to 2048 bytes (optional).

#### Database account settings
- **Bound Instance**: a MySQL instance or TDSQL instance of your choice.
- **Account Prefix**: contains 12 characters of lower-case letters and digits. **It must start with a letter**.
>? Two account names will be generated in the format of [prefix]_SSM_[three random digits]. These two account names will be shifted for rotation.
- **Server**:
 - Must be in IP format. % is supported.
 - Multiple servers should be separated with a carriage return or space.
- **Authorization**: enables you to set permissions on the database.
  ![](https://main.qcloudimg.com/raw/9c2c445ec104c5f6367911dde30a1cb0.png)

#### Rotation settings
- **Rotation Status**: **with rotation enabled, SSM will update the database credential password periodically. It is recommended to enable rotation for safety**.
- **Rotation Cycle**: ranges from 30 days to 365 days.
- **Next Rotation Start**: **enables you to set the start time (in seconds) for next rotation as needed**.

#### Others
- **Tag**: optional item.
- **Encryption Key**:
 - Use the default CMK that SSM has created in KMS.
 - Use a custom encryption key. 

> ! If you are using SSM, you have activated [KMS](https://intl.cloud.tencent.com/product/kms). You can create an encryption key in either of the following ways:
- Use the default Tencent Cloud managed CMK created in the [KMS console](https://intl.cloud.tencent.com/product/kms) as encryption key, and use the envelope encryption method for encrypted storage.
- Use a custom key created in the [KMS console](https://intl.cloud.tencent.com/product/kms) as encryption key for encrypted storage.
