## Introduction
This document describes how to set sub-user login password rules to regulate password character types, length, and validity period.

## Directions
>
> - The password rules set here only apply to sub-users that use passwords to log in. Collaborators are not subject to these rules.
> - After the login password expires, sub-users will not be able to log in via other login methods and must reset the password.

1. Log in to the CAM Console and select **User** > **[User Settings](https://console.cloud.tencent.com/cam/security/subAccount)** on the left sidebar.
2. Set the password rules.

<table>
<tr><th "width:20%;">Rule</th "width:40%;"><th>Options</th><th>Restriction</th></tr>
<tr><td>Character type</td><td>Select the characters that must be contained in the password. You can choose digits, uppercase letters, lowercase letters, and special symbols (except spaces)</td><td>At least one item must be selected
</td></tr>
<tr><td>Length</td><td>Restrict the minimum password length</td><td>  
  The length can be set to 8–32 characters
</td></tr>
<tr><td>Validity period</td><td>Restrict the password validity period. When the password expires, it must be reset</td><td>   
The period can be set to 0–365 days</td></tr>
<tr><td>Duplication restriction</td><td>Restrict reuse of old passwords</td><td>    
  0–24 recent passwords can be restricted from being reused</td></tr>
<tr><td>Retry restriction</td><td>Restrict the number of allows attempts with a wrong password. If the configured limit is exceeded, login will be automatically locked for one hour</td><td>  
This can be set to 0–10 attempts/hour</td></tr>
</table>

3. Click **Apply Changes** to make the password rules take effect. You can set the password of a sub-user according to the new rules. When sub-users reset passwords, they must do so according to the password rules you set.
>For the security of your account, sub-users will not be prompted of these rules when they reset passwords. You can go to [User Settings](https://console.cloud.tencent.com/cam/security/subAccount) in the console to download the current password rules and send them to the users as needed.
