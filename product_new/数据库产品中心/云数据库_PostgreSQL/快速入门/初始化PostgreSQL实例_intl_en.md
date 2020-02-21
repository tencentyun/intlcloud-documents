This document describes how to initialize a TencentDB for PostgreSQL instance for getting started with ease.

## Prerequisites
1. You have signed up for a Tencent Cloud account and verified your identity.
If you need to sign up for a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to sign up for a Tencent Cloud account</a></div>
2. You have purchased a TencentDB for PostgreSQL instance.
If you need to purchase a TencentDB for PostgreSQL instance:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://buy.cloud.tencent.com/pgsql" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn3">Click here to enter the purchase page</a></div>
## Directions
1. Log in to the [TencentDB for PostgreSQL Console](https://console.cloud.tencent.com/pgsql) and select **Instance List** on the left sidebar.
2. Select a TencentDB for PostgreSQL instance whose status is **to be initialized** and click **Initialize** in the "Operation" column.
3. In the pop-up window, select the configuration for initialization and click **OK**.
 - **Admin Username**: a username can contain 1–16 letters, digits, and special characters (\_). It must start with a letter and end with a letter or digit, is case-insensitive, and cannot be `postgres` or start with `pg\_`.
 - **Password**: a password can be a combination of 8–32 characters that must contain at least two of the following types of characters: letters, digits, and special characters `_+-&=!@#$%^*()`.
 - **Confirm Password**: enter the password again.
 - **Supported Character Sets**: LATIN1 and UTF8. The default character set is UTF8.
4. Return to the instance list. After the status of the instance changes to **running**, the initialization has succeeded.
