## Overview
This document describes how to set sub-user login password rules to regulate sub-users’ login password character types, length, and validity period.


>?After the login password expires, sub-users will not be able to log in via other login methods and must reset the password.

## Directions


1. Log in to the CAM console and select **Users** > [User Settings](https://console.cloud.tencent.com/cam/security/subAccount) in the left sidebar.
2. Set the password rule.
>!
>- This password rule applies to the password of a sub-user created via a custom method. For example, if you set the rule to "Should contain at least 10 characters of digits and lowercase letters", the password of the sub-user you created should comply with this rule.
>- This rule does not apply to sub-users that log in via WeCom or collaborators.
<table>
<tr><th "width:20%;">Rules</th "width:40%;"><th>Options</th><th>Restrictions</th></tr>
<tr><td>Character type</td><td>Select the characters that must be used in the password. You can choose numeric characters, uppercase letters, lowercase letters, special characters (except for spaces)</td><td> At least one item must be selected
</td></tr>
<tr><td>Length</td><td>Restrict the minimum password length</td><td>  
  The length can be set between 8 - 32 characters
</td></tr>
<tr><td>Validity period</td><td> Restrict the password validity period. When the password expires, it must be reset</td><td>   
The period can be set between 0 - 365 days</td></tr>
<tr><td>Duplication restrictions</td><td>Restrict the usage of old passwords</td><td>    
  Between 0 - 24 recent passwords can be restricted from being reused.</td></tr>
<tr><td>Retry restrictions</td><td>Restricts the number of times that the wrong password can be entered. If the number of times the wrong password is entered exceeds the limit set, the login will be locked for 1 hour automatically.</td><td>  
This can be set to 0-10 times/hour.</td></tr>
</table>

3. Click **Apply Changes** to set the configured password rules. You can set the password of a sub-user according to the new rules. When sub-users reset passwords, they must do so according to the password rules you have set.
> ?For the security of your account, sub-users will not be prompted by the rule when they are resetting the password. Sub-users with the cam:GetPasswordRules permission and the root account can go to **User Settings** in the console and click **Download current password rules** in **Note** to pass the current password rule to the user that needs it, as shown in the following figure:
![](https://main.qcloudimg.com/raw/9bc543bd73df838891437bed5fc5ea2c.png)

