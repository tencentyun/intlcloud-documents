>!This document describes the access management feature of **SMS**. For more information on access management for other Tencent Cloud services, please see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

The core feature of CAM is to **allow or forbid an account to perform certain operations or manipulate certain resources**. SMS access management supports [resource-level authorization](https://intl.cloud.tencent.com/document/product/598/10588#.E7.AE.80.E4.BB.8B). The resource granularity is the SMS application, and the operation granularity is the [TencentCloud API](https://intl.cloud.tencent.com/product/api), including [API 3.0](https://intl.cloud.tencent.com/document/product/382/34689) and APIs that may be used when the SMS console is accessed.

If you need to manage access to SMS, please log in to the Tencent Cloud [root account](https://intl.cloud.tencent.com/document/product/598/34899) and use a [preset policy](https://intl.cloud.tencent.com/document/product/382/38455) or a [custom policy](https://intl.cloud.tencent.com/document/product/382/38456) to complete the specific authorization operations.

## Authorizable Resource Types
The authorizable resource type in SMS access management is the application.

## APIs Supporting Resource-Level Authorization
SMS supports resource-level authorization for all console APIs listed in this section, but not for server APIs. The syntax descriptions of the resources manipulated by such APIs in the [authorization policy syntax](https://intl.cloud.tencent.com/document/product/382/38456#.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95) are identical, as detailed below:
- Grant the permission to access all applications: `qcs::sms::uin/$ownerUin:app/*`.
- Grant the permission to access a single application: `qcs::sms::uin/$ownerUin:app/$BizId`.

## Console API Actions

| API Name | Applicable Module | Feature Description |
|-----------------------------|--------------------------------------------------------|-------------|
| DescribeAppList             | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Application List | Gets the application list |
| DescribeAppInfo             | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Application List > Application Info | Gets the application information |
| ModifyAppInfo               | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Application List > Application Info | Edits the application information |
| ModifyAppStatus             | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Application List | Enables/Disables the application |
| DeleteAppInfo               | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Application List | Deletes the application |
| DescribeWarningThreshold    | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Over-limit Delivery Notification | Gets the over-limit delivery notification |
| ModifyWarningThreshold      | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Over-limit Delivery Notification | Edits the over-limit delivery notification |
| DescribeFreqRule            | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Delivery Rate Limit | Gets the delivery rate limit |
| ModifyFreqRule              | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Delivery Rate Limit | Edits the delivery rate limit |
| DescribeCallbackInfo        | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Event Callback Configuration | Gets the callback configuration |
| ModifyCallbackInfo          | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Event Callback Configuration | Edits the callback configuration |
| DescribeFrequencyWhiteList  | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Rate Limit Allowlist | Gets the rate limit allowlist |
| AddFrequencyWhiteList       | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Rate Limit Allowlist | Adds the rate limit allowlist |
| DeleteFrequencyWhiteList    | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Rate Limit Allowlist | Deletes the rate limit allowlist |
| DescribeNewsReceiver        | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Notifications & Alarms | Gets the alarm contact information |
| AddNewsReceiver             | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Notifications & Alarms | Adds the alarm contact information |
| ModifyNewsReceiver          | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Notifications & Alarms | Edits the alarm contact information |
| DeleteNewsReceiver          | [SMS console](https://console.cloud.tencent.com/smsv2) > Applications > Notifications & Alarms | Deletes the alarm contact information |
| ModifyTaskStatusStart       | [SMS console](https://console.cloud.tencent.com/smsv2) > Mainland China SMS/Global SMS > Bulk SMS | Starts the instant or scheduled delivery task |
| ModifyTaskStatusStop        | [SMS console](https://console.cloud.tencent.com/smsv2) > Mainland China SMS/Global SMS > Bulk SMS | Stops the instant delivery task |
| CancelSendSMSTask           | [SMS console](https://console.cloud.tencent.com/smsv2) > Mainland China SMS/Global SMS > Bulk SMS | Cancels the scheduled delivery task |


>!For an API that does not support resource-level permission control, you can still grant a user the permission to use it through a [custom policy](https://intl.cloud.tencent.com/document/product/382/38456), but you must specify `*` as the resource element in the policy statement.

## CAM Module Update

The CAM module of SMS has been updated from "consolesms" to "sms". If your Tencent Cloud account has granted a sub-account API permissions of the "consolesms" module in a preset policy, the sub-account will be automatically bound to the corresponding API permissions of the "sms" module. If a custom policy associated with a sub-account contains an API of the "consolesms" module, you need to replace the "consolesms" API with the corresponding "sms" API when updating the policy syntax subsequently. The following are the API mapping relationships:

| Legacy consolesms API | Mapped new sms API |
|-------------------------------------------|-----------------------------|
| SMS\_GetAPPList                           | DescribeAppList            |
| SMS\_GetAPPInfo                           | DescribeAppInfo            |
| SMS\_GetWarningThreshold                  | DescribeWarningThreshold    |
| SMS\_GetFreqRule                          | DescribeFreqRule            |
| SMS\_GetCallbackList                      | DescribeCallbackInfo        |
| SMS\_GetFrqWhiteList                      | DescribeFrequencyWhiteList |
| SMS\_GetNewsReceiver                      | DescribeNewsReceiver       |
| SMS\_GetBlackListByQappid                 | DescribeBlackList           |
| SMS\_SendSMSResultStatisticQuery\_export  | DescribeSmsResultFile       |
| SMS\_Statistic\_QuerySMS\_ByAppid\_export | DescribeSmsRecordFile       |
| SMS\_StatisticQueryByQAppid               | DescribeStatisticQuery      |
| SMS\_QuerySendSMSByQAppid                 | DescribeSendSmsRecord       |
| SMS\_GetPkgAutoRenew                      | DescribePkgAutoRenew        |
| SMS\_QueryDumpLogTask                     | DescribeQueryDumpLogTask    |
| SMS\_QuerySendSMSDumpLogTask              | DescribeSendSmsDumpLogTask  |
| SMS\_CancelDumpLogTask                    | CancelDumpLogTask           |
| SMS\_AddDumpLogTask                       | AddDumpLogTask              |
| SMS\_GetWarningThreshold                  | DescribeWarningThreshold    |
| SMS\_StatisticNationCode                  | DescribeNationCodeStatistic |
| SMS\_SendSMSResultStatisticQuery          | DescribeSendSMSResult       |
| SMS\_Stat\_InnerQuery\_Reply              | DescribeInnerSMSReply       |
| SMS\_QuerySendSMSTaskSummary              | DescribeSendSMSTaskSummary  |
| SMS\_StatisticMonth                       | DescribeMonthStatistic      |
| SMS\_QuerySendSMSStatistic                | DescribeSendSMSStatistic    |
| SMS\_QuerySendSMSDetail                   | DescribeSendSMSDetail       |
| SMS\_QuerySmsPkgRemain                    | DescribeSmsPkgRemain        |
| SMS\_GetPackageList                       | DescribePackageList         |
| SMS\_UnsubscribeQuery                     | DescribeUnsubscribe         |
| SMS\_ReceiptAnalysis                      | DescribeReceiptResult       |
| SMS\_GetTPLSignInfo                       | DescribeTPLSignInfo         |
| SMS\_GetTPLSignList                       | DescribeTPLSignList         |


Because of the console version upgrade, some APIs in the CAM module "consolesms" have been disused. If the following APIs are contained in the custom policies associated with your sub-accounts, please delete the relevant content in the policy syntax:

| API | Status |
|-------------------------------------------|-----------------------------|
| SMS\_Stat\_InnerQuery\_export             | Disused                        |
| SMS\_GetConsoleFlag                       | Disused                        |
| SMS\_IsWhiteDumpAppid                     | Disused                        |
| SMS\_IsWhiteAppId                         | Disused                        |
| SMS\_QueryBill\_export                    | Disused                        |
| SMS\_CheckAppidBizid                      | Disused                        |
| SMS\_GetAllBizList                        | Disused                        |
| SMS\_GetSMSNotice                         | Disused                        |
| Voice\_GetSelfAccountTypes                | Disused                        |
| Voice\_GetAccountTypeInfo                 | Disused                        |
| Voice\_GetBizTypes                        | Disused                        |
| Voice\_GetBizAndAccountTypeInfo           | Disused                        |
| SMS\_GetServiceState                      | Disused                        |
| SMS\_StatisticQueryIOTAnalysis            | Disused                        |
| SMS\_StatisticQueryIOTByOper              | Disused                        |
| SMS\_StatisticQueryIOT                    | Disused                        |
| SMS\_Stat\_InnerQueryVoice                | Disused                        |
| SMS\_StatisticQueryEx                     | Disused                        |
| SMS\_StatisticQueryNew                    | Disused                        |
| SMS\_GetNewsReceiverFlag                  | Disused                        |
| SMS\_QueryTemplateStatisticEx             | Disused                        |
| SMS\_QueryTemplateStatistic               | Disused                        |
| SMS\_QueryBill                            | Disused                        |
| SMS\_QuerySendSMSRemain                   | Disused                        |
| SMS\_QuerySendSMS                         | Disused                        |
| SMS\_IsWhiteUin                           | Disused                        |
| SMS\_GetBlackList                         | Disused                        |
| SMS\_Statistic\_QuerySMS\_export          | Disused                        |
| SMS\_GetSendList                          | Disused                        |
| SMS\_GetReceiver                          | Disused                        |
| SMS\_Query\_Black                         | Disused                        |



