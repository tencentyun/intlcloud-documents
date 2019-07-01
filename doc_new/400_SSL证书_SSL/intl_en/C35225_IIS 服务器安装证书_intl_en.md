## Scenario
This document guides you through how to install an SSL certificate in IIS.
>
>- This document takes the domain name `www.domain.com` as an example.
>- This document takes Windows 10 as an example. The detailed steps vary slightly by OS version.
>
## Prerequisites
- The certificate package for the domain name `www.domain.com` in the SSL Certificate Service Console has been downloaded and decompressed to a local directory.
After decompression, you can get the IIS folder and CSR file:
 - Folder name: IIS
 - Folder content:
    - `www.domain.com.pfx`   Certificate file
    - `keystorePass.txt`   Password file
  - CSR file content: 	`www.domain.com.csr` file
- If you have already set a private key password when applying for the SSL certificate, there is no keystorePass.txt file in this folder.

>The CSR file is uploaded by you or generated online by the system when you apply for the certificate and is provided to the CA, which can be ignored during installation.

## Directions

### Certificate Installation
1. Open the IIS Manager, select the computer name, and double-click "Server Certificates" to open it.

2. In the "Actions" column to the right of the Server Certificates window, click **Import**.

3. In the "Import Certificate" window that pops up, select the path where the certificate file is stored, enter the password, and click **OK**.
> If you set a private key password when applying for the certificate, enter the private key password; otherwise, enter the password in the keystorePass.txt file in the IIS folder. For more information, see [Private Key Guidelines](https://intl.cloud.tencent.com/document/product/1007/30172).

4. Select the name of a site in "Sites" and click **Site Bindings** in the "Actions" column on the right.
5. In the "Site Bindings" window that pops up, click **Add**.
6. In the "Add Site Binding" window, set the site type to https and the port to 443, specify the corresponding SSL certificate, and click **OK**.
7. Once the addition is completed, you can see the newly added content in the "Site Bindings" window.

### Security Configuration for Automatic Redirect from HTTP to HTTPS (Optional)

Download and install the [URL Rewrite module](https://www.iis.net/downloads/microsoft/url-rewrite) before performing the following steps.
>
>- For normal redirect, edit the rule in the following steps. If you have other needs, you can set it on your own.
>- During the redirect from HTTP to HTTPS, if your website element contains external links or uses the HTTP protocol, the entire webpage is not completely based on HTTPS. In this case, some browsers may prompt for insecurity such as "this link is insecure" due to those factors. You can view the error reason by clicking "Details" on the insecure page.
>
1. Open the IIS Manager.
2. Select the name of a site in "Sites", click "URL Rewrite", and click **Open Feature** in the "Actions" column on the right.
3. Enter the "URL Rewrite" page and click **Add Rule(s)** in the "Actions" column on the right.
4. In the "Add Rule(s)" window that pops up, select **Blank rule** and click **OK**.
5. Enter the "Edit Inbound Rule" page.
  - Name: Enter "Forced HTTPS"
  - Match URL: Enter `(.*)` in "Pattern"
  - Conditions: Click <img src="https://main.qcloudimg.com/raw/b55f713d199b5077dfa66fa960b08363.png" style="margin-bottom: -5px;"></img> to expand and click "Add" to pop up the "Add Condition" window.
    - Condition input: `{HTTPS}`.
    - Check if input string: Select "Matches the Pattern" by default.
    - Pattern: Enter `^OFF$`.
  - Action: Enter the following parameters.
	  - Action type: Select "Redirect".
	  - Redirect URL: `https://{HTTP_HOST}/{R:1}`.
	  - Redirect type: Select "See Other (303)".
6. Click **Apply** in the "Actions" column to save.
7. Return to the "Sites" page and click **Restart** in the "Manage Website" column on the right. Then, the website can be accessed using `http://www.domain.com`.

> If anything goes wrong during this procedure, [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).

