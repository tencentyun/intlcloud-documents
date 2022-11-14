This document describes the custom password strength feature of TDSQL-C for MySQL.

## Feature overview
Passwords are the most important means for protecting database security. As more data security regulations are introduced, there are higher requirements for the database password strength. TDSQL-C for MySQL supports the custom password strength feature to protect your database security and meet your needs for compliance with applicable regulations.

You can configure this feature in the console to enable password strength for all password-related operations. This helps protect your passwords from leakage or other risks. The feature offers the following configuration items:

| Parameter | Description |
|---------|---------|
| Min Number of Uppercase and Lowercase Pair | Default value: `1`. Value range: 1–50. |
| Min Number of Digits | Default value: `1`. Value range: 1–50. |
| Min Number of Symbols | Default value: `1`. Value range: 1–50. |
| Min Password Length | Default value: `8`. Value range: 8–256. |
| Non-Compliant Dictionary |         If the password strength level is **STRONG**, this parameter is configurable. Each non-compliant word can contain 4–100 letters. |
| Password Strength Level | You can select **MEDIUM** or **STRONG** as the strength level.<li>MEDIUM: The feature under this setting will check the length, digits, letters, and symbols.</li><li>STRONG: The feature under this setting will check the length, digits, letters, symbols, and non-compliant word dictionary.</li> |
| Modify Parameters | You can modify the feature parameters to flexibly adjust the password strength settings. |
| Parameter Sync | Parameter sync and batch disablement features are provided, so you can batch apply the configuration in multiple clusters at a time. |


After the custom password strength feature is enabled, you must meet the defined password strength requirements when setting passwords during operations such as account creation, password resetting, and account cloning.

When you connect to the database and use the command line to perform operations, if the custom password strength feature is enabled, all statements involving password setting will be restricted, such as CREATE USER, ALTER USER, and SET PASSWORD. When you use such statements to set or change an account password, the password must meet the defined password strength requirements.

## Prerequisites
You have created a TDSQL-C for MySQL cluster.

## Version limits
The custom password strength feature is supported by the following versions:
- MySQL 5.7 on kernel minor version 2.0.21 or later and 2.1.7 or later.
- MySQL 8.0 on kernel minor version 3.1.7.

You can use this feature only after upgrading the kernel to the above versions. For detailed directions, see [Upgrading Kernel Minor Version](https://intl.cloud.tencent.com/document/product/1098/44617).

## Mutually exclusive tasks
A password strength customization task cannot be executed while a cluster is running another task, such as isolation, rollback, creation, minor version upgrade, or parameter modification. The two tasks are mutually exclusive and will be performed sequentially.

## Relevant operations
- You can grant a sub-account the permission to use the custom password strength feature as instructed in [Granting Sub-User Feature Permissions](https://intl.cloud.tencent.com/document/product/1098/49980).
- You can enable/disable this feature as instructed in [Enabling/Disabling Custom Password Strength Feature](https://intl.cloud.tencent.com/document/product/1098/49979).
- After the custom password strength feature is enabled, you can modify the custom password strength and specific parameters as well as configure parameter sync as instructed in [Modifying Parameters and Configuring Parameter Sync](https://intl.cloud.tencent.com/document/product/1098/49978).

