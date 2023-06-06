## Overview

This document describes how to call Tencent Cloud eKYC APIs through API 3.0 Explorer and integrate SDKs in the corresponding programming language into your project after you purchase the eKYC service. You can access eKYC APIs quickly in the following steps.
## Prerequisites

You have entered the [API 3.0 Explorer](https://console.tencentcloud.com/api/explorer?Product=faceid&Version=2018-03-01&Action=ApplySdkVerificationToken) page.
## Directions

The following steps use the calling of the [ApplySdkVerificationToken](https://www.tencentcloud.com/zh/document/product/1061/49954) API as an example.
### Step 1.
On the [API 3.0 Explorer](https://console.tencentcloud.com/api/explorer?Product=faceid&Version=2018-03-01&Action=ApplySdkVerificationToken) page, select `ApplySdkVerificationToken` from the left sidebar, enter required parameters, initiate the call, and get the response.
![ApplySdkVerificationToken](https://staticintl.cloudcachetci.com/yehe/backend-news/Gnrv261_ApplySdkVerificationToken.png)

- `Region`: This is a required parameter that specifies the region information in the domain name and determines the access point. For example, `ap-hongkong` means accessing the Hong Kong access point. APIs may support different regions. For details, see the "Region List" section in the API document of the API you are calling. For example, for [ApplySdkVerificationToken](https://www.tencentcloud.com/zh/document/product/1061/49954), see the "Region List" section in [Common Params](https://www.tencentcloud.com/document/api/1061/36934#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8).
	![parameters](https://staticintl.cloudcachetci.com/yehe/backend-news/MUuN845_parameters.png)
- `NeedVerifyIdCard`: This is a required parameter that specifies whether to perform identity card authentication. If this parameter is not selected, only document OCR will be performed. You can select this parameter only when the value of `IdCardType` is `HK`.

### Step 2.

Select the corresponding backend language, generate the code, and integrate it into your project. Take Java as an example.
1. To integrate the code into your project, you need to import the SDK dependencies (see [Java](https://www.tencentcloud.com/zh/document/product/494/7245) in the top right corner of the figure below), get key information, and enter the `SecretId` and `SecretKey` in the code for successful calling.
2. Part of the field information in the generated code is subject to the entered content. To adjust an input parameter, modify its value on the left and generate the code again.

![api](https://staticintl.cloudcachetci.com/yehe/backend-news/mHPB015_api.png)
## Notes

- To generate a SecretId and a SecretKey, visit https://console.tencentcloud.com/cam/capi.
- To upload Base64-encoded images or videos for input parameters, remove the `data:image/jpg;base64,` prefix and the `\n` line break.
- If the following information is returned, manually configure the signature type:

  ```
  [TencentCloudSDKException]message:AuthFailure.SignatureFailure-The provided credentials
  could not be validated because of exceeding request size limit, please use new signature 
  method `TC3-HMAC-SHA256`. requestId:719970d4-5814-4dd9-9757-a3f11ecc9b20
  ```
  
  ​Configuring signature type:
  ```
   `clientProfile.setSignMethod("TC3-HMAC-SHA256"); // Specify the signature algorithm, which is HmacSHA256 by default`
   ```