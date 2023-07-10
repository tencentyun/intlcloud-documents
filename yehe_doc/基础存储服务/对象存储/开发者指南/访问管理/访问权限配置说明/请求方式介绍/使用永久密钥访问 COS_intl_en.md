## Background

With RESTful APIs, you can initiate anonymous HTTP requests or signed HTTP requests to COS. Anonymous requests are typically used for scenarios that require public access, such as hosting static websites; and signed requests are required in most other scenarios.

Compared with an anonymous request, a signed request carries an additional signature value. The signature is an encrypted string generated based on the key (SecretId/SecretKey) and request information. The SDK automatically calculates the signature. You only need to set the key when initializing user information and do not need to worry about signature calculation. For requests initiated through RESTful APIs, COS needs to calculate signatures based on the signature algorithm and add them to the requests.

## Getting a Permanent Key

You can log in to the CAM console and go to the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page to get a permanent key. A permanent key consists of a SecretId and a SecretKey. It represents the permanent identity of your account and does not expire.
- SecretId: used to identify the API caller.
- SecretKey: used to encrypt the signature string and server-side authentication signature string.


## Accessing COS Using a Permanent Key

### Accessing COS using an API request

When using an API request, you must use a signed request for a private bucket. A signature is generated based on a permanent key and put into the `Authorization` header to form a signed request. When the request is sent to COS, COS verifies whether the signature matches the request.

>? Because the signature generation algorithm is complex, you are advised to use an SDK to initiate a request and skip this step.
>

1. Use a permanent key to generate a signature.
For the signature algorithm, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778). COS provides a signature generation tool. You can also use a COS SDK to generate signatures. For more information, see [Implementing Signature in SDK](https://intl.cloud.tencent.com/document/product/436/7778#sdk-.E7.AD.BE.E5.90.8D.E5.AE.9E.E7.8E.B0). You can also write a program to generate signatures. However, this method is not recommended because the signature algorithm is complex.
2. Enter the signature into the `Authorization` header.
When initiating an API request, enter the signature into the standard HTTP `Authorization` header. The following is an example of a `GetObject` request:
```
GET /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: q-sign-algorithm=sha1&q-ak=SecretId&q-sign-time=KeyTime&q-key-time=KeyTime&q-header-list=HeaderList&q-url-param-list=UrlParamList&q-signature=Signature
```

### Accessing COS using an SDK tool

1. Initialize the identity information with the permanent key.
After installing the SDK tool, enter the permanent key (SecretId and SecretKey) of the root account or sub-account to initialize the user identity information.
2. Directly use the SDK tool to initiate requests to COS.
After initialization, you can directly use the SDK tool for upload, download, and other basic operations, without the need to generate signatures like using API requests, because the SDK tool generates signatures based on keys on your behalf and initiates requests to COS.

The following is an example of the corresponding Java SDK code. For demos of other languages, see the corresponding quick start documentation in [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474).
```
// 1. Initialize the user credentials (secretId, secretKey).
// Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to view and manage the `SecretId` and `SecretKey` of your project.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 2. Set the bucket region. For abbreviations of COS regions, please visit https://cloud.tencent.com/document/product/436/6224.
// `clientConfig` contains the set methods to set region, HTTPS (HTTP by default), timeout, and proxy. For detailed usage, please see the source code or the FAQs about the SDK for Java.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// The HTTPS protocol is recommended.
// Starting from 5.6.54, HTTPS is used by default.
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3. Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);

```


