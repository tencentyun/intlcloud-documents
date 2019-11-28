## Overview
The CreateKey API can be called to create a customer master key (CMK) used for DEK management. The CMK can be used in other APIs to create DEKs, perform encryption and decryption, and do more.

The `Alias` parameter is required for this API. You can add other descriptions for the CMK as instructed in the [CreateKey](https://cloud.tencent.com/document/product/573/34430) API document.

The examples below are called with [TCCLI](https://cloud.tencent.com/product/cli), which can also be called with any supported programming languages.



## Examples
This example shows you how to create a key named `test-gz01` in Guangzhou region with the description `this is test for gz key`.
#### Input
```shell
tccli kms CreateKey --region ap-guangzhou --Alias test-gz01 --Description 'this is test for gz key'
```

#### Output
After creation, the key will be enabled by default, with the key rotation feature disabled.
```shell
{
    "KeyId": "6xxxxxxx-xxxx-xxxx-xxxx-5xxxxxxxxc09",
    "Description": "this is test for gz key",
    "Alias": "test-gz01",
    "KeyUsage": "ENCRYPT_DECRYPT",
    "RequestId": "994bbd90-7c8e-4522-85f2-c712da23f863",
    "KeyState": "Enabled",
    "CreateTime": 1571903621
}
```
