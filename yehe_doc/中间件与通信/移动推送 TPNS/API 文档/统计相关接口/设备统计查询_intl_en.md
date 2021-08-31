
## API Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour.

```plaintext
request address/v3/statistics/get_device_stat_overview
```
The API request address is corresponding to the service access point. Select the [request address](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

**Feature**: this API is used to query "daily new devices", "daily active users", and "historically accumulated devices" of the application within a certain time period.

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

