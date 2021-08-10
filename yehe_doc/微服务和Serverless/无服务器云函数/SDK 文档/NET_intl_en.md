## Overview
* Welcome to Tencent Cloud Software Development Kit (SDK) 3.0, a companion tool for the TencentCloud API 3.0 platform. SDK 3.0 is unified and features the same SDK usage, API call methods, error codes, and returned packet formats for different programming languages.
* This document describes how to use, debug, and connect to TencentCloud APIs with the SDK for .NET 3.0 as an example.
* This version currently supports various Tencent Cloud products such as CVM, VPC, and CBS and will support more products in the future.

## Dependent Environment

* .NET Framework 4.5+ or .NET Core 2.1.
* Get the security credential, which consists of `SecretId` and `SecretKey`. `SecretId` is used to identify the API requester, while `SecretKey` is a key used for signature string encryption and authentication by the server. You can get them on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page as shown below:
![](https://main.qcloudimg.com/raw/53199c4c8465fb2c13a26fe18e42e63b.png)
>!**Your security credential represents your account identity and granted permissions, which is equivalent to your login password. Do not disclose it to others.**
* Get the calling address (endpoint), which is generally in the format of `*.tencentcloudapi.com` and varies by product. For example, the endpoint of CVM is `cvm.tencentcloudapi.com`. For specific endpoints, please see the [API documentation](https://intl.cloud.tencent.com/document/api) of the corresponding product .

## Installing SDK

### Method 1. Install through NuGet (recommended)
Install on the command line (**the version here is only an example. Please choose the latest version**):
```
    dotnet add package TencentCloudSDK --version 3.0.0
    # For other information, please go to www.nuget.org/packages/TencentCloudSDK
```
>!The commands should be executed in the home directory of the project.

Add a package through Visual Studio:
For example, to create a HelloWorld project, run:
```bash
dotnet new console -o HelloWorld
# Enter the home directory of the HelloWorld project
dotnet run
# The output is: Hello World!
dotnet add package TencentCloudSDK --version 3.0.0
# Download SDK dependencies for the project
```

>?
>- If you want to install the package of a certain product such as CVM, just add the dependency `TencentCloudSDK.Cvm`.
### Method 2. Install through source code
Go to the [GitHub code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-dotnet) to download the latest code, decompress and install it in your working directory, and then open it with Visual Studio 2017 for compiling.


## Using SDK

Each API has a corresponding request structure and a response structure. For example, the `DescribeInstances` API for querying the CVM instance list has a request structure `DescribeInstancesRequest` and a response structure `DescribeInstancesResponse`.

The following uses the CVM instance list querying API as an example to describe the basic usage of the SDK.

<dx-codeblock>
::: Simplified C#
```c#
using System;
using System.Threading.Tasks;
using TencentCloud.Common;
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
                 Credential cred = new Credential {"SecretId", "SecretKey"};
                 CvmClient client = new CvmClient(cred, "ap-guangzhou");
                 DescribeInstancesRequest req = new DescribeInstancesRequest();
                 DescribeInstancesResponse resp = client.DescribeInstancesSync(req);
                 Console.WriteLine(AbstractModel.ToJsonString(resp));
             }
             catch (Exception e)
            {
                 Console.WriteLine(e.ToString());
             }
         }
     }
}
```
:::
::: Detailed C#
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
                // Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters.
                // The example here uses the way to read from the environment variable, so you need to set these two values in the environment variable first.
                // You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others;
                // otherwise, the key pair may be leaked, causing damage to your properties.
                Credential cred = new Credential {
                    SecretId = Environment.GetEnvironmentVariable("TENCENTCLOUD_SECRET_ID"),
                    SecretKey = Environment.GetEnvironmentVariable("TENCENTCLOUD_SECRET_KEY")
                };               

                // (Optional) Instantiate a client option
                ClientProfile clientProfile = new ClientProfile();
                // Specify the signature algorithm. The default value is `HmacSHA256`
                clientProfile.SignMethod = ClientProfile.SIGN_SHA1;
                // Nonessential steps
                // Instantiate a client configuration object. You can specify the timeout period and other configuration items
                HttpProfile httpProfile = new HttpProfile();
                // The SDK uses the POST method by default.
                // If you have to use the GET method, you can set it here, but the GET method cannot handle some large requests.
                httpProfile.ReqMethod = "POST";
                // The SDK has a default timeout period. Do not adjust it unless absolutely necessary.
                // If needed, check in the code to get the latest default value.
                httpProfile.Timeout = 10; // Specify the request connection timeout value in seconds. The default value is 60s
                // The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance zone,
                // you have to manually specify the domain name. For example, the CVM domain name of the Shanghai Finance Zone is `cvm.ap-shanghai-fsi.tencentcloudapi.com`
                httpProfile.Endpoint = ("cvm.tencentcloudapi.com");
                // Proxy server. Set it when there is a proxy server in your environment
                httpProfile.WebProxy = Environment.GetEnvironmentVariable("HTTPS_PROXY");
    
                clientProfile.HttpProfile = httpProfile;
    
                // Instantiate the client object of the requested product (with CVM as an example)
                // The second parameter is the region information. You can directly enter the string `ap-guangzhou` or import the preset constant. `clientProfile` is optional
                CvmClient client = new CvmClient(cred, "ap-guangzhou", clientProfile);
    
                // Instantiate a request object. You can further set the request parameters according to the API called and actual conditions
                // You can directly check the SDK source code to determine which attributes of `DescribeInstancesRequest` can be set.
                // An attribute may be of a basic type or import another data structure.
                // We recommend you use the IDE for development where you can easily redirect to and view the documentation of each API and data structure.
                DescribeInstancesRequest req = new DescribeInstancesRequest();
    
                // Settings of a basic parameter.
                // This API allows setting the number of instances returned, which is specified as only one here.
                // The SDK uses the pointer style to specify parameters, so even for basic parameters, you need to use pointers to assign values to them.
                // The SDK provides encapsulation functions for importing the pointers of basic parameters
                req.Limit = 1;
                // Settings of an array.
                // This API allows filtering by specified instance ID; however, as it conflicts with the `Filter` parameter to be demonstrated next, it is commented out here.
                // req.InstanceIds = new string[] { "ins-r8hr2upy" };
    
                // Settings of a complex object.
                // In this API, `Filters` is an array whose elements are complex `Filter` objects, and the member `Values` of `Filter` are string arrays.
                // Populate the request parameters. Here, the member variables of the request object are the input parameters of the corresponding API
                // You can view the definition of the request parameters in the API documentation at the official website or by redirecting to the definition of the request object
                Filter respFilter = new Filter(); // Create a `Filter` object to query CVM instances in the `zone` dimension
                respFilter.Name = "zone";
                respFilter.Values = new string[] { "ap-guangzhou-1", "ap-guangzhou-2" };
                req.Filters = new Filter[] { respFilter }; // `Filters` is a list of `Filter` objects
    
                //// Here, you can assign values to the request parameters by using a string in standard JSON format. The following code is equivalent to the above parameter value assignment
                //string strParams = "{\"Filters\":[{\"Name\":\"zone\",\"Values\":[\"ap-guangzhou-1\",\"ap-guangzhou-2\"]}]}";
                //req = DescribeInstancesRequest.FromJsonString<DescribeInstancesRequest>(strParams);
    
                // Initialize the request by calling the `DescribeInstances` method on the client object. Note: the request method name corresponds to the request object
                // The returned `resp` is an instance of the `DescribeInstancesResponse` class which corresponds to the request object
                DescribeInstancesResponse resp = client.DescribeInstancesSync(req);
    
                // Call the result with a sync API
                // DescribeInstancesResponse resp = client.DescribeInstancesSync(req);
    
                // A string response packet in JSON format is output
                Console.WriteLine(AbstractModel.ToJsonString(resp));
    
                // You can also take a single value
                // You can view the definition of the return field in the API documentation at the official website or by redirecting to the definition of the response object
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
:::
</dx-codeblock>



### More samples

For more samples, please see the `TencentCloudExamples` directory in the [GitHub repository](https://github.com/TencentCloud/tencentcloud-sdk-dotnet). 

### Sync and async calls

The new version of the SDK provides both async and sync APIs. The sync APIs uniformly have the `Sync` suffix after the async APIs as demonstrated in the code above.


>!In the sample, as it is a console application, you can call the async APIs synchronously, i.e., `ConfigureAwait(false).GetAwaiter().GetResult()`. When developing ASP applications or Windows Forms applications, you cannot call the async APIs synchronously in the response method of UI controls; otherwise, the UI will stop responding.
>The solution is to change the response method of the UI controls to async and pay attention to the sync context. In addition, as async call immediately returns control to the user, it is prone to cause the user to click multiple times or perform unexpected operations. Such problems should be avoided in the program. For the source code, please refer to the `WindowsFormsDemo` project.



## Relevant Configuration

### Proxy

If you use the SDK to call an API in a proxy environment, you need to set the system environment variable `https_proxy` (as shown in the sample code); otherwise, it may not be called normally, and a connection timeout exception will be thrown.

## FAQs
The `FluentClient` on which the SDK depends is on v3.2, but this package is currently available on v4.0, which is incompatible with lower versions. Upgrading this package to v4.0 in NuGet will cause problems such as inability to call or call failure.
