## Overview
You can set threshold-triggered alarm policies to monitor CVM performance, and also event-triggered alarm polices to watch the status of CVM instances and the underlying platform infrastructure. When an exception occurs, you will receive notifications via the specified methods (email, SMS or phone call). A proper alarm policy will help improve the robustness and reliability of your applications. You can also see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).

## Directions
1. Log in to the Cloud Monitor console and click **Alarm Configuration** > [Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy) on the left sidebar.
2. On the **Alarm Policy** page, click **Create**.
3. In the pop-up window, configure basic information, alarm policy, and notification template as instructed below.
<table>
  <tr>
    <th>Configuration Type</th>
    <th width="19%" colspan=2>Configuration Item</th>
    <th>Description</th>
  </tr>
  <tr>
    <td  rowspan="5"> Basic Info</td>
    <td colspan=2>Policy Name</td>
    <td>A custom policy name</td>
  </tr>
  <tr>
    <td colspan=2>Remarks</td>
    <td>Remarks for the policy</td>
  </tr>
  <tr>
    <td colspan=2>Monitor Type</td>
    <td>Choose <b>Cloud Product Monitoring</b></td>
  </tr>
  <tr>
    <td colspan=2>Policy Type</td>
    <td>Select the desired policy type for monitoring Tencent Cloud services.</td>
  </tr>
  <tr>
    <td colspan=2>Project</td>
    <td>Choose a project as needed. You can later find this policy quickly by filtering by the project.
  </tr>
  <tr>
    <td rowspan="4">Configure Alarm Policies</td>
    <td colspan=2>Alarm Object</td>
    <td>
      <ul>
			         <li><b>Instance ID</b>: associate the policy with the specified CVM instance</li>
           <li><b>Tag</b>: associate the policy with CVM instances bound with the specified tag</li>
               <li><b>Instance Group</b>: associate the policy with the selected instance group</li>
		            <li><b>All Objects</b>: associate the policy with all instances under the current account (permission required)</li>
           </ul>
        </td>
		<tr>
		<td rowspan=3>Trigger Condition</td>
    <td><b>Manual Configuration </b>(Metric Alarm)</td>
    <td>
Trigger condition: specify the metric, comparison, threshold, statistical period, and the number of consecutive periods. You can expand the trigger condition to view the metric trend, and based on which, set a proper threshold.
  <tr>
    <td><b>Manual Configuration </b>(Event Alarm)</td>
    <td>Create an event alarm policy to get notifications in case of service resources or underlying infrastructure exceptions</td>
  </tr>
  <tr>
    <td>Select template</td>
    <td>Choose a configured template as needed. For more information about the configurations, please see <a href="https://intl.cloud.tencent.com/document/product/248/38911">Configuring Trigger Condition Template</a>.</td>
  </tr>
        <tr>
        <td>Configure Alarm Notification (optional)</td>
        <td colspan=2>Notification Template</td>
        <td>It defaults to the preset notification template (sending the notification to the root account admin via SMS and email). Up to 3 notification templates can be bound to each alarm policy. For more information about the configurations of notification templates, see <a href="https://intl.cloud.tencent.com/document/product/248/38922">Creating Notification Template</a>.</li></td>
    </tr>
		</table>
4. Click **Complete**.





