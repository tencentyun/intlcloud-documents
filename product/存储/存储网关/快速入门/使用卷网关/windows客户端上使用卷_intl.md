## Connecting to a Volume Using a Microsoft Windows Client
You need to use the Microsoft Windows iSCSI Initiator to connect to the volume as a local device on the Windows client.

*Note: Connecting multiple servers to the same iSCSI Target is not supported due to iSCSI protocol restrictions.*

### Finding and Starting the iSCSI Initiator
Enter iscsicpl.exe (iSCSI Initiator) in the search box on the Windows Start menu and select the program. If prompted, click Yes to run the iSCSI Initiator.
![](https://mc.qcloudimg.com/static/img/ae9a867a22344c46d54d06f8684942c2/image.png)


### Setting up the iSCSI Portal
In the iSCSI Initiator pop-up dialog box, select the **Discovery** tab and click the **Discover Portal** button.

![](https://mc.qcloudimg.com/static/img/92e517e7d4d977370504c31ab7ca969a/image.png)

Enter the IP address of the target in the pop-up, and then click **OK** to add the target portal.
*Note: The gateway IP address is the address of the server where the gateway is installed. It can also be viewed in gateway details. If you are using CVM as your gateway, you can get the server's IP address in the CVM Console.*
![](https://mc.qcloudimg.com/static/img/9bb7de1aea7642b67d4a0b98bdf40213/image.png)


### Connecting to iSCSI Target
Select the **Target** tab where the target portal added in the previous step still remains inactive. Click the **Connect** button after selecting the target.
![](https://mc.qcloudimg.com/static/img/659962a9f392eeee1bd70433bf7b566c/iscsi+taget.png)

Confirm the target name in the pop-up dialog box, check "Add this connection to the list of Favorite Targets." and click **OK**.
![](https://mc.qcloudimg.com/static/img/700ce70c906dc28dd7a39a0ec4c93383/image.png)

After confirming that the state is "Connected", click the **OK** button and exit.
![](https://mc.qcloudimg.com/static/img/ee71b2ba01d5227473296094c02ef0ec/image.png)



### Subsequent Steps
- Initialize the volume
  Enter "diskmgmt.msc" in the search box on the Windows Start menu to open "Create and format hard disk partitions".
  ![](https://mc.qcloudimg.com/static/img/9d8e1b3870599628ed94f5e0c072e849/image.png)
  The Initialize Disk window pops up. Select MBR (Master Boot Record) as the partition style and click the **OK** button.
  ![](https://mc.qcloudimg.com/static/img/5a0cbaffe94b8b980f2e6ab567a33c59/image.png)
  
- Create a simple volume
  In the Disk Management interface, select the disk found just now, right click in the area below and click "New Simple Volume...". Then, partition and format the disk as prompted.
  ![](https://mc.qcloudimg.com/static/img/5ca6d71637809651ba9c00ba5dc1d2f1/image.png)
	
- Write data to the disk added in the steps above, create a volume snapshot in the CSG Console and restore the snapshot to a volume.

### Optimization
**To ensure the stability of data reads/writes with CSG, it is strongly recommended that you follow the steps below to optimize your configuration.**

1. Modify the maximum time for request queuing
	a.	 Open Registry Editor (Regedit.exe).
	b.	 Navigate to the globally unique identifier (GUID) key in the device category which contains the iSCSI controller settings as shown below. 
		```
		HKEY_Local_Machine\SYSTEM\CurrentControlSet\Control\Class\{4D36E97B-E325-11CE-BFC1-08002BE10318}
		```
		**Note: Make sure you are in the CurrentControlSet subkey but not other control sets such as ControlSet001 or ControlSet002.**
	
	c. Find the subkey of the Microsoft iSCSI Initiator which is shown below as <instance number>. This item is represented by a four-digit number such as 0000.
	
		```
		HKEY_Local_Machine\SYSTEM\CurrentControlSet\Control\Class\{4D36E97B-E325-11CE-BFC1-08002BE10318}\<Instance Number>
	```
		Depending on what is installed on your computer, Microsoft iSCSI Initiator may not be subkey 0000. You can ensure that the correct subkey is selected by verifying that the string DriverDesc has the Microsoft iSCSI Initiator value as shown in the following example.
		![](https://mc.qcloudimg.com/static/img/344ceb4fedcb91867d2090a03d5466ed/iscsi-windows-registry-10.png) 
	d. To display the iSCSI settings, select the Parameters subkey.
	e. Open the menu for the MaxRequestHoldTime DWORD (32-bit) value (right click), select "Modify" and change the value to 600. The following example shows a MaxRequestHoldTime DWORD value of 600.  		*Note: This value indicates a hold time of 600 seconds.*
		![](https://mc.qcloudimg.com/static/img/d72cb08e6a9e92f61254f79a6d1b77f6/iscsi-windows-registry-20.png)
		

2. Modify the disk timeout configuration
	a.	 If you have not opened Registry Editor (Regedit.exe) yet, open it.
	b.	 Navigate to the Disk subkey in the Services subkey of CurrentControlSet as shown below. 				
		```
		HKEY_Local_Machine\SYSTEM\CurrentControlSet\Services\Disk
		```
	c. Open the context (right click) menu of the TimeOutValue DWORD (32-bit) value, select Modify and change the value to 600. The following example shows a TimeOutValue DWORD value of 600.
		*Note: This value indicates a timeout of 600 seconds.*
		![](https://mc.qcloudimg.com/static/img/e5c42772f04772539a99825c3d4fe72b/iscsi-windows-registry-30.png)

3. Restart the system for the configuration modified above to take effect.
	Before restarting, you must ensure that the results of all writes to the volume are refreshed. Please take any mapped storage volume disks offline before restarting.


