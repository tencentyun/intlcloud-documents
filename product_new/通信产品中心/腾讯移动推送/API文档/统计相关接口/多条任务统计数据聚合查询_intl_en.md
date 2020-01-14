## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.
```shell
https://api.tpns.tencent.com/v3/statistics/get_push_group_stat
```
**Feature**: This API can do a GroupID-based query of all the aggregation statistics data for pushed tasks with the **same GroupID in the last 3 days**.


## Parameter Descriptions
#### Request Parameters

| Parameter name | Required | Type | Description |
| --------- | ---- | ------------ | ------------------------------------------------------------ |
| groupId   | Yes   | string       | Field for aggregation statistics of multiple tasks, using corresponding “group_Id” in push parameters            |
| startDate | Yes   | string       | Start date of the query<li>Format: YYYY-MM-DD<li>Limit: can only provide aggregation statistics for push tasks in past 7 days |
| endDate   | Yes   | string | End date of the query, format: YYYY-MM-DD                               |

#### Response Parameters

| Parameter name | Type | Description |
| ------------ | ------ | -------------------------------------- |
| retCode      | int    | Returned status code                             |
| errMsg       | string | Error message                               |
| pushStatData | Json   | Returned results, with pushRecordData structure variables shown in following table  |

#### pushStatData (Android)

| Parameter name | Type | Description |
| ------------ | ------ | -------- |
| pushActiveUv | int    | Planned delivery |
| pushOnlineUv | int    | Actual delivery |
| verifySvcUv  | int    | Device arrival |
| verifyUv     | int    | Display     |
| clickUv      | int    | Click     |
| cleanupUv    | int    | Clear     |

#### pushStatData (iOS)

| Parameter name | Type | Description |
| ------------ | ------ | -------- |
| pushActiveUv | int    | Planned delivery |
| pushOnlineUv | int    | APNs successfully received |
| verifySvcUv  | int    | Arrival |
| clickUv      | int    | Click     |


## Example
#### Request Example

```json
{
 "groupid": "pt:testGroup",
 "startDate": "20190912",
 "endDate": "20190912"
}
```

#### Response Example

```json
{
 "retCode": 0,
 "errMsg": "NO_ERROR",
 "pushStatData": {
 "pushActiveUv": 14,
 "pushOnlineUv": 9,
 "verifySvcUv": 8,
 "verifyUv": 8,
 "clickUv": 0,
 "cleanupUv": 0
 }
}
```
