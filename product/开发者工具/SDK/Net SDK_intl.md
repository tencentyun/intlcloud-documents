## Overview
Welcome to Tencent Cloud Software Development Kit (SDK) 3.0, a companion tool for the TencentCloud API 3.0 platform. All cloud services and products will be integrated here for access in the future. The new version of SDK is unified and features the same SDK usage, API call methods, error codes and return packet formats for different languages.
To make it easier for .NET developers to debug and access the APIs of Tencent Cloud products, this document describes the Tencent Cloud SDK for .NET and provides a simple example of using the SDK for the first time, helping you quickly get the SDK and start calling.

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

1. Dependent environment: .NET Framework 4.5+ and .NET Core 2.1.
2. Activate the corresponding product in the Tencent Cloud [Console](https://console.cloud.tencent.com/).
3. Get the SecretID, SecretKey and call address (endpoint). The general format of endpoint is *.tencentcloudapi.com. For example, the call address of CVM is cvm.tencentcloudapi.com. For details, see the documentation of the specific product.
4. Download the relevant materials and configure the relevant files.


## Installation

Obtain the security credentials before installing the SDK for .NET. Before using the TencentCloud API for the first time, you need to first apply for security credentials in the Tencent Cloud Console, including SecretID and SecretKey. SecretID is used to identify the API caller, while SecretKey is used to encrypt the signature string and verify it on the server. You must keep the SecretKey private and avoid disclosure.

### Installation via NuGet (Recommended)

1. Install using the command line `dotnet add package TencentCloudSDK --version 3.0.0`. Please go to the [NuGet](https://www.nuget.org/packages/TencentCloudSDK/) page to get additional information.
2. Add the package via Visual Studio.

### Installing via Source Package
Go to the [Github code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-dotnet) or [quick download page](https://tencentcloud-sdk-1253896243.file.myqcloud.com/tencentcloud-sdk-dotnet/tencentcloud-sdk-dotnet.zip) to download the latest code, decompress and install it in your working directory and then open it with Visual Studio 2017 for compiling.

## Example
Each API has a corresponding request structure and a response structure. For example, the DescribeInstances API for querying CVM instance list has a corresponding request structure DescribeInstancesRequest and a response structure DescribeInstancesResponse.

The following uses the API for querying CVM instance list as an example to introduce the basic usage of the SDK. For the purpose of demonstration, some nonessential items have been added to show the common functions of the SDK, which makes the example look bloated. When using the SDK to write code, it is recommended to keep it simple.

```
using System;
using System.Threading.Tasks;
using TencentCloud.Common;
using TencentCloud.Common.Profile;
using TencentCloud.Cvm.V20170312;
using TencentCloud.Cvm.V20170312.Models;

namespace TencentCloudExamples
{
    class DescribeInstances
    {
        static void Main(string[] args)
        {
            try
            {
                // Essential steps:
                // Instantiate an authentication object. The Tencent Cloud account key pair secretId and secretKey need to be passed in as the input parameters.
                // The example here uses the way to read from environment variable, so you need to set these two values in the environment variable first.
                // You can also write the key pair directly into the code, but be careful not to copy, upload or share the code to others.
                // Otherwise, the key pair may be leaked, causing damage to your properties.
                Credential cred = new Credential {
                    SecretId = Environment.GetEnvironmentVariable("TENCENTCLOUD_SECRET_ID"),
                    SecretKey = Environment.GetEnvironmentVariable("TENCENTCLOUD_SECRET_KEY")
                };

                // Instantiate a client option (optional; skip if no special requirements are present).
                ClientProfile clientProfile = new ClientProfile();
                // Specify the signature algorithm (HmacSHA256 by default).
                clientProfile.SignMethod = ClientProfile.SIGN_SHA1;
                // Nonessential steps
                // Instantiate a client configuration object; you can specify the timeout and other configurations.
                HttpProfile httpProfile = new HttpProfile();
                // The SDK uses the POST method by default.
                // If you have to use the GET method, you can set it here, but the GET method cannot handle some large requests.
                httpProfile.ReqMethod = "POST";
                // The SDK has a default timeout; do not adjust it unless absolutely necessary.
                // If needed, check in the code to get the latest default value.
                httpProfile.Timeout = 10; // Request connection timeout in seconds (60 seconds by default).
                // The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a financial availability zone,
                // you have to manually specify the domain name, such as cvm.ap-shanghai-fsi.tencentcloudapi.com for the Shanghai financial availability zone.
                httpProfile.Endpoint = ("cvm.tencentcloudapi.com");
                // Proxy server; set when there is a proxy server in your environment.
                httpProfile.WebProxy = Environment.GetEnvironmentVariable("HTTPS_PROXY");

                clientProfile.HttpProfile = httpProfile;

                // Instantiate the client object to request the product (with CVM as an example).
                // The second parameter is the region information. You can directly enter the string ap-guangzhou or refer to the preset constant. clientProfile is optional.
                CvmClient client = new CvmClient(cred, "ap-guangzhou", clientProfile);

                // Instantiate a request object; you can further set the request parameters according to the API called and actual conditions.
                // You can directly query the SDK source code to determine which attributes of DescribeInstancesRequest can be set.
                // The attribute may be of a basic type or refer to another data structure.
                // It is recommended to use the IDE for development where you can easily jump to and view the documentation of each API and data structure.
                DescribeInstancesRequest req = new DescribeInstancesRequest();

                // Settings of a basic parameter.
                // This API allows you to set the number of instances returned. Here it is specified as only one.
                
                req.Limit = 1;
                // Settings of an array.
                // This API allows for filtering based on the specified instance ID; however, as it conflicts with the Filter parameter to be demonstrated next, it is skipped here.
                // req.InstanceIds = new string[] { "ins-r8hr2upy" };

                // Settings of a complex object.
                // In this API, "Filters" is an array whose elements are complex objects "Filter", and the Filter members "Values" are string arrays.
                // Populated request parameters. Here, the member variables of the request object are the input parameters of the corresponding API.
                // You can view the definition of the request parameter in the API documentation at the official website or by jumping to the definition of the request object.
                Filter respFilter = new Filter(); // Create a Filter object and query the CVM instance in the dimension of zone.
                respFilter.Name = "zone";
                respFilter.Values = new string[] { "ap-guangzhou-1", "ap-guangzhou-2" };
                req.Filters = new Filter[] { respFilter }; // Filters is a list of Filter objects.

                //// Here, you can assign values to the request parameters using a string in standard json format. The following code is equivalent to the parameter value assignment above.
                //string strParams = "{\"Filters\":[{\"Name\":\"zone\",\"Values\":[\"ap-guangzhou-1\",\"ap-guangzhou-2\"]}]}";
                //req = DescribeInstancesRequest.FromJsonString<DescribeInstancesRequest>(strParams);

                // Initialize the request by calling the DescribeInstances method on the client object. Note: The request method name corresponds to the request object.
                // The returned resp is an instance of the DescribeInstancesResponse class which corresponds to the request object.
                DescribeInstancesResponse resp = client.DescribeInstances(req).
                    ConfigureAwait(false).GetAwaiter().GetResult();

                // A string return packet in json format is output.
                Console.WriteLine(AbstractModel.ToJsonString(resp));

                // You can also take a single value.
                // You can view the definition of the return field in the API documentation at the official website or by jumping to the definition of the response object.
                Console.WriteLine(resp.TotalCount);

            }
            catch (Exception e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.Read();
        }
    }
}

```

## More Examples

For more examples, see the TencentCloudExamples directory at [GitHub](https://github.com/TencentCloud/tencentcloud-sdk-dotnet).
