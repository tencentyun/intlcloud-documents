## API Calling Description
**Request method**: POST.
**Calling frequency limit**: 200 times/hour

```plaintext
Service URL: v3/toolbox/getPushListByToken
```
API service URLs correspond to service access points one to one. Select the [service URL](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

**Feature**: Query the token-specific push data of the application on a day.

## Parameters
#### Request parameters

| Parameter | Required | Type | Description |
| --------- | ---- | ------ | ------------------------------------------------------------ |
| token | Yes   | String | Device token |

#### Response parameters

| Parameter                  | Type      | Description                                                |
| ------------------------- | --------- | --------------------------------------------------- |
| retCode         | Integer    | Returned status code                              |
| errMsg                    | string    | Error message                                            |
| pushTaskList | pushTask  | Push parameter |

#### pushTask

| Parameter | Type | Description |
| -------- | ------ | -------------- |
| pushId     | Integer |  Push task ID      |
| pushTime   | Integer    | Push timestamp     |
| pushTargetType    | Array    | Push type   |


## Samples
#### Sample request
    
```json
{
   "token":"05a305f6b71abb3a6b8c759fd1bc56b4bb44"
}
```
#### Sample response
```json
{
   "retCode": 0,
    "errMsg": "NO_ERROR",
    "pushTaskList": [
        {
            "pushId": 589840563,
            "pushTime": 1651662600,
            "pushTargetType": "TAG_PUSH"
        },
        {
            "pushId": 590166744,
            "pushTime": 1651741604,
            "pushTargetType": "TAG_PUSH"
        },
        {
            "pushId": 590178525,
            "pushTime": 1651742807,
            "pushTargetType": "TAG_PUSH"
        },
        {
            "pushId": 590179538,
            "pushTime": 1651742914,
            "pushTargetType": "TAG_PUSH"
        },
        {
            "pushId": 590179672,
            "pushTime": 1651742928,
            "pushTargetType": "TAG_PUSH"
        },
        {
            "pushId": 590235722,
            "pushTime": 1651750200,
            "pushTargetType": "TAG_PUSH"
        }
        ]
}
```
