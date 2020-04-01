## Scenario

Microsoft's operating system uses a security identifier (SID) to identify computers and users. CVM instances created with the same image will have the same SID and might experience domain log-in issues. If you need to build a Windows domain environment, you will need to modify the SID.
This document takes the CVM with Windows Server 2012 operating system as an example to describe how to modify the SID using sysprep and sidchg tools of the system.

## Notes

- This is only applicable to Windows Server 2008 R2, Windows Server 2012, and Windows Server 2016.
- To modify the SID in batch, you can create a custom image (select "run sysprep to create the image").
- Modify the SID may cause data loss or system damage. We recommend you create a system disk snapshot or image in advance.

## Directions

### Using sysprep to modify the SID

> 
> - After using sysprep to modify the SID, you need to manually reset some system parameters, including IP configuration information.
> - When you use sysprep to modify the SID, C:\Users\ Administrator will be reset and some data on the system disk will be erased. Please back up data.
> 
1. [Log in to the Linux CVM via VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. In the operating system interface, right-click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > **Run**, enter **cmd**, and press **Enter** to open a Admin command line.
3. <span id="step_03">In the admin command line, execute the following command to save the current network configuration.</span>
```
ipconfig /all
```
4. In the admin command line, execute the following command to open the sysprep tool.
```
C:\Windows\System32\Sysprep\sysprep.exe
```
5. In the “System Preparation Tool 3.14” window that pops up, make the following configuration, as shown below:
![](https://main.qcloudimg.com/raw/d94e4a96b8ca82052d91e9bb9d8fecbf.png)
 - Set **System Cleanup Action** to **Enter System Out-of-Box Experience (OOBE)** and check **General**.
 - Set **Shutdown Options** to **Reboot**.
6. Click **OK**, and the system will restart automatically.
7. After the startup is complete, follow the wizard to complete the configuration (select language, reset password, etc.).
8. In the operating system interface, right-click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > **Run**, enter **cmd**, and press **Enter** to open a Admin command line.
9. Execute the following command to verify whether the SID has been modified.
```
whoami /user
```
If a message similar to the following is returned, the SID has been modified.
![](https://main.qcloudimg.com/raw/34efb1f4128c753e6c0546f3e8d58678.png)
10. Reset ENI information (such as IP address, gateway address, DNS, etc.) based on the network configuration information saved in [Step 3](# step_03).


### Using sidchg to modify the SID

1. Log in to the CVM.
2. Access and download the sidchg tool through IE browser.
The download address of sidchg tool: `http://www.stratesave.com/html/sidchg.html`
3. Using the admin command line to execute the following command and open the sidchg tool, as shown below:
For example, the sidchg tool is saved on C: drive and its name is sidchg64-2.0p.exe.
![](https://main.qcloudimg.com/raw/284926ae1eae88228fb009f247b82068.png)
`/R` means automatic restart after modification, and` /S` means shutdown after modification. For details, please see [SIDCHG Official Instructions] (http://www.stratesave.com/html/sidchg.html).
4. Enter license key or trial key as prompted by the page, and press **Enter**.
5. Enter **Y** as prompted by the page, and press **Enter**, as shown below:
![](https://main.qcloudimg.com/raw/43c19634475517b183402d15fa32e962.png)
6 In the prompt box for modifying the SID, click [OK] to reset the SID, as shown below:
The system will be restarted during the reset.
![](https://main.qcloudimg.com/raw/b59ec21417cc0de1fd7d851fcd8a2a3b.png)
7. After the startup is completed, right-click <img src = "https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style = "margin: 0;">> **Run**, enter **cmd**, and press **Enter** to open the admin command line.
8. Execute the following command to verify whether the SID has been modified.
```
whoami /user
```
If a message similar to the following is returned, the SID has been modified.
![](https://main.qcloudimg.com/raw/34efb1f4128c753e6c0546f3e8d58678.png)
