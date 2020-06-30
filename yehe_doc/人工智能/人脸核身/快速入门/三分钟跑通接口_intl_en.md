## Operation Scenarios
This document describes how to call the Tencent Cloud Faceid API on the online API debugging page of API 3.0 Explorer and integrate the SDK in the corresponding programming language of the API into your project after you purchase the Faceid service. You can quickly connect to the Faceid API in the following steps.

## Prerequisites
You have [applied for activating Faceid](https://intl.cloud.tencent.com/apply/p/shcgszvmppc) and your application has been approved before you call the Faceid API.
After your application is approved, enter the Faceid [API 3.0 Explorer online API debugging page](https://console.cloud.tencent.com/api/explorer?Product=faceid&Version=2018-03-01&Action=DetectAuth&SignVersion=) to call the API in the following steps.

## Directions
### Step 1
Select the face comparison API on the left sidebar.

### Step 2
Enter your personal key information and required parameters.
![](https://main.qcloudimg.com/raw/1be14e17dfef3318aca8b169ffae6cb7.png)

 - Region: region information in the domain name, which determines the access point to be used; for example, `faceid.ap-shanghai.tencentcloudapi.com` indicates that the Shanghai access point will be accessed. The common parameter `Region` specifies the region of the business resources to be accessed; for example, `Region=ap-beijing` indicates that resources in the Beijing region will be manipulated. If the region information is not specified in the domain name, nearby access will be enabled by default, which may not always work as expected. If the IP cannot be resolved, the domain name will be pointed to the Guangzhou region by default. In addition, the domain name region and common parameter `Region` can be different, which, however, may increase the access latency. You are recommended to use the same region in the domain name and the common parameter `Region`, such as South China (Guangzhou)/ap-guangzhou.
 - RuleId: it is used to specify the use case. After your service activation application is approved, you can create a rule in self-service access in the [Faceid Console](https://console.cloud.tencent.com/faceid) and call it after it is approved. If you have any questions, please contact the Faceid assistant in WeChat (account: faceid001).

<span id="Step 3"></span>
### Step 3
Select the programming language and generate the corresponding code.
Enter the parameter values on the left and generate the code. Some field information in the generated code is subject to the entered content. If you want to adjust an input parameter, you only need to modify its value on the left and generate the code again.

### Step 4
Integrate the SDK into the project.
Import the SDK into the project as instructed in the SDK use instructions in the top-right corner. You can call the corresponding API by running the code generated in [step 3](#Step 3).
![](https://main.qcloudimg.com/raw/47505703a1645bf420f782c8dd3580af.png)

## Notes
- You only need to pay attention to the `Region` field in common parameters for SDK calls. You are recommended to use `ap-guangzhou` in both the domain name and `Region`.
- Address for generating `SecretId`/`SecretKey`: `https://console.cloud.tencent.com/cam/capi`.
- If you want to Base64-encode images/videos, you need to remove the relevant prefix `data:image/jpg;base64,` and the line break `\n`.
- If the request result is as shown below, you need to manually set the signature type:
 ```
[TencentCloudSDKException]message:AuthFailure.SignatureFailure-The provided credentials
could not be validated because of exceeding request size limit, please use new signature 
method `TC3-HMAC-SHA256`. requestId:719970d4-5814-4dd9-9757-a3f11ecc9b20
 ```
Set the signature type:
``` js
  clientProfile.setSignMethod("TC3-HMAC-SHA256"); // Specify the signature algorithm (default value: HmacSHA256)
```
- If the API request content exceeds 1 MB, only v3 authentication (TC3-HMAC-SHA256) can be used. The API 3.0 SDK supports the following programming languages: Node.js, Python, Java, PHP, and Go. Other programming languages such as .NET and C# are not supported for calls through SDK, and you should implement API authentication v3 on your own to call APIs. You are recommended to use the signature string generation tool in [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=faceid&Version=2018-03-01&Action=GetActionSequence) to verify the signature validity.
![](https://main.qcloudimg.com/raw/2f83cb6a567ff6a0c2477a10c6feab8d.png)



