## Overview
The operations of enabling and disabling a key involve the following two APIs:


| API Name | Description | Note |
|---------|---------|---------|
| EnableKey | Enables a CMK | The `KeyId` parameter is required for this API. For more information, please see the [EnableKey](https://cloud.tencent.com/document/product/573/34423) API document. |
| DisableKey | Disables a CMK | The `KeyId` parameter is required for this API. For more information, please see the [DisableKey](https://cloud.tencent.com/document/product/573/34426) API document. |

The examples below are called with [TCCLI](https://cloud.tencent.com/product/cli), which can also be called with any supported programming languages.

## Examples
#### Enabling a CMK

#### Input
```shell
tccli kms EnableKey --region ap-guangzhou --KeyId 5xxxxx-xxxx-xxxx-xxxx-52xxxxx4
```

#### Output
If the key is successfully enabled, the following request will be returned.
```shell
{
	"RequestId": "6b2187b0-f40a-46d0-8065-2434afc54619"
}
```



#### Disabling a CMK

#### Input
```shell
tccli kms DisableKey --region ap-guangzhou --KeyId 5xxxxx-xxxx-xxxx-xxxx-52xxxxx4
```

#### Output
If the key is successfully disabled, the following request will be returned.
```shell
{
	"RequestId": "e5674638-1466-4607-a3ea-b60d30f4e5e3"
}
```
