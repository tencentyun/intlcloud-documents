## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.

The API request address corresponds to the service access point one by one; therefore, please select the request address corresponding to your application service access point.

Service access point in Guangzhou:
```shell
https://api.tpns.tencent.com/v3/statistics/get_push_task_stat_channel
```
Service access point in Hong Kong (China):
```shell
https://api.tpns.hk.tencent.com/v3/statistics/get_push_task_stat_channel
```
Service access point in Singapore:
```shell
https://api.tpns.sgp.tencent.com/v3/statistics/get_push_task_stat_channel
```
Service access point in Shanghai:
```shell
https://api.tpns.sh.tencent.com/v3/statistics/get_push_task_stat_channel
```
**Feature**: this API is used to query the detailed statistics for each push task, including all channel information and summary results. The channel types in pushStatDataAll will be changed based on their differences in terms of iOS/Android and push channels.



## Parameter Description
#### Request parameters

| Parameter Name | Required | Type | Description |
| -------- | ---- | ------ | ------ |
| pushId   | Yes   | String | Message ID |

#### Response parameters

| Parameter Name | Type | Description |
| --------------- | ------ | ------------------------------------------------------------ |
| retCode         | Integer    | Returned status code                                                  |
| errMsg          | String | Error message                                                     |
| pushStatDataAll | Object   | Returned result: individual element formed by `channel` and `pushState`, where `channel` is the push channel name. `pushState` structure variables are shown in following table |

#### PushState (Android)

| Parameter Name | Type   | Description           |
| ------------------- | ---- | ------------------------------------------------------------ |
| pushActiveUv        | Integer  | Scheduled<br/>Number of available devices connected to the Internet within 90 days that meet the target push conditions and on which the notification bar is enabled.                                                |
| pushOnlineUv        | Integer  | Sent<br/>Actual number of available devices in the scheduled devices that have been delivered to vendor channels or to process online terminal using TPNS channel.                                                   |
| arrivalUv         | Integer  | Devices reached (including arrival receipts for TPNS and vendor channels. For the Huawei and Meizu channels, you need to configure the arrival receipts manually. For more information, see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246)）|
| verifySvcUv         | Integer  | Devices reached (only for TPNS, ROG and FCM channels.  Use the TPNS `pushOnlineUv` metric for other vendor channels.)**Note:** This field will be deprecated later. Use `arrivalUv ` to get the arrival data |
| callbackVerifySvcUv | Integer  | Vendor channel arrival receipt (For the Huawei and Meizu channels, you need to configure the arrival receipts manually. For more information, see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246)）**Note:** This field will be deprecated later. Use `arrivalUv ` to get the arrival data|
| verifyUv            | Integer  | Display (obsolete)|
| clickUv      | Integer    | Click     |
| cleanupUv    | Integer    | Dismissal |

>Note:
>The "all" channel in the array corresponds to the aggregated statistics.
>
>-  In the aggregated statistics, the `verifySvcUv` (device reached), `verifyUv` (display), `clickUv` (click), and `cleanupUv` (dismissal) metrics only aggregates the data of the TPNS, ROG, and FCM channels.
>-  In the aggregated statistics, `pushActiveUv` (scheduled delivery) and `pushOnlineUv` (actual delivery) aggregates the data of the TPNS channel and vendor channels.
>-  In the aggregated statistics, `callbackVerifySvcUv` (arrival receipt of vendor channel) aggregates the data of vendor channel's `callbackVerifySvcUv` (arrival receipt of vendor channel) + TPNS channel's `verifySvcUv` (device reached) + ROG channel's `verifySvcUv` (device reached) + FCM channel's `verifySvcUv` (device reached).
#### pushState (iOS and macOS)

| Parameter Name | Type | Description |
| ------------ | ------ | ------------ |
| pushActiveUv | Integer    | Scheduled delivery |
| pushOnlineUv | Integer    | APNs successfully received |
| verifySvcUv  | Integer    | Arrival |
| clickUv      | Integer    | Click     |

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
                "arrivalUv": 1000,
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
                "arrivalUv": 1000,
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
                "arrivalUv": 1000,
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
                "arrivalUv": 1000,
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
                "arrivalUv": 1000,
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
                "arrivalUv": 1000,
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
                "arrivalUv": 0,
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
                "arrivalUv": 0,
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
                "arrivalUv": 5800,
                "verifyUv": 5800,
                "clickUv": 300,
                "cleanupUv": 500
            }
        }
    ]
}
```

