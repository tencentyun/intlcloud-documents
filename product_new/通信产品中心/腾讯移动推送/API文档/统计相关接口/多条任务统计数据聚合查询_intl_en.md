## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.
```shell
https://api.tpns.tencent.com/v3/statistics/get_push_group_stat_channel
```
**Feature**: this API is used to query the aggregated statistics by push channel of all push tasks **with the same `GroupID`** in the last 3 days.


## Parameter Description
#### Request parameters

| Parameter Name | Required | Type | Description |
| --------- | ---- | ------------ | ------------------------------------------------------------ |
| groupId   | Yes   | string       | Field for aggregated statistics of multiple tasks, using corresponding "group_Id" in push parameters            |
| startDate | Yes   | string       | Queries the start date<li>Format: YYYY-MM-DD</li><li>Limit: can only provide aggregate statistics for push tasks in past 7 days </li> |
| endDate   | Yes   | string |Queries the end date. Format: YYYY-MM-DD                              |

#### Response parameters

| Parameter Name | Type | Description |
| ------------ | ------ | -------------------------------------- |
| retCode      | int    | Returned status code                             |
| errMsg | string | Error message |
| pushStatDataAll | JsonArray | Returned results: individual element formed by `channel` and `pushStat`, where `channel` is the channel name. `pushStat` structure variables are shown in following table |

#### pushStat (Android)

| Parameter Name | Type   | Description           |
| ------------------- | ---- | ------------------------------------------------------------ |
| pushActiveUv | int    | Attempted delivery |
| pushOnlineUv | int    | Actual sent to |
| verifySvcUv         | int  | Device reached (only valid for TPNS and iOS APNs channels. For other vendor channels, the `pushOnlineUv` metric of actual deliveries by TPNS will be used) |
| callbackVerifySvcUv | int  | Arrival receipt for vendor channel (only valid for Huawei, OPPO, Vivo, and Mi channels. For vendor channel receipt configuration, please see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246)) |
| verifyUv     | int    | Displayed     |
| clickUv      | int    | Clicked     |
| cleanupUv    | int    | Cleared     |

>The "all" channel in the array corresponds to the aggregated statistics. In the aggregated statistics, the `verifySvcUv`, `verifyUv`, `clickUv`, and `cleanupUv` metrics only aggregates the data of the TPNS and ROG channels. The `pushActiveUv` and `pushOnlineUv` metrics aggregate the data of the TPNS and vendor channels.

`callbackVerifySvcUv` aggregates the `verifySvcUv` data of the TPNS channel and the `callbackVerifySvcUv` data of vendor channels.


#### pushStat (iOS)

| Parameter Name | Type   | Description           |
| ------------ | ------ | -------- |
| pushActiveUv | int    | Attempted delivery |
| pushOnlineUv | int    | APNs successfully received |
| verifySvcUv  | int    | Reached |
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
