## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.
```shell
http://api.tpns.tencent.com/v3/statistics/get_push_channel_stat_overview
```
**Feature**: this API is used to query the daily push conversion summary within a certain time period by push channel.

## Parameter Description
#### Request parameters

| Parameter Name | Required | Type | Description |
| --------- | ---- | ------ | ------------------------------------------------------------ |
| startDate | Yes   | string | Query start date<li>Format: YYYYMMDD<li>Limit: only data in the last 30 days can be queried |
| endDate   | Yes   | string | Query end date. Format: YYYYMMDD                                 |


#### Response parameters

| Parameter Name | Type | Description |
| ------------------- | --------- | ------------------------------------------------------------ |
| retCode         | int    | Returned status code                                                  |
| errMsg          | string | Error message                                                     |
| pushDateChannelStat | JsonArray | Returned result: result array by day. <br/>Individual elements in the array represent daily statistics by channel, formed by `date` and `channelDatas`. The element structure of `channelDatas` is as follows |


#### channelDatas

| Parameter Name | Type   | Description           |
| --------- | ------ | ------------------------------------------------------------ |
| channel   | string | Push channel name. <br>  xg: TPNS channel<br> hw: Huawei channel<br> xm: Mi channel<br> mz: Meizu channel<br>oppo: OPPO channel<br> vivo: Vivo channel<br> apns: APNs channel<br> fcm: FCM channel |
| pushState | Json   | Push funnel statistics. For the data structures, please see `pushState` below |





#### pushState (Android)

| Parameter Name | Type   | Description           |
| ------------------- | ---- | ------------------------------------------------------------ |
| pushActiveUv | int    | Scheduled delivery |
| pushOnlineUv | int    | Actual delivery |
| verifySvcUv         | int  | Device reached (only valid for TPNS and iOS APNs channels. For other vendor channels, the `pushOnlineUv` metric of actual deliveries by TPNS will be used) |
| callbackVerifySvcUv | int  | Arrival receipt for vendor channel (only valid for Huawei, OPPO, Vivo, and Mi channels. For vendor channel receipt configuration, please see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246)) |
| verifyUv     | int    | Display     |
| clickUv      | int    | Click     |
| cleanupUv    | int    | Dismissal |

>Note:
>The "all" channel in the array corresponds to the aggregated statistics.
>
>-  In the aggregated statistics, the `verifySvcUv` (device reached), `verifyUv` (display), `clickUv` (click), and `cleanupUv` (dismissal) metrics only aggregates the data of the TPNS and ROG channels.
>-  In the aggregated statistics, `pushActiveUv` (scheduled delivery) and `pushOnlineUv` (actual delivery) aggregates the data of the TPNS channel and vendor channels.
>-  In the aggregated statistics, `callbackVerifySvcUv` (arrival receipt of vendor channel) aggregates the data of `verifySvcUv` (device reached) of the TPNS channel and `callbackVerifySvcUv` (arrival receipt of vendor channel) of vendor channels.




#### pushState (iOS)

| Parameter Name | Type   | Description           |
| ------------ | ---- | ------------- |
| pushActiveUv | int  | Scheduled delivery      |
| pushOnlineUv | int  | Successful APNs receipt |
| verifySvcUv  | int  | Arrival          |
| clickUv      | int  | Click |



## Samples
#### Sample request
```json
{
    "startDate": "20200216",
    "endDate": "20200216"
}
```

#### Sample response
```json
{
    "retCode": 0,
    "errMsg": "NO_ERROR",
    "pushDateChannelStat": [
        {
            "date": "20200216",
            "channelDatas": [
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
                    "channel": "all",
                    "pushState": {
                        "pushActiveUv": 4000,
                        "pushOnlineUv": 3800,
                        "verifySvcUv": 3800,
                        "callbackVerifySvcUv": 2400,
                        "verifyUv": 3800,
                        "clickUv": 300,
                        "cleanupUv": 500
                    }
                }
            ]
        }
    ]
}
```
