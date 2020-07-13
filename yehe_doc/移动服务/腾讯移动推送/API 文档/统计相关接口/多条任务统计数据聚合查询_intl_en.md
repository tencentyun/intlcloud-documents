## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.
```shell
https://api.tpns.tencent.com/v3/statistics/get_push_group_stat_channel
```
**Feature**: this API is used to query the aggregated statistics by push channel of all push tasks **with the same `GroupID`** in the last 7 days according to `GroupID`.


## Parameter Description
#### Request parameters

| Parameter Name | Required | Type | Description |
| --------- | ---- | ------------ | ------------------------------------------------------------ |
| groupId   | Yes   | string       | Field for aggregated statistics of multiple tasks, using corresponding "group_Id" in push parameters            |
| startDate | Yes   | string | Query start date<li>Format: YYYY-MM-DD</li><li>Limit: only data of push tasks in the last 7 days can be aggregated</li> |
| endDate | Yes | string | Query end date. Format: YYYY-MM-DD |

#### Response parameters

| Parameter Name | Type | Description |
| ------------ | ------ | -------------------------------------- |
| retCode      | int    | Returned status code                             |
| errMsg | string | Error message |
| pushStatDataAll | JsonArray | Returned result: individual element formed by `channel` and `pushState`, where `channel` is the channel name. `pushState` structure variables are shown in following table |

#### pushState (Android)

| Parameter Name | Type   | Description           |
| ------------------- | ---- | ------------------------------------------------------------ |
| pushActiveUv | int    | Attempted |
| pushOnlineUv | int    | Sent |
| verifySvcUv         | int  | Reached devices (only valid for TPNS, ROG, and FCM channels. For other vendor channels, the `pushOnlineUv` metric of actual deliveries by TPNS will be used) |
| callbackVerifySvcUv | int  | Arrival receipt for vendor channel (only valid for Huawei, OPPO, Vivo, and Mi channels. For vendor channel receipt configuration, please see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246)) |
| verifyUv     | int    | Displayed     |
| clickUv      | int    | Clicked     |
| cleanupUv    | int    | Cleared |

>The "all" channel in the array corresponds to the aggregated statistics.
- In the aggregated statistics, the `verifySvcUv` (reached devices), `verifyUv` (displayed), `clickUv` (clicked), and `cleanupUv` (cleared) metrics only aggregates the data of the TPNS, ROG, and FCM channels.
- In the aggregated statistics, `pushActiveUv` (attempted) and `pushOnlineUv` (sent) aggregates the data of the TPNS channel and vendor channels.
- In the aggregated statistics, `callbackVerifySvcUv` (arrival receipt of vendor channel) aggregates the data of vendor channel's `callbackVerifySvcUv` (arrival receipt of vendor channel) + TPNS channel's `verifySvcUv` (reached devices) + ROG channel's `verifySvcUv` (reached devices) + FCM channel's `verifySvcUv` (device reached).



#### pushState (iOS)

| Parameter Name | Type   | Description           |
| ------------ | ------ | -------- |
| pushActiveUv | int    | Attempted |
| pushOnlineUv | int    | Successfully received by APNs |
| verifySvcUv  | int    | Arrival |
| clickUv      | int    | Clicked     |



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
            "channel": "hw",
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
            "channel": "xm",
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
            "channel": "oppo",
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
            "channel": "vivo",
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
            "channel": "mz",
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
            "channel": "xg",
            "pushState": {
                "pushActiveUv": 4641,
                "pushOnlineUv": 4641,
                "verifySvcUv": 4641,
                "callbackVerifySvcUv": 0,
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
                "verifyUv": 4639,
                "clickUv": 3818,
                "cleanupUv": 4200
            }
        }
    ]
}
```
