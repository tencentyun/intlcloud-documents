
Depending on the exception, maintenance tasks vary by failure type and task status as detailed below:

## Maintenance Task Type

<table>
<thead>
<tr>
<th>Task Type</th>
<th>Description</th>
<th>Suggested Solution</th>
<th>Available Authorization Policy</th>
</tr>
</thead>
<tbody><tr>
<td>Instance running exception</td>
<td>The instance crashes or restarts, or a failure suddenly occurs on the host or the underlying platform.</td>
<td>When you receive a task of this type, it indicates that the instance had already stopped running when the failure occurred, and the system had promptly performed maintenance operations. In this case, you can pay attention to the processing progress of the maintenance task.</td>
<td>Pay attention to the maintenance task status and determine the processing policy in the next step based on it:
<ul style="margin-bottom:0px">
<li>If the task is in the **Ended** status, you can pay attention to the task processing status and verify whether the instance and application have restored to normal after the processing is completed.</li>
<li>If the task is in the **To be authorized** status, you can promptly back up the business data and authorize maintenance to prevent more crashes.</li>
</ul>
</td>
</tr>
<tr>
<td>Instance running risk</td>
<td>The instance can still run normally, but the host or underlying platform faces a risk, which may cause a high instance load or instance crash.</td>
<td>You can promptly authorize maintenance and back up the business data:
<ol style="margin-bottom:0px">
<li>Go to the maintenance task console for authorization to avoid risks.</li>
<li>You can authorize immediate maintenance or schedule maintenance within 48 hours.</li>
<li>(Optional) Back up the instance data.</li>
</ol>
</td>
<td>Shutdown for authorization (the instance is restarted for maintenance). <br>If you do not authorize maintenance within 48 hours, the system will restart the instance for maintenance by default after 48 hours.</td>
</tr>
<tr>
<td>Instance disk exception</td>
<td>A local disk in the instance failed or is compromised in performance or functionality.</td>
<td>You can promptly authorize maintenance and back up the business data:
<ol style="margin-bottom:0px">
<li>Go to the maintenance task console to authorize the policy to fix the exception.</li>
<li>You can authorize immediate maintenance or schedule maintenance within 48 hours.</li>
<li>(Optional) Back up the instance data.</li>
<td>You can use the following methods:
<ul style="margin-bottom:0px">
<li>Shutdown for maintenance (the local disk data may be retained, but a long maintenance period is required).</li>
<li>Migration without using the disk (data will be discarded and recovered within minutes).</li>
</ul>If you do not authorize maintenance within 48 hours, the system will restart the instance for maintenance by default after 48 hours.
</td>
</tr>
<tr>
<td>Instance network connection exception</td>
<td>A failure occurred during instance network connection, which may cause network jitter or a network connection exception.</td>
<td>You can promptly authorize maintenance:
<ol style="margin-bottom:0px">
<li>Go to the maintenance task console for authorization to avoid risks.</li>
<li>You can authorize immediate maintenance or schedule maintenance within 48 hours.</li>
</ol>
</td>
<td>Shutdown for authorization (the instance is restarted for maintenance)<br>If you do not authorize maintenance within 48 hours, the system will restart the instance for maintenance by default after 48 hours.</td>
</tr>
</tbody></table>



## Job Status

| Task Status | Description                                                         |
| -------- | ------------------------------------------------------------ |
| To be authorized   | The task is to be authorized by you. You can specify the maintenance method and time. If you do not authorize it within 48 hours, the task will automatically enter the **Processing** status to perform maintenance operations. |
| Scheduled   | You have authorized and scheduled a maintenance task. You can change the authorization status within 48 hours after creating a task. |
| Processing   | The maintenance task is being processed.                                               |
| Ended   | The maintenance task has been completed.                                            |
| Avoided   | The instance maintenance task is interrupted and avoided when operations such as instance return, termination, and configuration adjustment are performed.  |
| Canceled   | The maintenance task is canceled by the system.                                       |

