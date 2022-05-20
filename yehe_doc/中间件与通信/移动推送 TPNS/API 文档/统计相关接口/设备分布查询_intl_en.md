## API Description

**Request method**: POST.
**Calling frequency limit**: 200 times/hour

```plaintext
Service URL/v3/statistics/get_device_distribute_info
```
API service URLs correspond to service access points one to one. Select the [service URL](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

**API Feature**: Query the device distribution at a specific dimension of the application.



## Parameters
#### Request parameters

| Parameter Name  | Required | Type   | Description       |
| --------- | ---- | ------ | ---------- |
| date | Yes   | String | Query the date <li>Format: YYYYMMDD<li>Scope: A month as of the current date|
| type | Yes | String | Query dimensions:<li>`city`: City<li>province: Province<li>`app_version`: App version<li>`sdk_version`: SDK version<li>`system_version`: System version<li>`device_brand`: Device brand<li>`device_version`: Device version|

#### Response parameters

| Parameter Name       | Type      | Description                                     |
| -------------- | --------- | ---------------------------------------- |
| retCode         | Integer    | Response status code                              |
| errMsg       | String | Error message                               |
| data           | Array  | Response result. See the table below for the data structure. |

#### data

| Parameter Name | Type   | Description           |
| ---------------- | ------------------ | ---------------------- |
| city             | String             | City, which is returned when the query dimension is `city` |
| province           | String               | Province, which is returned when the query dimension is `province` |
| app_version          | String             | App version, which is returned when the query dimension is `app_version`  |
| sdk_version          | String               | SDK version, which is returned when the query dimension is `sdk_version` |
| system_version      | String             | System, which is returned when the query dimension is `system_version |
| device_brand      | String             | Device brand, which is returned when the query dimension is `device_brand` |
| device_version       | String             | Device version, which is returned when the query dimension is `device_version` |
| count         | Integer             | Device count            |

## Examples
#### Sample request
```json
{
        "date":"20220413",
        "type":"sdk_version"
}
```
#### Sample response
```json
{
        "retCode": 0,
        "errMsg": "",
        "data": [
                {
                        "sdk_version": "1.3.3.3",
                        "count": 8
                },
                {
                        "sdk_version": "1.3.3.0",
                        "count": 2
                }
        ]
}
```
