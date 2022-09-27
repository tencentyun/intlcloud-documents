CAR PaaS allows you to run your application in the cloud, so that users can access and interact with the cloud application through a video stream, with no need to download the application on their own device.
![](https://qcloudimg.tencent-cloud.cn/raw/6db9536d93dfad8c4a3113229b9144ce.jpg)

## TencentCloud API
- **TencentCloud API:** TencentCloud API [3.0](https://intl.cloud.tencent.com/product/api) is the basis of Tencent Cloud open ecosystem and boasts strengths such as ease of automation and remote call, high compatibility, and low system requirements. It enables you to quickly manipulate Tencent Cloud products with only a small amount of code, and improves the efficiency for frequently called features. You can also combine different TencentCloud APIs to implement more advanced features. 
- **Access key:**
An access key is a TencentCloud API key, which is a security credential used for authentication when you access TencentCloud APIs. It consists of a `SecretId` and `SecretKey`. If you don't have an API key yet, you need to create one in **Manage API Key**; otherwise, you cannot call TencentCloud APIs. You can get the access key on the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page in the console.

## Running Environment
### Cloud software environment
- **Deployment prerequisites**: The installation package of the cloud application must support portable deployment and installation; that is, the application operations don't rely on modification of the registry or other system configurations.
- **System limits**: PowerShell and CMD services on Windows cannot be called.
- **Port limits**: Port listening is not supported because the public IP provided by the service is not fixed. Subnet broadcasting is not supported. If you have such needs, we recommend you use the public network for communication.

### CAR service environment
**Network conditions**: The network of CAR relies on UDP data reception and sending, so you need to open UDP port 8000 to all source IPs on the client. If there are no special security concerns, we recommend you open all UDP ports.

## Service Integration Capabilities
CAR is a frontend/backend integrated PaaS product. It provides backend APIs and client SDKs. You need to set up your own client program and backend service to serve your users.
![](https://qcloudimg.tencent-cloud.cn/raw/eddd4735374bf4605d1b233561c239aa.jpg)

- **Backend APIs:**
CAR provides backend [TencentCloud APIs](https://intl.cloud.tencent.com/document/product/1158/49958) that can be called to perform operations such as applying for a concurrency and creating a session.
- **Client SDKs:**
CAR provides the client SDKs to support integration on Android, iOS, and other platforms, and you need to integrate the SDK into your client. The SDK provides a rich variety of APIs to meet most integration needs. For more information, see [JavaScript SDK](https://intl.cloud.tencent.com/document/product/1158/49627), [SDK for Android](https://intl.cloud.tencent.com/document/product/1158/49628), and [SDK for iOS](https://intl.cloud.tencent.com/document/product/1158/49629).

