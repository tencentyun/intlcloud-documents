When you configure a custom callback API, you can insert system variables to the API. The system automatically parses the variables when alarms are sent. The following is a list of variables that are applicable to custom callback APIs. For more information, please see [Receiving Alarm Notifications via Custom Callback APIs](https://intl.cloud.tencent.com/document/product/614/41986) and [Configuring Alarm Policy](https://intl.cloud.tencent.com/document/product/614/39574).

>! The following variables are applicable only to custom callback APIs. For more information about the custom notification content of alarm policies, please see [Notification Content Variables](https://intl.cloud.tencent.com/document/product/614/41984).
>

## Variable List

| Variable                      | Description                             | Variable Value Example                                              |
| :------------------------ | :------------------------------- | :--------------------------------------------- |
| {{.UIN}}                  | User account                         | 10000753XX27                                            |
| {{.User}}                 | Username                         | XX enterprise                                        |
| {{.Region}}               | Region                             | Guangzhou                                                    |
| {{.AlarmName}}            | Alarm policy name                     | XX policy                                                  |
| {{.AlarmID}}              | Alarm policy ID                      | alarm-74495f68-24ba-4b42-a8c1-61460721xxxx              |
| {{.LogsetName}}           | Logset name                       | XX logset                                                |
| {{.LogsetID}}             | Logset ID                        | 1c012db7-2cfd-4418-bb7b-7342c7a4xxxx                    |
| {{.TopicID}}              | Log topic ID                      | 380fe1f1-0c7b-4b0d-9d70-d514959dxxxx                    |
| {{.Condition}}            | Trigger condition                         | $1.success_counts < 100                       |
| {{.Query}}                | Monitoring statement                     | code:200 \| select count(\*) as success_counts           |
| {{.StartTime}}            | Time when the alarm is triggered for the first time | 2021-09-22 11:40:51                                 |
| {{.TriggerTime}}          | Trigger time                         | 2021-09-22 11:31:51                           |
| {{.ConsecutiveAlertNums}} | Number of consecutive alarms                     | 2                                                       |
| {{.Duration}}             | Alarm duration (minutes)             | 0                                                       |
| {{.TriggerParams}}            | Alarm trigger parameters             |  $1.success_counts=15;                                            |
| {{.CustomizeMessage}}     | Custom alarm notification content               |  -                                             |
| {{.NotifyType}}      |   Alarm notification type. 1: alarm notification; 2: alarm clearing notification     | 1     |
 

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
	"TopicID":"{{.TopicID}}",
	"LogsetName":"{{.LogsetName}}",
	"LogsetID":"{{.LogsetID}}",
	"FireTime":"{{.FireTime}}",
	"Duration":"{{.Duration}}",
	"Query":"{{.Query}}",
	"CustomizeMessage":"{{.CustomizeMessage}}"
}
```
