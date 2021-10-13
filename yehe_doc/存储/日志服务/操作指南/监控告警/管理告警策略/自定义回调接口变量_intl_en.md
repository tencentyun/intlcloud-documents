When you configure a custom callback API, you can insert system variables to the API. The system automatically parses the variables when alarms are sent. The following is a list of variables that are applicable to custom callback APIs. For more information, please see [Receiving Alarm Notifications via Custom Callback APIs](https://intl.cloud.tencent.com/document/product/614/41986) and [Configuring Alarm Policy](https://intl.cloud.tencent.com/document/product/614/39574).

## Variable List

<table>
	<thead>
		<tr><th>Variable</th><th>Description</th></tr>
	</thead>
	<tbody>
		<tr><td>{{.UIN}}</td><td>User account</td></tr>
		<tr><td>{{.User}}</td><td>Username</td></tr>
		<tr><td>{{.Region}}</td><td>Region</td></tr>
		<tr><td>{{.AlarmID}}</td><td>Alarm policy ID</td>
		</tr><tr><td>{{.AlarmName}}</td><td>Alarm policy name</td></tr>
		<tr><td>{{.Condition}}</td><td>Trigger condition and parameter</td></tr>
		<tr><td>{{.TriggerTime}}</td><td>Trigger time</td></tr>
		<tr><td>{{.ConsecutiveAlertNums}}</td><td>Number of consecutive alarms</td></tr>
		<tr><td>{{.TopicName}}</td><td>Log topic name</td></tr>
		<tr><td>{{.TopicID}}</td><td>Log topic ID</td></tr>
		<tr><td>{{.LogsetName}}</td><td>Logset name</td></tr>
		<tr><td>{{.LogsetID}}</td><td>Logset ID</td></tr>
		<tr><td>{{.FireTime}}</td><td>Time when the alarm is triggered for the first time</td></tr>
		<tr><td>{{.Duration}}</td><td>Alarm duration</td></tr>
		<tr><td>{{.Query}}</td><td>Monitoring statement</td></tr>
		<tr><td>{{.CustomizeMessage}}</td><td>Custom alarm notification content</td></tr>
	</tbody>
</table>


## Example

Custom API callback configuration:

Request header: `Content-Type: application/json `

Request content:
```json
{
	"UIN":"{{.UIN}}",
	"User":"{{.User}}",
	"Region":"{{.Region}}",
	"AlarmID":"{{.AlarmID}}",
	"AlarmName":"{{.AlarmName}}",
	"Condition":"{{.Condition}}",
	"TriggerTime":"{{.TriggerTime}}",
	"ConsecutiveAlertNums":"{{.ConsecutiveAlertNums}}",
	"TopicName":"{{.TopicName}}",
	"TopicID":"{{.TopicID}}",
	"LogsetName":"{{.LogsetName}}",
	"LogsetID":"{{.LogsetID}}",
	"FireTime":"{{.FireTime}}",
	"Duration":"{{.Duration}}",
	"Query":"{{.Query}}",
	"CustomizeMessage":"{{.CustomizeMessage}}"
}
```
