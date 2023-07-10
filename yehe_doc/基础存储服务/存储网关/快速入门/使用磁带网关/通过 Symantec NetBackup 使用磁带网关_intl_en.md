Once a tape gateway and tape are created, you can back up data to virtual tapes, archive tapes, and manage virtual tape library (VTL) devices with Symantec NetBackup. The following describes how to configure storage, write data to a tape, archive a tape, and restore data in NetBackup 8 as an example.

For more information on how to use NetBackup, please see the [help documentation](https://www.veritas.com/content/support/zh_CN/search-results.html?q=*&fq=((document_type%3A%22document%22)%20AND%20(product_name%3A%22NetBackup%22)%20AND%20(locale%3A%22zh_CN%22))%20AND%20version%3A(%228.1.2%22)&docRepo=true&requestedRecords=20) on Veritas website.

## Connecting to VTL Device

### Connecting to VTL device through Windows client
1. Enter iscsicpl.exe (iSCSI Initiator) in the search box on the Windows Start menu and select the program. If prompted, click **Yes** to run the iSCSI Initiator.
2. In the iSCSI Initiator pop-up dialog box, select the **Discovery** tab and click **Discover Portal**. 
3. Enter the IP address of the target in the pop-up window and then click **OK** to add the target portal.
  >The gateway IP address is the address of the server where the gateway is installed. It can also be viewed in gateway details. If you are using a CVM instance as your gateway, you can get the server's IP address in the CVM Console.
4. Select the **Target** tab and click **Refresh**. All the ten tape drives and media converters are then displayed in the **Discovered targets** box. The state of the target is "inactive". 
5. Select the first device and click **Connect**. Then, repeat the steps to connect all the devices listed one by one. 
6. In the Windows client, the driver provider for the tape drive must be Microsoft. Follow the procedure below to verify the driver provider and update the driver and provider as necessary.
	1. In the Windows client, open "Device Manager".
	2. Expand "Tape Drive", select a driver, right-click it, and click **Properties** in the expanded menu. 
	3. In the "Device Properties" dialog, select "Driver" and confirm that "Driver Provider" is Microsoft. 
	4. If the "Driver Provider" is not Microsoft, set the following values: 
	 1. Click **Update Driver**. 
	 2. In the "Update Driver Software" dialog, click "Browse my computer for driver software." 
	 3. In the "Browse my computer for driver software" dialog, click "Let me pick from a list of device drivers on my computer". 
	 4. Select "LTO Tape drive" and click **Next**. After the update is completed, close the window. 
	5. Close the "Update Driver Software" window and verify that the "Driver Provider" value has been set to Microsoft. 
	6. Repeat the steps above to update all tape drives.


### Connecting to VTL device through Linux client
1. Install the iscsi-initiator-utils RPM package by running the following command:
	```shell
	sudo yum install iscsi-initiator-utils
	```
	
2. Make sure that the iSCSI daemon is running. For RHEL 5 or RHEL 6, run the following command:
	```
	## Running the Following Command for RHEL 5 or RHEL 6
	sudo /etc/init.d/iscsi status
	
	## Running the Following Command for RHEL 7
	sudo service iscsid status
	```
	
3. Discover the VTL device by running the following discovery command.
	```
	sudo /sbin/iscsiadm --mode discovery --type sendtargets --portal [gateway IP]:3260
	```
	
	The output of the command is similar to the sample below:
	Tape gateway: iqn.2003-07.com.qcloud:csg-022ef55-tapedrive-01
	
4. Run the following command to connect to the target. Note: you need to specify the correct "[media converter target name/drive target name]" and "[gateway IP]" in the connection command. 
	```
	sudo /sbin/iscsiadm --mode node --targetname [media converter target name/drive target name] --portal [gateway IP]:3260,1 --login
	
	For example:
	sudo /sbin/iscsiadm --mode node --targetname iqn.2003-07.com.qcloud:csg-022ef55-tapedrive-01 --portal 10.10.192.11:3260,1 --login
	```
	 The "media converter target name" and "drive target name" can be found in the tape gateway details.
	 
5. Verify whether the volume is attached to the client (initiator) by running the following command:
	```
	ls -l /dev/disk/by-path
	```
	 	The output of the command is similar to the sample below.
	```
	lrwxrwxrwx. 1 root root 9 Apr 16 19:31 ip-[gateway IP]:iqn.2003-07.com.qcloud:csg-022ef55-tapedrive-01 -> ../../sda
	```
	After the initiator is set up, you are strongly recommended to optimize the iSCSI configuration by using the recommended settings as described in [Using Volume in Linux Client - Optimization](https://intl.cloud.tencent.com/document/product/581/35684#.E4.BC.98.E5.8C.96.E9.85.8D.E7.BD.AE).
	
## Configuring NetBackup
### Discovering tape gateway driver

1. Open the NetBackup Administration Console as an administrator.
2. Click "Configure Storage Devices" to open the device configuration wizard.
	![](https://mc.qcloudimg.com/static/img/44b63cd016a09aa6118d2caebb3ce064/NBU01.png)
3. Click **Next**. 
   ![](https://mc.qcloudimg.com/static/img/029e0cfa3d9ea4eae0f0ad8dd1eda738/NBU02.png)
4. In the "Device Hosts" column, select your computer and click **Next**. Then, the NetBackup program will scan your computer and discover all devices.
	![](https://mc.qcloudimg.com/static/img/8b052a75fba490bffe3212861ef7416c/NBU03.png) 
5. After the scan is completed, on the "Scanning Hosts" page, click **Next**. On the pop-up page, click **Next**. The page lists the 10 tape drives discovered and the media converters on your computer.
	![](https://mc.qcloudimg.com/static/img/c46bec6b7598e137d0db40e83473d1ab/NBU05.png) 
6. In the "Backup Devices" window, click **Next**. 
7. In the "Drag and Drop Configuration" window, confirm that the media converter provided by the gateway has been selected and then click **Next**. 
	![](https://mc.qcloudimg.com/static/img/7cab243b2893c912526eaad17eecd6e5/NBU06.png)
8. In the dialog that appears, click **Yes** to save the configuration to your computer. The NetBackup program then updates the device configuration. Click **Continue** in the dialog for secondary confirmation.
   ![](https://mc.qcloudimg.com/static/img/4a7ccc2f31ca15a76efd7b573dd44594/NBU07.png)
9. After the update is completed, click **Next** to make these devices available to the NetBackup program.
	![](https://mc.qcloudimg.com/static/img/5dfca347fc025606ab26c4ba5810159b/NBU09.png)
10. Click **Finish** to complete the setup.


### Verifying your device
1. In the NetBackup console, expand the "Media and Device Management" node and then expand the "Devices" node. Select "Drives" to display all tape drives. 
![](https://mc.qcloudimg.com/static/img/ed8f57139f9ea6a00ed2a93690b56cfb/NBU10.png)
2. In the "Devices" node, select "Robots" to display all your media converters. 
![](https://mc.qcloudimg.com/static/img/0e2bf5e5248fa561be47ae63612736e9/NBU11.png)
3. In the "All Robots" pane, select "TLD(0)" (i.e., your robot), right-click and select **Inventory Robot**. 
4. In the "Robot Inventory" window, verify that your host is selected in the "Device-Host" list in the "Select robot" item. 
5. Confirm that your robot is selected from the "Robot" list. 
6. In the "Robot Inventory" window, select "Update volume configuration" -> "Empty media access port prior to update" and then click **Start**. 
	![](https://mc.qcloudimg.com/static/img/dfae26a009432ca616ae225dd91b354f/NBU23.png)  	This process will then inventory your media converters and virtual tapes in the NetBackup Enterprise Media Management (EMM) database. NetBackup stores media information, device configuration, and tape status in EMM. 

7. After the inventory is completed, the tapes that have been created on the tape gateway will appear in the "Robot Inventory" window. Click **Yes**. Selecting **Yes** here will update the configuration and move the virtual tapes found in the import/export slot to the virtual tape library. 
8. Close the "Robot Inventory" window. 
9. In the "Media" node, expand the "Robots" node and select "TLD(0)" to display all the virtual tapes available to your robot (media converter). Note: if you have previously connected other devices to your NetBackup application, there may be multiple robots. Make sure that the correct robot is selected. After the steps above are completed, your NetBackup program will be connected to the tape gateway devices and make these devices available to the backup program.

## Backing up Data to Tape Gateway

### Creating volume pool
#### A volume pool is a collection of virtual tapes to be backed up

1. Open the NetBackup Console.
2. Expand the "Media" node, right-click **Volume Pools**, and select **New Volume Pool**. 
3. In the "New Volume Pool" dialog that pops up, enter the name and description of the volume pool and click **OK**. The created volume pool will be added to the volume pool list.   ![](https://mc.qcloudimg.com/static/img/a2b2e6583523ae10ef4be1c910885d48/NBU13.png)

#### Adding virtual tape to volume pool
1. Check "Media" and the page will list the previously discovered volumes.
2. Right-click the volume to be added to a volume pool, click **Change** in the pop-up window, change the Volume Pool in the pop-up window, and then click **OK**.
![](https://mc.qcloudimg.com/static/img/76b71d3fde55f22e11ce93bb49016fc6/NBU24.png)
3. At this point, you can confirm that the newly created volume is already in your volume pool by expanding the "Volume Pools" node and the volume pool just created. 


#### Creating a backup policy
The backup policy specifies when to perform a backup operation, what data to back up, and which volume pool to store the backup data.

1. Select "NetBackup Management" and click "Create a Policy" to open the "Policy Configuration Wizard" window. 
![](https://mc.qcloudimg.com/static/img/de6f7daf3c2e306c52fd6366db956239/NBU18.png)
2. Select "File systems, databases, applications" and click **Next**. 
3. Enter the name of the policy, select "MS-Windows" in the "Select the policy type" list and click **Next**. 
4. In the Client List window, click **Add**, enter the host name of your computer in the Name column and then click **Next**. This step applies the defined policy to the local host (client computer). 
5. In the "Backup Selection" window, click **Add** and then click the folder icon. In the "Browse" window, browse to the folder or file you want to back up, click **OK** and then click **Next**. 
![](https://mc.qcloudimg.com/static/img/52351ea25943c88fd21b45b8b3f57d96/NBU19.png)
6. In the "Backup Types" window, use the default values and click **Next**. If you want to start the backup by yourself, select **User Backup**. 
![](https://mc.qcloudimg.com/static/img/6ff080e3bb32de65cbba32932b8a4349/NBU20.png)
7. In the "Frequency and Retention" window, select the frequency and retention policy to be applied to the backup. Set the backup frequency according to your needs and then click **Next**. 
8. In the "Start" window, select "Off hours" (which means your folder will be backed up only in off hours) and click **Next**.
![](https://mc.qcloudimg.com/static/img/a436b3674b5e5beffa2799e51a525b4a/NBU21.png) 
9. In the "Policy Configuration" wizard, select **Finish**. 

#### Performing manual backup
In addition to the automatic backup policy, you can perform manual backups at any time through the following steps.

1. On the navigation pane in the NetBackup Console, expand the "NetBackup Management" node. 
2. Expand the "Policies" node. 
3. In the context menu, click **Manual Backup**.
![](https://mc.qcloudimg.com/static/img/f697db1611516a1014b34a4248e9fdf9/NBU22.png) 
4. In the "Manual Backup" window, enter the plan name, select a client, and click **OK**. 
5. In the pop-up confirmation dialog, select "Incremental Backup" or "Full Backup", click **OK** and exit the settings. 
6. On the navigation pane, select "Activity Monitor" to view the status of the backup in the "Job ID" column.   
To find the barcode of the virtual tape to which NetBackup writes the file data during the backup, view the "Job Details" window (as described in the following procedure). This barcode will be used during the tape archiving process in the next section.

#### Finding the barcode of a tape
1. In Activity Monitor, right-click in the "Job ID" column to open the ID menu for your backup job and then click **Details**. 
2. In the "Job Details" window, click the **Detailed Status** tab. 
3. In the "Status" box, find the media ID which helps you identify which tape the data has been written to.   
Through the steps above, you have successfully deployed a tape gateway, created a virtual tape, and backed up your data.

## Archiving Tape
When a tape is archived, the tape gateway will move the tape from the gateway's virtual tape library (VTL) to the archive, which provides offline storage. You can archive the tape by using the backup application to eject the tape in the following steps:

1. In the NetBackup Administration Console, expand the "Media and Device Management node" and then expand the "Media" node. 
2. In the listed tapes, right-click the tape you want to eject and click **Eject Volume From Robot**. 
![](https://mc.qcloudimg.com/static/img/c56830bab8e729835590388ec2e2d70e/NBU25.png)
3. In the "Eject Volumes" window, confirm the media ID again and click **Eject**. 
4. In the pop-up dialog box, click **Yes**. After the ejection process is completed, the state of the tape in the Eject Volumes dialog will indicate that the ejection has succeeded. 
5. Click **Close** to close the "Eject Volumes" window. 
6. After the tape ejection operation is performed, the tape state will change from "normal" to "archiving" in the CSG Console. After the tape is ejected, the data will be transferred to the archive storage and the tape state will change to "archived". 

## Retrieving Archived Tape

The application cannot retrieve data from an archived tape. In order to read the archived data, you need to retrieve the tape data.

1. Retrieve an archived tape back to the tape gateway. In the CSG Console, select "Tape List", select the corresponding archived tape, and click **Retrieve**. For detailed directions, please see [Retrieving a Tape](https://intl.cloud.tencent.com/document/product/581/35694#.E7.A3.81.E5.B8.A6.E5.8F.96.E5.9B.9E). 
2. After the tape is retrieved, you can use the "Backup, Archive and Restore" tool that is installed with the Symantec NetBackup application. This process is the same as restoring data from a physical tape.

