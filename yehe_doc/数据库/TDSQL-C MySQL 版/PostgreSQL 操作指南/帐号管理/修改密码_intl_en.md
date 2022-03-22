
This document describes how to change the password of the DBA account in the console.

## Overview
If you forgot the DBA account password, you can reset it in the console.
>!Tencent Cloud does not keep passwords for database accounts. All password changes are directly sent to the database over an encrypted channel for execution, and the database manages them all in a unified manner.

## Directions
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb?dbType=POSTGRESQL) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Account Management** tab to view the admin account under the current cluster. Click **Reset Password** in the **Operation** column.
3. In the pop-up window, enter the new password and confirm password and click **OK**.
>? The password must comply with the following rules:
>- It can contain 8–64 characters.
>- It must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special symbols `~!@#$%^&*_-+=|\(){}[]:;'<>,.?/`.
>

