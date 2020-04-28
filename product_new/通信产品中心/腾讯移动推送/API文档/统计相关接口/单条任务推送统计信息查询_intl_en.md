## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.
```shell
https://api.tpns.tencent.com/v3/statistics/get_push_task_stat_channel
```
**Feature**: this API is used to query the detailed statistics for each push task, including all channel information and summary results. The channel types in `pushStatDataAll` will be changed based on their differences in terms of iOS/Android and push channels.



## Parameter Description
#### Request parameters

| Parameter Name | Required | Type | Description |
| -------- | ---- | ------ | ------ |
| pushId   | Yes   | string | Message ID |

#### Response parameters

| Parameter Name | Type | Description |
| --------------- | ------ | ------------------------------------------------------------ |
| retCode         | int    | Returned status code                                                  |
| errMsg          | string | Error message                                                     |
| pushStatDataAll | Json   | Returned results: formed by `channe`l and `pushStat`, where `channel` is the channel name. `PushStatDataAll` structure variables are shown in following table |

#### PushStatDataAll (Android)

| Parameter Name | Type   | Description           |
| ------------ | ------ | -------- |
| pushActiveUv | int    | Attempted delivery |
| pushOnlineUv | int    | Actual sent to |
| verifySvcUv  | int    | Device reached (only valid for TPNS and iOS channels. For other vendor channels, the `pushOnlineUv` metric of expected deliveries by TPNS will be used) |
|callbackVerifySvcUv | int |  Arrival receipt for vendor channel (only valid for Huawei, OPPO,  Vivo, and Mi channels. For vendor channel receipt configuration, please see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246)) |
| verifyUv     | int    | Displayed     |
| clickUv      | int    | Clicked     |
| cleanupUv    | int    | Cleared     |

#### PushStatOverviewData (iOS and macOS)

| Parameter Name | Type | Description |
| ------------ | ------ | ------------ |
| pushActiveUv | int    | Attempted delivery |
| pushOnlineUv | int    | APNs successfully received |
| verifySvcUv  | int    | Reached |
| clickUv      | int    | Clicked     |



## Samples
#### Sample request

```json
{
 "pushId": "130248"
}
```

#### Sample response

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

