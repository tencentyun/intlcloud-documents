


## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.
```shell
https://api.tpns.tencent.com/v3/statistics/get_device_stat_overview
```
**Feature**: this API is used to query "daily new devices", "daily connected devices", and "historically accumulated devices" of the application within a certain time period.

## Parameter Description
#### Request parameters

| Parameter Name  | Required | Type   | Description         | Note                                            |
| --------- | ---- | ------ | ------------ | ----------------------------------------------- |
| startDate | Yes   | string | Queries the start date | start Date, query limit: only data for the past 3 months can be queried |
| endDate   | Yes   | string | Queries the end date  | -                                               |

#### Response parameters

| Parameter Name                  | Type      | Description                                                |
| ------------------------- | --------- | --------------------------------------------------- |
| retCode                   | int       | Returned status code                                          |
| errMsg                    | string    | Error message                                            |
| getDeviceStatOverviewData | JsonArray | Returned results, with getDeviceStatOverviewData structure variables shown in following table |

#### getDeviceStatOverviewData

| Parameter Name | Type   | Description           |
| -------- | ------ | -------------- |
| date     | int | Data date       |
| accuUv   | int    | Accumulated devices     |
| newUv    | int    | Daily new devices   |
| activeUv | int    | Daily peak of online devices |


## Samples
#### Sample request
```json
{
 "startDate": "20190724",
 "endDate": "20190726"
}
```
#### Sample response
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

