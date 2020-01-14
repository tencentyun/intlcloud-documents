## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.
```shell
https://api.tpns.tencent.com/v3/statistics/get_push_stat_overview
```
**Feature**: This API queries the daily push conversion summary within a certain time period.

## Parameter Descriptions
#### Request Parameters

| Parameter name  | Required | Type   | Description                                           |
| --------- | ---- | ------ | ---------------------------------------------- |
| startDate | Yes   | string | start Date, query limit: only data for the past 3 months can be queried |
| endDate   | Yes   | string | Data is timestamp                                   |

#### Response Parameters

| Parameter name | Type | Description |
| -------------------- | --------- | ------------------------------------------------------------ |
| retCode              | int       | Returned status code                                                   |
| errMsg               | string    | Error message                                                     |
| PushStatOverviewData | JsonArray | Returned results with [PushStatOverviewData], with PushStatOverviewData structure variables shown in following table  |

#### PushStatOverviewData (Android)

| Parameter name | Type   | Description           |
| ------------ | ------ | -------- |
| date         | string | Data date |
| pushActiveUv | int    | Planned delivery |
| pushOnlineUv | int    | Actual delivery |
| verifySvcUv  | int    | Device arrival |
| verifyUv     | int    | Display     |
| clickUv      | int    | Click     |
| cleanupUv    | int    | Clear     |

#### PushStatOverviewData (iOS & macOS)

| Parameter name | Type | Description |
| ------------ | ------ | -------- |
| date         | string | Data date |
| pushActiveUv | int    | Planned delivery |
| pushOnlineUv | int    | APNs successfully received |
| verifySvcUv  | int    | Arrival |
| clickUv      | int    | Click     |



## Example
#### Request Example
```json
{
 "startDate": "20190724",
 "endDate": "20190725"
}
```

#### Response Example
```json
{
 "retCode": 0,
 "errMsg": "NO_ERROR",
 "pushStatOverviewData": [
 {
 "date": "20190724",
 "pushActiveUv": 2,
 "pushOnlineUv": 2,
 "verifySvcUv": 2,
 "verifyUv": 2,
 "clickUv": 0,
 "cleanupUv": 0
 },
 {
 "date": "20190725",
 "pushActiveUv": 2,
 "pushOnlineUv": 2,
 "verifySvcUv": 2,
 "verifyUv": 2,
 "clickUv": 1,
 "cleanupUv": 1
 }
 ]
}
```
