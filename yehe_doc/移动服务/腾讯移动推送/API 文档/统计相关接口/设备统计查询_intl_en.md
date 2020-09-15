
## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.

The API request address corresponds to the service access point one by one; therefore, please select the request address corresponding to your application service access point.

Service access point in Guangzhou:
```shell
https://api.tpns.tencent.com/v3/statistics/get_push_record
```
Service access point in Hong Kong (China):
```shell
https://api.tpns.hk.tencent.com/v3/statistics/get_push_record
```
Service access point in Singapore:
```shell
https://api.tpns.sgp.tencent.com/v3/statistics/get_push_record
```
Service access point in Shanghai:
```shell
https://api.tpns.sh.tencent.com/v3/statistics/get_device_stat_overview
```
**Feature**: this API is used to query "daily new devices", "daily connected devices", and "historically accumulated devices" of the application within a certain time period.

## Parameter Description
#### Request parameters

| Parameter Name | Required | Type | Description |
| --------- | ---- | ------ | ------------------------------------------------------------ |
| startDate | Yes   | String | Query start date<li>Format: YYYYMMDD<li>Limit: only data in the last 3 months can be queried |
| endDate   | Yes   | String | Query end date. Format: YYYYMMDD                                 |

#### Response parameters

| Parameter Name                  | Type      | Description                                                |
| ------------------------- | --------- | --------------------------------------------------- |
| retCode                   | Integer       | Returned status code                                          |
| errMsg                    | String    | Error message                                            |
| getDeviceStatOverviewData | Array | Returned result, with `getDeviceStatOverviewData` structure variables shown in following table |

#### getDeviceStatOverviewData

| Parameter Name | Type   | Description           |
| -------- | ------ | -------------- |
| date     | Integer | Data date       |
| accuUv   | Integer    | Accumulated devices     |
| newUv    | Integer    | Daily new devices   |
| activeUv | Integer    | Daily peak of online devices |


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

