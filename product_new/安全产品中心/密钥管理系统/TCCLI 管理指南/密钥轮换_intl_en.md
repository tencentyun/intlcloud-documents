## Overview
The key rotation feature involves three APIs:


| API Name | Description | Note |
|---------|---------|---------|
|GetKeyRotationStatus | Views key rotation status | The `KeyId` parameter is required for this API. For more information, please see the [GetKeyRotationStatus](https://cloud.tencent.com/document/product/573/34418) API document. |
|EnableKeyRotation | Enables key rotation | The `KeyId` parameter is required for this API. For more information, please see the [EnableKeyRotation](https://cloud.tencent.com/document/product/573/34422) API document. |
|DisableKeyRotation | Disables key rotation | The `KeyId` parameter is required for this API. For more information, please see the [DisableKeyRotation](https://cloud.tencent.com/document/product/573/34425) API document. |

The examples below are called with [TCCLI](https://cloud.tencent.com/product/cli), which can also be called with any supported programming languages.

## Examples
#### Viewing key rotation status

#### Input
```shell
tccli kms GetKeyRotationStatus --region ap-guangzhou --KeyId 5xxxxx-xxxx-xxxx-xxxx-52xxxxx4
```

#### Output
If the API is called successfully, the key rotation status of the CMK will be returned.
```shell
{
   "KeyRotationEnabled": false,
   "RequestId": "e1432224-4dc2-48da-a8e8-e84d30afd9ef"
}
```



#### Enabling key rotation

#### Input
```shell
tccli kms EnableKeyRotation --region ap-guangzhou --KeyId 5xxxxx-xxxx-xxxx-xxxx-52xxxxx4
```

#### Output
If the feature is enabled normally, the request information as shown below will be returned.
```shell
{
	"RequestId": "4e0fa96f-e86e-4517-af27-3dfe6e5b2a72"
}
```





#### Disabling key rotation

#### Input
```shell
tccli kms DisableKeyRotation --region ap-guangzhou --KeyId 5xxxxx-xxxx-xxxx-xxxx-52xxxxx4
```

#### Output
If the feature is disabled normally, the request information as shown below will be returned.
```shell
{
	"RequestId": "c8b73c8b-1ee5-4b23-b800-7cccc58e7ffb"
}
```
