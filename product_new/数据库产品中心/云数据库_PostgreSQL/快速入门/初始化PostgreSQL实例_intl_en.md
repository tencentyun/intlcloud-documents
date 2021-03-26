After creating a TencentDB for PostgreSQL instance, you need to initialize it before you can enable it.

## Prerequisites
1. You have signed up for a Tencent Cloud account and verified your identity.
If you need to sign up for a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 375px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to sign up for a Tencent Cloud account</a></div>
2. You have purchased a TencentDB for PostgreSQL instance.


## Directions
1. Log in to the [TencentDB for Console](https://console.cloud.tencent.com/pgsql). In the instance list, locate the uninitialized instance, and click **Initialize** in the "Operation" column.

   ![](https://main.qcloudimg.com/raw/63731685a6c959999e938a9132b99196.png)

2. In the pop-up dialog box, configure initialization parameters and click **OK**.

 - **Admin Username**: a username can contain 1–16 letters, digits, and special characters (\_). It must start with a letter and end with a letter or digit, is case-insensitive, and cannot be `postgres` or start with `pg\_`.
 - **Password**: a password can be a combination of 8–32 characters that must contain at least two of the following types of characters: letters, digits, and special characters `_+-&=!@#$%^*()`.
 - **Confirm Password**: enter the password again.
 - **Support Character Set**: LATIN1 and UTF8 are supported.
3. You will be returned to the instance list. When the instance status changes to **Running**, the instance can be used.
