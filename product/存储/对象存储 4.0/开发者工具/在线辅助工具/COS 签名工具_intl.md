## Overview

The COS signature tool is a web tool provided by COS for users to generate request signatures. You can enter the corresponding parameters on the COS signature tool page to generate a request signature and verify whether the request signature is correct.
## Directions

### XML signature tool

#### Start COS signature tool

Click **[COS Signature Tool](https://cos5.cloud.tencent.com/static/cos-sign/)** to go to the **COS Signature Tool** page.

#### Enter basic configuration information

In the **Basic Information** section, enter the API version and the validity period of the signature, as shown below:
![](https://main.qcloudimg.com/raw/6855a2f6b18779037090e0769303bbc7.png)
All the parameters in the basic information are required.
-  API Version: Select **XML API**.
-  Validity Period of Signature: The validity period of the signature. You can click **Obtain** to get a signature with a validity period of 60 minutes. You can also enter valid start and end time to reproduce the signature results generated within the period from the start time to the end time. For more information on the validity period of signature, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778#.E7.AD.BE.E5.90.8D.E5.86.85.E5.AE.B9).

#### Enter API key information

In the **API Key** section, enter your API key information, as shown below:
![](https://main.qcloudimg.com/raw/c28b93819a8fdd9e121e6b0702d098d4.png)
All the information in the API key section is required.
-  Parameters for the API key can be found in the [API Key Management](https://console.cloud.tencent.com/cam/capi) page of the console.
-  Make sure you enter the correct information. If the information is incorrect, your signature will be invalid.

#### Enter HTTP parameters

In the **HTTP Parameters** section, enter the corresponding parameters, as shown below:
![avatar](https://main.qcloudimg.com/raw/8fbc5566b31777e646aa457239468cda.png)
The main parameters are as follows:
-  **HttpMethod:** Required. HTTP request method, which can be GET, POST, PUT, or DELETE.
-  **HttpURI:** Required. The URI part of the HTTP request, i.e. the name of the object to which you need to initiate the request.
-  **HttpParameters:** Optional. HTTP request parameter. You can enter this parameter when you need to verify the url parameter. The key should be lowercase, and the value should be URL encoded. Multiple keys must be sorted in lexicographic order.
 For example, "prefix=abc" indicates limiting the access objects to be those with the prefix of abc.
-  **HttpHeaders:** Optional. HTTP request header. You can enter this parameter when you need to verify the url parameter. The key should be lowercase, and the value should be URL encoded. Multiple keys must be sorted in lexicographic order.
 For example, "Host: bucket1-1254000000.cos.ap-beijing.myqcloud.com" means that the signature can access the specified files in bucket1 of the account 1254000000.

For more information on the HTTP request parameters, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778#signature-.E8.AE.A1.E7.AE.97).

#### Generate signature and review process parameters

Click **Generate Signature**, and the request signature result will be displayed in **Result Feedback** on the right, as shown below:
The COS signature tool presents the final signature generated and the process parameters of the signature computing process. For more information on process parameters, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778#signature-.E8.AE.A1.E7.AE.97).

![avatar](https://main.qcloudimg.com/raw/4e5d3164848078e4ac2dc0b9b767ca00.png)

### JSON signature tool

#### Enter basic configuration information

1. Click **[COS Signature Tool](https://cos5.cloud.tencent.com/static/cos-sign/)** to go to the **COS Signature Tool** page.
2. In the **Basic Information** section, enter the API version, the bucket name and the current time, as shown below:
![](https://main.qcloudimg.com/raw/8b764cd2bef9d2d64a3b8faeb26afff1.png)
All the information in the API key section is required.
-  API Version: Select **JSON API**.
-  Bucket Name: Enter the name of the bucket to be accessed, such as bucketname-appid.
-  Current Time: The current system time, which is a value that conforms to the Unix Epoch timestamp specification (in sec); you can also enter a specified time to reproduce the signature results under the specified timestamp.

#### Enter API key information

In the **API Key** section, enter your API key information.
The API key is required, which can be found in the [API Key Management](https://console.cloud.tencent.com/cam/capi) page of the console.
Make sure you enter the correct information. If the information is incorrect, your signature will be invalid.

#### Enter HTTP parameters

In the **HTTP Parameters** section, enter the corresponding parameters, as shown below:
![avatar](https://main.qcloudimg.com/raw/621bd5458b8da2dcfc6eea7d707fecbb.png)
The main parameters are as follows:
-  **ExpiredTime:** Required. The expiration time of the signature (in sec). You can get the expiration time of the signature by adding a validity period to the **Current Time** parameter. **For a one-time signature, the expiration time must be set to 0**.
-  **RandomId:** Required. A random string of unsigned decimal integers.
-  **FilePath:** Optional. It identifies the relative path of the resource stored, in the format of "/[dirname]/[filename]".
   - If the object to be operated is a folder, leave the filename with the default value. The filename should include the file extension.
   - If the FilePath is empty, the generated request signature can be used to access all objects in the bucket.

For more information on the HTTP request parameters, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

#### Generate signature and review process parameters

Click **Generate Signature**, and the request signature result will be displayed in **Result Feedback** on the right.
The COS signature tool presents the final signature generated and the process parameters of the signature computing process. For more information on process parameters, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

## Notes
-  The signature tool does not recognize and prompt you for incorrect parameters. If you use this tool to compute the request signature and compare it with the computing results of the SDK or other tools, the tool will not correct the incorrect parameters you entered.
-  The signature tool recognizes and prompts you for invalid parameters. However, a request signature that fails the signature verification may be generated.
-  The signature tool recognizes and prompts you for required parameters that have not been entered. If you do not enter all required parameters, the request signature may not be generated.

