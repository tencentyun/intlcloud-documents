## Overview

The COS request tool is a Web debugging tool provided by Cloud Object Storage (COS), which is integrated in the Cloud API 3.0 Explorer platform and can be used for API debugging.

>Requests sent by the COS request tool will be sent to the COS business server. **All operations are equivalent to real operations, so proceed with caution when you perform such operations as "DELETE".**

The COS request tool supports XML APIs, and does not support JSON APIs.
-  JSON APIs are the APIs provided by COS for users to access COS before XML APIs are launched. JSON APIs have the same underlying architecture as the standard XML APIs. Their data is interoperable and can be cross-used, but the two APIs are incompatible.
-  XML APIs provide a richer set of features and advantages over JSON APIs. It is strongly recommended that you upgrade to XML APIs for COS.

## Directions

Click the [COS Request Tool](https://console.cloud.tencent.com/api/explorer?Product=cos) page, and then select the product **COS** and the desired API. Enter the corresponding parameters for the API, and click **Send Request** to get the response result.

The COS request tool page shows the product, the API, the parameter and the result sections (from left to right). You can perform the corresponding operations in different sections, and send the request in the result section to get the response result and the process parameters, as shown below:
![](https://main.qcloudimg.com/raw/6329b432ed56516ca311bcbe5720d13f.png)

The detailed operation procedure of the COS request tool is shown as follows.

**1. Select the product COS**.

Click **Cloud Object Storage** in the leftmost product section, and then you can see the COS-related APIs in the API section.

>The COS request tool is integrated in the Cloud API 3.0 platform that provides the API debugging tools for many Tencent Cloud products. You can also select other products to debug their APIs on the platform as needed.

**2. Select the API to be debugged**.

You can select the API for debugging as needed. Three types of COS-related APIs are shown in the API section: Service APIs, Bucket APIs, and Object APIs.

-  We will take GET Service as an example to introduce the Service APIs. The GET Service API can list the information of all buckets under your account. Your API key is required. To get the bucket information of your account in a specified region, you can select the corresponding region in the parameter section. For more information on this API, see [GET Service](https://intl.cloud.tencent.com/document/product/436/8291).
-  The Bucket APIs are the APIs used to operate buckets, such as PUT Bucket lifecycle. For more information on Bucket APIs, see [Bucket APIs](https://intl.cloud.tencent.com/document/product/436/7731).
-  The Object APIs are the APIs used to operate objects, such as PUT Object. For more information on Object APIs, see [Object APIs](https://intl.cloud.tencent.com/document/product/436/7739).

**3. Enter parameters for the API**.

The parameter section lists the corresponding parameters for the API you selected. For more information on the parameters of various COS-related APIs, see [API Documentation](https://intl.cloud.tencent.com/document/product/436/10009).

API key is a required parameter for API calling. When using an API to operate resources such as buckets or objects, you need to enter your API key to authorize this API request. Your API key can be found on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page of the CAM Console.

>For each API, the COS request tool displays a red asterisk behind each required parameter to remind you that the parameter is required. You can also select **Only Required Parameters** to view the required parameters only in the parameter section.

**4. Send request and view response result**.

After selecting an API and entering the corresponding parameters, click **Send Request** in the **Online Call** tab. Your request will be sent to the server, and then the server will operate your buckets or objects according to your request.

>Requests sent by the COS request tool will be sent to the COS business server. **All operations are equivalent to real operations, so be careful when you perform operations such as "DELETE".**

After the request is sent, the returned result and the request parameters will be displayed in the lower part of the result section. The **Request Parameters** lists your HTTP request body; the **Response Result** lists the response body of the request; the **Signature Process** lists the signature involved in the request and its generation process; and the **Curl** lists the statement called by Curl.

**Example**

For example, a GET Object request is sent to obtain a file named 0001.txt, as shown below. The **Request Parameters** lists the corresponding parameters of the request.

```
GET https://bucketname-appid.cos.ap-region.myqcloud.com/0001.txt
Host: bucketname-appid.cos.ap-region.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDwqaGoCIWIG4hDWdJUTL5e3hn04xiD5kI&q-sign-time=1543398166;1543405366&q-key-time=1543398166;1543405366&q-header-list=host&q-url-param-list=&q-signature=f50ddd3e0b54a92df9d4efe2d0c3734a8c9007ec
```

The first line shows your HTTP Verb and the link to be visited; the second line shows the domain to be visited; and the last line shows the signature information for the request. For requests of the PUT type, the request header is complicated, but there are some common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

The signature involved in the request and its generation process can be found in **Signature Process**. For more information on the signature algorithm, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778). If you need to generate and debug a request signature, it is recommended that you use the [COS signature tool](https://cos5.cloud.tencent.com/static/cos-sign/).

The response result returned by COS is as follows:

```
200 OK
content-type: text/plain
content-length: 6
connection: close
accept-ranges: bytes
date: Wed, 28 Nov 2018 09:42:49 GMT
etag: "5a8dd3ad0756a93ded72b823b19dd877"
last-modified: Tue, 27 Nov 2018 20:05:26 GMT
server: tencent-cos
x-cos-request-id: NWJmZTYzMTlfOWUxYzBiMDlfOTA4NF8yMWI2YjE=
x-cos-version-id: MTg0NDY3NDI1MzAzODkyMjUzNjM
hello!
```

The `200 OK` in the first line is the status code returned by the request. If the request fails, the corresponding error code will be returned. For more information on error code, see [Error Code](https://intl.cloud.tencent.com/document/product/436/7730). The other content is the response header. The response bodies of different APIs are different, but there are some common response headers. For more information on the common response header, see [Common Response Header](https://intl.cloud.tencent.com/document/product/436/7729).



## Note
After you click **Send Request** to send the request with its required parameters entered to the COS server, COS will perform corresponding operations on your buckets and objects. The operation cannot be undone or rolled back, so use it carefully.

