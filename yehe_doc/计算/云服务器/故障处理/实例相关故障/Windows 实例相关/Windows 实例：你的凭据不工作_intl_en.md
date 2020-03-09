## Issue Description

The following error message appears when trying to log in to a Windows CVM remotely via RDP protocol, such as using MSTSC.
Your credentials did not work. The credentials that were used to connect to `XXX.XXX.XXX.XXX` did not work. Please enter new credentials.
![](https://main.qcloudimg.com/raw/47a299873e3df8f1f160c1594fc56644.png)

## Instructions
> These instructions use Windows Server 2012 as an example. Different versions of Windows might have slightly different instructions.
> Follow these instructions carefully and try to connect to your Windows CVM after each step. If one did not work, proceed to the next.
>

### Step 1: Modify Network Access Policy
1. [Log in to the Windows instance using VNC](https://ihttps://intl.cloud.tencent.com/document/product/213/5435#login-via-vnc).
2. Once logged in, click <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> to open a Windows PowerShell window.
3. In the Windows PowerShell window, enter **gpedit.msc** and press **Enter** to open the **Local Group Policy Editor**.
4. Use the navigation pane on the left to navigate to **Computer Configuration** > **Windows Settings** > **Computer Settings** > **Security Options**.
5. Locate and open **Network access: Sharing and security model for local accounts** under **Security Options**, as shown in the following image:
![](https://main.qcloudimg.com/raw/4ffb48c55d2f4aeedee127d97a4378ee.png)
6. Select **Classic - local users authenticate as themselves** and click **OK**, as shown in the following image:
![](https://main.qcloudimg.com/raw/0f460bef7a7e35e1295149bb1f5f0d03.png)
7. Check whether you can connect to your Windows CVM now.
 - Yes. Problem solved.
 - No. Proceed to Step 2 Modify Credentials Delegation

### Step 2: Modify Credentials Delegation
1. Open Local Group Policy Editor. In the left navigation pane, navigate to **Computer Configuration** > **Administrative Templates** > **System** > **Credentials Delegation**.
2. Locate and open **Allow delegating saved credentials with NTLM-only server authentication** under **Credentials Delegation**, as shown in the following image:
![](https://main.qcloudimg.com/raw/7643737fdfa2be299c21f6bc82b0165b.png)
3. Select **Enable**. Click **Show…** under **Options** and enter `TERMSRV/*`. Click **OK**, as shown in the following image:
![](https://main.qcloudimg.com/raw/6a9af6aa4c3c3b3c4d1b9eba53d202b1.png)
4. Click **OK**.
5. Click <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> to open a Windows PowerShell window.
6. In the Windows Powershell window, enter **gpupdate /force** and press **Enter** to update group policy, as shown in the following image:
![](https://main.qcloudimg.com/raw/98d0b757e65e3617145c05513ba652dc.png)
7. Check whether you can connect to your Windows CVM now.
 - Yes. Problem solved.
 - No. Proceed to Step 3 Configure Local Credentials

### Step 3: Configure Local Credentials
1. Click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> and navigate to **Control panel** > **Users and accounts**. Select **Manage Windows credentials** under **Credential manager**. The Windows credential window then appears, as shown in the following image:
![](https://main.qcloudimg.com/raw/2726e3d109fdaadd1d90a1f3e692601a.png)
2. Check to see if there is an entry for the credentials you used to log in to Windows CVM.
 - No. Follow the next step to add it.
 - Yes. Proceed to Step 4 Turn Off Password Protected Sharing
3. Click **Add Windows credentials**. The **Add Windows credentials** window then appears, as shown in the following image:
![](https://main.qcloudimg.com/raw/87077862379ea7d9e86d5fdc7e0af1da.png)
4. Input the IP of the CVM, the username you use to log in to the Windows CVM and the corresponding password. Click **OK**.
5. Check whether you can connect to your Windows CVM now.
 - Yes. Problem solved.
 - No. Proceed to Step 4 Turn Off Password Protected Sharing

### Step 4: Turn off password protected sharing
1. From Desktop, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> and navigate to **Control panel** > **Network and sharing center** > **Change advanced sharing settings**. The **Change advanced sharing settings** page then appears, as shown in the following image:
![](https://main.qcloudimg.com/raw/d1cc8fd023642654091d1b152bb67ef1.png)
2. Expand **All networks** and select **Turn off password protected sharing** under **Password protected sharing**. Click **Save changes**.
3. Check whether you can connect to your Windows CVM now.
 - Yes. Problem solved.
 - No. Please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1).

