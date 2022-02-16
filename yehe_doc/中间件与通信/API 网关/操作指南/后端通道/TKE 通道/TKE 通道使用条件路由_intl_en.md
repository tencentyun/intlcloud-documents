## Overview

You can forward requests to different TKE backends based on the request/system parameter values, such as the Host or UserName in the request header. This is suitable for various scenarios, including grayscale release, blue-green deployment, and tenant routing. The TKE backend tunnel can be combined with the conditional routing plugin to implement data distribution.

For the usage and features of conditional routing, see [Conditional Routing Plugin](https://intl.cloud.tencent.com/document/product/628/44308).

## Prerequisites

- You have a dedicated instance.
- You have created multiple TKE tunnels.

## Directions

1. Create an API on the [API Gateway](https://console.cloud.tencent.com/apigateway/service) service page. Select VPC resources as the backend type of the API and select TKE tunnel as the tunnel.[](id:step1)
   ![](https://qcloudimg.tencent-cloud.cn/raw/f35af2e585b2542a647dadcdef158a46.png)        
2. After the API is published, create a conditional routing plugin.
   1. Select **Plugin** > **System Plugin** on the left sidebar in the console.
   2. Click **Create** and select **Conditional routing** as the type.
      <img src="https://qcloudimg.tencent-cloud.cn/raw/2291584bab61ecc63b2e1dec59879783.png" width="450px">                         
   3. Create a conditional routing policy: the semantics of the conditional routing in the following example is that when the value of UserName in the request header is `admin`, the request will be forwarded to the TKE tunnel `upstream-1ca1d6yi`.
      ![](https://qcloudimg.tencent-cloud.cn/raw/2dfe8aa99b540e172305f4d4d6d0cb3e.png)        
      Policy details:
```yaml
ServiceType: HTTP
ServiceConfig:
  Method: ANY
  Path: /
  Url: 'http://127.0.0.1/'
  UniqVpcId: vpc-s0g8gpo5
  UpstreamId: upstream-1ca1d6yi
  Product: upstream
```
3. The conditional routing plugin is bound to the API created in **[step 1](#step1)**.
4. If the request matches the conditional routing policy (header with UserName as `admin`), it will be forwarded to `upstream-1ca1d6yi`; otherwise, the default backend configured for the API will be used.


## Notes

Conditional routing can match not only request headers but also clientIp. For more capabilities of conditional routing, see [Conditional Routing Plugin](https://intl.cloud.tencent.com/document/product/628/44308).
