## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.
```shell
https://api.tpns.tencent.com/v3/statistics/get_push_task_stat_channel
```
**Feature**: This API queries the detailed statistics for each push task, including all channel information and summary results. The channel types in pushStatDataAll will be changed based on their differences in terms of iOS/Android and push channels.



## Parameter Descriptions
#### Request Parameters

| Parameter Name | Required | Type | Description |
| -------- | ---- | ------ | ------ |
| pushId   | Yes   | string | Message ID |

#### Response Parameters

| Parameter name | Type | Description |
| --------------- | ------ | ------------------------------------------------------------ |
| retCode         | int    | Returned status code                                                  |
| errMsg          | string | Error message                                                     |
| pushStatDataAll | Json   | Returned results: formed by channel and pushStat, where channel is the channel name. PushStatDataAll structure variables are shown in following table |

#### PushStatDataAll (Android)

| Parameter name | Type | Description |
| ------------ | ------ | -------- |
| pushActiveUv | int    | Planned delivery |
| pushOnlineUv | int    | Actual delivery |
| verifySvcUv  | int    | Device arrival |
| verifyUv     | int    | Display     |
| clickUv      | int    | Click     |
| cleanupUv    | int    | Clear     |

#### PushStatOverviewData (iOS & macOS)

| Parameter name | Type | Description |
| ------------ | ------ | ------------ |
| pushActiveUv | int    | Planned delivery |
| pushOnlineUv | int    | APNs successfully received |
| verifySvcUv  | int    | Arrival |
| clickUv      | int    | Click     |



## Example
#### Request Example

```json
{
 "pushId": "130248"
}
```

#### Response Example

```json

{
 "retCode": 0,
 "errMsg": "NO_ERROR",
 "pushStatDataAll": [
 {
 "channel": "mz",
 "pushState": {
 "pushActiveUv": 11,
 "pushOnlineUv": 0,
 "verifySvcUv": 0,
 "verifyUv": 0,
 "clickUv": 0,
 "cleanupUv": 0
 }
 },
 {
 "channel": "oppo",
 "pushState": {
 "pushActiveUv": 3,
 "pushOnlineUv": 2,
 "verifySvcUv": 2,
 "verifyUv": 2,
 "clickUv": 0,
 "cleanupUv": 0
 }
 },
 {
 "channel": "rog",
 "pushState": {
 "pushActiveUv": 3,
 "pushOnlineUv": 2,
 "verifySvcUv": 1,
 "verifyUv": 1,
 "clickUv": 0,
 "cleanupUv": 0
 }
 },
 {
 "channel": "oppo",
 "pushState": {
 "pushActiveUv": 1,
 "pushOnlineUv": 0,
 "verifySvcUv": 0,
 "verifyUv": 0,
 "clickUv": 0,
 "cleanupUv": 0
 }
 },
 {
 "channel": "xg",
 "pushState": {
 "pushActiveUv": 3,
 "pushOnlineUv": 2,
 "verifySvcUv": 1,
 "verifyUv": 1,
 "clickUv": 0,
 "cleanupUv": 0
 }
 },
 {
 "channel": "xm",
 "pushState": {
 "pushActiveUv": 7,
 "pushOnlineUv": 0,
 "verifySvcUv": 0,
 "verifyUv": 0,
 "clickUv": 0,
 "cleanupUv": 0
 }
 },
 {
 "channel": "all",
 "pushState": {
 "pushActiveUv": 28,
 "pushOnlineUv": 6,
 "verifySvcUv": 1,
 "verifyUv": 1,
 "clickUv": 0,
 "cleanupUv": 0
 }
 }
 ]
}
```

