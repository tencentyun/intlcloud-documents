## API Description
**Request method**: POST
**Calling frequency limit**: 200 times/hour

```plaintext
Service URL/v3/statistics/get_push_task_stat_channel
```
API service URLs correspond to service access points one by one. Please select the [service URL](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

**Feature**: This API is used to query the detailed statistics for each push task, including all channel information and the summary. The channel types in `pushStatDataAll` vary depending on the OS (iOS/Android) and push channels.



## Parameters
#### Request parameters

| Parameter | Required | Type | Description |
| -------- | ---- | ------ | ------ |
| pushId | Yes | String | ID of a push task. You can only query push tasks within last 30 days. |

#### Response parameters

| Parameter | Type | Description |
| --------------- | ------ | ------------------------------------------------------------ |
| retCode         | Integer    | Returned status code                              |
| errMsg          | String | Error message                                                     |
| pushStatDataAll | Array   | Variables in the `pushStatDataAll` structure. See the table below for details. |

#### pushStatDataAll

| Parameter | Type | Description |
| --------------- | ------ | ------------------------------------------------------------ |
| channel | String | Name of a push channel<br> `xg`: TPNS<br> `hw`: Huawei<br> `xm`: Mi<br> `mz`: Meizu<br>`oppo`: OPPO<br> `vivo`: vivo<br> `apns`: APNs<br> `fcm`: FCM<br> `rog`: ROG <br> `all`: all channels |
| pushState          | Object | Variables in the `pushState` structure. See  the table below for details.             |

#### pushState (Android)

| Parameter | Type   | Description           |
| ------------------- | ---- | ------------------------------------------------------------ |
| pushActiveUv        | Integer  | Scheduled delivery count<br/>Number of available devices online in last 90 days with the notification bar enabled in the push target devices                                                     |
| pushOnlineUv        | Integer  | Actual delivery count<br/>Number of available devices to which the message was successfully delivered through the vendor or TPNS channel out of the devices for scheduled delivery                                                     |
| arrivalUv | Integer | Number of reached devices (including arrival receipts for the TPNS and vendor channels. For Huawei and Meizu channels, you need to configure the arrival receipt manually. For more information, please see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246)). |
| verifySvcUv | Integer | Number of reached devices (only for TPNS, ROG, and FCM channels. The arrival data of other vendor channels is displayed using the `pushOnlineUv` parameter of TPNS). **Note:** This parameter will be discontinued later. Therefore, you are advised to use `arrivalUv` for the arrival data. |
| callbackVerifySvcUv | Integer | Arrival receipt for vendor channels (for Huawei and Meizu channels, you need to configure the arrival receipt manually. For more information, please see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246)). **Note:** This parameter will be discontinued later. Therefore, you are advised to use `arrivalUv` for the arrival data. |
| verifyUv            | Integer  | Displayed (this parameter has been discarded and will be discontinued later)                                                         |
| clickUv             | Integer  | Clicked                                                         |
| cleanupUv           | Integer  | Cleared                                                         |

>?
>The `all` channel in the array corresponds to the aggregated statistics.
>-  In the aggregated statistics, the `verifySvcUv` (reached devices), `verifyUv` (displayed), `clickUv` (clicked), and `cleanupUv` (cleared) metrics only aggregate the data of the TPNS, ROG, and FCM channels. 
>-  In the aggregated statistics, `pushActiveUv` (scheduled delivery) and `pushOnlineUv` (actual delivery) aggregate the data of the TPNS channel and vendor channels.
>-  In the aggregated statistics, `callbackVerifySvcUv` (arrival receipt of vendor channel) aggregates the data of vendor channel's `callbackVerifySvcUv` (arrival receipt of vendor channel) + TPNS channel's `verifySvcUv` (reached devices) + ROG channel's `verifySvcUv` (reached devices) + FCM channel's `verifySvcUv` (reached devices).

#### pushState (iOS and macOS)

| Parameter | Type | Description |
| ------------ | ------ | ------------ |
| pushActiveUv | Integer    | Scheduled delivery |
| pushOnlineUv | Integer    | Successfully received by APNs |
| verifySvcUv  | Integer    | Reached |
| clickUv      | Integer    | Clicked     |

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

