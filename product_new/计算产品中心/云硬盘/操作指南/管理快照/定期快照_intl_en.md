## Overview
Tencent Cloud Block Storage has made a **scheduled snapshot** function available. This function allows developers to set up a task backup policy.
Common policies include:
- You can set non-core business data disks to perform an automatic snapshot backup at 00:00 every Monday, and the backup will be automatically deleted after 1 month.
- You can set core business data disks to perform a snapshot backup every 24 hours, and the backup will be automatically deleted after 1 week.



## Policy Description
<table>
     <tr>
         <th>Policy item</th>  
         <th>Description</th>  
     </tr>
	 <tr>
         <td>Object</td>
         <td>All cloud disks, including system disks and data disks.</td>
     </tr> 
	 <tr>
         <td>Execution policy</td>
         <td>Point in time for automatic snapshot can be down to every hour - every day. After the execution policy has been configured, it takes effect for the long term.</br>When an existing execution policy is modified, the modification takes effect immediately.</td>
     </tr>
	 <tr>
         <td nowrap="nowrap">Scheduled termination<b>(Important)</b></td>
         <td>Scheduled snapshots provide the scheduled termination function. Snapshot lifecycle (1 day-30 days) is set in advance. After expiration, snapshots that are generated automatically will be deleted automatically, reducing backup costs.</br>If scheduled termination policy is not configured, automatic snapshots will be stored for the long term.</td>
     </tr>
	 <tr>
         <td>Batch</td>
         <td>You can select multiple cloud disks and apply the same scheduled snapshot policy on them in one batch.</td>
     </tr>
	 <tr>
         <td>Script pausing</td>
         <td>Cloud disks not in use do not execute scheduled snapshot policies.</br>Not in use refer to cloud disk whose associated CVM is in <b>shutdown</b> status or the data disk is not mounted.</td>
     </tr>
	 <tr>
         <td>Naming rules</td>
         <td>Automatic snapshots should be named in the format of snap_yyyyMMdd_HH. yyyyMMdd is the creation date, and HH is the creation hour. </br>For instance, snap_20140418_11 means an automatic snapshot is created at 11 o'clock on April 18, 2018.</td>
     </tr>
	 <tr>
         <td nowrap="nowrap">Lifecycle<b>(Important)</b></td>
         <td>There are 2 kinds of snapshot lifecycles: <li>For manually created snapshots, the lifecycle is <b>long-term storage</b> by default, and it can be stored indefinitely as long as the account balance is sufficient. </li><li>For scheduled snapshots, you can set a <b>scheduled termination</b> time according to the creation rules. You can also set long-term storage for scheduled snapshots.</li></td>
     </tr>
	 <tr>
         <td>Snapshot conflict</td>
         <td>Automatic snapshots do not conflict with custom snapshots in use, but they may conflict with each other during creation.</br><li>When performing an automatic snapshot on a disk, user needs to wait for the automatic snapshot to be completed before creating a custom snapshot, and vice versa.</li><li>If there is a large amount of data on the disk, and the duration of a snapshot is longer than the interval between two points in time for automatic snapshot, the automatic snapshot will not be taken at the next point in time. For example, user sets 9:00, 10:00, and 11:00 as points in time for automatic snapshot. The execution duration of the automatic snapshot at 9:00 takes 70 minutes (that is, it finishes at 10:10). In this case, the automatic snapshot will not be taken at 10:00. The next snapshot point in time is 11:00.</li></td>
     </tr>
	 <tr>
         <td>Snapshot Quota</td>
         <td>Each disk has a certain snapshot quota. If the maximum quota for snapshots on a disk has been reached, automatic snapshot will be suspended and blocked.</br>Snapshot quota is to prevent the endless increase in storage cost if developers forget about an automatic snapshot policy.</td>
     </tr>
	 <tr>
         <td>ASP</td>
         <td>Specified scheduled snapshot policy, that is, Auto Snapshot Policy.</td>
     </tr>
	 <tr>
         <td>ASP quota</td>
         <td>Under a single Tencent Cloud account, a maximum of 30 ASP policies can be set in each region. A single ASP can be associated with a maximum of 200 cloud disks.</td>
     </tr>
	 <tr>
         <td>Storage period</td>
         <td><li>For automatic snapshots, the console displays the countdown for repossession. Manual changing of the storage duration of automatic snapshots to long-term storage is supported.</li><li>For manually created snapshots, the console displays long-term storage.</td>
     </tr>
	 <tr>
         <td>ASP pause function</td>
         <td><li>Auto Snapshot Policy (ASP) provides a manually triggered <b>pause</b> function. After pausing, snapshots will no longer be automatically created. However, lifecycles of previously generated automatic snapshots will not be affected by this function. They will still be terminated or stored for the long term according to configured rules.</td>
     </tr>
	 <tr>
         <td>Operation logs</td>
         <td>Show the creation process of all automatic snapshots, the same as that of manually added snapshots.</td>
     </tr>
</table>


## Operational Guidelines
### Creating a scheduled snapshot policy
>A maximum of 30 snapshot policies can be created in one region under a single Tencent Cloud account.

1. Log in to the [Scheduled snapshot policy](https://console.cloud.tencent.com/cvm/snapshot/asp) page.
<span id="step2"></span>
2. Select a region.
3. Click **Create**.
<span id="step4"></span>
4. In the **New snapshot policy** dialog box, set the following parameters, and click **OK**.
 <table>
     <tr>
         <th>Parameter item</th>  
         <th>Parameter description</th>  
     </tr>
	 <tr>
         <td>Name</td>
         <td>Required parameter.</br>Name of the scheduled snapshot policy. Maximum length of 60 characters.</td>
     </tr> 
	 <tr>
         <td>Region</td>
         <td>Required parameter.</br>This parameter can not be changed on the current page. For specific configuration method, see <a href="#step2">Step 2</a>.</td>
     </tr>
	 <tr>
         <td>Backup date</td>
         <td>Required parameter.</br>Date when the scheduled snapshot is taken. Value range: Every Sunday - every Saturday.</td>
     </tr>
	 <tr>
         <td>Backup point in time</td>
         <td>Required parameter.</br>Point in time when the scheduled snapshot is taken. Value range: 00:00-23:00 on the hour.</td>
     </tr>
	 <tr>
         <td>Snapshot storage duration</td>
         <td>Required parameter.<ul><li>Snapshot will be automatically deleted after being stored for a fixed number of days. You can choose 1 - 30 days. The default storage duration is 7 days.</li><li>Long-term storage.</li></ul></td>
     </tr>
</table>

 

### Associating cloud disks
>The same scheduled snapshot policy can be associated with a maximum of 200 cloud disks.

1. Log in to the [Scheduled snapshot policy](https://console.cloud.tencent.com/cvm/snapshot/asp) page.
2. Select a region.
3. Click **Associate a cloud disk** in the row of the target policy.
4. In the **Associate a cloud disk** dialog box, choose the cloud disk you want to associate.
5. Click **OK**.

### Enable/Disable scheduled snapshot policies

1. Log in to the [Scheduled snapshot policy](https://console.cloud.tencent.com/cvm/snapshot/asp) page.
2. Select a region.
3. In the row of the target policy, click <img src="https://main.qcloudimg.com/raw/01c32381ab9636998476d35b00ef0825.png"  style="margin:0;"> to enable the scheduled snapshot policy, and <img src="https://main.qcloudimg.com/raw/731b456318822b8d478ea961e55369f1.png"  style="margin:0;"> to disable the scheduled snapshot policy.

### Modifying scheduled snapshot policies

1. Log in to the [Scheduled snapshot policy](https://console.cloud.tencent.com/cvm/snapshot/asp) page.
2. Select a region.
3. Click **Modify Policy** in the row of the target policy.
4. In the **Modify snapshot policy** dialog box, modify the related parameters (for parameter descriptions see [Step 4](#step4)). Click **OK**.

### Deleting scheduled snapshot policies

1. Log in to the [Scheduled snapshot policy](https://console.cloud.tencent.com/cvm/snapshot/asp) page.
2. Select a region.
3. You can delete scheduled snapshot policies by the following methods:
 a. Single delete: Click **Delete** in the row of the target policy.
 b. Batch delete: Check the scheduled snapshot policies that you want to delete. Click **Delete** at the top of the list.

### Turning automatic snapshots into long-term stored snapshots 
>If **Snapshot storage time** in the automatic snapshot policy has already been set to **Long-term Storage**, there is no need to perform the following operations on snapshots that are automatically generated by this policy.

1. Log in to the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) page.
2. Select a region.
3. Click the ID of the target automatic snapshot.
4. In the details page, click **Save Long-term** to set the automatic snapshot to be stored for the long term.
5. Return to the snapshot list. You can see that the **Storage Time** of this snapshot has changed to **Long-term Storage**.
