## Overview
This document describes how to call Tencent Cloud FaceID APIs through API 3.0 Explorer and integrate SDKs in the corresponding programming language into your project after you purchase the FaceID service. You can access FaceID APIs quickly in the following steps.

## Prerequisites
Enter [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=faceid&Version=2018-03-01&Action=DetectAuth&SignVersion=) to call APIs in the following steps.

## Directions
### Step 1
Select the CompareFace API on the left sidebar.

### Step 2
Enter your private key information and required parameters.
![](https://main.qcloudimg.com/raw/800146cb41268ffd2909a60322fa4e5d.png)

 - Region: region information in the domain name that determines the access point. For example, `faceid.ap-shanghai.tencentcloudapi.com` indicates that Shanghai is the access point. The common parameter `Region` specifies the region of business resources to be accessed; for example, `Region=ap-beijing` indicates resources in the Beijing region will be accessed. If no region is specified in the domain name, a nearby region will be accessed by default, which may cause problems. If an IP cannot be resolved, Guangzhou region will be used by default. The region for the domain name and the common parameter `Region` can be different, but this may increase access latency. We recommend using the same region for the domain name and the common parameter `Region`, such as South China (Guangzhou)/ap-guangzhou.
 - RuleId: Used to specify use cases. After your apply to activate the service, you can create RuleId in the [FaceID console](https://console.cloud.tencent.com/faceid) and call it after your application is approved. If you have any questions, contact the FaceID WeChat assistant (account: faceid001).

<span id="Step 3"></span>
### Step 3
Select the programming language to generate codes.
Enter the parameters on the left to generate codes. Part of the field information in the generated code is subject to the entered content. To adjust an input parameter, modify its value on the left and generate the code again.

### Step 4
Integrate the SDK into the project.
Integrate the SDK into the project as instructed in the usage guide on the upper right-hand corner. You can call the corresponding API using the code generated in [Step 3](https://intl.cloud.tencent.com/document/product/1061/37029?lang=en&pg=#step-3).
![](https://main.qcloudimg.com/raw/426025dfc6dcaa3b42525821804c92a7.png)

## Notes
- You only need to focus on the `Region` field in common parameters when using SDKs to make calls. We recommend using `ap-guangzhou` for both the domain name and `Region`.
- Address for generating `SecretId`/`SecretKey`: `https://console.cloud.tencent.com/cam/capi`.
- For base64-encoded images or videos, remove the `data:image/jpg;base64,` prefix and the `\n` line break.
- If the request result is as shown below, you need to manually configure the signature type:
 ```
[TencentCloudSDKException]message:AuthFailure.SignatureFailure-The provided credentials
could not be validated because of exceeding request size limit, you need to use new signature 
method `TC3-HMAC-SHA256`. requestId:719970d4-5814-4dd9-9757-a3f11ecc9b20
 ```
Configure the signature type:
``` js
  clientProfile.setSignMethod("TC3-HMAC-SHA256"); // Specify the signature algorithm (default value: HmacSHA256)
```
- If the API request exceeds 1 MB, only v3 authentication (TC3-HMAC-SHA256) can be used. API 3.0 SDK supports Node.js, Python, Java, PHP, and Go, but not .NET and C#.  For unsupported languages, you need to implement API authentication v3 to call APIs, and we recommend using the signature generation tool in [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=faceid&Version=2018-03-01&Action=GetActionSequence) to verify the signature.
![](https://main.qcloudimg.com/raw/29fe779dac02bfef2024265f928556f3.png)



