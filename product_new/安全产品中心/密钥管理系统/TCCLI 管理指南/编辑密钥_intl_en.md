## Overview
The operations of renaming a key and modifying key description involve the following two functions:

| API Name | Description | Note |
|---------|---------|---------|
| UpdateAlias | Renames a key | The `KeyId` and `Alias` parameters are required for this API. For more information, please see the [UpdateAlias](https://cloud.tencent.com/document/product/573/34413) API document. |
| UpdateKeyDescription | Modifies key description | The `KeyId` and `Description` parameters are required for this API. For more information, please see the [UpdateKeyDescription](https://cloud.tencent.com/document/product/573/34412) API document. |


The examples below are called with [TCCLI](https://cloud.tencent.com/product/cli), which can also be called with any supported programming languages.

## Examples
#### Renaming a key

#### Input
```shell
tccli kms UpdateAlias --region ap-guangzhou --KeyId 52xxxx-xxxx-xxxx-xxxx-5xxxx4 --Alias test-gz-01-d
```



#### Output
If the modification is successful, the following information will be returned.
```shell
{
    "RequestId": "489a4274-0b81-4db7-8160-542c5c5bed68"
}
```


#### Modifying key description
#### Input
```shell
tccli kms UpdateKeyDescription --region ap-guangzhou --KeyId 5xxxxx-xxxx-xxxx-xxxx-52xxxxx4 --Description 'this is change message for test'
```


#### Output
If the modification is successful, the following information will be returned.
```shell
{
    "RequestId": "31134207-5de8-44f2-8c00-8bd0e88f95a6"
}
```
