## Overview
Welcome to Tencent Cloud Software Development Kit (SDK) 3.0, a companion tool for the Cloud API 3.0 platform. All cloud services and products will be integrated here for access in the future. The new version of SDK is unified and features the same SDK usage, API call methods, error codes and return packet formats for different languages.
To make it easier for Go developers to debug and access the APIs of Tencent Cloud products, this document describes the Tencent Cloud SDK for Go and provides a simple example of using the SDK for the first time, helping you quickly get the SDK and start calling.

## List of Products Supporting SDK 3.0

<table>
  <tr>
    <td><a href="https://cloud.tencent.com/document/api/213/15689">CVM</a></td>
    <td><a href="https://cloud.tencent.com/document/api/362/15634">CBS</a></td>
    <td><a href="https://cloud.tencent.com/document/api/583/17235">SCF</a></td>
    <td><a href="https://cloud.tencent.com/document/api/236/15830 ">TencentDB for MySQL</a></td>
  </tr>
  <tr>
    <td><a href="https://cloud.tencent.com/document/api/571/18122">DTS</a></td>
	<td></td>
	<td></td>
	<td></td>
  </tr>
</table>


## Dependent Environment
1. Go version 1.9 or higher. Plus, the necessary environment variables such as GOPATH have to be set properly.
2. Before using, make sure to activate the corresponding product in the Tencent Cloud [Console](https://console.cloud.tencent.com/).
3. Get the SecretID and SecretKey on the [Access Management](https://console.cloud.tencent.com/cam/capi) page in the Tencent Cloud Console.

## Installation
Obtain the security credentials before installing the SDK for Go. Before using the Cloud API for the first time, you need to first apply for security credentials in the Tencent Cloud Console, including SecretID and SecretKey. SecretID is used to identify the API caller, while SecretKey is used to encrypt the signature string and verify it on the server. You must keep the SecretKey private and avoid disclosure.
### Installing via go get (Recommended)
It is recommended to install the SDK using the tool that comes with the language:
```
 go get -u github.com/tencentcloud/tencentcloud-sdk-go
```
### Installing via Source Code
Go to the [Github code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-go) or [quick download page](https://tencentcloud-sdk-1253896243.file.myqcloud.com/tencentcloud-sdk-go/tencentcloud-sdk-go.zip) to download the latest code, decompress and install it in the `$GOPATH/src/github.com/tencentcloud` directory.

## Example
Each API has a corresponding request structure and a response structure. For example, the DescribeZones API for querying availability zones has a corresponding request structure DescribeZonesRequest and a response structure DescribeZonesResponse.
The following uses the API for querying availability zones as an example to introduce the basic usage of the SDK.
```
package main

import (
        "fmt"

        "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
        "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/errors"
        "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/profile"
        cvm "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/cvm/v20170312"
)

func main() {
        // Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
        credential := common.NewCredential(
                "your-secret-id",
                "your-secret-key",
        )

        // Instantiate a client configuration object; you can specify the timeout and other configurations.
        cpf := profile.NewClientProfile()
        cpf.HttpProfile.ReqMethod = "GET"
        cpf.HttpProfile.ReqTimeout = 5
        cpf.SignMethod = "HmacSHA1"

        // Instantiate the client object to request the product (with CVM as an example).
        client, _ := cvm.NewClient(credential, "ap-beijing", cpf)
        // Instantiate a request object; you can further set the request parameters according to the API called and actual conditions.
        request := cvm.NewDescribeZonesRequest()
        // Call the API you want to access through the client object; you need to pass in the request object.
        response, err := client.DescribeZones(request)
        // Handle the exception
        if _, ok := err.(*errors.TencentCloudSDKError); ok {
                fmt.Printf("An API error has returned: %s", err)
                return
        }
        // unexpected errors
        if err != nil {
                panic(err)
        }
        // Print the returned json string
        fmt.Printf("%s", response.ToJsonString())
}
```

## More Examples

For more examples, see the [examples](https://github.com/TencentCloud/tencentcloud-sdk-go/tree/master/examples) directory. For an example of request initialization for complex APIs, see examples/cvm/v20170312/run_instances.go. For an example of initializing a request using a json string, see examples/cvm/v20170312/describe_instances.go.
