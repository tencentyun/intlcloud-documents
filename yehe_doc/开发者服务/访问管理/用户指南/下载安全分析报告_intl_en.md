## Overview

You can download a user credential report to view the credential status of all Tencent Cloud sub-accounts and their sub-users, as well as the console login password, access key and account security settings. This report can also be used for compliance audit.


## Directions

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview), and click **Overview** in the left sidebar.
2. In the “Security Analysis Report” module, click **Download User Credential Report** and complete identity verification as prompted. Then the report will be automatically generated.
3. After downloading the report, you can view it locally.
>?A user credential report in CSV format is generated in the console every four hours. If you click **Download User Credential Report** within four hours after the last report is generated, you will get the same report rather than a new one. 

## Report Format

The user credential report is in CSV format. You can use common spreadsheet software to open the CSV file for further analysis or use the file programmatically and perform custom analysis.
The CSV file contains the following information:

| Field                           | Description                      | Value                                                     |
| ------------------------------ | ------------------------- | ------------------------------------------------------------ |
| AccountID                      | Account ID                   | Sub-account ID                                                    |
| Username                       | Username                  | Sub-account username                                               |
| UserType                       | User type                  | <li>`Sub-user`: sub-user </li><li>`Collaborator`: collaborator </li><li>`WeWork-Sub-user`: WeCom sub-user </li><li>`Message-receiver`: message recipient |
| CreationTime                   | Creation time                  | Sample value: 2019/8/16 9:25:56                                      |
| PasswordEnabled                | Whether the console login password is enabled        | <li>`TRUE`: enabled </li><li>`FALSE`: disabled. Console access is disabled and the login password is not set. </li><li>`not_supported`: not supported. A WeCom sub-user logs in by scanning the QR code without a password. A message recipient only receives messages and does not have a password. A collaborator logs in as a root account and is not subject to this field. </li> |
| PasswordLastRotation           | Time when the password was last modified          | <li>`FALSE`: Console access is disabled and the login password is not set. </li><li>`not_supported`: not supported. A WeCom sub-user logs in by scanning the QR code without a password. A message recipient only receives messages and does not have a password. A collaborator logs in as a root account and is not subject to this field.</li> |
| LoginConsoleActive             | Whether console login is supported        | <li>`TRUE`: enabled </li><li>`FALSE`: disabled </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password. A collaborator logs in as a root account and is not subject to this field. |
| LoginProtectionActive          | Whether login protection is enabled          | <li>`TRUE`: enabled </li><li>`FALSE`: disabled </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password.</li> |
| OperationProtectionActive      | Whether operation protection is enabled          | `TRUE`: enabled <br />`FALSE`: disabled <br />`not_supported`: not supported. A message recipient only receives messages and does not have a login password. |
| MFADeviceActive                | Whether MFA is enabled              | <li>`TRUE`: enabled </li><li>`FALSE`: disabled </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password. The sub-user has not been bound to a mobile number or WeChat account. </li> |
| Abnormal LoginsNumWithin30Days | Whether suspicious login behavior is detected in 30 days             | <li>`TRUE`: suspicious login behavior detected </li><li>`FALSE`: suspicious login behavior not detected  </li>             |
| AccessKey1SecretId             | SecretId of key 1           | `N/A`: no key                                                  |
| AccessKey1MayBeAtRisk          | Whether key 1 has leakage risk | <li>`TRUE`: at risk </li><li>`FALSE`: no risk </li><li>`N/A`: no key 1 </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password. </li> |
| AccessKey1CreationTime         | Creation time of key 1           | <li>`N/A`: no key 1 </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password. </li> |
| AccessKey1Status               | Status of key 1               | <li>`Active`: enabled </li><li>`Disable`: disabled </li><li>`N/A`: no key 1 </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password. </li> |
| AccessKey1lastUsedDate         | Time when key 1 was last used  | <li>`N/A`: no key 1 </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password. </li> |
| AccessKey1CreatedOver90Days    | Whether key 1 has been created for over 90 days   | <li>`N/A`: no key 1 </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password. </li> |
| AccessKey1CreatedOver30Days    | Whether key 1 has been created for over 30 days   | <li>`N/A`: no key 1 </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password. |
| AccessKey2SecretId             | SecretId of key 2          | `N/A`: no key 2                                                 |
| AccessKey2MayBeAtRisk          | Whether key 2 has leakage risk | <li>`TRUE`: at risk </li><li>`FALSE`: no risk </li><li>`N/A`: no key 2 </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password. </li> |
| AccessKey2CreationTime         | Creation time of key 2           | <li>`N/A`: no key 2 </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password. </li> |
| AccessKey2Status               | Status of key 2               | <li>`Active`: enabled </li><li>`Disable`: disabled </li><li>`N/A`: no key 2 </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password. </li> |
| AccessKey2lastUsedDate         | Time when key 2 was last used  | <li>`N/A`: no key 2 </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password. </li> |
| AccessKey2CreatedOver90Days    | Whether key 2 has been created for over 90 days   | <li>`N/A`: no key 2 </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password. </li> |
| AccessKey2CreatedOver30Days    | Whether key 2 has been created for over 30 days   | <li>`N/A`: no key 2 </li><li>`not_supported`: not supported. A message recipient only receives messages and does not have a login password. |
