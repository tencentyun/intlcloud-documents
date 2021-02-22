## API Description
**Request method**: POST
**Calling frequency limit**: 200 times/hour

```plaintext
Service URL/v3/statistics/get_push_group_stat_channel
```
API service URLs correspond to service access points one by one. Please select the [service URL](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

**Feature**: this API is used to query the aggregated statistics by push channel of all push tasks with the same `GroupID` or `planId` in the last 7 days according to `GroupID` or `planId`.

>?`GroupID` will be disused gradually, and `planId` is recommended for querying aggregated statistics.

## Parameter Description
#### Request parameters

| Parameter | Required | Type | Description |
| --------- | ---- | ------------ | ------------------------------------------------------------ |
| planId   | Yes   | String       | Parameter for aggregated statistics of multiple tasks, using corresponding `planId` in push parameters        |
| groupId   | Yes   | String       | Parameter for aggregated statistics of multiple tasks, using corresponding `group_Id` in push parameters<br>**Note:** this parameter will be disused gradually, and `planId` is recommended for querying aggregated statistics.           |
| startDate | Yes   | String       | Query start date<li>Format: YYYYMMDD</li><li>Limit: only data of push tasks in the last 7 days can be aggregated.</li> |
| endDate   | Yes   | String | Query end date. Format: YYYYMMDD                               |
>?If both `planId` and `groupId` are specified, the query will be based on `planId` by default.

#### Response parameters

| Parameter | Type | Description |
| ------------ | ------ | -------------------------------------- |
| retCode      | Integer    | Returned status code                             |
| errMsg       | String | Error message                               |
| pushStatDataAll | Array  | Returned result: individual element formed by `channel` and `pushState`, where `channel` is the channel name. `pushState` structure variables are shown in following table |

#### pushState (Android)

| Parameter | Type   | Description           |
| ------------------- | ---- | ------------------------------------------------------------ |
| pushActiveUv        | Integer  | Scheduled delivery count<br/>Number of available devices online in the last 90 days with the notification bar enabled in the push target devices                                                     |
| pushOnlineUv        | Integer  | Actual delivery count<br/>Number of available devices to which the message was successfully delivered through the vendor or TPNS channel out of the devices for scheduled delivery                                                     |
| arrivalUv         | Integer  | Number of reached devices (including arrival receipts for the TPNS and vendor channels. For the Huawei and Meizu channels, you need to add a configuration item for arrival receipt manually. For more information, see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246) |
| verifySvcUv         | Integer  | Number of reached devices (only valid for TPNS, ROG, and FCM channels. For other vendor channels, the `pushOnlineUv` metric of actual deliveries by TPNS will be used). **Note:** this parameter will be deactivated subsequently. You are recommended to check the `arrivalUv` parameter for arrival data |
| callbackVerifySvcUv | Integer  | Arrival receipt for vendor channel (for the Huawei and Meizu channels, you need to add a configuration item for arrival receipt manually. For more information, see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246). **Note:** this parameter will be deactivated subsequently. You are recommended to check the `arrivalUv` parameter for arrival data |
| verifyUv            | Integer  | Displayed (this parameter has been disused and will be deactivated subsequently)                                                         |
| clickUv             | Integer  | Clicked                                                         |
| cleanupUv           | Integer  | Cleared                                                         |

>?The "all" channel in the array corresponds to the aggregated statistics.
-  In the aggregated statistics, the `verifySvcUv` (reached devices), `verifyUv` (displayed), `clickUv` (clicked), and `cleanupUv` (cleared) metrics only aggregate the data of the TPNS, ROG, and FCM channels.
-  In the aggregated statistics, `pushActiveUv` (scheduled delivery) and `pushOnlineUv` (actual delivery) aggregate the data of the TPNS channel and vendor channels.
-  In the aggregated statistics, `callbackVerifySvcUv` (arrival receipt of vendor channel) aggregates the data of vendor channel's `callbackVerifySvcUv` (arrival receipt of vendor channel) + TPNS channel's `verifySvcUv` (reached devices) + ROG channel's `verifySvcUv` (reached devices) + FCM channel's `verifySvcUv` (reached devices).



#### pushState (iOS)

| Parameter | Type | Description |
| ------------ | ------ | -------- |
| pushActiveUv | Integer    | Scheduled delivery |
| pushOnlineUv | Integer    | Successfully received by APNs |
| verifySvcUv  | Integer    | Reached |
| clickUv      | Integer    | Clicked     |



## Samples

#### Sample request

```json
{
    "groupid": "pt:testGroup",
    "startDate": "20190912",
    "endDate": "20190912"
}
```

#### Sample response

```json
{
    "retCode": 0,
    "errMsg": "NO_ERROR",
    "pushStatDataAll": [
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
            "channel": "hw",
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
            "channel": "xm",
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
            "channel": "oppo",
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
            "channel": "vivo",
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
            "channel": "mz",
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
            "channel": "xg",
            "pushState": {
                "pushActiveUv": 4641,
                "pushOnlineUv": 4641,
                "verifySvcUv": 4641,
                "callbackVerifySvcUv": 0,
                "arrivalUv": 0,
                "verifyUv": 4639,
                "clickUv": 3818,
                "cleanupUv": 4200
            }
        },
        {
            "channel": "all",
            "pushState": {
                "pushActiveUv": 4641,
                "pushOnlineUv": 4641,
                "verifySvcUv": 4641,
                "callbackVerifySvcUv": 4641,
                "arrivalUv": 4641,
                "verifyUv": 4639,
                "clickUv": 3818,
                "cleanupUv": 4200
            }
        }
    ]
}
```
