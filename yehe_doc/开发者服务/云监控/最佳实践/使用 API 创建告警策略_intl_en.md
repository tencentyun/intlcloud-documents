This document describes how to use <dx-tag-link link="https://intl.cloud.tencent.com/document/product/248/39326" tag="API">CreateAlarmPolicy </dx-tag-link>  and  <dx-tag-link link="https://intl.cloud.tencent.com/document/product/248/35985" tag="API">Binding Policy Object </dx-tag-link> to create alarm policies and bind alarm objects.



<span id="preparationsteps"></span>

## Preparations

Before calling the <dx-tag-link link="https://intl.cloud.tencent.com/document/product/248/39326" tag="API">Create Alarm Policy</dx-tag-link> , you need to prepare the following information.



#### Preparing personal key

 1. Go to the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM console.
 2. Click **Show** to get the `SecretKey`.


> ?If no key has been created, please click **Create Key** to create one.

#### Preparing alarm policy type

 You can query all policy types through the  <dx-tag-link link="https://intl.cloud.tencent.com/document/product/248/39319" tag="API">DescribeAllNamespaces</dx-tag-link>  in the following steps:
1. Log in to the [API Explorer console](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=DescribeAllNamespaces) and enter the input parameters as shown below:
<table>
	<tr>
	<th>Parameter</th>
	<th>Description</th>
	</tr>
	<tr>
		<td>SecretId, SecretKey</td>
		<td>Enter the prepared `SecretId` and `SecretKey`</td>
	</tr>
	<tr>
		<td>Region</td>
		<td>Select the corresponding region</td>
	</tr>
	<tr>
		<td>SceneType</td>
		<td>Enter `ST_ALARM`</td>
	</tr>
	<tr>
		<td>Module</td>
		<td>Enter `monitor`</td>
	</tr>
	<tr>
		<td>MonitorTypes.N </td>
		<td>Optional</td>
	</tr>
</table>

2. Click **Online Call** > **Send Request** to get the response, where `Response.QceNamespacesNew.N.Id` is the `Namespace` required by alarm policy creation. 


  >! Here, `Namespace` is the alarm policy type, which is different from the Tencent Cloud service namespace used to pull monitoring data.


#### Preparing metric list
 You can query all alarm metrics under the policy type through the <dx-tag-link link="https://intl.cloud.tencent.com/document/product/248/39322" tag="API">DescribeAlarmMetrics</dx-tag-link>.

1. Log in to the [API Explorer console](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=DescribeAlarmMetrics) and enter the input parameters as shown below:
<table>
	<tr>
	<th>Parameter</th>
	<th>Description</th>
	</tr>
	<tr>
		<td>SecretId, SecretKey</td>
		<td>Enter the prepared `SecretId` and `SecretKey`</td>
	</tr>
	<tr>
		<td>Region</td>
		<td>Select the corresponding region</td>
	</tr>
	<tr>
		<td>Module</td>
		<td>Enter `monitor`</td>
	</tr>
		<tr>
		<td>MonitorType</td>
		<td>Enter `MT_QCE`</td>
	</tr>
	<tr>
		<td>Namespace</td>
		<td>Enter the alarm policy type obtained in the "Preparing alarm policy type" step, i.e., `Response.QceNamespacesNew.N.Id` in the returned result</td>
	</tr>
</table>
2. Click **Online Call** > **Send Request** on the right to get the response, where `Response.Metrics.N` lists all the alarm metrics under the policy type. 

#### Preparing event list
You can query all the alarm events under the policy type through the  <dx-tag-link link="https://intl.cloud.tencent.com/document/product/248/39324" tag="API">DescribeAlarmEvents</dx-tag-link>.

1. Log in to the [API Explorer console](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=DescribeAlarmEvents&SignVersion=) and enter the input parameters as shown below:

<table>
	<tr>
	<th>Parameter</th>
	<th>Description</th>
	</tr>
	<tr>
		<td>SecretId, SecretKey</td>
		<td>Enter the prepared `SecretId` and `SecretKey`</td>
	</tr>
	<tr>
		<td>Region</td>
		<td>Select the corresponding region</td>
	</tr>
	<tr>
		<td>Module</td>
		<td>Enter `monitor`</td>
	</tr>
	<tr>
		<td>Namespace</td>
		<td>Enter the alarm policy type obtained in the "Preparing alarm policy type" step, i.e., `Response.QceNamespacesNew.N.Id` in the returned result</td>
	</tr>
</table>
2. Click <b>Online Call</b> > <b>Send Request</b> to get the response, where `Response.Events.N.EventName` is the `EventName` required by alarm policy creation.



## Directions

This document describes how to use APIs such as  <dx-tag-link link="https://intl.cloud.tencent.com/document/product/248/39326" tag="API">CreateAlarmPolicy</dx-tag-link> to create an alarm policy for CVM - basic monitoring with the following example.

<span id="createalarm"></span>

### Creating alarm policy

1. Log in to the [API Explorer console](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=CreateAlarmPolicy&SignVersion=).
2. Copy the [prepared personal key](#preparationsteps) into the corresponding `SecretId` and `SecretKey` text boxes.
3. Find **Region** in the **Input Parameters** section and select the relevant region.
4. Enter `monitor` in **Module**, a custom policy name in **PolicyName**, and `MT_QCE` in **MonitorType**.
5. Enter the alarm policy type obtained in the [Preparing alarm policy type](#preparationsteps) step above in **Namespace**. For example, the alarm policy type of CVM - basic monitoring is `cvm_device`.
6. In the CVM - basic monitoring use case, `Remark` and `Enable` are optional, while `ProjectId` is required.
	- **Remark**: remark, which is optional.
	- **Enable**: whether to enable the alarm policy. 0 indicates to disable, 1 indicates to enable, and the default value is 1. This parameter is optional.
	- **ProjectId**: project ID, which should be **0** for CVM - basic monitoring.
> ? `ProjectId` is the project ID. -1 indicates no project, 0 indicates the default project, and the default value is -1. This parameter is optional depending on the policy type. For example, some alarm policy types don't have the concept of project (such as VPC), and the default value `-1` can be used. If the alarm policy type has the concept of project (such as CVM - basic monitoring), an error will be reported if the default value `-1` is passed in, and the input parameter should be changed to "0".
7. Configure `Condition` as shown below:
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>IsUnionRule</td>
<td>Yes</td>
<td>Metric trigger condition operator. Valid values: 0 (OR), 1 (AND). OR means that the alarm will be sent when any condition is triggered, while AND means that the alarm will be sent when all conditions are triggered</td>
</tr>
<tr>
<td>Rules.N</td>
<td>Yes</td>
<td>List of alarm trigger conditions, which can be configured by referring to the `AlarmPolicyRule` parameter <ul><li> <strong>MetricName</strong>: enter the `MetricName` (Metrics.N.MetricName) returned in the <a href="#preparationsteps">Preparing metric list</a> step </li><li><strong>Period</strong>: enter the `Period` (Metrics.N.MetricConfig.Period) returned in the <a href="#preparationsteps">Preparing metric list</a> step </li><li><strong>Operator</strong>: enter the `Operator` (Metrics.N.MetricConfig.Operator) returned in the <a href="#preparationsteps">Preparing metric list</a> step </li><li><strong>Value</strong>: enter a threshold without the unit, such as 80</li><li><strong>ContinuePeriod</strong>: enter the `ContinuePeriod` (Metrics.N.MetricConfig.ContinuePeriod) returned in the <a href="#preparationsteps">Preparing metric list</a> step </li><li><strong>NoticeFrequency</strong>: set the alarm frequency in seconds. Parameter description: alarm interval in seconds. Valid values: 0 (do not repeat), 300 (alarm once every 5 minutes), 600 (alarm once every 10 minutes), 900 (alarm once every 15 minutes), 1800 (alarm once every 30 minutes), 3600 (alarm once every hour), 7200 (alarm once every 2 hours), 10800 (alarm once every 3 hours), 21600 (alarm once every 6 hours), 43200 (alarm once every 12 hours), 86400 (alarm once every day) </li><li><strong>IsPowerNotice</strong>: set whether the alarm frequency grows exponentially. Valid values: 0 (no), 1 (yes) </li><li>Other parameters can be left empty </li></ul></td>
</tr>
</tbody></table>
8. If you want to trigger an event alarm, you need to configure the `EventCondition` parameter. Under `EventCondition`, you **only need** to enter the **`EventName`** obtained in the <a href="#preparationsteps">Preparing event list</a> step in `Rules.N.MetricName`, and you can leave other parameters empty.
9. Enter the alarm notification template ID in `NoticeIds.N`, such as notice-qvq836vc, which can be obtained through the <dx-tag-link link="https://intl.cloud.tencent.com/document/product/248/39300" tag="API">DescribeAlarmNotices</dx-tag-link>.
10. After entering the above parameters, click **Online Call** > **Send Request**. The following figure shows the successful creation of the alarm policy for CVM - basic monitoring.

11. After the creation is successful, you can view the alarm policy on the [Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy) page in the Cloud Monitor console.





### Binding alarm object

1. Log in to the [API Explorer console](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=BindingPolicyObject&SignVersion=).
2. Copy the [prepared personal key](#spreparationsteps) into the corresponding `SecretId` and `SecretKey` text boxes.
3. Find **Region** in the **Input Parameters** section and select the relevant region.
4. Enter `monitor` in **Module**.
5. Enter 0 in **GroupId**.
6. Enter either the `InstanceGroupId` or `Dimensions` as detailed below:
	- **InstanceGroupId:** instance group ID. If you want to bind alarm objects by instance group, you need to pass in the instance group ID (such as 1234), which can be found on the [instance group](https://console.cloud.tencent.com/monitor/instanceGroup) page in the Cloud Monitor console by clicking the corresponding instance name as shown below:

	- **Dimensions.N:** if you wany to bind an alarm policy by instance ID, you need to enter `Dimensions` as detailed below:
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>RegionId, Region</td>
<td>Please see the instance region description; for example, for the Guangzhou region, `RegionId` is `1`, and `Region` is `gz`</td>
</tr>
<tr>
<td>Dimensions</td>
<td>Enter the CVM instance ID, which can be obtained through the <dx-tag-link link="https://cloud.tencent.com/document/product/213/15728" tag="API">DescribeInstances</dx-tag-link> API. The input parameter format is {"unInstanceId":"ins-xxxxxxxx'"}</td>
</tr>
<tr>
<td>EventDimensions</td>
<td>Enter the globally unique instance ID, which can be obtained through the <dx-tag-link link="https://cloud.tencent.com/document/product/213/15728" tag="API">DescribeInstances</dx-tag-link> API. The input parameter format is {"uuid":"9d51a69e-0e4a-4120-ae58-9c073c851e24"}</td>
</tr>
</tbody></table>
7. Enter the `PolicyId` (Response.PolicyId) returned in the [Creating alarm policy](#createalarm) step in `PolicyId`, such as `policy-zg2sk27j`.
8. After entering the above parameters, click **Online Call** > **Send Request**. The following figure shows that the alarm policy is successfully bound.

9. After the creation is successful, you can view the number of instances associated with the corresponding alarm policy on the [Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy) page in the Cloud Monitor console.




