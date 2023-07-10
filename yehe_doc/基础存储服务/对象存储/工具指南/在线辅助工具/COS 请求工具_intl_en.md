## Feature Overview

The COS request tool is a web-based debugging tool provided by COS. It is integrated on the TencentCloud API 3.0 Explorer platform for API debugging.

>! Requests sent by the COS request tool will be sent to the real COS server. **As all operations are real, be careful when performing operations such as `DELETE`.**

The COS request tool supports XML APIs but not JSON APIs.
- JSON APIs were provided by COS for you to access COS before XML APIs were released. Both types of APIs have the same underlying architecture where data is interconnected; however, they are incompatible with each other.
- XML APIs have a richer set of features and strengths over JSON APIs. We strongly recommend you upgrade to XML APIs for COS.

## Tool URL

Click [here](https://console.cloud.tencent.com/api/explorer?Product=cos) to enter the COS request tool.

## Directions

Select the **Cloud Object Storage** product, select the required API, enter parameters for the API, and click **Send Request** to get the corresponding response.

The COS request tool page shows the sections of product, API, parameter, and result from left to right. You can perform operations in different sections and send the request in the result section to get the response and process parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/2304f363c6f61cef274e47804f34e3a4.png)

The detailed steps to use the COS request tool are as shown below:

**1. Select the COS product.**

Click **Cloud Object Storage** in the product section on the far left, and then you can see COS APIs in the API section.

>?The COS request tool is integrated on the TencentCloud API 3.0 platform that provides API debugging tools for many Tencent Cloud products. You can also select other products to debug their APIs as needed.

**2. Select the API to be debugged.**

You can select the API for debugging as needed. Three types of COS APIs are shown in the API section: service APIs, bucket APIs, and object APIs.

- Take `GET Service` as an example for service APIs. This API can list the information of all buckets under your account. Your API key is required. To get the bucket information of your account in a specified region, select the corresponding region in the parameter section. For more information on this API, see [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291).
- Bucket APIs are used to manipulate buckets, such as `PUT Bucket lifecycle`. For more information, see [Bucket APIs](https://www.tencentcloud.com/document/product/436/7731).
- Object APIs are used to manipulate objects, such as `PUT Object`. For more information, see [Object APIs](https://www.tencentcloud.com/document/product/436/7739).

**3. Enter parameters for the API.**

The parameter section lists the corresponding parameters for the selected API. For more information on the parameters of COS APIs, see [API Documentation](https://www.tencentcloud.com/document/product/436/10009).

API key is a required parameter for API calling. When using an API to manipulate resources such as buckets or objects, you need to enter your API key to authorize the API request, which can be obtained on the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page in the CAM console.

>?For each API, the COS request tool displays a red asterisk behind each required parameter. You can also select **Only Required Parameters** to view required parameters only in the parameter section.

**4. Send a request and view the response.**

After selecting an API and entering parameters, click **Send Request** on the **Online Call** tab. Your request will be sent to the server, and the server will manipulate your buckets or objects accordingly.

>!Requests sent by the COS request tool will be sent to the real COS server. **As all operations are real, be careful when performing operations such as `DELETE`.**

After the request is sent, the returned result and the request parameters will be displayed in the result section. The **Request Parameters** part lists your HTTP request body; the **Response Result** part lists the response body of the request; the **Signature Process** part lists the signature involved in the request and its generation process; and the **Curl** part lists the statement called by Curl.

**Sample**

For example, a `GET Object` request is sent to get a file named `0001.txt` as shown below. The **Request Parameters** part lists the corresponding parameters of the request.
```http
GET https://bucketname-appid.cos.ap-region.myqcloud.com/0001.txt
Host: bucketname-appid.cos.ap-region.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDwqaGoCIWIG4hDWdJUTL5e3hn04xi****&q-sign-time=1543398166;1543405366&q-key-time=1543398166;1543405366&q-header-list=host&q-url-param-list=&q-signature=f50ddd3e0b54a92df9d4efe2d0c3734a8c90****
```

The first line shows your HTTP Verb and the link to be accessed; the second line shows the domain name to be accessed; and the last line shows the signature information of the request. For requests of the `PUT` type, request headers are complicated, but there are some common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

The **Signature Process** part shows the signature involved in this request and its generation process. For more information on signature algorithms, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778). If you need to generate and debug request signatures, we recommend you use the COS signature tool.

The response result returned by COS is as follows:

```http
200 OK
content-type: text/plain
content-length: 6
connection: close
accept-ranges: bytes
date: Wed, 28 Nov 2018 09:42:49 GMT
etag: "5a8dd3ad0756a93ded72b823b19dd877"
last-modified: Tue, 27 Nov 2018 20:05:26 GMT
server: tencent-cos
x-cos-request-id: NWJmZTYzMTlfOWUxYzBiMDlfOTA4NF8yMWI2****
x-cos-version-id: MTg0NDY3NDI1MzAzODkyMjU****
hello!
```

The `200 OK` in the first line is the status code returned for the request. If the request fails, the corresponding error code will be returned. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). Other lines are response headers, which vary by API, but there are some common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).



## Notes
After you click **Send Request** to send the request with its required parameters entered to the COS server, COS will perform the corresponding operation on your buckets or objects. The operation cannot be undone or reverted; therefore, proceed with caution.
