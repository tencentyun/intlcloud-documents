


## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.
```shell
https://api.tpns.tencent.com/v3/statistics/get_device_stat_overview
```
**Feature**: This API queries an app’s daily “new devices on current day”, “daily connected devices”, and “historically accumulated devices” within a certain time period.

## Parameter Descriptions
#### Request Parameters

| Parameter name  | Required | Type   | Description         | Note                                            |
| --------- | ---- | ------ | ------------ | ----------------------------------------------- |
| startDate | Yes   | string | Start date of the query | start Date, query limit: only data for the past 3 months can be queried |
| endDate   | Yes   | string | End date of the query | -                                               |

#### Response Parameters

| Parameter name                  | Type      | Description                                                |
| ------------------------- | --------- | --------------------------------------------------- |
| retCode                   | int       | Returned status code                                          |
| errMsg                    | string    | Error message                                            |
| getDeviceStatOverviewData | JsonArray | Returned results, with getDeviceStatOverviewData structure variables shown in following table |

#### getDeviceStatOverviewData

| Parameter name | Type   | Description           |
| -------- | ------ | -------------- |
| date     | int | Data date       |
| accuUv   | int    | Accumulated devices     |
| newUv    | int    | New devices on current day   |
| activeUv | int    | Daily peak of online devices |


## Example
#### Request Example
```json
{
 "startDate": "20190724",
 "endDate": "20190726"
}
```
#### Response Example
```json
{
 "retCode": 0,
 "errMsg": "",
 "getDeviceStatOverviewData": [
 {
 "date": 20190724,
 "accuUv": 0,
 "newUv": 0,
 "activeUv": 0
 },
 {
 "date": 20190725,
 "accuUv": 0,
 "newUv": 5,
 "activeUv": 0
 },
 {
 "date": 20190726,
 "accuUv": 5,
 "newUv": 0,
 "activeUv": 2
 }
 ]
}
```

