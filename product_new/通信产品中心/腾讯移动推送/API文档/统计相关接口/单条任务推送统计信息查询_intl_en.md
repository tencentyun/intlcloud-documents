## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.
```shell
https://api.tpns.tencent.com/v3/statistics/get_push_task_stat_channel
```
**Feature**: this API is used to query the detailed statistics for each push task, including all channel information and summary results. The channel types in pushStatDataAll will be changed based on their differences in terms of iOS/Android and push channels.



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
| pushStatDataAll | Json   | Returned result: individual element formed by `channel` and `pushState`, where `channel` is the push channel name. `pushState` structure variables are shown in following table |

#### PushState (Android)

| Parameter Name | Type   | Description           |
| ------------------- | ---- | ------------------------------------------------------------ |
| pushActiveUv | int    | Scheduled delivery |
| pushOnlineUv | int    | Actual delivery |
| verifySvcUv         | int  | Device reached (only valid for TPNS, ROG, and FCM channels. For other vendor channels, the `pushOnlineUv` metric of actual deliveries by TPNS will be used) |
| callbackVerifySvcUv | int  | Arrival receipt for vendor channel (only valid for Huawei, OPPO, Vivo, and Mi channels. For vendor channel receipt configuration, please see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246)) |
| verifyUv     | int    | Display     |
| clickUv      | int    | Click     |
| cleanupUv    | int    | Dismissal |

>Note:
>The "all" channel in the array corresponds to the aggregated statistics.
>
>- In the aggregated statistics, the `verifySvcUv` (device reached), `verifyUv` (display), `clickUv` (click), and `cleanupUv` (dismissal) metrics only aggregates the data of the TPNS, ROG, and FCM channels.
>-  In the aggregated statistics, `pushActiveUv` (scheduled delivery) and `pushOnlineUv` (actual delivery) aggregates the data of the TPNS channel and vendor channels.
>- In the aggregated statistics, `callbackVerifySvcUv` (arrival receipt of vendor channel) aggregates the data of vendor channel's `callbackVerifySvcUv` (arrival receipt of vendor channel) + TPNS channel's `verifySvcUv` (device reached) + ROG channel's `verifySvcUv` (device reached) + FCM channel's `verifySvcUv` (device reached).
#### pushState (iOS & macOS)

| Parameter Name | Type | Description |
| ------------ | ------ | ------------ |
| pushActiveUv | int    | Scheduled delivery |
| pushOnlineUv | int    | APNs successfully received |
| verifySvcUv  | int    | Arrival |
| clickUv      | int    | Click     |

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
            "channel": "xm",
            "pushState": {
                "pushActiveUv": 1000,
                "pushOnlineUv": 1000,
                "verifySvcUv": 1000,
                "callbackVerifySvcUv": 800,
                "verifyUv": 1000,
                "clickUv": 0,
                "cleanupUv": 0
            }
        },
        {
            "channel": "mz",
            "pushState": {
                "pushActiveUv": 1000,
                "pushOnlineUv": 1000,
                "verifySvcUv": 1000,
                "callbackVerifySvcUv": 800,
                "verifyUv": 1000,
                "clickUv": 0,
                "cleanupUv": 0
            }
        },
        {
            "channel": "vivo",
            "pushState": {
                "pushActiveUv": 1000,
                "pushOnlineUv": 1000,
                "verifySvcUv": 1000,
                "callbackVerifySvcUv": 800,
                "verifyUv": 1000,
                "clickUv": 0,
                "cleanupUv": 0
            }
        },
        {
            "channel": "hw",
            "pushState": {
                "pushActiveUv": 1000,
                "pushOnlineUv": 1000,
                "verifySvcUv": 1000,
                "callbackVerifySvcUv": 800,
                "verifyUv": 1000,
                "clickUv": 0,
                "cleanupUv": 0
            }
        },
        {
            "channel": "xg",
            "pushState": {
                "pushActiveUv": 1000,
                "pushOnlineUv": 800,
                "verifySvcUv": 800,
                "callbackVerifySvcUv": 0,
                "verifyUv": 800,
                "clickUv": 300,
                "cleanupUv": 500
            }
        },
        {
            "channel": "oppo",
            "pushState": {
                "pushActiveUv": 1000,
                "pushOnlineUv": 1000,
                "verifySvcUv": 1000,
                "callbackVerifySvcUv": 800,
                "verifyUv": 1000,
                "clickUv": 0,
                "cleanupUv": 0
            }
        },
        {
            "channel": "fcm",
            "pushState": {
                "pushActiveUv": 0,
                "pushOnlineUv": 0,
                "verifySvcUv": 0,
                "callbackVerifySvcUv": 0,
                "verifyUv": 0,
                "clickUv": 0,
                "cleanupUv": 0
            }
        },
        {
            "channel": "rog",
            "pushState": {
                "pushActiveUv": 0,
                "pushOnlineUv": 0,
                "verifySvcUv": 0,
                "callbackVerifySvcUv": 0,
                "verifyUv": 0,
                "clickUv": 0,
                "cleanupUv": 0
            }
        },
        {
            "channel": "all",
            "pushState": {
                "pushActiveUv": 6000,
                "pushOnlineUv": 5800,
                "verifySvcUv": 5800,
                "callbackVerifySvcUv": 4000,
                "verifyUv": 5800,
                "clickUv": 300,
                "cleanupUv": 500
            }
        }
    ]
}
```

