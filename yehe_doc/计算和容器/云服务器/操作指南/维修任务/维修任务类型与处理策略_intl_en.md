
When exceptions that affect instance availability and performance are detected, the maintenance process is initiated automatically, record the maintenance tasks, and notify users about the affected instances. Users can go to the [Maintenance Task console](https://console.cloud.tencent.com/cvm/repair/list) to check details and authorize Tencent Cloud to perform maintenance.

**The maintenance tasks of CVM instances are classified into the following types based on the reasons the tasks are triggered. See below for details:**
## Maintenance Task Types

<table>
<thead>
<tr>
<th style="
    width: 12%;
">Task Type</th>
<th style="
    width: 24%;
">Description</th>
<th style="
    width: 32%;
">Suggestion</th>
<th style="
    width: 32%;
">Applicable Authorization Policies</th>
</tr>
</thead>
<tbody><tr>
<td>Instance running exception</td>
<td>Sudden software and hardware failures or system errors of the underlying host of the instance, which cause abnormal downtime or restart of the instance.</td>
<td>When a maintenance task of abnormal instance running is triggered, the platform immediately performs relevant maintenance and tries to restart the abnormal instance.<br/>It is recommended to wait for the completion of instance restarting, and check the update progress of maintenance task.</td>
<td>Choose the policy based on the current status of the maintenance task:
<ul style="margin-bottom:0px">
<li>When the task is in "Processing" status, the platform is urgently performing related maintenance on the abnormal instance. After the maintenance is completed, the task status will be updated immediately, and relevant notifications will be pushed to you.</li>
<li>When the task is in "Ended" status, the abnormal instance has automatically restarted and restored. You can verify whether the instance and application have been restored to normal mode.</li>
</ul>
</td>
</tr>
<tr>
<td>Instance running risk</td>
<td>The instance is currently running normally, but there are risks on software and hardware of the host or the underlying platform, which may cause the fluctuation of the instance performance or the abnormal downtime.</td>
<td>To complete the maintenance as soon as possible to avoid risks of the underlying software and hardware and potential downtime, it is recommended to back up your business data in advance and go to the Maintenance Task console to perform the following operations:
<ol style="margin-bottom:0px">
<li>(Optional) Back up the instance data.</li>
<li>Authorize the platform to initiate maintenance immediately, or reserve a planned maintenance within 48 hours in advance.</li>
<li>Wait for the system to automatically initiate maintenance at the scheduled maintenance time.</li>
</ol>
</td>
<td>According to the fixing method of the underlying risks of the instance, the following authorization methods can be selected:
<ul style="margin-bottom:0px">
<li>Authorization for migration without CVM shutdown (the instance does not need to be shut down, and the CVM may experience short-term high load or network jitter during the migration).</li>
<li>Authorization for shutdown maintenance (the instance is fast restored after restart).</li><br>
</ul><b>Note:</b><br>
1. If the user does not authorize within 48 hours, the system will initiate maintenance at the scheduled maintenance time.<br>
2. Local disk instances do not support fast restoration after restart, and require a longer maintenance period to fix underlying hardware risks. Users can choose to redeploy local disk instances to quickly avoid the risks (local disk data cannot be retained).
</ul>
</td>
</tr>
<tr>
<td>Instance disk exception</td>
<td>A sudden failure occurs on the local disk, which may cause reduced I/O performance of the instance or damage to the disk.</td>
<td>To complete the maintenance as soon as possible to restore the disk, it is recommended to back up your business data in advance and go to the Maintenance Task console to perform the following operations:
<ol style="margin-bottom:0px">
<li>(Optional) Back up the instance data.</li>
<li>Authorize the platform to change the abnormal disk immediately, or reserve a planned maintenance within 48 hours in advance.</li>
<li>Wait for the platform to replace the abnormal disk, and reattach and use the replaced disk according to the prompts in the restoration notification.</li>
<td>According to the fixing method of the abnormal disk, the following authorization methods can be selected:
<ul style="margin-bottom:0px">
<li>Change disk without CVM shutdown (replace the abnormal disk without CVM shutdown. During the maintenance, the I/O of the abnormal disk is temporarily unavailable. After the maintenance is completed, you can attach and use the new disk).</li>
<li>Shut down to change disk (the instance needs to be shut down to replace the abnormal disk. The local disk data may be retained. A long maintenance period is required).</li>
<li>(Optional) Migrate without the disk: The local disk instance is redeployed, and the local disk data cannot be retained. The instance availability can be restored in minutes.</li>
</td>
</tr>
<tr>
<td>Instance disk warning</td>
<td>The local disk of the instance may be damaged, or its service life is about to end, which may cause instance I/O exceptions or disk offline.</td>
<td>To complete the maintenance as soon as possible to eliminate the potential failure risks of the local disk, it is recommended to back up your business data in advance and go to the Maintenance Task console to perform the following operations:
<ol style="margin-bottom:0px">
<li>(Optional) Back up the instance data.</li>
<li>Authorize the platform to change the disk with potential failure risks immediately, or reserve a planned maintenance within 48 hours in advance.</li>
<li>Wait for the platform to replace the abnormal disk, and reattach and use the replaced local disk according to the prompts in the restoration notification.</li>
<td>According to the fixing method of the abnormal disk, the following authorization methods can be selected:
<ul style="margin-bottom:0px">
<li>Change disk without CVM shutdown (replace the abnormal disk without CVM shutdown. During the maintenance, the I/O of the abnormal disk is temporarily unavailable. After the maintenance is completed, you can attach and use the new disk).</li>
<li>Shut down to change disk (the instance needs to be shut down to replace the abnormal disk. The local disk data may be retained. A long maintenance period is required).</li>
<li>(Optional) Migrate without the disk: The local disk instance is redeployed, and the local disk data cannot be retained. The instance availability can be restored in minutes.</li>
</ul>
</td>
</tr>
<tr>
<td>Instance network connection exception</td>
<td>A sudden failure occurs at the underlying network connection of the instance, which may cause network jitter or abnormal network connection.</td>
<td>When a maintenance task of an abnormal instance network connection is triggered, the platform immediately performs relevant maintenance on the underlying network and tries to restore the network connection of the abnormal instance.<br/>It is recommended to wait for the completion of the automatic fixing of the network connection, and check the update progress of the maintenance task.
<ol style="margin-bottom:0px">
</ol>
<td>Choose the policy based on the current status of the maintenance task:
<ul style="margin-bottom:0px">
<li>When the task is in "Processing" status, the platform is urgently performing related maintenance on the underlying network of the abnormal instance. After the maintenance is completed, the task status will be updated immediately, and relevant notifications will be pushed to you.</li>
<li>When the task is in "Ended" status, the network connection of the abnormal instance has been recovered. You can verify whether the instance and application have been restored to normal mode.</li>
</ul>
</td>
<tr>
<td>Instance maintenance and upgrade</td>
<td>Maintenance without CVM shutdown is initiated due to reasons such as underlying host architecture and software upgrades to improve instance performance and security.</td>
<td>To complete maintenance as soon as possible to improve instance performance and security, it is recommended to back up your business data in advance, and go to the Maintenance Task console to perform the following operations:
<ol style="margin-bottom:0px">
<li>(Optional) Back up the instance data.</li>
<li>Authorize the platform to initiate maintenance immediately, or reserve a planned maintenance within 48 hours in advance.</li>
<li>Wait for the system to automatically initiate maintenance at the scheduled maintenance time.</li>
</ol>
</td>
<td>You can choose from the following authorization methods:
<ul style="margin-bottom:0px">
<li>Maintenance without CVM shutdown (the instance does not need to be shut down, and the CVM may experience short-term high load or network jitter during the maintenance).</li>
</ul><b>Note:</b><br>
  1. If the user does not authorize within 48 hours, maintenance starts at the next scheduled maintenance time.
</tr>
</tbody></table>




## Task Status

| Task Status | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Pending authorization | Wait for user authorization. The user can choose the maintenance method and time. If the user does not authorize for a non-disk maintenance task within 48 hours, the system will initiate maintenance at the scheduled maintenance time and the maintenance task status will be changed into “Processing”. |
| Scheduled | The user has authorized for maintenance and reserved a maintenance time. The default scheduled maintenance time can be modified within 48 hours after the task is created. |
| Processing | The maintenance task is being processed. |
| Ended | The maintenance task is completed. |
| Avoided | If the instance has an unfinished maintenance task, when the user returns or terminates the instance, or adjusts the instance configuration, the avoidance of the maintenance task will be interrupted. |
| Canceled | The maintenance task is canceled by the system. |

