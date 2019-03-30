When creating or managing sub-users, you can set requirements that sub-users need to go through two-step authentication before they can log in to Tencent Cloud or perform sensitive operations within Tencent Cloud. Since these settings directly affect account security, if you are a sub-account user or collaborator,  you can only accept these security settings made by the primary account or users who have CAM administrative privileges.

CAM sub-users are allowed to configure the following operation settings:

<table>
<tr><th>Settings</th><th>Attributes</th></tr>
<tr><td rowspan="3">Operation Protection</td><td>Mobile number verification code</td></tr>
<tr><td>MFA</td></tr>
<tr><td>Disable</td></tr>
<tr><td rowspan="3">Login Protection</td><td>Mobile number verification code</td></tr>
<tr><td>MFA</td></tr>
<tr><td>Disable</td></tr>
</table>

A CAM collaborator can set the following attributes:

<table>
<tr><th>Settings</th><th>Attributes</th></tr>
<tr><td rowspan="3">Operation Protection</td><td>Mobile number verification code</td></tr>
<tr><td>MFA</td></tr>
<tr><td>Disable</td></tr>
<tr><td rowspan="3">Login Protection</td><td>Mobile number verification code</td></tr>
<tr><td>MFA</td></tr>
<tr><td>Disable</td></tr>
</table>

In **Security Settings**, you can only see what is displayed to a primary account. To change any configuration, you can make a request to the user who owns the primary account or a sub-user with CAM management permission to configure it in **CAM** -> **User**.

## Enable MFA

1. When creating a sub-user, you can configure MFA settings after granting the sub-user the permission to log in to the console; 
2. When MFA verification is enabled, a sub-user needs to bind an MFA device before he/she can access the console.

## <span id="resetMFA">Reset MFA</span>

1. Go to the **Security Settings** in the sub-user (collaborator) detail page, and then go to MFA settings;
2. Manage and configure the MFA settings for the sub-user (collaborator) in MFA settings; 
3. If MFA verification is already enabled for the sub-user (collaborator), you can reset his/her device status. After the reset, a sub-user needs to rebind an MFA device before he/she can access the console. If the device is lost, the sub-user (collaborator) can rebind a device by resetting MFA.


## FAQ

### What should I do if I forget my MFA device?

Please make a request to the user who holds the primary account or has management permissions to reset MFA in CAM console. For more information, see [Reset MFA](#resetMFA).

