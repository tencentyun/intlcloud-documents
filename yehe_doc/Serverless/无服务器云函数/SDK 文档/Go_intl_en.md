## Overview
* Welcome to Tencent Cloud Software Development Kit (SDK) 3.0, a companion tool for the TencentCloud API 3.0 platform. SDK 3.0 is unified and features the same SDK usage, API call methods, error codes, and returned packet formats for different programming languages.
* This document describes how to use, debug, and connect to TencentCloud APIs with the SDK for Go 3.0 as an example.
* This version currently supports various Tencent Cloud products such as CVM, VPC, and CBS and will support more products in the future.

## Dependent Environment

* Go 1.9 or above (Go 1.14 is required if `go mod` is used). Plus, the necessary environment variables such as `GOPATH` should be set properly.
* Get the security credential, which consists of `SecretId` and `SecretKey`. `SecretId` is used to identify the API requester, while `SecretKey` is a key used for signature string encryption and authentication by the server. You can get them on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page as shown below:
![](https://main.qcloudimg.com/raw/53199c4c8465fb2c13a26fe18e42e63b.png)
>!**Your security credential represents your account identity and granted permissions, which is equivalent to your login password. Do not disclose it to others.**
* Get the calling address (endpoint), which is generally in the format of `*.tencentcloudapi.com` and varies by product. For example, the endpoint of CVM is `cvm.tencentcloudapi.com`. For specific endpoints, please see the [API documentation](https://intl.cloud.tencent.com/zh/document/apii) of the corresponding product.

## Installing SDK

### Method 1. Install through go get (recommended)
We recommend you use a Tencent Cloud mirror for faster download:
<table>
   <tr>
      <th width="0px" style="text-align:center">OS</td>
      <th width="0px" style="text-align:center">Command</td>

   </tr>
   <tr>
      <td style="text-align:center">
Linux/macOS 
</td>
      <td ><dx-codeblock>
::: 1 go
export GOPROXY=https://mirrors.tencent.com/go/
:::
</dx-codeblock></a></td>
</tr>
   <tr>
      <td style="text-align:center">
Windows
</td>
      <td><dx-codeblock>
::: 1 go
set GOPROXY=https://mirrors.tencent.com/go/
:::
</dx-codeblock></a></td>
</tr>
</table>

Starting from v1.0.170, you can download packages by product. You only need to download the basic package and the corresponding product package (such as CVM) instead of downloading the packages of all Tencent Cloud products, which speeds up the image build and compilation. Of course, you can also download the packages of all products at once in the same way as before.
>?
>- On-Demand installation method: you can only use the **Go Modules** mode for dependency management, that is, the environment variable `GO111MODULE` should be `auto` or `on`, and `go mod init xxx` should be executed in your project . If you use `GOPATH`, please see the [full installation method](#fullInstallation).
>- Full installation method: it supports both `GOPATH` and `Go Modules`.
[](id:fullInstallation)
<table>
   <tr>
      <th width="0px" style="text-align:center">Installation Method</td>
      <th width="0px" style="text-align:center">Description</td>
      <th width="0px" style="text-align:center">Command</td>
   </tr>
	    <tr>
    <td style="text-align:center" rowspan= "2">On-Demand installation (recommended)</td>
    <td style="text-align:center">Install the common basic package</td>
    <td><dx-codeblock>
::: 1 bash
go get -v -u github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common
:::
</dx-codeblock></td>
  </tr>
	   <tr>
    <td style="text-align:center">Install the corresponding product package (such as CVM)</td>
    <td ><dx-codeblock>
::: 1 bash
go get -v -u github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/cvm
:::
</dx-codeblock></td>
  </tr>
		   <tr>
    <td style="text-align:center">Full installation</td>
    <td style="text-align:center">Download the packages of all Tencent Cloud products at once</td>
		    <td><dx-codeblock>
::: 1 bash
go get -v -u github.com/tencentcloud/tencentcloud-sdk-go
:::
</dx-codeblock></td>
</tr>
</table>

>?In order to support `go mod`, the SDK version number has been reduced from v3.x to v1.x, and all tags of `v3.0.*` and `3.0.*` were removed on May 10, 2021. If you need to backtrack previous tags, please refer to the `commit2tag` file in the root directory of the project.

### Method 2. Install through source code
Go to the [GitHub](https://github.com/tencentcloud/tencentcloud-sdk-go) or [Gitee](https://gitee.com/tencentcloud/tencentcloud-sdk-go) code hosting page to download the latest code, decompress, and install it in the `$GOPATH/src/github.com/tencentcloud` directory.

## Using SDK
Each API has a corresponding request structure and a response structure. For example, the `DescribeInstances` API for querying the CVM instance list has a request structure `DescribeInstancesRequest` and a response structure `DescribeInstancesResponse`.

The following uses the CVM instance list querying API as an example to describe the basic usage of the SDK.
<dx-codeblock>
::: Simplified Go
```go
package main

import (
     "fmt"
     "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
     "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/errors"
     "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/profile"
     "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/regions"
     cvm "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/cvm/v20170312"
)

func main() {
     credential := common.NewCredential("secretId", "secretKey")
     client, _ := cvm.NewClient(credential, regions.Guangzhou, profile.NewClientProfile())

     request := cvm.NewDescribeInstancesRequest()
     response, err := client.DescribeInstances(request)

     if _, ok := err.(*errors.TencentCloudSDKError); ok {
          fmt.Printf("An API error has returned: %s", err)
          return
     }
     if err != nil {
          panic(err)
     }
     fmt.Printf("%s\n", response.ToJsonString())
}
```
:::
::: Detailed Go
```go
package main

import (
     "fmt"
     "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
     "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/errors"
     "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/profile"
     "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/regions"
     cvm "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/cvm/v20170312"
)

func main() {
     // Essential steps:
     // Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters.
     // You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others;
     // otherwise, the key pair may be leaked, causing damage to your properties.
     credential := common.NewCredential("secretId", "secretKey")

     // Nonessential steps
     // Instantiate a client configuration object. You can specify the timeout period and other configuration items
     cpf := profile.NewClientProfile()
     // The SDK uses the POST method by default.
     // If you have to use the GET method, you can set it here, but the GET method cannot handle some large requests.
     // Do not modify the default settings unless absolutely necessary.
     cpf.HttpProfile.ReqMethod = "POST"
     // The SDK has a default timeout period. Do not adjust it unless absolutely necessary.
     // If needed, check in the code to get the latest default value.
     cpf.HttpProfile.ReqTimeout = 30
     // The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance availability zone,
     // you have to manually specify the domain name, such as cvm.ap-shanghai-fsi.tencentcloudapi.com for the Shanghai Finance availability zone
     cpf.HttpProfile.Endpoint = "cvm.tencentcloudapi.com"
     // The SDK uses `TC3-HMAC-SHA256` for signing by default, which is more secure but slightly reduces the performance.
     // Do not modify the default settings unless absolutely necessary.
     cpf.SignMethod = "TC3-HMAC-SHA256"
     // The SDK uses `zh-CN` calls to return Chinese content by default. You can also set it to `en-US` to return English content.
     // However, most products or APIs do not fully support returns in English.
     // Do not modify the default settings unless absolutely necessary.
     cpf.Language = "en-US"
     // Print logs. The default value is `false`
     // cpf.Debug = true
     // Instantiate the client object to request the product (with CVM as an example).
     // The second parameter is the region information. You can directly enter the string `ap-guangzhou` or import the preset constant
     client, _ := cvm.NewClient(credential, regions.Guangzhou, cpf)
     // Instantiate a request object. You can further set the request parameters according to the API called and actual conditions
     // You can directly check the SDK source code to determine which attributes of `DescribeInstancesRequest` can be set.
     // An attribute may be of a basic type or import another data structure.
     // You are recommended to use the IDE for development where you can easily redirect to and view the documentation of each API and data structure.
     request := cvm.NewDescribeInstancesRequest()

     // Settings of a basic parameter.
     // This API allows setting the number of instances returned, which is specified as only one here.
     // The SDK uses the pointer style to specify parameters, so even for basic parameters, you need to use pointers to assign values to them.
     // The SDK provides encapsulation functions for importing the pointers of basic parameters
     request.Limit = common.Int64Ptr(1)

     // Settings of an array.
     // This API allows filtering by specified instance ID; however, as it conflicts with the `Filter` parameter to be demonstrated next, it is commented out here.
     // request.InstanceIds = common.StringPtrs([]string{"ins-r8hr2upy"})

     // Settings of a complex object.
     // In this API, `Filters` is an array whose elements are complex objects `Filter`, and the member `Values` of `Filter` are string arrays.
     request.Filters = []*cvm.Filter{
         &cvm.Filter{
          Name: common.StringPtr("zone"),
          Values: common.StringPtrs([]string{"ap-guangzhou-1"}),
         },
     }

     // Call the API you want to access through the client object; you need to pass in the request object.
     response, err := client.DescribeInstances(request)
     // Handle the exception
     if _, ok := err.(*errors.TencentCloudSDKError); ok {
         fmt.Printf("An API error has returned: %s", err)
         return
     }
     // This is a direct failure instead of SDK exception. You can add other troubleshooting measures in the real code.
     if err != nil {
         panic(err)
     }
     // Print the returned JSON string
     fmt.Printf("%s\n", response.ToJsonString())
}
```
:::
</dx-codeblock>

>?For the purpose of demonstration, some nonessential items such as modification of the default configuration have been included to show the features of the SDK. When you write code to use the SDK, we recommend you use the default configuration as much as possible and make changes as needed.

## More Examples
For more samples, please see the [examples](https://github.com/TencentCloud/tencentcloud-sdk-go/tree/master/examples) directory. For the sample of initializing a request for a complicated API, please see [example 1](https://github.com/TencentCloud/tencentcloud-sdk-go/blob/master/examples/cvm/v20170312/run_instances.go). For the sample of initializing a request by using a JSON string, please see [example 2](https://github.com/TencentCloud/tencentcloud-sdk-go/blob/master/examples/cvm/v20170312/describe_instances.go).


## Relevant Configuration
**If you have no special needs, we recommend you use the default configuration.**

Before creating a client, if necessary, you can make some configuration changes by modifying the field values in `profile.ClientProfile`.

```go
// Nonessential steps
// Instantiate a client configuration object. You can specify the timeout period and other configuration items
cpf := profile.NewClientProfile()
```
The specific configuration items are as described below:

### Request method

The SDK uses the POST method by default. If you have to use the GET method, you can set it here, **but the GET method cannot handle some large requests**.

```go
cpf.HttpProfile.ReqMethod = "POST"
```

### Timeout period

The SDK has a default timeout period. Do not adjust it unless absolutely necessary. If needed, check in the code to get the latest default value.  
Unit: second

```go
cpf.HttpProfile.ReqTimeout = 30
```

### Specifying domain name

The SDK automatically specifies the domain name, so you generally don't need to do so. However, if you are accessing a service in a finance zone, you have to manually specify the domain name. For example, the CVM domain name of the Shanghai Finance Zone is `cvm.ap-shanghai-fsi.tencentcloudapi.com`.

```go
cpf.HttpProfile.Endpoint = "cvm.tencentcloudapi.com"
```

### Signature algorithm

The SDK uses `TC3-HMAC-SHA256` for signing by default, which is more secure but slightly reduces the performance.

```go
cpf.SignMethod = "HmacSHA1"
```

### DEBUG mode

More detailed logs will be printed in DEBUG mode, which can be enabled when you need to troubleshoot in detail.  
The default value is `false`.

```go
cpf.Debug = true
```

### Proxy

If there is a proxy in your environment, you need to set the system environment variable `https_proxy`; otherwise, it may not be called normally, and a connection timeout exception will be thrown.

### Enabling DNS cache

Currently, the SDK for Go always requests the DNS server without using the cache of nscd. You can export the environment variable `GODEBUG=netdns=cgo` or specify the `-tags 'netcgo'` parameter when compiling `go build` so as to get the nscd cache.

### Ignoring server certificate verification

When the SDK is used to call a public cloud service, the server certificate must be verified to identify forged servers and ensure request security. However, in some extreme cases such as testing, you may need to ignore self-signed server certificates. Below is one of the possible methods:

```
import "crypto/tls"
...
      client, _ := cvm.NewClient(credential, regions.Guangzhou, cpf)
      tr := &http.Transport{
          TLSClientConfig: &tls.Config{InsecureSkipVerify: true},
      }
      client.WithHttpTransport(tr)
...
```

>!Unless you know what you are doing and understand the risks involved, do not try to disable server certificate verification.

## Error Handling
Starting from `v1.0.181`, Tencent Cloud SDK for Go defines the error codes returned by each product as constants. You can directly call them for handling without manual definition required. If you use an IDE (such as GoLand) for development, you can use their code hint features to choose directly; for example,

```go
...//Your other go code

// Handling errors
response, err := client.DescribeInstances(request)
if terr, ok := err.(*errors.TencentCloudSDKError); ok {
      code :=terr.GetCode()
      if code == cvm.FAILEDOPERATION_ILLEGALTAGKEY{
          fmt.Printf("Handling error: FailedOperation.IllegalTagKey,%s", err)
      }else if code == cvm.UNAUTHORIZEDOPERATION{
          fmt.Printf("Handling error: UnauthorizedOperation,%s", err)
      }else{
          fmt.Printf("An API error has returned: %s", err)
      }
      return
}
...
```

At the same time, the comment section of each API function also lists the error codes it may return for your reference:

```go
// DescribeInstances
// This API is used to query the details of one or multiple instances.
//
// 
//
// * You can query the details of an instance according to its `ID`, name, billing mode, or other information. For more information on how to filter information, please see `Filter`.
//
// * If no parameter is defined, the status of a certain number of instances under the current account will be returned. The number is specified by `Limit` and is 20 by default.
//
// * The latest operation (LatestOperation) and the latest operation status (LatestOperationState) of the instance can be queried.
//
// Possible error codes:
//  FAILEDOPERATION_ILLEGALTAGKEY = "FailedOperation.IllegalTagKey"
//  FAILEDOPERATION_ILLEGALTAGVALUE = "FailedOperation.IllegalTagValue"
//  FAILEDOPERATION_TAGKEYRESERVED = "FailedOperation.TagKeyReserved"
//  INTERNALSERVERERROR = "InternalServerError"
//  INVALIDFILTER = "InvalidFilter"
//  INVALIDFILTERVALUE_LIMITEXCEEDED = "InvalidFilterValue.LimitExceeded"
//  INVALIDHOSTID_MALFORMED = "InvalidHostId.Malformed"
//  INVALIDINSTANCEID_MALFORMED = "InvalidInstanceId.Malformed"
//  INVALIDPARAMETER = "InvalidParameter"
//  INVALIDPARAMETERVALUE = "InvalidParameterValue"
//  INVALIDPARAMETERVALUE_IPADDRESSMALFORMED = "InvalidParameterValue.IPAddressMalformed"
//  INVALIDPARAMETERVALUE_INVALIDIPFORMAT = "InvalidParameterValue.InvalidIpFormat"
//  INVALIDPARAMETERVALUE_INVALIDVAGUENAME = "InvalidParameterValue.InvalidVagueName"
//  INVALIDPARAMETERVALUE_LIMITEXCEEDED = "InvalidParameterValue.LimitExceeded"
//  INVALIDPARAMETERVALUE_SUBNETIDMALFORMED = "InvalidParameterValue.SubnetIdMalformed"
//  INVALIDPARAMETERVALUE_TAGKEYNOTFOUND = "InvalidParameterValue.TagKeyNotFound"
//  INVALIDPARAMETERVALUE_VPCIDMALFORMED = "InvalidParameterValue.VpcIdMalformed"
//  INVALIDSECURITYGROUPID_NOTFOUND = "InvalidSecurityGroupId.NotFound"
//  INVALIDSGID_MALFORMED = "InvalidSgId.Malformed"
//  INVALIDZONE_MISMATCHREGION = "InvalidZone.MismatchRegion"
//  RESOURCENOTFOUND_HPCCLUSTER = "ResourceNotFound.HpcCluster"
//  UNAUTHORIZEDOPERATION_INVALIDTOKEN = "UnauthorizedOperation.InvalidToken"
func (c *Client) DescribeInstances(request *DescribeInstancesRequest) (response *DescribeInstancesResponse, err error){
    ...
}

```



## Common Client
Starting from `v1.0.189`, Tencent Cloud SDK for Go supports the use of `Common Client` mode for requests. You only need to install the `common` package to initiate calls to any Tencent Cloud product.

>?You must clearly know the parameters required by the called API; otherwise, the call may fail.

Currently, only the POST method is supported, and the signature algorithm must be signature algorithm v3. For detailed usage, please see the [Using Common Client to Call](https://github.com/TencentCloud/tencentcloud-sdk-go/blob/master/examples/common/common_client.go) sample.

## Request Retry
### Retry upon network error

The SDK can be configured to automatically retry when a network error or timeout occurs. This is not enabled by default. You can configure the number of retries and retry interval through `ClientProfile`.

>?The `Request` structure is checked for whether it has the `ClientToken` field, and if so, it will be considered an idempotent request. Only idempotent requests will be retried automatically in case of network errors, while exceptions will be thrown for non-idempotent requests to prevent inconsistent results caused by multiple replays of the requests.

```golang
package main
import (
	     "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	     "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/profile"
	     "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/regions"
	     cvm "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/cvm/v20170312"
)

func main() {
	     credential := common.NewCredential("secretId", "secretKey")
	     prof := profile.NewClientProfile()
	     prof.NetworkFailureMaxRetries = 3                               // Define the maximum number of retry attempts
	     prof.NetworkFailureRetryDuration = profile.ExponentialBackoff   // Define the retry interval time
	     client, _ := cvm.NewClient(credential, regions.Guangzhou, prof)

	// ...
}
```
For more usage information, please see the [testing file](https://github.com/TencentCloud/tencentcloud-sdk-go/tree/master/tencentcloud/common/netretry_test.go).

### Retry upon frequency limiting

The SDK can be configured to automatically retry when API call frequency limiting is triggered. This is not enabled by default. You can configure the number of retries and retry interval through `ClientProfile`.

```golang
package main

import (
	     "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	     "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/profile"
	     "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/regions"
	     cvm "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/cvm/v20170312"
)

func main() {
	     credential := common.NewCredential("secretId", "secretKey")
	     prof := profile.NewClientProfile()
	     prof.RateLimitExceededMaxRetries = 3                               // Define the maximum number of retry attempts
	     prof.RateLimitExceededRetryDuration = profile.ExponentialBackoff   // Define the retry interval time
	     client, _ := cvm.NewClient(credential, regions.Guangzhou, prof)

	// ...
}
```

### Idempotence flag

When retry upon network timeout or frequency limiting is enabled, the `ClientToken` parameter will be automatically injected into the request (if the request has an empty `ClientToken` field). If you manually specify `ClientToken`, the injection process will be skipped.

>?The injected `ClientToken` provides global uniqueness below a `100000/s` concurrency.

## FAQs
### Package import failed
For example, if the error `imported and not used: "os"` is reported, it means that the package `os` is not used in the code. Therefore, simply remove it.
