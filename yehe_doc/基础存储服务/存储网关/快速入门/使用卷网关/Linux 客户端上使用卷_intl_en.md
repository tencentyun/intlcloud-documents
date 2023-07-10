## Connecting to Volume Through Linux Client
The following describes how to connect to a gateway's iSCSI Target by using the iscsi-initiator-utils RPM package on Linux.

### Installing the iscsi-initiator-utils RPM Package 
Run the following command to install the package. Skip this step if you have already installed it.
```
sudo yum install iscsi-initiator-utils
```

### Verifying iSCSI daemon running status
Run the following command to verify that the iSCSI daemon is running.
```
sudo /etc/init.d/iscsi status    //Applicable for RHEL 5 or RHEL 6

sudo service iscsid status    //Applicable for RHEL 7
```

If the command above does not return a "running" state, run the following command to run the program.
```
sudo /etc/init.d/iscsi start    
```

### Discovering volume
Run the following command to discover the volume on the gateway. If the command above does not return a "running" state, run the following command to run the program. GATEWAY_IP needs to be replaced with the IP variable of your gateway which can be found in the iSCSI Target Info attribute of the volume in the CSG Console.
```
sudo /sbin/iscsiadm --mode discovery --type sendtargets --portal <GATEWAY_IP>:3260  
 
For example:
sudo /sbin/iscsiadm --mode discovery --type sendtargets --portal 192.168.190.11:3260
```

### Mounting volume
Run the following command to mount the discovered volume. TargetName needs to be replaced with the TargetName of the volume to be mounted which can be found on the volume details page; GATEWAY_IP needs to be replaced with the IP variable of your gateway.
>Due to iSCSI protocol restrictions, do not mount the same volume to multiple clients.

```
sudo /sbin/iscsiadm --mode node --targetname <TargetName> --portal <GATEWAY_IP> -l 
For example:
sudo /sbin/iscsiadm --mode node --targetname iqn.2003-07.com.qcloud:vol-10098 --portal 192.168.190.11:3260 -l
```

### Viewing volume
You can run commands such as `fdisk -l` or `lsblk` to view the mounted volume. In the current state, the volume has become available as a bare disk. If you need to install a file system, please see the next step.

![](https://main.qcloudimg.com/raw/616893311123b8912d996821a53511a2.png)

### Partitioning and formatting file system
- **Run the following command to partition the data disk.**
	```
	fdisk /dev/vdb
	```
	
	Follow on-screen instructions to enter `n` (to create a partition), `p` (to create an extended partition), and `1` (to use the first primary partition) in sequence, press Enter twice (to use the default configuration), enter `wq` (to save the partition table), and press Enter to start partitioning. Here is an example of creating one partition. You can also create multiple partitions as needed.
	![](https://main.qcloudimg.com/raw/626e704268a87000aa443ed781ce7849.png)
	
- **View partition**
	Run the "fdisk -l" command and you can see that the new partition vdb1 has been created.
	![](https://main.qcloudimg.com/raw/743c1027c37f8dfb3dec48f40da93ff8.png)
	
	
- **Format partition**
	After partitioning, you need to format the new partition. You can select a desired format for the file system such as XFS and EXT4. "EXT3" is used as an example below. Use the following command to format the new partition.
	>An XFS file system has relatively weak stability but can be formatted fast; an EXT file system has strong stability, but the larger its storage, the longer its formatting time. Please set the file format as needed.
	
	```
	mkfs.ext3 /dev/vdb1
	```
	Run the command as shown below:
	![](https://main.qcloudimg.com/raw/d54b711e170ff000ef5a360a0e9ce381.png)

- **Mount and view partition**
	Run the following command to create a mydata directory and mount the partition to it:
	```
	mkdir /mydata
	mount /dev/vdb1 /mydata
	```

	Then run the following command to view the result:
	```
	df -h
	```
	
	If the following message appears, the mounting is successful, i.e., the data disk can be viewed.
	![](https://main.qcloudimg.com/raw/e2b0a2d9bc5d99989cc4873637cf540a.png)
	
- 	**Auto mount partition**
	If you want the CVM instance to automatically mount the data disk when restarting or powering on, you must add the partition information to `/etc/fstab`. If it is not added, the CVM instance won't be able to automatically mount the data disk after being restarted or powered on. Use the following command to add partition information:
	```
	echo '/dev/vdb1 /mydata ext3 defaults 0 0' >> /etc/fstab
	```

	Run the following command to view the result:
	```
	cat /etc/fstab
	```

	If the following message appears, the partition information is successfully added.
	![](https://main.qcloudimg.com/raw/fcf8458823bae33e434a33687cc95922.png)
	
	
### Unmounting volume
If the mounting is incorrect or you need to replace the mounted server, you can use the following statement to unmount:
```
sudo /sbin/iscsiadm --mode node --targetname <TargetName> --portal <GATEWAY_IP> -u
 
For example:
sudo /sbin/iscsiadm --mode node --targetname iqn.2003-07.com.qcloud:vol-10098 --portal 192.168.190.11:3260 -u
```

### Optimization

To ensure the stability of data reads/writes with CSG, you are strongly recommended to follow the steps below to optimize your configuration.

- Modify IO request timeout configuration
  You can guarantee the connection to the volume by increasing the `deadline timeout` of the IO request. The timeout period is in seconds. You are recommended to set a longer time (e.g., one hour or above), which helps ensure business continuity in the event of sudden network failures.
  
  Locate and open the `/etc/udev/rules.d/50-udev.rules` file and find the following line of code. If it is not found in the Initiator of RHEL 6 / 7, add the following code to the file and save.
	```
	ACTION=="add", SUBSYSTEM=="scsi", SYSFS{type}=="0|7|14",\
	RUN+="/bin/sh -c 'echo 7200 > /sys$$DEVPATH/timeout'"  // RedHat 5
	
	ACTION=="add", SUBSYSTEM=="scsi",  ATTR{type}=="0|7|14",\
	RUN+="/bin/sh -c 'echo 7200 > /sys$$DEVPATH/timeout'"  // RedHat 6 and RedHat 7
	```
	
  >Unmounting a volume will invalidate this configuration item, so please perform the operation each time the volume is mounted.
  
  To see whether the rules configured above can be applied to the current system, enter the following command where "device name" needs to be replaced with the real device name.
  	
	```
	udevadm test device name
	For example: udevadm test /dev/sda
	```
	Run the following command to verify that the rules have been applied and taken effect.
  ```
	udevadm control --reload-rules && udevadm trigger 
	```
  
	
- Modify the maximum time for request queuing
  Locate and open the /etc/iscsi/iscsi.conf file, find the following code and modify it to the suggested value or longer.
	```
	node.session.timeo.replacement_timeout = 3600  //The original value is 120 seconds
	```
	
	Note: after this value is modified, when the network connection between the Initiator and CSG is exceptionally interrupted, the Initiator will try to repair connection till the `replacement_timeout` elapses and then set the state of the volume to error and return `-EIO` for every IO request.
	```
	node.conn[0].timeo.noop_out_interval = 60  // The original value is 5 seconds
	node.conn[0].timeo.noop_out_timeout = 600  // The original value is 5 seconds
	```
	
	After this value is modified, the Initiator will extend the interval and timeout of sending HA requests (ping) to CSG, so that it will tolerate errors with network connection to CSG as much as possible instead of determining that it encounters an irrecoverable network failure with CSG.
	
	After the modification above, run the following command to restart the iSCSI service for the configuration to take effect.
	```
	service iscsid restart 
	```
	



