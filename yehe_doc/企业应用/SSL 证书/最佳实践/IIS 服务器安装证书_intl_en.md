## Scenarios
This document describes how to install an SSL certificate on an IIS server.
>?
>- This document uses the certificate name `cloud.tencent.com` as an example. For your purposes, please use the name used in your certificate.
>- This document takes Windows Server 2012 R2 as an example. The detailed steps may vary slightly depending on the operating system.
>- Before you install an SSL certificate, enable port 443 on the IIS server so that HTTPS can be enabled after the certificate is installed. For more information, see [How do I enable port 443 for a server?](https://intl.cloud.tencent.com/document/product/1007/36738).
>- To upload a SSL certificate to CVMs, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).

## Directions

### Certificate installation
1. Download the certificate package for the domain name `cloud.tencent.com` from the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl) and decompress it to a local directory.
After decompression, you can get the certificate files of the relevant types, including the IIS folder and CSR file:
 - Folder name: `IIS`
 - Folder content:
    - `cloud.tencent.com.pfx`: certificate file
    - `keystorePass.txt`: password file (If a private key password is set, there is no `keystorePass.txt`.)
  - CSR file content: `cloud.tencent.com.csr` file
  >?The CSR file is uploaded by you or generated online by the system when you apply for the certificate and is provided to the CA. It is not relevant to installation.
2. Open the IIS Manager, select the computer name, and double-click **Server Certificates** to open it, as shown in the following figure.
![](https://main.qcloudimg.com/raw/dc34b3e08aeb07949782ac874be1fa45.png)
3. In the **Actions** column to the right of the **Server Certificates** window, click **Import**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/1f81c471c61418396a7d6951f323c6a1.png)
4. In the **Import Certificate** pop-up window, select the path where the certificate file is stored, enter the password, and click **OK**, as shown in the following figure.
>? 
>- If you set a private key password when applying for the certificate, enter the private key password; otherwise, enter the password in the `keystorePass.txt` file in the `IIS` folder.
>- If you forgot the private key password, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to ask Tencent Cloud engineers to delete the certificate. You need to re-apply for the domain name certificate.

![](https://main.qcloudimg.com/raw/ca0b599728d99a079a2fde7325b3a0d3.png)
5. Select the name of a site under **Sites** and click **Site Bindings** in the **Actions** column on the right, as shown in the following figure.
![](https://main.qcloudimg.com/raw/e683da3789f65ac6c7d27fc08fc6fbe3.png)
6. In the **Site Bindings** pop-up window, click **Add**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/e034799a4a854d12348ded423151f83b.png)
7. In the **Add Site Binding** window, set the site type to **https**, the port to **443**, and the host name to the domain name corresponding to the certificate, specify the corresponding SSL certificate, and click **OK**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/e5ca25bbe1b6fe1ba8abd535562f0840.png)
8. Once you made the addition, the new content will be available to view in the **Site Bindings** window, as shown in the following figure.

9. Access `https://cloud.tencent.com` .

### (Optional) Security configuration for automatic redirect from HTTP to HTTPS

>?
>- For normal redirect, edit the rule according to the following steps. If you have other needs, you can configure as needed.
>- During the redirect from HTTP to HTTPS, if your website element contains external links or uses HTTP protocol, it will cause the entire web page to not be completely based on HTTPS protocol. In this case, some browsers may issue security warnings such as "this link is insecure". You can view the reason for the error by clicking **Details** on message page.

1. Open the IIS Manager.
2. Select a site name under **Sites**, and double-click **URL Rewrite**, as shown in the following figure.
>!Download and install the [URL Rewrite module](https://www.iis.net/downloads/microsoft/url-rewrite) before proceeding to the following steps.

![](https://main.qcloudimg.com/raw/e5cb93191202ba7e285003f6a12887a1.png)
3. On the **URL Rewrite** page, click **Add Rule(s)** in the **Actions** column on the right, as shown in the following figure.
![](https://main.qcloudimg.com/raw/91c2ce545cd1a5439c545db8f39d0b07.png)
4. In the **Add Rule(s)** pop-up window, select **Blank rule** and click **OK**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/043dc754d6479b5adcd239b197bddbd5.png)
5. Go to the **Edit Inbound Rules** page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/e51778c3fee46a2d45b83191707d81fb.png)
  - **Name**: enter forced HTTPS.
  - **Matching URL**: enter `(.*)` in the **Pattern** text box.
  - **Conditions**: click <img src="https://main.qcloudimg.com/raw/b55f713d199b5077dfa66fa960b08363.png" style="margin-bottom: -5px;"></img> to expand and click **Add** to pop up the **Add Condition** window.
    - **Condition input**: `{HTTPS}`.
    - **Check if input string**: select **Matches the Pattern** by default.
    - **Pattern**: enter `^OFF$`.
  - **Action**: enter the following parameters.
	  - **Action Type**: select **Redirect**.
	  - **Redirect URL**: `https://{HTTP_HOST}/{R:1}`.
	  - **Redirect Type**: select **See Other (303)**.
6. Click **Apply** in the **Actions** column to save the settings.
7. Return to the **Sites** page and click **Restart** in the **Manage Website** column on the right. Then, the website can be accessed using `http://cloud.tencent.com`.

>!If you experience any issues with the steps outlined above, please [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).
