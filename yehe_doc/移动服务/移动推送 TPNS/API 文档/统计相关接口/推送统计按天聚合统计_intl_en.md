## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.

```plaintext
request address/v3/statistics/get_push_channel_stat_overview
```
The API request address is corresponding to the service access point. Select the [request address](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

**Feature**: this API is used to query the daily push conversion summary within a certain time period by push channel.

## Parameter Description
#### Request parameters

| Parameter Name | Required | Type | Description |
| --------- | ---- | ------ | ------------------------------------------------------------ |
| startDate | Yes   | String | Query start date<li>Format: YYYYMMDD<li>Limit: only data in the last 30 days can be queried |
| endDate   | Yes   | String | Query end date. Format: YYYYMMDD                                 |


#### Response parameters

| Parameter Name | Type | Description |
| ------------------- | --------- | ------------------------------------------------------------ |
| retCode      | Integer   | Returned status code                             |
| errMsg              | String    | Error message                                                     |
| pushDateChannelStat | Array | Returned result: result array by day. <br/>Individual elements in the array represent daily statistics by channel, formed by `date` and `channelDatas`. The element structure of `channelDatas` is as follows. |


#### channelDatas

| Parameter Name | Type   | Description           |
| --------- | ------ | ------------------------------------------------------------ |
| channel   | String | Push channel name <br>  xg: TPNS channel<br> hw: Huawei channel<br> xm: Mi channel<br> mz: Meizu channel<br>oppo: OPPO channel<br> vivo: Vivo channel<br> apns: APNs channel<br> fcm: FCM channel<br> rog: ROG channel |
| pushState | Object   | Push funnel statistics. For the data structures, please see `pushState` below. |


#### pushState (Android)

| Parameter Name | Type   | Description           |
| ------------------- | ---- | ------------------------------------------------------------ |
| pushActiveUv        | Integer  | Scheduled<br/>Number of available devices connected to the Internet within 90 days that meet the target push conditions and on which the notification bar is enabled.                                                |
| pushOnlineUv        | Integer  | Sent<br/>Actual number of available devices in the scheduled devices that have been delivered to vendor channels or to process online terminal using TPNS channel.                                                   |
| arrivalUv         | Integer  | Number of reached devices (including arrival receipts for the TPNS and vendor channels. For the Huawei and Meizu channels, you need to add a configuration item for arrival receipt manually. For more information, please see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246)) |
| verifySvcUv         | Integer | Number of reached devices (only valid for TPNS, ROG, and FCM channels. For other vendor channels, the `pushOnlineUv` metric of actual deliveries by TPNS will be used). <br>**Note:** this field will be disused subsequently. You are recommended to check the `arrivalUv` field for arrival data. |
| callbackVerifySvcUv | Integer  | Arrival receipt for vendor channel (for the Huawei and Meizu channels, you need to add a configuration item for arrival receipt manually. For more information, please see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246)). <br>**Note:** this field will be disused subsequently. You are recommended to check the `arrivalUv` field for arrival data. |
| clickUv             | Integer  | Clicked                                                         |
| cleanupUv           | Integer  | Cleared                                                         |

>?
>The "all" channel in the array corresponds to the aggregated statistics.
>- In the aggregated statistics, the `verifySvcUv` (reached devices), `verifyUv` (displayed), `clickUv` (clicked), and `cleanupUv` (cleared) metrics only aggregates the data of the TPNS, ROG, and FCM channels.
>- In the aggregated statistics, `pushActiveUv` (attempted) and `pushOnlineUv` (sent) aggregates the data of the TPNS channel and vendor channels.
>- In the aggregated statistics, `callbackVerifySvcUv` (arrival receipt of vendor channel) aggregates the data of vendor channel's `callbackVerifySvcUv` (arrival receipt of vendor channel) + TPNS channel's `verifySvcUv` (reached devices) + ROG channel's `verifySvcUv` (reached devices) + FCM channel's `verifySvcUv` (device reached).




#### pushState (iOS)

| Parameter Name | Type   | Description           |
| ------------ | ---- | ------------- |
| pushActiveUv | Integer  | Attempted |
| pushOnlineUv | Integer  | Successfully received by APNs |
| verifySvcUv  | Integer  | Reached          |
| clickUv      | Integer  | Clicked          |



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
                    "channel": "all",
                    "pushState": {
                        "pushActiveUv": 4000,
                        "pushOnlineUv": 3800,
                        "verifySvcUv": 3800,
                        "callbackVerifySvcUv": 2400,
			            "arrivalUv": 3800,
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
