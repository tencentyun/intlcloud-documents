## Scenarios
This guide introduces how to call OCR APIs 3.0 through API 3.0 Explorer, and integrate SDKs in corresponding languages to the project after the OCR service is activated.


## Prerequisites
Before calling an OCR API, [apply to activate the corresponding OCR service](https://console.cloud.tencent.com/ocr/general).
After activating the service, go to [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=ocr&Version=2018-11-19&Action=GeneralBasicOCR&SignVersion=) and make an OCR API call as follows.

## Directions
1. Select the API you want to call in the left sidebar.
![](https://main.qcloudimg.com/raw/34586e7780f7cd729e83c275d8b12ffb.png)
2. Enter the private key and required input parameters.
![](https://main.qcloudimg.com/raw/9e6fc5a1f2c9ce915c2eef7d869bffb9.png)
 - `Region`: region information in the domain name. This parameter determines the access point. For example, `ocr.ap-shanghai.tencentcloudapi.com` means Shanghai is the access point. The common parameter `Region` determines where business resources to be accessed reside. For example, `Region=ap-beijing` means resources in the Beijing region will be accessed. If no region is specified in the domain name, the nearest point will be accessed by default. But if the IP address fails to be resolved, Guangdong region will be accessed by default. You can configure different regions for domain name and common parameter, but this may cause latency. Thus, we recommend selecting the same `Region`, such as ap-guangzhou for South China (Guangzhou).
 - String will be parsed to Json.
![](https://main.qcloudimg.com/raw/b40b2d9f0a1198e05d3a551c574d34e4.png)
3. Select the language to generate codes.
The codes will be generated according to parameter values you entered on the left. To modify input parameters, you need to change parameter values on the left to generate codes again.
4. Integrate SDKs to the project.
See SDK Usage Guide on the top right to integrate SDKs to the project and call APIs with codes generated in **Step 3**.
![](https://main.qcloudimg.com/raw/ef2357291426913a4f88e890473634ee.png)

## Demo (recommended)

```
const tencentcloud = require("../../../../tencentcloud-sdk-nodejs");

const OcrClient = tencentcloud.ocr.v20181119.Client;
const models = tencentcloud.ocr.v20181119.Models;

const Credential = tencentcloud.common.Credential;
const ClientProfile = tencentcloud.common.ClientProfile;
const HttpProfile = tencentcloud.common.HttpProfile;

Credential cred = new Credential("secretId", "secretKey");
let httpProfile = new HttpProfile();
let clientProfile = new ClientProfile();
/*
We recommend using V3 authentication, which is required if the request size exceeds 1 MB. Except for Node.js, SDKs in all other languages support V3.
clientProfile.signMethod = "TC3-HMAC-SHA256";
*/
clientProfile.httpProfile = httpProfile;
let client = new OcrClient(cred, "ap-guangzhou", clientProfile);

let req = new models.IDCardOCRRequest();

req.ImageUrl = "[https://test.jpg](https://test.jpg/)";
req.CardSide = "FRONT";
let config = {"CropPortrait":true};
req.Config = JSON.stringify(config)

client.IDCardOCR(req, function(errMsg, response) {

    if (errMsg) {
        console.log(error);
        return;
    }

    console.log(response.to_json_string());
		
	});
```
## Notes

- When you call APIs with SDKs, take note of the `Region` field for common parameters. We recommend using “ap-guangzhou” for both the domain name and `Region`.
- SecretId/SecretKey generation: [**Access Key** -> **API Key Management**](https://console.cloud.tencent.com/cam/capi). Currently, only the root account can call OCR APIs. Sub-account will be supported soon.
- For Base64-encoded image or video, remove the `data:image/jpg;base64,` prefix and the line break `\n`.
- If the following request result appears, configure the signature type manually:

  ```
  [TencentCloudSDKException]message:AuthFailure.SignatureFailure-The provided credentials
  could not be validated because of exceeding request size limit, please use new signature 
  method `TC3-HMAC-SHA256`. requestId:719970d4-5814-4dd9-9757-a3f11ecc9b20
  ```

  Configure the signature type:

  ```js
  clientProfile.setSignMethod("TC3-HMAC-SHA256"); // Specifies the signature algorithm, which is HmacSHA256 by default
  ```

  If the API request size exceeds 1 MB, V3 authentication (TC3-HMAC-SHA256) is required. Except for Node. js, SDKs in all other languages support V3.
- API 3.0 SDK supports Node, Python, Java, PHP, Go and .Net. To call APIs with SDKs in other languages such as C++, you need to complete V3 authentication. We recommend using the string signature generation tool in [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=faceid&Version=2018-03-01&Action=GetActionSequence) for verification.
![](https://main.qcloudimg.com/raw/421420a45963a7b86225e041908abbdb.png)





