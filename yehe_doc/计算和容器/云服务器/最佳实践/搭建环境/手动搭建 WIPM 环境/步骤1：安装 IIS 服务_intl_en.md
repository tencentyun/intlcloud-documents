## Overview

This document describes how to add and install IIS roles on a CVM instance with Windows Server 2012 R2 or Windows Server 2008.

## Directions
### Windows Server 2012 R2 
1. Log in to Windows CVM.
2. On the desktop, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> and open **Server Manager**, as shown below:
![](https://main.qcloudimg.com/raw/cae0fe0bfebf5ad58b6e5d3451795230.png)
3. Click **Add roles and features** and enter the “Add Roles and Features Wizard” window.
4. In the pop-up window, click **Next** and enter the “Select installation type” page.
5. Select **Role-based or feature-based installation** and click **Next** twice, as shown below:
![](https://main.qcloudimg.com/raw/9eaff4f125fb23a7180cba6f38f9f879.png)
6. Check **Web Server (IIS)** on the “Select server roles” page, as shown below:
The “Add features that are required for Web Server (IIS)” dialog box will pop up.
![](https://main.qcloudimg.com/raw/d0aa5fa075275bfb2bd0c68da66616e4.png)
7. Click **Add Features** in the pop-up dialog box, as shown below:
![](https://main.qcloudimg.com/raw/817d1f22107836c77af2fd963888824f.png)
8. Click **Next**.
9. On the **Features** page, check **.NET Framework 3.5 Features** and click **Next** twice, as shown below:
![](https://main.qcloudimg.com/raw/4876efa4308912eb4bdbb6074d35fd20.png)
10. On the **Role Services** page, check **CGI** and click **Next**, as shown below:
![](https://main.qcloudimg.com/raw/c571820b1a4290d9b04abbc65cf81fd9.png)
11. Review your installation selections and click **Install**. Wait for the installation process to complete.
![](https://main.qcloudimg.com/raw/1e51aed773aad8eac28f88c401a1814e.png)
12. When the installation has completed, open a browser on CVM and visit `http://localhost/` to verify if IIS has been successfully installed.
If the following page appears, it indicates that IIS has been successfully installed.
![](https://mc.qcloudimg.com/static/img/e064cc1f765d68edf3dcfb0051d5dbfa/image.png)

### Windows Server 2008

1. Log in to Windows CVM.
2. On the desktop, click <img src="https://main.qcloudimg.com/raw/0e33f3dc1042244ab225ca32c5396296.png" style="margin: 0;"></img> and open **Server Manager**, as shown below:
![](https://main.qcloudimg.com/raw/36c9cf3d9fd246f0930a4be3516446b5.png)
3. Select **Roles** in the left sidebar, and click **Add Roles** in the right panel, as shown below:
![](https://main.qcloudimg.com/raw/b18a3c84aa193d3c64d1e25353154baf.png)
4. Click **Next** in the “Add Roles Wizard” window, as shown below:
![](https://main.qcloudimg.com/raw/4ab72f46730ecf10f2fe2768b2cc24cc.png)
5. On the “Server Roles” page, check **Web Server (IIS)** , and click **Next** twice, as shown below:
![](https://main.qcloudimg.com/raw/7a41185e562a62ca586b6b677381b3a1.png)
6. On the **Role Services** page, check **CGI** and click **Next**, as shown below:
![](https://main.qcloudimg.com/raw/7e7a96b106292e87d44807369db66842.png)
7. Review your installation selections and click **Install**. Wait for the installation process to complete.
![](https://main.qcloudimg.com/raw/877b71930f11d9d2a6fecf946f0bebfe.png)
8. When the installation has completed, open a browser on CVM and visit `http://localhost/` to verify if IIS has been successfully installed.
If the following page appears, it indicates that IIS has been successfully installed.
![](https://main.qcloudimg.com/raw/b11cd8170e7646daa3b9ca904b181cf4.png)

