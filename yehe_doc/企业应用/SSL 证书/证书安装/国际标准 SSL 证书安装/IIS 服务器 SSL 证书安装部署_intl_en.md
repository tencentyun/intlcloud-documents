## Overview

This document describes how to install an SSL certificate in IIS.

>?
> 
> - The certificate name `cloud.tencent.com` is used as an example. The actual name in your certificate shall prevail.
> - Windows Server 2012 R2 is used as an example. Detailed steps vary slightly by OS.
> - Before you install an SSL certificate, enable port `443` on the IIS server so that HTTPS can be enabled after the certificate is installed. For more information, see [How Do I Enable Port 443 for a VM?](https://intl.cloud.tencent.com/document/product/1007/36738).
> - For detailed directions on how to upload SSL certificate files to a server, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).


## Directions

### Installing the certificate
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), and click **Download** for the certificate you need to install.

2. In the pop-up window, select **IIS** for the server type, click **Download**, and decompress the `cloud.tencent.com` certificate file package to a local directory.
After decompression, you can get the certificate file of the corresponding type, which contains the `cloud.tencent.com.iis` folder.

  - **Folder**: `cloud.tencent.com.iis`

  - **Files in the folder**:

    - `cloud.tencent.com.pfx`: certificate file

    - `keystorePass.txt`: password file (if you have set a private key password, this file will not be generated)

3. Open the IIS Manager, select the computer name, and double-click **Server Certificates**.

4. In the **Actions** column on the right of the **Server Certificates** window, click **Import**.

5. In the **Import Certificate** pop-up window, select the path where the certificate file is stored, enter the password, and click **OK** as shown below:
   

>?
>   - If you have set a private key password when applying for the certificate, enter the private key password; otherwise, enter the password in the `keystorePass.txt` file in the `cloud.tencent.com.iis` folder.
>   - If you forgot your private key password, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to have the certificate deleted and reapply for one under the domain.

  

6. Select the name of a site in **Sites** and click **Bindings** in the **Actions** column on the right.

7. In the **Site Bindings** pop-up window, click **Add**.

8. In the **Add Site Binding** window, set **Type** to **https**, **IP address** to **All Unassigned**, and **Port** to **443**, enter the domain of your current certificate in **Host name**, specify the corresponding SSL certificate, and click **OK**.

9. Then, you can see the newly added content in the **Site Bindings** window.

10. Access the website through `https://cloud.tencent.com`.

  - If the security lock icon is displayed in the browser, the certificate has been installed successfully.

  - In case of a website access exception, troubleshoot the issue by referring to the following FAQs:

    - [Website Inaccessible After an SSL Certificate is Deployed](https://intl.cloud.tencent.com/document/product/1007/39821)

    - ["Your Connection is Not Secure" is Displayed After the SSL Certificate is Installed](https://intl.cloud.tencent.com/document/product/1007/40674)

    - [Why Does the Website Prompt "Connection Is Untrusted"?](https://intl.cloud.tencent.com/document/product/1007/30184)


    - [404 Error After the SSL Certificate is Deployed on IIS](https://intl.cloud.tencent.com/document/product/1007/39820)


### (Optional) Security configuration for automatic redirect from HTTP to HTTPS

>?
> 
> - For normal redirect, edit the rule in the following steps. If you have other needs, you can set it on your own.
> - During the redirect from HTTP to HTTPS, if your website element contains external links or uses the HTTP protocol, the entire webpage is not completely based on HTTPS. In this case, some browsers may prompt for risk such as "this link is unsecure" due to those factors. You can view the error cause by clicking **Details** on the unsecure page.

1. Open the IIS Manager.

2. Select the name of a site in **Sites** and double-click to open **URL Rewrite**.
   

   >?
   > Download and install the [URL Rewrite module](https://www.iis.net/downloads/microsoft/url-rewrite) before performing this step.
   > 


3. Go to the **URL Rewrite** page and click **Add Rule(s)** in the **Actions** column on the right.

4. In the **Add Rule(s)** pop-up window, select **Blank rule** and click **OK**.

5. Go to the **Edit Inbound Rule** page.
  - Name: Enter **Forced HTTPS**.

  - Match URL: Enter `(.*)` in **Pattern**.

  - Conditions: Click ![](https://qcloudimg.tencent-cloud.cn/image/document/ef5b891415dd9085bcbe6e0c83dcb089.png) to expand and click **Add** to pop up the **Add Condition** window.

    - Condition input: `{HTTPS}`.

    - Check if input string: Select "Matches the Pattern" by default.

    - Pattern: Enter `^OFF$`.

  - Action: Enter the following parameters.

    - Action Type: Select "Redirect".

    - Redirect URL: `https://{HTTP_HOST}/{R:1}`.

    - Redirect Type: Select "See Other (303)".

6. Click **Apply** in the **Actions** column to save.

7. Return to the **Sites** page and click **Restart** in the **Manage Website** column on the right. Then, the website can be accessed through `http://cloud.tencent.com`.
   

>?
> If anything goes wrong during this process, [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).

