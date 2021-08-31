You can create alarms to stay informed on product status change. The specific metrics will be monitored for a certain time period, and alarms will be sent at specified intervals based on the given threshold.

An alarm consists of the following components:
- Alarm name
- Alarm policy type
- Alarm trigger (under what conditions will an alarm be sent)
- Alarm object (which object will send an alarm)
- Alarm channel

This document describes how to create alarms for one or more objects, and select the objects to receive alarms.

## Basic Concepts

<table>
<thead>
<tr>
<th>Term</th>
<th>Definition</th>
</tr>
</thead>
<tbody><tr>
<td nowrap="nowrap">Alarm policy</td>
<td>It consists of alarm name, alarm policy type, alarm trigger, alarm object, and alarm channel</td>
</tr>
<tr>
<td nowrap="nowrap">Alarm policy type</td>
<td>Alarm policy type identifies policy category and corresponds to specific Tencent Cloud products. For example, if you choose the CVM policy, you can customize metric alarms for CPU utilization, disk utilization, and more</td>
</tr>
<tr>
<td nowrap="nowrap">Alarm trigger</td>
<td>An alarm trigger is a semantic condition consisting of metric, comparison, threshold, statistical period, and duration</td>
</tr>
<tr>
<td nowrap="nowrap">Alarm rule</td>
<td>It refers to the action performed when the monitoring data of a metric meets the configured alarm trigger</td>
</tr>
<tr>
<td nowrap="nowrap">Alarm policy group</td>
<td>An alarm policy group is a set of alarm rules. It is related to project and alarm policy type. Up to 15 alarm policy groups can be created in each alarm policy type for each project</td>
</tr>
<tr>
<td nowrap="nowrap">Default policy group</td>
<td>There is only one default policy group for each project in each policy type. The default group is automatically created after you purchase an instance. It can be modified but not deleted. Note: for the default alarm policy created by the system, you need to associate it with an alarm recipient group before you can receive alarm notifications</td>
</tr>
</tbody></table>







## Alarm Status
<table class="t">
<tbody><tr>
<th> <b>Alarm Status</b>
</th><th> <b>Description </b>
</th></tr>
<tr>
<td> <b>Unresolved </b>
</td><td> The alarm has not been processed or is being processed.
</td></tr>
<tr>
<td> <b>Resolved </b>
</td><td> Normal status has been restored.
</td></tr>
<tr>
<td> <b>Insufficient data</b>
</td><td> The alarm policy that triggered an alarm has been deleted.<br>CVM has been migrated from one project to another one.<br>No data reporting because Agent has not been installed or has been uninstalled.
</tbody></table>
