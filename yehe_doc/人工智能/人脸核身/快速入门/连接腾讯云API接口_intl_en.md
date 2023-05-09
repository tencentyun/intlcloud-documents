# Connecting to TencentCloud API

TencentCloud API 3.0 integrates SDKs for multiple programming languages, making it easier for you to call APIs. It supports nearby access, and the domain name for nearby access is `faceid.tencentcloudapi.com`. It also supports access using a domain name with a specified region, for example, the domain name for the Singapore region is `faceid.ap-singapore. tencentcloudapi.com`.

We recommend that you use the domain name for nearby access. When you call an API, the request is automatically resolved to a server in the region **nearest** to the location where the API is called. For example, if a request is made in Singapore, it will be automatically resolved to a server in Singapore, which has the same effect as specifying `faceid.ap-singaporef.tencentcloudapi.com`.

**Note:**

1. **For latency-sensitive businesses, we recommend that you specify the region in the domain name.**

2. **A domain name is an API access point and does not represent the region where the product or API actually provides services. For the list of regions supported by the product, see the call method/common parameter document. For the regions supported by the API, see the input parameters part in the API document.**

You can select the language you are familiar with for coding. This section uses the Go language as an example to show how to integrate the Tencent Cloud SDK into your server.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python-intl-en/blob/master/tencentcloud/faceid/v20180301/faceid_client.py)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java-intl-en/blob/master/src/main/java/com/tencentcloudapi/faceid/v20180301/FaceidClient.java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php-intl-en/blob/master/src/TencentCloud/Faceid/V20180301/FaceidClient.php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go-intl-en/blob/master/tencentcloud/faceid/v20180301/client.go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs-intl-en/blob/master/tencentcloud/faceid/v20180301/faceid_client.js)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet-intl-en/blob/master/TencentCloud/Faceid/V20180301/FaceidClient.cs)
* [Tencent Cloud SDK 3.0 for C++](https://github.com/TencentCloud/tencentcloud-sdk-cpp-intl-en/blob/master/faceid/src/v20180301/FaceidClient.cpp)

### Environmental dependency

1. Go 1.9 or above, with the necessary environment variables such as `GOPATH` set properly
2. Activate the FaceID product by following the [process guide](https://www.tencentcloud.com/document/product/1061/37028?lang=en&pg=)
3. Obtain SecretId and SecretKey by following the [guide to getting the secret key](https://console.tencentcloud.com/cam/capi)

### Installation

#### Installing through go get (recommended)

We recommend you install the SDK by using the tool that comes with the language.

```shell
go get -u github.com/tencentcloud/tencentcloud-sdk-go-intl-en
```

#### Installing through source code

Go to the [GitHub](https://github.com/tencentcloud/tencentcloud-sdk-go-intl-en) page to download the latest code, and decompress it to `$GOPATH/src/github.com/tencentcloud`.

### Integrating into the server

After the Tencent Cloud SDK is installed, you can use the import command to integrate the SDK into the server. The sample code is as follows:

```go
package main

import (
   "fmt"
   cloud "github.com/tencentcloud/tencentcloud-sdk-go-intl-en/tencentcloud/common"
   "github.com/tencentcloud/tencentcloud-sdk-go-intl-en/tencentcloud/common/profile"
   faceid "github.com/tencentcloud/tencentcloud-sdk-go-intl-en/tencentcloud/faceid/v20180301"
)

func main() {
   // Instantiate a client configuration object. You can specify the timeout period and other configuration items
   prof := profile.NewClientProfile()
   prof.HttpProfile.ReqTimeout = 60
   // TODO replace the SecretId and SecretKey string with the API SecretId and SecretKey
   credential := cloud.NewCredential("SecretId", "SecretKey")
   // Instantiate the client object of the requested faceid
   FaceIdClient, _ := faceid.NewClient(credential, "ap-singapore", prof)

   // Instantiate the request object and provide necessary parameters
   request := faceid.NewGetFaceIdTokenIntlRequest()
   var SecureLevel = "4"
   request.SecureLevel = &SecureLevel
   // Call the Tencent Cloud API through FaceIdClient
   response, _ := FaceIdClient.GetFaceIdTokenIntl(request)
   // Process the Tencent Cloud API response
   fmt.Println("response: ", *response.Response.SdkToken)
}

```
