## Overview


| API Name | Description | Note |
|---------|---------|---------|
| ListKeys | Shows the list of keys (KeyId information) under an account. | There are no required parameters for this API. For more information, please see the [ListKeys](https://cloud.tencent.com/document/product/573/34415) API document. |
| DescribeKey | Views the details of the specified CMK, including CMK name, ID, status, and region. | The `KeyId` parameter is required for this API. For more information, please see the [DescribeKey](https://cloud.tencent.com/document/product/573/34428) API document. |



The examples below are called with [TCCLI](https://cloud.tencent.com/product/cli), which can also be called with any supported programming languages.


## Examples
#### Viewing the list of key IDs
This example describes how to view the information of the first five KeyIds in Guangzhou region.

#### Input
```shell
tccli kms ListKeys --region ap-guangzhou --Limit 5
```



#### Output
```shell
{
    "Keys": [
        {
            "KeyId": "6xxxxxxx-xxxx-xxxx-xxxx-5xxxxxxxxc09"
        },
        {
            "KeyId": "6xxxxxxx-xxxx-xxxx-xxxx-5xxxxxxxxc09"
        },
        {
            "KeyId": "6xxxxxxx-xxxx-xxxx-xxxx-5xxxxxxxxc09"
        },
        {
            "KeyId":"6xxxxxxx-xxxx-xxxx-xxxx-5xxxxxxxxc09"
        },
        {
            "KeyId": "6xxxxxxx-xxxx-xxxx-xxxx-5xxxxxxxxc09"
        }
    ],
    "TotalCount": 114,
    "RequestId": "afaaeb5e-c97d-4726-8012-6ae337d62928"
}
```



#### Viewing key ID details
This example describes how to view the details of the specified CMK.

#### Input
```shell
tccli kms DescribeKey --region ap-guangzhou --KeyId 521xxxxx-xxxx-xxxx-xxxx-52xxxxd4
```



#### Output
If the API is successfully executed, the details of the CMK will be returned.
```shell
{
 "KeyMetadata": {
        "KeyId": "6xxxxxxx-xxxx-xxxx-xxxx-5xxxxxxxxc09",
        "Description": "this is test for gz key",
        "CreatorUin": 10xxxxxxxxxx,
        "KeyRotationEnabled": false,
        "NextRotateTime": 1603439621,
        "CreateTime": 1571903621,
        "Alias": "test-gz01",
        "KeyUsage": "ENCRYPT_DECRYPT",
        "DeletionDate": 0,
        "KeyState": "Enabled",
        "Type": 4,
        "Owner": "user"
    },
    "RequestId": "608f514c-3279-44ea-8e4c-c00b69e3521c"
}
```

