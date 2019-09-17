Here is a use case to help you quickly get started with TencentDB for MongoDB APIs.

This sample shows how to create an instance: First, query the supported specification of the instance; then, query the fees for creating the instance and create the instance using the instance creation API; finally, query the instance creation progress using the order details querying API.

## 1. Querying Supported Instance Specifications
Before creating an instance, query the specifications of instances that can be created using the [Query Available Specification API](https://intl.cloud.tencent.com//document/product/240/8318).

The input parameters for this API (supporting custom availability zones and configurations) are as follows: 

| Parameter Name | Required | Type | Description | Value |
|---------|---------|---------|---------|---------|
| zoneIds.n | No | String | The array of availability zone IDs, with the array subscript starting at 0. If this parameter is not passed in, the product information of all availability zones will be returned | 100002 |

Availability zones are defined as follows:

| Availability Zone | zoneId |
|:---------|---------|
| Guangzhou Zone 1 | 100001 |
| Guangzhou Zone 2 | 100002 |
| Guangzhou Zone 3 | 100003 |
| Shanghai Zone 1 | 200001 |
| Hong Kong Zone 1 | 300001 |
| Toronto Zone 1 | 400001 |
| Beijing Zone 1 | 800001 |

The return value of the Query Available Specification API (supporting custom availability zones and configurations) is the configuration information of the creatable instances under each availability zone. Taking the configuration information of instances in Guangzhou Zone 2 in the return value as an example, the fields are as defined below:

| Parameter Name | Type | Description |
|:---------|---------|---------|
| region | String | The ID of the region. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/213/6976) |
| isSupportVpc | Bool | Whether VPC is supported. Valid values: true, false |
| types | Object | Supported instance specification information |

Here, `types` indicates the supported instance specification information and is composed as follows:

| Parameter Name | Type | Description |
|:---------|---------|---------|
| typeId | String | The name of the instance type. GIO: high-IO edition; TGIO: 10-Gigabit high-IO edition |
| replicationNodeNum | Array | Number of nodes of replica set. Only 2 and 3 are supported currently |
| memory | Int | The memory size of the instance in MB. Each memory value corresponds to a selectable disk capacity range |
| volumeMax | Int | The maximum value of the selectable disk capacity of the instance in GB after the memory size is specified |
| volumeMin | Int | The minimum value of the selectable disk capacity of the instance in GB after the memory size is specified |
| volumeStep | Int | The increment of the disk capacity of the instance in GB after the memory size is specified. For instance creation, the value for the disk (volume) is: volume = volumeMin + volumeStep * n, where volumeMin <= volume <= volumeMax |
| version | Array | Supported database version number, for example: MONGO_3_MMAP, MONGO_3_WT  |

By combining common request parameters and API request parameters, you can generate the final request as shown below:
		
		https://mongodb.api.qcloud.com/v2/index.php?
		Action=DescribeMongoDBProduct
		&SecretId=AKIDVxZ0PsvtPCgNEtsO0pSFwqkeTMFCu7z1
		&Signature=eSCz5paiDrXsdifc0Eq0GEihzsI%3D
		&Nonce=23284
		&Timestamp=1468329994
		&Region=gz
		&zoneIds.0=100002

The return result of the above request is as follows:
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "timeSpan": [
            1,
            2,
            3,
            4,
            5,
            6,
            7,
            8,
            9,
            10,
            11,
            12,
            24,
            36
        ],
        "timeUnit": "m",
        "goodsDescription": {
            "100002": {
                "region": "gz",
                "isSupportVpc": true,
                "types": [
                    {
                        "typeId": "GIO",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 2048,
                        "volumeMax": 250,
                        "volumeMin": 25,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "GIO",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 4096,
                        "volumeMax": 250,
                        "volumeMin": 25,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "GIO",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 6144,
                        "volumeMax": 250,
                        "volumeMin": 25,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "GIO",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 8192,
                        "volumeMax": 500,
                        "volumeMin": 25,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "GIO",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 12288,
                        "volumeMax": 500,
                        "volumeMin": 25,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "GIO",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 16384,
                        "volumeMax": 500,
                        "volumeMin": 25,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "GIO",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 24576,
                        "volumeMax": 500,
                        "volumeMin": 25,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "GIO",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 32768,
                        "volumeMax": 500,
                        "volumeMin": 25,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "GIO",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 49152,
                        "volumeMax": 750,
                        "volumeMin": 25,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "GIO",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 61440,
                        "volumeMax": 1000,
                        "volumeMin": 25,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "GIO",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 65536,
                        "volumeMax": 1000,
                        "volumeMin": 25,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "CY",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 4096,
                        "volumeMax": 300,
                        "volumeMin": 50,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "CY",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 8192,
                        "volumeMax": 300,
                        "volumeMin": 100,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "CY",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 16384,
                        "volumeMax": 600,
                        "volumeMin": 200,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "CY",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 32768,
                        "volumeMax": 1200,
                        "volumeMin": 400,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "CY",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 65536,
                        "volumeMax": 4000,
                        "volumeMin": 750,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "CY",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 131072,
                        "volumeMax": 6000,
                        "volumeMin": 1500,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "CY",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 245760,
                        "volumeMax": 6000,
                        "volumeMin": 1500,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    },
                    {
                        "typeId": "CY",
                        "replicationNodeNum": [
                            2,
                            3
                        ],
                        "memory": 524288,
                        "volumeMax": 6000,
                        "volumeMin": 4000,
                        "volumeStep": 5,
                        "version": [
                            "MONGO_3_MMAP",
                            "MONGO_3_WT"
                        ]
                    }
                ]
            }
        }
    }
}

```

## 2. Querying the Price of an Instance (Monthly Subscription)
Creating a replica set instance will incur fees which will be deducted from your account balance. For more information on the incurred fees, call the [instance price (monthly subscription) querying API](/document/product/240/8311). Here, take purchasing a high-IO instance in Guangzhou Zone 2 as an example. The input parameters for price query are as follows: 

| Parameter Name | Required | Type | Description | Value |
|:---------|---------|---------|---------|---------|
| operation | Yes | String | newmongodb is required, indicating the purchase of an instance | newmongodb |
| zoneId | Yes | Int | The ID of the availability zone. Call the [supported instance specification querying API](/document/product/240/8318) to obtain the supported availability zones | 100002 |
| typeId | Yes | String | The type name of the instance. GIO: high-IO edition; TGIO: 10-Gigabit high-IO edition | GIO |
| memory | Yes | Int | The memory size of the instance in MB. Each memory value corresponds to a selectable disk capacity range | 8192 |
| diskSize | Yes | Int | The disk capacity of the instance in GB | 245 |
| secondaryNum | Yes | Int | Number of slave nodes of the replica set instance. Only 1 and 2 are currently supported | 2 |
| version | Yes | Int | Database version number, for example: MONGO_3_MMAP, MONGO_3_WT  | MONGO_3_MMAP |
| goodsNum | Yes | Int | Number of instances purchased at a time | 1 |
| period | Yes | Int | The usage period purchased in months. Value range: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 24, 36] | 1 |

By combining common request parameters and API request parameters, you can generate the final request as shown below:
	
	https://mongodb.api.qcloud.com/v2/index.php?
	Action=InquiryMongoDBReplSetPrice
	&Timestamp=1468328627
	&Nonce=51897
	&SecretId=AKIDVxZ0PsvtPCgNEtsO0pSFwqkeTMFCu7z1
	&Signature=u34AneL09yCx50BwrUZtibiHxNw%3D
	&Region=gz
	&operation=newmongodb
	&zoneId=100002
	&typeId=GIO
	&memory=8192
	&diskSize=245
	&secondaryNum=2
	&version=MONGO_3_MMAP
	&goodsNum=1
	&period=1

Based on the return value, you can see that the total price of the instance with the above specification is 1,888 CNY.
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "price": 188800
    }
}

```

## 3. Creating a Replica Set Instance
Next, you can call the [instance creating (monthly subscription) API](/document/product/240/8308) to create an instance of the above specification. The input parameters are as follows: 

| Parameter Name | Required | Type | Description | Value |
|:---------|---------|---------|---------|---------|
| zoneId | Yes | Int | The ID of the availability zone. Call the [supported instance specification querying API](/document/product/240/8318) to obtain the supported availability zones | 100002 |
| typeId | Yes | String | The type name of the instance. GIO: high-IO edition; TGIO: 10-Gigabit high-IO edition | GIO |
| memory | Yes | Int | The memory size of the instance in MB. Each memory value corresponds to a selectable disk capacity range | 4096 |
| diskSize | Yes | Int | The disk capacity of the instance in GB | 30 |
| secondaryNum| Yes | Int | Number of slave nodes of replica set. Only 1 and 2 are supported currently | 2 |
| version | Yes | Int | Database version number, for example: MONGO_3_MMAP, MONGO_3_WT  | MONGO_3_MMAP |
| goodsNum | Yes | Int | Number of instances purchased at a time | 1 |
| period | Yes | Int | The usage period purchased in months. Value range: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 24, 36] | 1 |
| password | Yes | String | The password for the instance. Password rule: 1. It can only contain 8-16 characters; 2. It must contain at least two of the following types of characters: letters, digits, and special characters (!@#%^()) | 49A2d!e@f12e |
| vpcId | No | Int | The ID of the VPC. In a basic network, vpcId = 0. In a VPC, the value is subject to the vpcid returned by the [VPC list querying API](https://intl.cloud.tencent.com/doc/api/245/1372) | 0 |
| subnetId | No | Int | In a basic network, subnetId is invalid. In a VPC subnet, the value is subject to the subnetid returned by the [VPC list querying API](https://intl.cloud.tencent.com/doc/api/245/1372) | 0 |
| projectId | No | Int | The ID of the project. The value is subject to the projectId returned by User Account > User Account API Query > [Project List](https://intl.cloud.tencent.com/doc/api/403/4400) | 0 |

By combining common request parameters and API request parameters, you can generate the final request as shown below:
	
	https://mongodb.api.qcloud.com/v2/index.php?
	Action=CreateMongoDBReplSet
	&Timestamp=1468328920
	&Nonce=27412
	&SecretId=AKIDVxZ0PsvtPCgNEtsO0pSFwqkeTMFCu7z1
	&Signature=4Dvpkk1bJov%2FUd%2FElWjAHfJaoD8%3D
	&zoneId=100002
	&typeId=GIO
	&memory=4096
	&diskSize=30
	&secondaryNum=2
	&version=MONGO_3_MMAP
	&goodsNum=1
	&period=1
	&password=49A2d!e@f12e

According to the returned values, the order ID for the purchase of the instance with the above specification is 3373037. You can query the details of this order through API [Query Order Details](/document/product/240/8313)

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "dealId": "3373037"
    }
}

```

## 4. Querying Order Details
After creating an instance, use the [Query Order Details API](/document/product/240/8313) to query the order details with the ` dealId` in the return value.

| Parameter Name | Required | Type | Description | Value |
|---------|---------|---------|---------|
| dealIds.n | Yes | String | The array of order IDs, with the array subscript starting at 0 | 3373037 |

By combining common request parameters and API request parameters, you can generate the final request as shown below:

	https://mongodb.api.qcloud.com/v2/index.php?
	Action=DescribeMongodbDealDetail
	&Timestamp=1468329117
	&Nonce=40727
	&SecretId=AKIDVxZ0PsvtPCgNEtsO0pSFwqkeTMFCu7z1
	&Signature=Y9rMVWyvjoijSl6zJxMW822edGk%3D
	&dealIds.0=3373037

The output is as follows: 
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
        }
    ]
}

```

The `details` in the return value of the Query Order Details API indicates the array of order details with the following fields:

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
| clusterType | Array | The cluster type of the instance. Only replica set is available currently |
| secondaryNum| Array | Number of slave nodes of replica set. Only 1 and 2 are supported currently |
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
