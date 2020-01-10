## Operation Scenarios

A visiting client must be in the same network as the file system, for which a permission group needs to be configured to manage the access and read/write permissions of the client. This document describes how to do so.


## Directions
### Creating a permission group
1. Log in to the [CFS Console](https://console.cloud.tencent.com/cfs) and click **Permission Group** on the left sidebar.
2. On the permission group page, click **Create** and configure the name and remarks for the new permission group in the pop-up window.


### Creating a permission group rule
You can add, edit, or delete rules in the rule list. If no rule is added to the permission group, all IPs will be allowed. The rules are described as follows:
<table>
  <tr>
    <th>Field</th>
    <th>Meaning</th>
  </tr>
  <tr>
    <td>Visiting address</td>
		<td>You can enter a single IP or IP range, such as 10.1.10.11 or 10.10.1.0/24. The default visiting address is <code>*</code>, indicating that all IPs are allowed. Please note that you need to enter the CVM instance's private IP here.</td>
  </tr>
  <tr>
    <td>Read/write permission</td>
    <td>Read-only or read/write.</td>
  </tr>
  <tr>
    <td>User permission</td>
    <td> 
    <p>The four options below are used for controlling the permissions of a visiting user.<b>Note: CIFS/SMB file system does not support this permission item, so the configuration will not take effect.</b></p>
    <li>all_squash: any visiting user will be mapped to an anonymous user or user group.</li>
    <li>no_all_squash: a visiting user will be first matched with a local user, and if the match fails, it will be mapped to an anonymous user or user group.</li>
    <li>root_squash: a visiting root user will be mapped to an anonymous user or user group.</li>
    <li>no_root_squash: a visiting root user will be allowed to maintain root account privileges.</li>
    <p><b>Note: the default permission is 755 for each file system, and nfsnobody does not have write permission. Therefore, if there are no special needs, `no_root_squash` is recommended. If the root user creates a file directory and mounts the file system, when the visiting IP is set to `all_squash` or `root_squash`, the visiting IP can only read files. (because the mount path requires root privileges, but the visiting IP has been mapped to an anonymous user).<b></p>
    </td>
  </tr>  
  <tr>
    <td>Priority</td>
    <td>You can configure an integer between 1 and 100 as the priority level, where 1 indicates the highest priority. If the permission of a single IP conflicts with that of an IP within an IP range in the same permission group, the permission with a higher priority will prevail, and if their priority levels are the same, the permission of the single IP will prevail. If two IP ranges that have overlaps are configured with different permissions but the same priority levels, the permissions of the overlapping ranges will take effect randomly. Please avoid configuring overlapping IP ranges. <b>Note: priority configuration is not supported for CIFS/SMB file systems and will not take effect.</b>
    </td>
  </tr>
</table>

### Configuring a permission group for a file system
The configuration of a permission group can be modified after the file system is created. You can choose to create a permission group first and select it when creating a file system. You can also select the default permission group when creating a file system and then go to the file system details page to change the permission group.

>Note: if the file system is mounted with the NFS v4 protocol, the modification to the permission group rules of the file system will take effect in 2 minutes.


### Modifying the information and rule of a permission group
You can enter the permission group details page to modify the name, remarks, and rule of a permission group.


