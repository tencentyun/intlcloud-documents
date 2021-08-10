## Overview
Welcome to Tencent Cloud Software Development Kit (SDK) 3.0, a companion tool for the TencentCloud API 3.0 platform.

## Dependent Environment
1. Dependent environment: Ruby 2.3 or above.
2. Activate your product in the [Tencent Cloud console](https://console.cloud.tencent.com/).
3. Get the `SecretID`, `SecretKey`, and endpoint. The general format of endpoint is `\*.tencentcloudapi.com`. For example, the endpoint of CVM is `cvm.tencentcloudapi.com`. For more information, please see the documentation of the specified product.

## Getting and Installing
Before installing the SDK for Ruby and using TencentCloud API for the first time, you need to apply for security credentials in the [Tencent Cloud console](https://console.cloud.tencent.com/), which consists of `SecretId` and `SecretKey`.
- `SecretId` is used to identify the API requester.
- `SecretKey` is used to encrypt the string to sign that can be verified on the server.
>!You must keep the `SecretKey` private and avoid disclosure.

### Installing through source package
Go to the [GitHub code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-ruby) to download the latest code, decompress it, and run the following command (with the CVM SDK as an example):

    $ cd tencentcloud-sdk-ruby/tencentcloud
    $ cd tencentcloud-sdk-common
    $ gem build tencentcloud-sdk-common.gemspec
    $ gem install tencentcloud-sdk-common-1.0.0.gem
    $ cd ../tencentcloud-sdk-cvm
    $ gem build tencentcloud-sdk-cvm.gemspec
    $ gem install tencentcloud-sdk-cvm-1.0.0.gem 

>!For the above version numbers, the actual values shall prevail.

## Example
The following takes the instance list querying API as an example.

### Simplified version
```ruby
# -*- coding: UTF-8 -*-
require 'tencentcloud-sdk-common'
require 'tencentcloud-sdk-cvm'

include TencentCloud::Common
include TencentCloud::Cvm::V20170312

begin
   cre = Credential.new('SecretId', 'SecretKey')
   req = DescribeInstancesRequest.new(nil, nil, 0, 1)
  
   cli = Client.new(cre, 'ap-guangzhou')
   cli.DescribeInstances(req)
rescue TencentCloudSDKException => e
   puts e.message  
   puts e.backtrace.inspect  
end
```

### Detailed version
```ruby
# -*- coding: UTF-8 -*-
require 'tencentcloud-sdk-common'
require 'tencentcloud-sdk-cvm'

begin
   include TencentCloud::Common
   # Import the client module of the corresponding product module
   include TencentCloud::Cvm::V20170312

  # Instantiate an authentication object. Pass in `secretId` and `secretKey` of your Tencent Cloud account as the input parameters and keep them confidential
   cred = Credential.new('SecretId', 'SecretKey')
   # Instantiate an HTTP option
   httpProfile = HttpProfile.new()
   # If you need to specify the proxy for API access, you can initialize HttpProfile as follows
   # httpProfile = HttpProfile.new(proxy='http://username:password@proxy IP:proxy port')
   httpProfile.scheme = "https"  # HTTP is supported if the network environment has access to the public network, and HTTPS is used by default and recommended
   httpProfile.req_method = "GET"  # GET request (POST request is used by default)
   httpProfile.req_timeout = 30    # Specify the request timeout value in seconds. The default value is 60s
   httpProfile.endpoint = "cvm.tencentcloudapi.com"  # Specify the endpoint. If you do not specify the endpoint, nearby access is enabled by default

  # (Optional) Instantiate a client option
   clientProfile = ClientProfile.new()
   clientProfile.sign_method = "TC3-HMAC-SHA256"  # Specify the signature algorithm
   clientProfile.language = "en-US"  # Specify to display in English (the default value is Chinese)
   clientProfile.http_profile = httpProfile
   clientProfile.debug = true # Print `debug` logs

  # Instantiate the client object of the requested product (with CVM as an example). `clientProfile` is optional.
   client = Client.new(cred, "ap-shanghai", clientProfile)

  # Instantiate a CVM instance information query request object. Each API corresponds to a request object
   req = DescribeInstancesRequest.new()

  # Populate the request parameters. Here, the member variables of the request object are the input parameters of the corresponding API.
   # You can view the definition of the request parameters in the API documentation at the official website or by redirecting to the definition of the request object.
   respFilter = Filter.new()  # Create a `Filter` object to query CVM instances in the `zone` dimension.
   respFilter.Name = "zone"
   respFilter.Values = ["ap-shanghai-1", "ap-shanghai-2"]
   req.Filters = [respFilter]  # `Filters` is a list of `Filter` objects

  # Initialize the request by calling the `DescribeInstances` method on the client object. Note: the request method name corresponds to the request object
   # The returned `resp` is an instance of the `DescribeInstancesResponse` class which corresponds to the request object
   resp = client.DescribeInstances(req)

  # A string return packet in JSON format is outputted
   puts resp.serialize

  # You can also take a single value.
   # You can view the definition of the return field in the API documentation at the official website or by redirecting to the definition of the response object.
   puts resp.TotalCount
rescue TencentCloudSDKException => e
   puts e.message  
   puts e.backtrace.inspect  
end
```

## Relevant Configuration

### Proxy

If there is a proxy in your environment, you can set the proxy in the following two ways:

1. Specify the `proxy` when initializing `HttpProfile`.
2. You need to set the system environment variable `https_proxy`.

>!Otherwise, it may not be called normally, and a connection timeout exception will be thrown.
