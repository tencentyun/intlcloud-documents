## 1. API Description
This API (DescribeMongodbDealDetail) is used to query order details.
API domain name: **mongodb.api.qcloud.com**.

## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/372/4153). The Action field of this API is `DescribeMongodbDealDetail`.

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| dealIds.n | Yes | String | The array of order IDs, with the array subscript starting at 0 |


## 3. Output Parameters
| Parameter Name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/377/8946). |
| message | String | Error message. A null value indicates a success |
| codeDesc | String | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. |
| details | Array | Array of returned order details |

`details` indicates the array of order details and is composed as follows:

| Parameter Name | Type | Description |
|:---------|---------|---------|
| details.dealId | String | Short order ID. Use this ID when calling the TencentCloud API |
| details.dealName | String | Long order ID. Use this ID when reporting order-related problems to customer service |
| details.zoneId | Int | Availability Zone ID |
| details.goodsNum | Int | Number of instances associated with the order |
| details.creater | String | The UIN of the order creator |
| details.creatTime | String | Order creation time |
| details.overdueTime | String | Order expiration time |
| details.endTime | String | The completion time of the order |
| details.status | Int | The status of the order. <br>1: unpaid; <br>2: paid but not shipped; <br>3: in transition; <br>4: successfully shipped; <br>5: shipment failed; <br>6: refunded; <br>7: order closed; <br>8: order expired; <br>9: order invalidated; <br>10: product invalidated; <br>11: requested payment rejected; <br>12: payment in process |
| details.price | Int | The actual total price of the order in 0.01 CNY |
| details.goodsDetail | Object | Details of the items associated with the order |

**`goodsDetail` returned upon instance creation:**

| Parameter Name | Type | Description |
|:---------|---------|---------|
| memSize| int | The memory size of the instance in MB |
| disksize | int | The disk capacity of the instance in GB |
| typeId | String | The type name of the instance. GIO: high-IO edition; TGIO: 10-Gigabit high-IO edition |
| clusterType | Array | The cluster type of the instance. 0: replica set |
| secondaryNum | Array | Number of slave nodes of the replica set instance. Only 1 and 2 are currently supported |
| zoneId | Array | Availability Zone ID |
| mongoVersion | Array | Database version number, for example: MONGO_3_MMAP, MONGO_3_WT |
| timeSpan | Array | The validity period of the instance, with the unit being subject to the return value of `timeUnit` |
| timeUnit | Array | The unit of the validity period of the instance, m: month; d: day |
| SerialIds | Array | The array of instance IDs |

**goodsDetail returned when the instance is renewed:**

| Parameter Name | Type | Description |
|:---------|---------|---------|
| curDeadline | String | The expiration time of the instance before renewal |
| timeSpan | int | Renewed period, with the unit being subject to the return value of `timeUnit` |
| timeUnit | String | The unit of the renewed period, m: month; d: day |
| SerialIds | Array | The array of instance IDs |

**goodsDetail returned when the instance is upgraded:**

| Parameter Name | Type | Description |
|:---------|---------|---------|
| curDeadline | String | Instance expiration time |
| newMemsize | int | The memory size of the instance after upgrade in MB |
| newDisksize | int | The disk capacity of the instance after upgrade in GB |
| oldMemsize | int | The memory size of the instance before upgrade in MB |
| oldDisksize | int | The disk capacity of the instance before upgrade in GB |
| SerialIds | Array | The array of instance IDs |

## 4. Error Codes
The following lists the error codes related to this API.

| Error Code | Error Message | Error Description |
|---------|---------|---------|
|11201|InvalidParameter| Invalid service parameter. |

## 5. Samples
Input
<pre>
https://mongodb.api.qcloud.com/v2/index.php?Action=DescribeMongodbDealDetail
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common request parameter</a>>
&dealIds.0=3373037
&dealIds.1=3374462
&dealIds.2=3374558
</pre>
Output
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "details": [
        {
            "dealId": "3373037",
            "dealName": "20170206121420",
            "zoneId": 100002,
            "goodsNum": 1,
            "creater": "3374998458",
            "creatTime": "2017-02-06 14:07:46",
            "overdueTime": "2017-02-21 14:07:46",
            "endTime": "2017-02-06 14:11:54",
            "status": 4,
            "price": 72200,
            "goodsDetail": {
                "memSize": 4096,
                "disksize": 30,
                "typeId": "GIO",
                "clusterType": "ReplSet",
                "secondaryNum": 2,
                "zoneId": 100002,
                "mongoVersion": "MONGO_3_MMAP",
                "timeSpan": 1,
                "timeUnit": "m",
                "SerialIds": [
                    "cmgo-6ozqe0uh"
                ]
            }
        },
        {
            "dealId": "3374462",
            "dealName": "20170206124372",
            "zoneId": 100002,
            "goodsNum": 1,
            "creater": "3374998458",
            "creatTime": "2017-02-06 16:32:45",
            "overdueTime": "2017-02-21 16:32:45",
            "endTime": "2017-02-06 16:32:46",
            "status": 4,
            "price": 72200,
            "goodsDetail": {
                "curDeadline": "2017-03-06 14:07:46",
                "timeSpan": 1,
                "timeUnit": "m",
                "SerialIds": [
                    "cmgo-6ozqe0uh"
                ]
            }
        },
        {
            "dealId": "3374558",
            "dealName": "20170206124575",
            "zoneId": 100002,
            "goodsNum": 1,
            "creater": "3374998458",
            "creatTime": "2017-02-06 16:43:17",
            "overdueTime": "2017-02-21 16:43:17",
            "endTime": "2017-02-06 16:45:49",
            "status": 4,
            "price": 142421,
            "goodsDetail": {
                "curDeadline": "2017-04-06 14:07:46",
                "newMemsize": 8192,
                "newDisksize": 60,
                "oldMemsize": 4096,
                "oldDisksize": 30,
                "SerialIds": [
                    "cmgo-6ozqe0uh"
                ]
            }
        }
    ]
}

```
