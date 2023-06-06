

腾讯云API 3.0集成支持多种编程语言的SDK，让你调用API更简单，云API 支持就近地域接入，本产品就近地域接入域名为 faceid.tencentcloudapi.com ，也支持指定地域域名访问，例如新加坡地域的域名为 faceid.ap-singapore.tencentcloudapi.com。

推荐使用就近地域接入域名。根据调用接口时客户端所在位置，会自动解析到**最近的**某个具体地域的服务器。例如在新加坡发起请求，会自动解析到新加坡的服务器，效果和指定 faceid.ap-singaporef.tencentcloudapi.com 是一致的。

**注意：**

1. **对时延敏感的业务，建议指定带地域的域名。**

2. **域名是 API 的接入点，并不代表产品或者接口实际提供服务的地域。产品支持的地域列表请在调用方式/公共参数文档中查阅，接口支持的地域请在接口文档输入参数中查阅**

你可以选择你所熟悉的语言进行编码，这部分将使用golang语言作为示例演示如何将腾讯云SDK继承到自己的服务端模块中。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python-intl-en/blob/master/tencentcloud/faceid/v20180301/faceid_client.py)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java-intl-en/blob/master/src/main/java/com/tencentcloudapi/faceid/v20180301/FaceidClient.java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php-intl-en/blob/master/src/TencentCloud/Faceid/V20180301/FaceidClient.php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go-intl-en/blob/master/tencentcloud/faceid/v20180301/client.go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs-intl-en/blob/master/tencentcloud/faceid/v20180301/faceid_client.js)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet-intl-en/blob/master/TencentCloud/Faceid/V20180301/FaceidClient.cs)
* [Tencent Cloud SDK 3.0 for C++](https://github.com/TencentCloud/tencentcloud-sdk-cpp-intl-en/blob/master/faceid/src/v20180301/FaceidClient.cpp)

### 环境依赖

1. Go1.9或者更高版本，并且必须正确设置必要的环境变量，比如GOPATH
2. 使用前请阅读[流程指引](https://www.tencentcloud.com/document/product/1061/37028?lang=en&pg=)开通人脸核身产品
3. 按照[获取秘钥指引](https://console.tencentcloud.com/cam/capi)操作获取SecretId和SecretKey

### 安装

#### 通过go get安装（推荐）

推荐使用语言自带的工具安装SDK。

```shell
go get -u github.com/tencentcloud/tencentcloud-sdk-go-intl-en
```

#### 通过源码安装

到[Github](https://github.com/tencentcloud/tencentcloud-sdk-go-intl-en)代码托管页面下载最新代码，解压安装到$GOPATH/src/github.com/tencentcloud目录下。

### 集成到服务端

腾讯云SDK安装完成之后，可以通过import指令将SDK集成服务端，示例代码如下：

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