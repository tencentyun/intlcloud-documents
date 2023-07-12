
You need to use the Microsoft Windows iSCSI Initiator to connect to the volume as a local device on the Windows client.

>Connecting multiple servers to the same iSCSI Target is not supported due to iSCSI protocol restrictions.

### Finding and starting the iSCSI initiator
Enter `iscsicpl.exe` (iSCSI Initiator) in the search box on the Windows Start menu and select the program. If prompted, click **Yes** to run the iSCSI Initiator.
![](https://mc.qcloudimg.com/static/img/ae9a867a22344c46d54d06f8684942c2/image.png)


### Setting up the iSCSI portal
In the iSCSI Initiator pop-up dialog box, select the **Discovery** tab and click **Discover Portal**.

Enter the IP address of the target in the pop-up window, and then click **OK** to add the target portal.
>The gateway IP address is the address of the server where the gateway is installed. It can also be viewed in gateway details. If you are using a CVM instance as your gateway, you can get the server's IP address in the CVM Console.


### Connecting to iSCSI Target
Select the **Target** tab where the target portal added in the previous step still remains inactive. Click **Connect** after selecting the target.


Confirm the target name in the pop-up dialog box, check "Add this connection to the list of Favorite Targets." and click **OK**.


After confirming that the state is "Connected", click **OK** and exit.

### Subsequent steps
- Initialize the volume
  Enter "diskmgmt.msc" in the search box on the Windows Start menu to open "Create and format hard disk partitions".
  
  The Initialize Disk window pops up. Select MBR (Master Boot Record) as the partition style and click **OK**.
  
- Create a simple volume
  On the Disk Management page, select the disk found just now, right click in the area below and click "New Simple Volume...". Then, partition and format the disk as prompted.
  
- Write data to the disk added in the steps above, create a volume snapshot in the CSG Console and restore the snapshot to a volume.

### Optimization
To ensure the stability of data reads/writes with CSG, you are strongly recommended to follow the steps below to optimize your configuration.

1. Modify the maximum time for request queuing
	a.	 Open Registry Editor (Regedit.exe).
	b.	 Navigate to the globally unique identifier (GUID) key in the device category which contains the iSCSI controller settings as shown below.
```
HKEY_Local_Machine\SYSTEM\CurrentControlSet\Control\Class\{4D36E97B-E325-11CE-BFC1-08002BE10318}
```

	>Make sure that you are in the CurrentControlSet subkey but not other control sets such as ControlSet001 or ControlSet002.
	
	c. Find the subkey of the Microsoft iSCSI Initiator which is shown below as <instance number>. This item is represented by a four-digit number such as 0000.
	```
	HKEY_Local_Machine\SYSTEM\CurrentControlSet\Control\Class\{4D36E97B-E325-11CE-BFC1-08002BE10318}\<Instance Number>
	```		
Depending on what is installed on your computer, Microsoft iSCSI Initiator may not be subkey 0000. You can ensure that the correct subkey is selected by verifying that the string DriverDesc has the Microsoft iSCSI Initiator value as shown in the following example.

​	d. To display the iSCSI settings, select the Parameters subkey.
​	e. Open the menu for the MaxRequestHoldTime DWORD (32-bit) value (right click), select "Modify" and change the value to 600. The following example shows a MaxRequestHoldTime DWORD value of 600. This value indicates a hold time of 600 seconds.
![](https://mc.qcloudimg.com/static/img/d72cb08e6a9e92f61254f79a6d1b77f6/iscsi-windows-registry-20.png)
​		

2. Modify the disk timeout configuration
	a.	 If you have not opened Registry Editor (Regedit.exe) yet, open it.
	b. Navigate to the Disk subkey in the Services subkey of CurrentControlSet as shown below.
	```
	HKEY_Local_Machine\SYSTEM\CurrentControlSet\Services\Disk
	```
	c. Open the context (right click) menu of the TimeOutValue DWORD (32-bit) value, select Modify and change the value to 600. The following example shows a TimeOutValue DWORD value of 600. This value indicates a timeout period of 600 seconds.
![](https://mc.qcloudimg.com/static/img/e5c42772f04772539a99825c3d4fe72b/iscsi-windows-registry-30.png)
3. Restart the system for the configuration modified above to take effect.
	Before restarting, you must ensure that the results of all writes to the volume are refreshed. Please take any mapped storage volume disks offline before restarting.


