SDK 3.0 is a companion tool for the TencentCloud API 3.0 platform. You can use all [SMS APIs](https://intl.cloud.tencent.com/document/product/382/40463) through the SDK. The new SDK version is unified and features the same SDK usage, API call methods, error codes, and returned packet formats for different programming languages.
>!
>- API version required for connecting to Tencent Cloud International:
>SMS API v2021-01-11 is required. For details, see the sample code.
>- SMS delivery APIs: 
>One message can be sent to up to 200 numbers at a time.
>- Signature and body template APIs: 
>Individual users have no permission to use signature and body template APIs and can only [manage SMS signatures](https://intl.cloud.tencent.com/document/product/382/35456) and [SMS body templates](https://intl.cloud.tencent.com/document/product/382/35457) in the SMS console. To use the APIs, change "Individual Verification" to "Organization Verification". For details, see [Identity Verification Change Guide](https://intl.cloud.tencent.com/document/product/378/37276).



## Prerequisites
- You have learned about the concept of [Region](https://intl.cloud.tencent.com/document/product/382/13299#.E5.9C.B0.E5.9F.9F) and selected a region as needed.
- You have activated the SMS service and created a signature and SMS template that have been approved. For details, see [Getting Started](https://intl.cloud.tencent.com/document/product/382/35449).
- You have purchased a Chinese Mainland SMS package (if you need to send Chinese Mainland SMS messages).
- You have got the `SecretId` and `SecretKey` on the [**Manage API Key**](https://console.cloud.tencent.com/cam/capi) page in the CAM console.
  - `SecretId` is used to identify the API caller.
  - `SecretKey` is a key used to encrypt the signature and help the server verify the signature. **You should keep it private and avoid disclosure**.
- The endpoint of the SMS service is `sms.tencentcloudapi.com`.

## Reference
- For more information on the APIs and their parameters, see [API Documentation](https://intl.cloud.tencent.com/document/product/382/40463).
- You can download the SDK source code [here](https://github.com/TencentCloud/tencentcloud-sdk-cpp).

## Installing SDK
### Environmental dependency
See [Environmental dependency](https://github.com/TencentCloud/tencentcloud-sdk-cpp#%E7%8E%AF%E5%A2%83%E4%BE%9D%E8%B5%96).

### Building SDK from source code
See [Building SDK from source code](https://github.com/TencentCloud/tencentcloud-sdk-cpp#%E4%BB%8E%E6%BA%90%E4%BB%A3%E7%A0%81%E6%9E%84%E5%BB%BA-sdk).


## Sample Code
>?All samples are for reference only and cannot be directly compiled and executed. You need to modify them based on your actual needs. You can also use [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sms&Version=2021-01-11&Action=SendSms) to automatically generate the demo code as needed.

Each API has its own request and response structures. This document only lists the sample code of several common features as shown below:

### Sending SMS messages

```
#include <tencentcloud/core/TencentCloud.h>
#include <tencentcloud/core/profile/HttpProfile.h>
#include <tencentcloud/core/profile/ClientProfile.h>
#include <tencentcloud/core/Credential.h>
#include <tencentcloud/core/NetworkProxy.h>
#include <tencentcloud/core/AsyncCallerContext.h>
#include <tencentcloud/sms/v20210111/SmsClient.h>
#include <tencentcloud/sms/v20210111/model/SendSmsRequest.h>
#include <tencentcloud/sms/v20210111/model/SendSmsResponse.h>

#include <iostream>
#include <string>

using namespace TencentCloud;
using namespace TencentCloud::Sms::V20210111;
using namespace TencentCloud::Sms::V20210111::Model;
using namespace std;

int main()
{
    TencentCloud::InitAPI();

    // Use the SDK.
    // Instantiate an authentication object. The Tencent Cloud account SecretId and SecretKey need to be passed in as the input parameters. Do not disclose the SecretKey to others.
    // You can get the API SecretId and SecretKey at https://console.cloud.tencent.com/cam/capi.
    string secretId = "<your secret id>";
    string secretKey = "<your secret key>";
    Credential cred = Credential(secretId, secretKey);
    
    // (Optional) Instantiate an HTTP option.
    HttpProfile httpProfile = HttpProfile();
    httpProfile.SetKeepAlive(true);  // Specify whether to enable the keepalive feature. The default value is “false”.
    httpProfile.SetEndpoint("sms.tencentcloudapi.com");  // Specify the endpoint. If you do not specify it, nearby access is enabled by default.
    httpProfile.SetReqTimeout(30);  // Specify the request timeout value, in seconds. The default value is 60s.
    httpProfile.SetConnectTimeout(30); // Specify the response timeout value, in seconds. The default value is 60s.

    ClientProfile clientProfile = ClientProfile(httpProfile);

    SendSmsRequest req = SendSmsRequest();
    
    /* Help link:
     * SMS console: https://console.cloud.tencent.com/smsv2
      */
    /* SMS application ID: The SdkAppId generated after an application is added in the [SMS console], such as 1400006666 */
    // You can view the application ID in the [SMS console](https://console.cloud.tencent.com/smsv2/app-manage).
    req.SetSmsSdkAppId("1400787878");

    /* SMS signature content: You must enter an approved signature that is encoded in UTF-8.*/
    // The signature information can be viewed on the [Chinese Mainland SMS](https://console.cloud.tencent.com/smsv2/csms-sign) or [Global SMS](https://console.cloud.tencent.com/smsv2/isms-sign) signature management page.
    req.SetSignName("Tencent Cloud");

    /* Template ID: You must enter the ID of an approved template.*/
    // The template ID can be viewed on the [Chinese Mainland SMS](https://console.cloud.tencent.com/smsv2/csms-template) or [Global SMS](https://console.cloud.tencent.com/smsv2/isms-template) body template management page.
    req.SetTemplateId("449739");

    /* Template parameter: The number of template parameters must be the same as that of the variables in the template. If no template parameters are involved, leave this field empty.*/
    req.SetTemplateParamSet(std::vector<std::string>{"1234"});

    /* Target mobile number in the E.164 standard (+[country/region code][mobile number])
     * Example: +8613711112222, which has a “+” sign followed by 86 (country/region code) and then by 13711112222 (mobile number). Up to 200 mobile numbers are supported */
    req.SetPhoneNumberSet(std::vector<std::string>{"+8613711112222"});

    /* (Ignorable) User session content: Context information like the user ID can be carried and will be returned by the server as is.*/
    req.SetSessionContext("");

    /* (Ignorable) SMS code number extension, which is not activated by default. If you need to activate it, submit a ticket.*/
    req.SetExtendCode("");

    /* (Ignorable) SenderId for Global SMS, which is not activated by default. If you need to activate it, submit a ticket. For Chinese Mainland SMS, leave it empty.*/
    req.SetSenderId("");

    /* Instantiate the client object of the product (with SMS as an example) to be requested.
     * The second parameter is used to specify region information. You can enter a string like “ap-guangzhou”. For more supported regions, see https://cloud.tencent.com/document/api/382/52071#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8 */
    SmsClient sms_client = SmsClient(cred, "ap-guangzhou", clientProfile);

    // (Ignorable) Set a proxy.
    // NetworkProxy proxy = NetworkProxy(NetworkProxy::Type::HTTP, "localhost.proxy.com", 8080);
    // sms_client.SetNetworkProxy(proxy);

    auto outcome = sms_client.SendSms(req);
    if (!outcome.IsSuccess())
    {
        cout << outcome.GetError().PrintAll() << endl;
        TencentCloud::ShutdownAPI();
        return -1;
    }
    SendSmsResponse rsp = outcome.GetResult();
    cout<<"RequestId="<<rsp.GetRequestId()<<endl;
    cout<<"SendSmsResponse="<<rsp.ToJsonString()<<endl;
    
    TencentCloud::ShutdownAPI();

    /* Below are some error codes and the corresponding solutions to them:
     * [FailedOperation.SignatureIncorrectOrUnapproved](https://intl.cloud.tencent.com/document/product/382/9558)
     * [FailedOperation.TemplateIncorrectOrUnapproved](https://intl.cloud.tencent.com/document/product/382/9558)
     * [UnauthorizedOperation.SmsSdkAppIdVerifyFail](https://intl.cloud.tencent.com/document/product/382/9558)
     * [UnsupportedOperation.ContainDomesticAndInternationalPhoneNumber](https://intl.cloud.tencent.com/document/product/382/9558)
     */

    return 0;
}
```



### Pulling receipt status

```
#include <tencentcloud/core/TencentCloud.h>
#include <tencentcloud/core/profile/HttpProfile.h>
#include <tencentcloud/core/profile/ClientProfile.h>
#include <tencentcloud/core/Credential.h>
#include <tencentcloud/core/NetworkProxy.h>
#include <tencentcloud/core/AsyncCallerContext.h>
#include <tencentcloud/sms/v20210111/SmsClient.h>
#include <tencentcloud/sms/v20210111/model/PullSmsSendStatusRequest.h>
#include <tencentcloud/sms/v20210111/model/PullSmsSendStatusResponse.h>

#include <iostream>
#include <string>

using namespace TencentCloud;
using namespace TencentCloud::Sms::V20210111;
using namespace TencentCloud::Sms::V20210111::Model;
using namespace std;

int main()
{
    TencentCloud::InitAPI();

    // Use the SDK.
    // Instantiate an authentication object. The Tencent Cloud account SecretId and SecretKey need to be passed in as the input parameters. Do not disclose the SecretKey to others.
    // You can get the API SecretId and SecretKey at https://console.cloud.tencent.com/cam/capi.
    string secretId = "<your secret id>";
    string secretKey = "<your secret key>";
    Credential cred = Credential(secretId, secretKey);
    
    // (Optional) Instantiate an HTTP option.
    HttpProfile httpProfile = HttpProfile();
    httpProfile.SetKeepAlive(true);  // Specify whether to enable the keepalive feature. The default value is “false”.
    httpProfile.SetEndpoint("sms.tencentcloudapi.com");  // Specify the endpoint. If you do not specify it, nearby access is enabled by default.
    httpProfile.SetReqTimeout(30);  // Specify the request timeout value, in seconds. The default value is 60s.
    httpProfile.SetConnectTimeout(30); // Specify the response timeout value, in seconds. The default value is 60s.

    ClientProfile clientProfile = ClientProfile(httpProfile);

    PullSmsSendStatusRequest req = PullSmsSendStatusRequest();
    
    /* Help link:
     * SMS console: https://console.cloud.tencent.com/smsv2
     */
    /* SMS application ID, which is the SdkAppId generated after an application is added in the [SMS console], such as 1400006666 */
    req.SetSmsSdkAppId("1400787878");
    // Set the max number of pulled entries. Max value: 100.
    req.SetLimit(100);

    SmsClient sms_client = SmsClient(cred, "ap-guangzhou", clientProfile);

    // set proxy.
    // NetworkProxy proxy = NetworkProxy(NetworkProxy::Type::HTTP, "localhost.proxy.com", 8080);
    // cvm_client.SetNetworkProxy(proxy);

    auto outcome = sms_client.PullSmsSendStatus(req);
    if (!outcome.IsSuccess())
    {
        cout << outcome.GetError().PrintAll() << endl;
        TencentCloud::ShutdownAPI();
        return -1;
    }
    PullSmsSendStatusResponse rsp = outcome.GetResult();
    cout<<"RequestId="<<rsp.GetRequestId()<<endl;
    cout<<"PullSmsSendStatusResponse="<<rsp.ToJsonString()<<endl;
    
    TencentCloud::ShutdownAPI();

    return 0;
}
```

### Collecting SMS sending statistics

```
#include <tencentcloud/core/TencentCloud.h>
#include <tencentcloud/core/profile/HttpProfile.h>
#include <tencentcloud/core/profile/ClientProfile.h>
#include <tencentcloud/core/Credential.h>
#include <tencentcloud/core/NetworkProxy.h>
#include <tencentcloud/core/AsyncCallerContext.h>
#include <tencentcloud/sms/v20210111/SmsClient.h>
#include <tencentcloud/sms/v20210111/model/SendStatusStatisticsRequest.h>
#include <tencentcloud/sms/v20210111/model/SendStatusStatisticsResponse.h>

#include <iostream>
#include <string>

using namespace TencentCloud;
using namespace TencentCloud::Sms::V20210111;
using namespace TencentCloud::Sms::V20210111::Model;
using namespace std;

int main()
{
    TencentCloud::InitAPI();

    // Use the SDK.
    // Instantiate an authentication object. The Tencent Cloud account SecretId and SecretKey need to be passed in as the input parameters. Do not disclose the SecretKey to others.
    // You can get the API SecretId and SecretKey at https://console.cloud.tencent.com/cam/capi.
    string secretId = "<your secret id>";
    string secretKey = "<your secret key>";
    Credential cred = Credential(secretId, secretKey);
    
    // (Optional) Instantiate an HTTP option.
    HttpProfile httpProfile = HttpProfile();
    httpProfile.SetKeepAlive(true);  // Specify whether to enable the keepalive feature. The default value is “false”.
    httpProfile.SetEndpoint("sms.tencentcloudapi.com");  // Specify the endpoint. If you do not specify it, nearby access is enabled by default.
    httpProfile.SetReqTimeout(30);  // Specify the request timeout value, in seconds. The default value is 60s.
    httpProfile.SetConnectTimeout(30); // Specify the response timeout value, in seconds. The default value is 60s.

    ClientProfile clientProfile = ClientProfile(httpProfile);

    SendStatusStatisticsRequest req = SendStatusStatisticsRequest();
    
    /* Help link:
     * SMS console: https://console.cloud.tencent.com/smsv2
     */
    /* SMS application ID, which is the SdkAppId generated after an application is added in the [SMS console], such as 1400006666 */
    req.SetSmsSdkAppId("1400787878");
    // Upper limit, which is currently fixed at 0.
    req.SetLimit(0);
    /* Offset, which is currently fixed at 0 */
    req.SetOffset(0);
    /* Start time in the format of “yyyymmddhh” accurate down to the hour, such as 2021050113 (13:00 on May 1, 2021).*/
    req.SetBeginTime("2019071100");
    /* End time in the format of “yyyymmddhh” accurate down to the hour, such as 2021050118 (18:00 on May 1, 2021).*/
        * Note: “EndTime” must be after “BeginTime”.*/
    req.SetEndTime("2019071123");

    SmsClient sms_client = SmsClient(cred, "ap-guangzhou", clientProfile);

    // set proxy.
    // NetworkProxy proxy = NetworkProxy(NetworkProxy::Type::HTTP, "localhost.proxy.com", 8080);
    // cvm_client.SetNetworkProxy(proxy);

    auto outcome = sms_client.SendStatusStatistics(req);
    if (!outcome.IsSuccess())
    {
        cout << outcome.GetError().PrintAll() << endl;
        TencentCloud::ShutdownAPI();
        return -1;
    }
    SendStatusStatisticsResponse rsp = outcome.GetResult();
    cout<<"RequestId="<<rsp.GetRequestId()<<endl;
    cout<<"SendStatusStatisticsResponse="<<rsp.ToJsonString()<<endl;
    
    TencentCloud::ShutdownAPI();

    return 0;
}
```

### Applying for SMS template

```
#include <tencentcloud/core/TencentCloud.h>
#include <tencentcloud/core/profile/HttpProfile.h>
#include <tencentcloud/core/profile/ClientProfile.h>
#include <tencentcloud/core/Credential.h>
#include <tencentcloud/core/NetworkProxy.h>
#include <tencentcloud/core/AsyncCallerContext.h>
#include <tencentcloud/sms/v20210111/SmsClient.h>
#include <tencentcloud/sms/v20210111/model/AddSmsTemplateRequest.h>
#include <tencentcloud/sms/v20210111/model/AddSmsTemplateResponse.h>

#include <iostream>
#include <string>

using namespace TencentCloud;
using namespace TencentCloud::Sms::V20210111;
using namespace TencentCloud::Sms::V20210111::Model;
using namespace std;

int main()
{
    TencentCloud::InitAPI();

    // Use the SDK.
    // Instantiate an authentication object. The Tencent Cloud account SecretId and SecretKey need to be passed in as the input parameters. Do not disclose the SecretKey to others.
    // You can get the API SecretId and SecretKey at https://console.cloud.tencent.com/cam/capi.
    string secretId = "<your secret id>";
    string secretKey = "<your secret key>";
    Credential cred = Credential(secretId, secretKey);
    
    // (Optional) Instantiate an HTTP option.
    HttpProfile httpProfile = HttpProfile();
    httpProfile.SetKeepAlive(true);  // Specify whether to enable the keepalive feature. The default value is “false”.
    httpProfile.SetEndpoint("sms.tencentcloudapi.com");  // Specify the endpoint. If you do not specify it, nearby access is enabled by default.
    httpProfile.SetReqTimeout(30);  // Specify the request timeout value, in seconds. The default value is 60s.
    httpProfile.SetConnectTimeout(30); // Specify the response timeout value, in seconds. The default value is 60s.

    ClientProfile clientProfile = ClientProfile(httpProfile);

    AddSmsTemplateRequest req = AddSmsTemplateRequest();
    
    /* Help link:
     * SMS console: https://console.cloud.tencent.com/smsv2
     */
    /* Template name */
    req.SetTemplateName("Tencent Cloud");
    /* Template content */
    req.SetTemplateContent("{Your login verification code is {1}. Please enter it within {2} minutes. If the login was not initiated by you, please ignore this message");
    /* SMS type. 0: Regular SMS, 1: Marketing SMS.*/
    req.SetSmsType(0);
    /* A parameter used to specify whether it is Global SMS:
    * 0: Chinese Mainland SMS
    * 1: Global SMS.*/
    req.SetInternational(0);
    /* Template remarks, such as the reason for application and its use cases.*/
    req.SetRemark("xxx");

    SmsClient sms_client = SmsClient(cred, "ap-guangzhou", clientProfile);

    // set proxy.
    // NetworkProxy proxy = NetworkProxy(NetworkProxy::Type::HTTP, "localhost.proxy.com", 8080);
    // cvm_client.SetNetworkProxy(proxy);

    auto outcome = sms_client.AddSmsTemplate(req);
    if (!outcome.IsSuccess())
    {
        cout << outcome.GetError().PrintAll() << endl;
        TencentCloud::ShutdownAPI();
        return -1;
    }
    AddSmsTemplateResponse rsp = outcome.GetResult();
    cout<<"RequestId="<<rsp.GetRequestId()<<endl;
    cout<<"AddSmsTemplateResponse="<<rsp.ToJsonString()<<endl;
    
    TencentCloud::ShutdownAPI();

    return 0;
}
```
