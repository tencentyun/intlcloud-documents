## Issue

The following error message appears when trying to log in to a Windows CVM remotely via RDP protocol, such as using MSTSC.
The credentials that were used to connect to `XXX.XXX.XXX.XXX` did not work. Please enter new credentials.
![](https://main.qcloudimg.com/raw/47a299873e3df8f1f160c1594fc56644.png)

## Solutions
>? This document uses a Tencent Cloud CVM with the Windows Server 2012 operating system as an example. The procedure may vary slightly according to the operating system version.
> Follow the instructions below and try to connect to your Windows CVM after each step. If the issue persists, proceed to the next step.

### Step 1: modify the network access policy
1. [Log in to the Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Once you log in, click <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> to open the **Windows PowerShell** window.
3. In the **Windows PowerShell** window, enter **gpedit.msc** and press **Enter**. The **Local Group Policy Editor** window appears.
4. In the left sidebar, expand the following directories in order: **Computer Configuration** > **Windows Settings** > **Security Settings** > **Local Policies** > **Security Options**.
5. Locate and open **Network access: Sharing and security model for local accounts** under **Security Options**, as shown below:
![](https://main.qcloudimg.com/raw/4ffb48c55d2f4aeedee127d97a4378ee.png)
6. Select **Classic - local users authenticate as themselves** and click **OK**, as shown below:
![](https://main.qcloudimg.com/raw/0f460bef7a7e35e1295149bb1f5f0d03.png)
7. Check whether you can connect to your Windows CVM now.
 - If yes, the problem has been solved.
 - If no, proceed to “Step 2: modify credentials delegation”.

### Step 2: modify credentials delegation
1. In the left sidebar of **Local Group Policy Editor**, expand the following directories in order: **Computer Configuration** > **Administrative Templates** > **System** > **Credentials Delegation**.
2. Locate and open **Allow delegating saved credentials with NTLM-only server authentication** under **Credentials Delegation**, as shown below:
![](https://main.qcloudimg.com/raw/7643737fdfa2be299c21f6bc82b0165b.png)
3. In the pop-up window, select **Enabled**. Click **Show…** under **Options**, enter `TERMSRV/*` for **Show Contents** and click **OK**, as shown below:
![](https://main.qcloudimg.com/raw/6a9af6aa4c3c3b3c4d1b9eba53d202b1.png)
4. Click **OK**.
5. On the desktop, click <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> to open the **Windows PowerShell** window.
6. In the **Windows PowerShell** window, enter **gpupdate /force** and press **Enter** to update the group policy, as shown below:
![](https://main.qcloudimg.com/raw/98d0b757e65e3617145c05513ba652dc.png)
7. Check whether you can connect to your Windows CVM now.
 - If yes, the problem has been solved.
 - If no, proceed to “Step 3: configure local credentials”.

### Step 3: configure local credentials
1. On the desktop, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> and navigate to **Control Panel** > **Users Accounts** > **Credential Manager**. Click **Windows Credentials** to display Windows credentials, as shown below:
![](https://main.qcloudimg.com/raw/2726e3d109fdaadd1d90a1f3e692601a.png)
2. Check whether the credential you used to log in to your Windows CVM exists.
 - If no, proceed to the next step to add Windows credentials.
 - If yes, proceed to "Step 4: turn off password protected sharing".
3. Click **Add a Windows credential** to go to the **Add a Windows Credential** window, as shown below:
![](https://main.qcloudimg.com/raw/87077862379ea7d9e86d5fdc7e0af1da.png)
4. Enter the IP address, username, and password of the CVM instance and click **OK**.
>?
> - The IP address refers to the public IP address of your CVM instance. For more information, see [Getting Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/17940).
> - The default username for a Windows instance is `Administrator` and the password is set when you create the instance. If you’ve forgotten your password, you can [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
>
5. Check whether you can connect to your Windows CVM now.
 - If yes, the problem has been solved.
 - If no, proceed to “Step 4: turn off password protected sharing”.

### Step 4: turn off password protected sharing
1. On the desktop, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> and navigate to **Control Panel** > **Network and Sharing Center** > **Advanced sharing settings**, as shown below:
![](https://main.qcloudimg.com/raw/d1cc8fd023642654091d1b152bb67ef1.png)
2. Expand the **All Networks** tab, select **Turn off password protected sharing** under **Password protected sharing**, and click **Save changes**.
3. Check whether you can connect to your Windows CVM now.
 - If yes, the problem has been solved.
 - If no, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) for assistance.


