## Overview
Microsoft Windows Server's Active Directory Federation Services (ADFS) is a new technology for authenticating users of multiple web applications during one session. Tencent Cloud supports identity federation with Security Assertion Markup Language 2.0 (SAML 2.0). SAML 2.0 is an open standard used by many identity providers (IdPs). SAML 2.0-based federation can be used to integrate ADFS with Tencent Cloud. Then, federated single sign-on (SSO) can be implemented by using an ADFS account, and admins can authorize users that have their federated identity authenticated to log in to the Tencent Cloud console for resource management, eliminating the need to create a CAM sub-user for each employee in the organization.
## Prerequisites
- You have a Windows Server CVM instance. For more information on how to purchase one, see [Billing Overview](https://intl.cloud.tencent.com/document/product/213/2179).
- You have entered the **Server Management** > **Dashboard** page and found the **Add Roles and Features Wizard** in your computer (see [Install or Uninstall Roles, Role Services, or Features](https://docs.microsoft.com/zh-cn/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-the-add-roles-and-features-wizard)).
- You have a verified domain name.
## Directions
### Installing the AD domain services and DNS services
1. On the dashboard management page, click **Add Roles and Features**, keep the default settings for options on the page, and click **Next** repeatedly to enter the **Add Roles and Features Wizard** page.
2. On the **Add Roles and Features Wizard** page, keep the default settings for options on the page, and click **Next** repeatedly. <span id="step1">Then, select **Active Directory Domain Services** and **DNS Server** on the **Server Roles** page.
3. Keep the default settings for options on the page, click **Next** repeatedly, and click **Install**. On the page indicating the successful installation, click ![](https://main.qcloudimg.com/raw/32f3dcf3b4c58c0acb3485f2dab0f9a7.png) in the top-right corner.
4. Click **Promote this server to a domain controller** to go to the deployment configuration page. 
5. Click **Next**. After the installation is completed, enter the password. Keep the default settings for options on the page and click **Next** repeatedly.
6. Click **Install** and restart the server after the installation is completed.
7. At this point, the AD domain services and DNS service have been installed, and the server has been promoted to a domain controller.

### Installing the web server
1. Refer to [step 2](#step1) in **Installing the AD domain services and DNS services** to enter the **Server Roles** page. Select **Web Server**.
2. Keep the default settings for options on the page and click **Next** > **Install** repeatedly to install the web server.

### Applying for a certificate
If you already have an SSL certificate, you can directly [install ADFS](#step0).

1. Click the **Windows** icon in the bottom-left corner, enter the "mmc" command in the search box, and press **Enter** to run it and access the **Console 1-[Console Root]** page.

2. On the **Console 1-[Console Root]** page, click **File**>**Add/Remove Snap-in**, select a certificate in the pop-up window, and click **Add**>* *Finish**.

3. Click **Certificates - Current User**. <span id="step3">In the expanded directory, right-click **Personal**, click **All Tasks** > **Advanced Operations** > **Create Custom Request**.

4. Keep the default settings for options on the page, click **Next** repeatedly to enter the **Certificate Enrollment** page, and click **Proceed without enrollment policy**.

5. On the **Custom request** page, select the following information:
 - Template: (No template) Legacy key
 - Request format: PKCS#10
6. Click **Details** > **Properties**. On the **General** tab, enter a friendly name and description.
7. On the **Subject** tab, enter **Value** (`*.example.com` in this example) and click **Add**.

8. On the **Private Key** tab, select **Microsoft RSA SChanel Cyptograhic Provider (Encryption)** and **Make private key exportable**.

9. Click **OK** > **Next**, select the directory for saving the certificate, and click **Finish**.

### Installing an ADC (AD certificate server)
1. Refer to [step 2](#step1) in **Installing the AD domain services and DNS services** to select **Active Directory Certificate Services**.
2. Keep the default settings and click **Next** repeatedly. On the **Role Services** page, select **Certification Authority** and **Certification Authority Web Enrollment**.
3. Click **Install**. On the page indicating the successful installation, click ![](https://main.qcloudimg.com/raw/32f3dcf3b4c58c0acb3485f2dab0f9a7.png) in the top-right corner and click **Configure Active Directory Certificate Services on the destination server**.
4. Keep the default settings for options on the page and click **Next** repeatedly. On the **Role Services** page, select **Certification Authority** and **Certification Authority Web Enrollment**.
5 Keep the default settings for options on the page, click **Next** repeatedly, and click **Configure** to install the ADC.

### Generating an SSL certificate
1. Visit http://localhost/certsrv and click **Request a certificate**.
2. On the **Request a Certificate** page, click **advanced certificate request**.

3. On the **Advanced Certificate Request** page, click **Submit a certificate request by using a base-64-encoded CMC or PKCS#10 file, or submit a renewal request by using a base-64-encoded PKCS#7 file**.
4. Copy and paste the certificate file content saved in **Applying for a certificate** to the input box, select **Web Server** for **Certificate Template**, and click **Submit**.
5. After the application succeeds, click **Download certificate** to download the certificate in both formats.<span id="step5">

6. Refer to [step 3](#step3) in **Applying for a certificate**, right-click **Personal**, and click **All Tasks** > **Import**.
7. Select the certificate file saved in [step 5](#step5), keep the default settings for options on the page, click **Next** repeatedly, and click **Finish**.
8. Refer to [step 3](#step3) in **Applying for a certificate**, right-click **Personal**, and click **All Tasks** > **Export**.
9. On the **Certificate Export Wizard** page, select **Yes, export the private key** and **Group or user names (recommended)**, and click **Next** to export the saved file.<span id="step9">


### Installing the ADFS
1. <span id="step0">Refer to [step 2](#step1) in **Installing the AD domain services and DNS services** to enter the **Server Roles** page. Select **Active Directory Federation Services**.
2. Keep the default settings for options on the page, click **Next** repeatedly, and click **Finish**. On the result page, click **Configure the federation service on this server.** 
![](https://main.qcloudimg.com/raw/a68753820c34fef24ab06c1ced2ac729.png
3. Keep the default settings for options on the page, click **Next** repeatedly to enter the **Specify Service Properties** page, and enter and import the following information:
SSL Certificate: Import the certificate file saved in [step 9](#step9) in **Generating an SSL certificate**.
Federation Service Name: Enter the name of the destination server (same as the name in the top-right corner) or an sts. or .adfs domain name.
Federation Service Display Name: Enter the name displayed during login.
4. On the **Specify Service Account** page, enter an account name and password<span id="step4">, keep the default settings for other options, and click **Next** repeatedly until the ADFS is installed successfully.

5. Visit the following link to download the XML file.
```
https://federation service name/federationmetadata/2007-06/federationmetadata.xml
```

6. Run `Set-AdfsProperties –EnableIdpInitiatedSignonPage $True` in PowerShell:
Access the following entry for login:

```
https://federation service name/adfs/ls/idpinitiatedSignOn.htm
```
7. Enter the account name and password configured in [step 4](#step4) to log in. 
>?If `400 Bad Request` is returned in the browser, perform the following operations in PowerShell:
Get the user starting the ADFS service, open PowerShell, and run the script `setspn -s http/URL of ADFS server domain controller\user`. For example, if the full name of the ADFS server is `172_21_0_13.weezer.club`, the domain controller is `WEEZER`, and the user is `Administrator`, you need to run the script `setspn -s http/172_21_0_13.weezer.club WEEZER\Administrator`.

### Creating an IdP in Tencent Cloud
>?You can perform this step to configure the trust between ADFS and Tencent Cloud.

Create a SAML IdP in Tencent Cloud and save the IdP name, which can contain only letters.<span id="step6"></span> For more information, see [Creating IdP](https://intl.cloud.tencent.com/document/product/598/30391).


### Creating a role for an IdP
>?You can perform this step to grant the ADFS user the Tencent Cloud SSO access permission.
>
Create a role for your IdP and save the role name, which can contain only letters.<span id="step7"></span> For more information, see [Creating Role](https://intl.cloud.tencent.com/document/product/598/19381).
Here, select the IdP created in [Creating an IdP in Tencent Cloud](#step6).

### Configuring a user and user group
1. On the **Dashboard** page in the Server Manager, click **Tools** in the top-right corner and select **Active Directory Users and Computers**.
2. On the **Active Directory Users and Computers** page, click **Action** > **New** > **Group**.
3. On the **New Object - Group** page, enter the group name.
>?
>-  Replace <your root account ID> with your Tencent Cloud account ID, which can be viewed in **Account Center** in the [console](https://console.cloud.tencent.com/developer).
> - Replace <Tencent Cloud role name> with the [role name](#step7) created for the IdP in Tencent Cloud.
4. On the **Active Directory Users and Computers** page, click **Action** > **New** > **User**.
5. Create an employee, enter the basic employee information, set a username that can contain only letters, and save the username.
6. On the **Active Directory Users and Computers** page, find the new user in the **Users** directory and add the user to the user group.


### Configuring a mapping rule
1. On the **AD FS** page in the Server Manager, click **Tools** in the top-right corner.
2. Select **AD FS Management** and click **Add Relying Party Trust**.
3. On the **Add Relying Party Trust Wizard** page, select **Claims aware** and click **Start**.

4. Visit the following link to download the XML file provided by Tencent Cloud IdP.

```
https://cloud.tencent.com/saml.xml
```
5. Import the file of the Tencent Cloud IdP.
6. Keep the default settings for options on the page, click **Next** repeatedly, and click **Finish**.
7. Click **Relying Party Trusts** > **Edit Claim Issuance Policy** > **Add Rule**.
8. On the **Add Transform Claim Rule Wizard** page, click **Choose Rule Type** > **Transform an Incoming Claim** > **Next**.
9. On the **Configure Rule** page, enter the rule information and click **OK**.
>? 
> - Claim rule name: Enter `NameID`.
> - Incoming claim type: Select **Windows account name**.
> - Outgoing claim type: Select **Name ID**.
> - Outgoing name ID format: Select **Persistent Identifier**.
> - Select **Pass through all claim values**.
10. On the **Add Transform Claim Rule Wizard** page, click **Choose Rule Type** > **Send Claims Using a Custom Rule** > **Next**.

11. On the **Configure Rule** page, enter the rule information and click **OK**.
>? 
> - Claim rule name: Enter `Get AD Groups`.
> - Custom rule: Add the following information:
>```
c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]
 => add(store = "Active Directory", types = ("http://temp/variable"), query = ";tokenGroups;{0}", param = c.Value);


12. On the **Add Transform Claim Rule Wizard** page, click **Choose Rule Type** > **Send Claims Using a Custom Rule** > **Next**.

13. On the **Configure Rule** page, enter the rule information and click **OK**.
>? 
> - Claim rule name: Enter `Role`.
> - Custom rule: Add the following information:
>```
c:[Type == "http://temp/variable", Value =~ "(?i)^Tencent-([\d]+)"]
 => issue(Type = "https://cloud.tencent.com/SAML/Attributes/Role", Value = RegExReplace(c.Value, "Tencent-([\d]+)-(.+)", "qcs::cam::uin/$1:roleName/$2,qcs::cam::uin/$1:saml-provider/IdP name")); 

Here, replace `IdP name` with the name of the IdP created in [Creating an IdP in Tencent Cloud](#step6).

14. On the **Add Transform Claim Rule Wizard** page, click **Choose Rule Type** > **Send Claims Using a Custom Rule** > **Next**.
15. On the **Configure Rule** page, enter the rule information and click **OK** as shown below:
> - Claim rule name: Enter `RoleSessionName`.
> - Custom rule: Add the following information:
>```
c:[Type == "http://temp/variable", Value =~ "(?i)^Tencent-([\d]+)"]
 => issue(Type = "https://cloud.tencent.com/SAML/Attributes/RoleSessionName", Value = RegExReplace(c.Value, "Tencent-([\d]+)-(.+)", "test"));
```

>? 
> - To enable SSO to Tencent Cloud in another browser other than the ADFS server, you can configure a subdomain (your federation service name) at your IdP for access and login.

