When configuring custom alarm content, you can insert system variables. The system automatically parses the variables when alarms are sent.

>! The following variables are applicable only to custom notification content of alarm policies. For more information about custom callbacks, please see [Custom Callback API Variables](https://intl.cloud.tencent.com/document/product/614/41985).
>

## Variable List

| Variable                      | Description                             | Variable Value Example                                              |
| :------------------------ | :------------------------------- | :------------------------------------------------------- |
| {{.UIN}}                  | User account                         | 10000753XX27                                            |
| {{.Nickname}}             | Username                         | XX enterprise                                                  |
| {{.Region}}               | Region                             | Guangzhou                                                    |
| {{.AlertName}}            | Alarm policy name                     | XX policy                                                  |
| {{.AlertID}}              | Alarm policy ID                      | alarm-74495f68-24ba-4b42-a8c1-61460721xxxx              |
| {{.LogsetName}}           | Logset name                       | XX logset                                                |
| {{.LogsetId}}             | Logset ID                        | 1c012db7-2cfd-4418-bb7b-7342c7a4xxxx                    |
| {{.TopicName}}            | Log topic name                     | XX log topic                                              |
| {{.TopicId}}              | Log topic ID                      | 380fe1f1-0c7b-4b0d-9d70-d514959dxxxx                    |
| {{.Trigger}}              | Trigger condition                         | $1.success_counts < 100                                 |
| {{.Query}}                | Alarm execution statement                     | code:200 \| select count(\*) as success_counts           |
| {{.HappenThreshold}}      | Number of times the alarm trigger condition is continuously met    | 1                                                       |
| {{.AlertThreshold}}       | Alarm interval (minutes)             | 15                                                      |
| {{.StartTime}}           | Time when the alarm is triggered for the first time      | 2021-09-22 11:40:51                                                    |
| {{.NotifyTime}}           | Notification time                         | 2021-09-22 11:40:51                                     |
| {{.ConsecutiveAlertNums}} | Number of consecutive alarms                     | 2                                                       |
| {{.Duration}}             | Alarm duration (minutes)             | 0                                                       |
| {{.TriggerParams}}        | Alarm trigger parameters                   | $1.success_counts=5;                    |
| {{.DetailUrl}}            | Alarm details page link (login-free)       | https://alarm.cls.tencentcs.com/CJNmxxxx                |
| {{.QueryUrl}}             | Search and analysis link for the first execution statement     | https://alarm.cls.tencentcs.com/Olw8xxxx                |
| {{.AlertHistoryUrl}}      | Link for alarm history query             | https://console.cloud.tencent.com/cls/alarm/history?xxx |
