After elastic cloud disks are released, their hot swapping operations are supported by current CVM instance images.
>! Before unmounting a disk, run the `umount` command (Linux) or set it to offline status (Windows); otherwise, it may not be recognized when mounted the next time.
>
If you have purchased CVM instances in the following list and plan to add elastic cloud disks to them, we recommend you run the `modprobe acpiphp` command before purchasing elastic cloud disks, so that a driver can be added to enable the hot swapping feature.
<table>
<tbody>
<tr><th>CVM Instance Operating System</th><th>Version</th>
</tr><tr><td rowspan="4">CentOS</td><td>5.11 64-bit</td>
</tr><tr><td>5.11 32-bit</td>
</tr><tr><td>5.8 64-bit</td>
</tr><tr><td>5.8 32-bit</td>
</tr><tr><td>Debian</td><td>6.0.3 32-bit</td>
</tr><tr><td rowspan="2">Ubuntu</td><td>10.04 64-bit</td>
</tr><tr><td>10.04 32-bit</td>
</tr><tr><td rowspan="2">openSUSE</td><td>12.3 64-bit</td>
</tr><tr><td>12.3 32-bit</td>
</tr></tbody>
</table>

In addition, if you need to load the acpiphp driver module again after shutting down or restarting the CVM instance, we recommend you configure automatic acpiphp loading at startup. The detailed directions for different systems are as follows:

### CentOS 5 series

Run the following command to create a file.
```
vi /etc/sysconfig/modules/acpiphp.modules
```
Add the following content to the file:
```
 #!/bin/bash
 modprobe acpiphp >& /dev/null
```
Run the following command to add execution permissions, after which the script can be loaded at startup:
```
chmod a+x /etc/sysconfig/modules/acpiphp.modules
```

### Debian 6 series and Ubuntu 10.04 series

Run the following command to modify the file.
```
vi /etc/modules
```
Write the following content:
```
acpiphp
```
 	  
### openSUSE 12.3 series

Run the following command to modify the file.
```
vi /etc/sysconfig/kernel
```
Write the following content:
```
MODULES_LOADED_ON_BOOT="acpiphp"
```

