SDK 3.0 is a companion tool for the TencentCloud API 3.0 platform. You can use all [SMS APIs](https://intl.cloud.tencent.com/document/product/382/40463) through the SDK. The new SDK version is unified and features the same SDK usage, API call methods, error codes, and returned packet formats for different programming languages.
>!
>- API version required for connecting to Tencent Cloud International
>SMS API v2021-01-11 is required. For details, see the sample code.
>- SMS sending APIs
>One message can be sent to up to 200 numbers at a time.
>- Signature and body template APIs
>Individual users have no permission to use signature and body template APIs and can [manage SMS signatures](https://intl.cloud.tencent.com/document/product/382/35456) and [SMS body templates](https://intl.cloud.tencent.com/document/product/382/35457) only in the SMS console. To use the APIs, change "Individual Identity" to "Organizational Identity".


## Prerequisites

- You have learned about the concept of [region](https://intl.cloud.tencent.com/document/product/382/13299#.E5.9C.B0.E5.9F.9F) and selected a region as needed.
- You have activated SMS. For detailed directions, please see [Getting Started with Mainland China SMS](https://intl.cloud.tencent.com/document/product/382/35449).
- If you need to send Mainland China SMS messages, you need to purchase a Mainland China SMS package first.
- You have prepared the dependent environment: Go 1.9 or above.
- You have obtained the `SecretID` and `SecretKey` on the **[API Key Management](https://console.cloud.tencent.com/cam/capi)** page in the CAM console.
 - `SecretID` is used to identify the API caller.
 - `SecretKey` is used to encrypt the string to sign that can be verified on the server. **You should keep it private and avoid disclosure.**
- The endpoint of the SMS service is `sms.tencentcloudapi.com`.

## Relevant Documents
- For more information on the APIs and their parameters, please see [API Documentation](https://intl.cloud.tencent.com/document/product/382/40463).
- You can download the SDK source code [here](https://github.com/TencentCloud/tencentcloud-sdk-go).

## Installing SDK
### Installing through go get (recommended)
We recommend you install the SDK by using the tool that comes with the language:
```
 go get -u github.com/tencentcloud/tencentcloud-sdk-go
```

### Installing through source code
1. Go to the [GitHub code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-go) or [quick download address](https://tencentcloud-sdk-1253896243.file.myqcloud.com/tencentcloud-sdk-go/tencentcloud-sdk-go.zip) to download the latest code.
2. Decompress and install in the `$GOPATH/src/github.com/tencentcloud` directory.

## Sample Code
>?All samples are for reference only and cannot be directly compiled and executed. You need to modify them based on your actual needs. You can also use [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sms&Version=2021-01-11&Action=SendSms) to automatically generate the demo code as needed.

Each API has a corresponding request structure and a response structure. This document only lists the sample code of several common features as shown below:

### Sending SMS message

```
package main
    
import (
    "encoding/json"
    "fmt"
    
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/errors"
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/profile"
    sms "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/sms/v20210111" // Import SMS
)

func main() {
    /* Required steps:
     * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters.
     * The example here uses the way to read from the environment variable, so you need to set these two values in the environment variable first.
     * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others;
     * otherwise, the key pair may be leaked, causing damage to your properties.
     * Query the CAM key: https://console.cloud.tencent.com/cam/capi*/
    credential := common.NewCredential(
        // os.Getenv("TENCENTCLOUD_SECRET_ID"),
        // os.Getenv("TENCENTCLOUD_SECRET_KEY"),
        "xxx",
        "xxx",
    )
    /* Optional steps:
     * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
    cpf := profile.NewClientProfile()

    /* The SDK uses the POST method by default
     * If you have to use the GET method, you can set it here, but the GET method cannot handle some large requests */
    cpf.HttpProfile.ReqMethod = "POST"

    /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
     * If needed, check in the code to get the latest default value */
    // cpf.HttpProfile.ReqTimeout = 5

    /* The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance zone,
     * you need to manually specify the domain name. For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com` */
    cpf.HttpProfile.Endpoint = "sms.tencentcloudapi.com"

    /* The SDK uses `TC3-HMAC-SHA256` to sign by default. Do not modify this field unless absolutely necessary */
    cpf.SignMethod = "HmacSHA1"

    /* Instantiate the client object of the requested product (with SMS as an example)
     * The second parameter is the information on the region you select in Tencent Cloud International. If you select Singapore, you should enter the string `ap-singapore`. Click https://intl.cloud.tencent.com/document/api/382/40466?lang=en#region-list to view the region list. */
    client, _ := sms.NewClient(credential, "ap-singapore", cpf)

    /* Instantiate a request object. You can further set the request parameters according to the API called and actual conditions
     * You can directly check the SDK source code to determine which attributes of the API can be set
     * An attribute may be of a basic type or import another data structure
     * We recommend you use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
    request := sms.NewSendSmsRequest()

    /* Settings of a basic parameter:
     * The SDK uses the pointer style to specify parameters, so even for basic parameters, you need to use pointers to assign values to them.
     * The SDK provides encapsulation functions for importing the pointers of basic parameters
     * Help link:
     * SMS console: https://console.cloud.tencent.com/smsv2
     * sms helper: https://cloud.tencent.com/document/product/382/3773 */

    /* SMS application ID, which is the `SdkAppId` generated after an application is added in the [SMS console], such as 1400006666 */
    request.SmsSdkAppId = common.StringPtr("1400787878")
    /* SMS signature content, which should be encoded in UTF-8. You must enter an approved signature, which can be viewed in the [SMS console] */
    request.SignName = common.StringPtr("xxx")
    /* `SenderId` for Global SMS, which is not activated by default. If you need to activate it, please contact [SMS Helper] for assistance. This parameter should be left empty for Mainland China SMS */
    request.SenderId = common.StringPtr("")
    /* User session content, which can carry context information such as user-side ID and will be returned as-is by the server */
    request.SessionContext = common.StringPtr("xxx")
    /* SMS code number extension, which is not activated by default. If you need to activate it, please contact [SMS Helper] */
    request.ExtendCode = common.StringPtr("")
    /* Template parameters. If there are no template parameters, leave it empty */
    request.TemplateParamSet = common.StringPtrs([]string{"0"})
    /* Template ID. You must enter the ID of an approved template, which can be viewed in the [SMS console] */
    request.TemplateId = common.StringPtr("449739")
    /* Target mobile number in the E.164 standard (+[country/region code][mobile number])
     * Example: +8613711112222, which has a + sign followed by 86 (country/region code) and then by 13711112222 (mobile number). Up to 200 mobile numbers are supported */
    request.PhoneNumberSet = common.StringPtrs([]string{"+8613711112222"})

    // Call the API you want to access through the client object. You need to pass in the request object
    response, err := client.SendSms(request)
    // Handle the exception
    if _, ok := err.(*errors.TencentCloudSDKError); ok {
        fmt.Printf("An API error has returned: %s", err)
        return
    }
    // This is a direct failure instead of SDK exception. You can add other troubleshooting measures in the real code.
    if err != nil {
        panic(err)
    }
    b, _ := json.Marshal(response.Response)
    // Print the returned JSON string
    fmt.Printf("%s", b)
}
```

### Pulling receipt status

```
package main
    
import (
    "encoding/json"
    "fmt"
    
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/errors"
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/profile"
    sms "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/sms/v20210111" // Import SMS
)

func main() {
    /* Required steps:
     * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters.
     * The example here uses the way to read from the environment variable, so you need to set these two values in the environment variable first.
     * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others;
     * otherwise, the key pair may be leaked, causing damage to your properties.
     * Query the CAM key: https://console.cloud.tencent.com/cam/capi*/
    credential := common.NewCredential(
        // os.Getenv("TENCENTCLOUD_SECRET_ID"),
        // os.Getenv("TENCENTCLOUD_SECRET_KEY"),
        "xxx",
        "xxx",
    )
    /* Optional steps:
     * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
    cpf := profile.NewClientProfile()

    /* The SDK uses the POST method by default
     * If you have to use the GET method, you can set it here, but the GET method cannot handle some large requests */
    cpf.HttpProfile.ReqMethod = "POST"

    /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
     * If needed, check in the code to get the latest default value */
    // cpf.HttpProfile.ReqTimeout = 5

    /* The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance zone,
     * you need to manually specify the domain name. For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com` */
    cpf.HttpProfile.Endpoint = "sms.tencentcloudapi.com"

    /* The SDK uses `TC3-HMAC-SHA256` to sign by default
     * Do not modify this field unless absolutely necessary */
    cpf.SignMethod = "HmacSHA1"

    /* Instantiate the client object of the requested product (with SMS as an example)
     * The second parameter is the information on the region you select in Tencent Cloud International. If you select Singapore, you should enter the string `ap-singapore`. Click https://intl.cloud.tencent.com/document/api/382/40466?lang=en#region-list to view the region list. */
    client, _ := sms.NewClient(credential, "ap-singapore", cpf)

    /* Instantiate a request object. You can further set the request parameters according to the API called and actual conditions
     * You can directly check the SDK source code to determine which attributes of the API can be set
     * An attribute may be of a basic type or import another data structure
     * We recommend you use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
    request := sms.NewPullSmsSendStatusRequest()

    /* Settings of a basic parameter:
     * The SDK uses the pointer style to specify parameters, so even for basic parameters, you need to use pointers to assign values to them.
     * The SDK provides encapsulation functions for importing the pointers of basic parameters
     * Help link:
     * SMS console: https://console.cloud.tencent.com/smsv2
     * sms helper: https://cloud.tencent.com/document/product/382/3773 */

    /* SMS application ID, which is the `SdkAppId` generated after an application is added in the [SMS console], such as 1400006666 */
    request.SmsSdkAppId = common.StringPtr("1400787878")
    /* Maximum number of pulled entries. Maximum value: 100 */
    request.Limit = common.Uint64Ptr(10)

    // Call the API you want to access through the client object. You need to pass in the request object
    response, err := client.PullSmsSendStatus(request)
    // Handle the exception
    if _, ok := err.(*errors.TencentCloudSDKError); ok {
        fmt.Printf("An API error has returned: %s", err)
        return
    }
    // This is a direct failure instead of SDK exception. You can add other troubleshooting measures in the real code.
    if err != nil {
        panic(err)
    }
    b, _ := json.Marshal(response.Response)
    // Print the returned JSON string
    fmt.Printf("%s", b)
}
```

### Collecting SMS message sending data

```
package main
    
import (
    "encoding/json"
    "fmt"
    
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/errors"
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/profile"
    sms "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/sms/v20210111" // Import SMS
)

func main() {
    /* Required steps:
     * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters.
     * The example here uses the way to read from the environment variable, so you need to set these two values in the environment variable first.
     * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others;
     * otherwise, the key pair may be leaked, causing damage to your properties.
     * Query the CAM key: https://console.cloud.tencent.com/cam/capi*/
    credential := common.NewCredential(
        // os.Getenv("TENCENTCLOUD_SECRET_ID"),
        // os.Getenv("TENCENTCLOUD_SECRET_KEY"),
        "xxx",
        "xxx",
    )
    /* Optional steps:
     * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
    cpf := profile.NewClientProfile()

    /* The SDK uses the POST method by default
     * If you have to use the GET method, you can set it here, but the GET method cannot handle some large requests */
    cpf.HttpProfile.ReqMethod = "POST"

    /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
     * If needed, check in the code to get the latest default value */
    // cpf.HttpProfile.ReqTimeout = 5

    /* The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance zone,
     * you need to manually specify the domain name. For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com` */
    cpf.HttpProfile.Endpoint = "sms.tencentcloudapi.com"

    /* The SDK uses `TC3-HMAC-SHA256` to sign by default
     * Do not modify this field unless absolutely necessary */
    cpf.SignMethod = "HmacSHA1"

    /* Instantiate the client object of the requested product (with SMS as an example)
     * The second parameter is the information on the region you select in Tencent Cloud International. If you select Singapore, you should enter the string `ap-singapore`. Click https://intl.cloud.tencent.com/document/api/382/40466?lang=en#region-list to view the region list. */
    client, _ := sms.NewClient(credential, "ap-singapore", cpf)

    /* Instantiate a request object. You can further set the request parameters according to the API called and actual conditions
     * You can directly check the SDK source code to determine which attributes of the API can be set
     * An attribute may be of a basic type or import another data structure
     * We recommend you use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
    request := sms.NewSendStatusStatisticsRequest()

    /* Settings of a basic parameter:
     * The SDK uses the pointer style to specify parameters, so even for basic parameters, you need to use pointers to assign values to them.
     * The SDK provides encapsulation functions for importing the pointers of basic parameters
     * Help link:
     * SMS console: https://console.cloud.tencent.com/smsv2
     * sms helper: https://cloud.tencent.com/document/product/382/3773 */

    /* SMS application ID, which is the `SdkAppId` generated after an application is added in the [SMS console], such as 1400006666 */
    request.SmsSdkAppId = common.StringPtr("1400787878")
    /* Maximum number of pulled entries. Maximum value: 100 */
    request.Limit = common.Uint64Ptr(10)
    /* Offset. Note: this parameter is currently fixed at 0 */
    request.Offset = common.Uint64Ptr(0)
    /* Start time of pull in the format of `yyyymmddhh` accurate to the hour */
    request.BeginTime = common.StringPtr("2019122400")
    /* End time of pull in the format of `yyyymmddhh` accurate to the hour
     * Note: `EndTime` must be after `BeginTime` */
    request.EndTime = common.StringPtr("2019122523")

    // Call the API you want to access through the client object. You need to pass in the request object
    response, err := client.SendStatusStatistics(request)
    // Handle the exception
    if _, ok := err.(*errors.TencentCloudSDKError); ok {
        fmt.Printf("An API error has returned: %s", err)
        return
    }
    // This is a direct failure instead of SDK exception. You can add other troubleshooting measures in the real code.
    if err != nil {
        panic(err)
    }
    b, _ := json.Marshal(response.Response)
    // Print the returned JSON string
    fmt.Printf("%s", b)
}
```

### Applying for SMS template
```
package main
    
import (
    "encoding/json"
    "fmt"
    
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/errors"
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/profile"
    sms "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/sms/v20210111" // Import SMS
)

func main() {
    /* Required steps:
     * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters
     * This example uses the way to read from the environment variable, so you need to set these two values in the environment variable in advance
     * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others
     * Query the CAM key: https://console.cloud.tencent.com/cam/capi
     */
    credential := common.NewCredential(
        // os.Getenv("TENCENTCLOUD_SECRET_ID"),
        // os.Getenv("TENCENTCLOUD_SECRET_KEY"),
        "xxx",
        "xxx",
    )
    /* Optional steps:
     * Instantiate a client configuration object. You can specify the timeout period and other configuration items */

    cpf := profile.NewClientProfile()

    /* The SDK uses the POST method by default
     * If you need to use the GET method, you can set it here, but the GET method cannot handle some large requests */
    cpf.HttpProfile.ReqMethod = "POST"

    /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
     * If needed, check in the code to get the latest default value */
    // cpf.HttpProfile.ReqTimeout = 5

    /* The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance AZ, you must manually specify the domain name
     * For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com` */
    cpf.HttpProfile.Endpoint = "sms.tencentcloudapi.com"

    /* The SDK uses `TC3-HMAC-SHA256` to sign by default. Do not modify this field unless absolutely necessary */
    cpf.SignMethod = "HmacSHA1"

    /* Instantiate an SMS client object
     * The second parameter is the information on the region you select in Tencent Cloud International. If you select Singapore, you should enter the string `ap-singapore`. Click https://intl.cloud.tencent.com/document/api/382/40466?lang=en#region-list to view the region list. */
    client, _ := sms.NewClient(credential, "ap-singapore", cpf)

    /* Instantiate a request object. You can further set the request parameters according to the API called and actual conditions
    * You can directly check the SDK source code to determine which attributes of the API can be set
     * An attribute may be of a basic type or import another data structure
     * We recommend you use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
    request := sms.NewAddSmsTemplateRequest()
    /* Settings of a basic parameter:
     * The SDK uses the pointer style to specify parameters, so even for basic parameters, you need to use pointers to assign values to them
     * The SDK provides encapsulation functions for importing the pointers of basic parameters
     * Help link:
     * SMS console: https://console.cloud.tencent.com/smsv2
     * sms helper：https://cloud.tencent.com/document/product/382/3773
     */
    /* Template name */
    request.TemplateName = common.StringPtr("Tencent Cloud")
    /* Template content */
    request.TemplateContent = common.StringPtr("Your login verification code is {1}. Please enter it within {2} minutes. If the login was not initiated by you, please ignore this message.")
    /* SMS type. 0: regular SMS; 1: marketing SMS */
    request.SmsType = common.Uint64Ptr(0)
    /* Whether it is Global SMS:
       0: Mainland China SMS
       1: Global SMS */
    request.International = common.Uint64Ptr(0)
    /* Template remarks, such as reason for application and use case */
    request.Remark = common.StringPtr("xxx")
    // Call the API you want to access through the client object. You need to pass in the request object
    response, err := client.AddSmsTemplate(request)
    // Handle the exception
    if _, ok := err.(*errors.TencentCloudSDKError); ok {
        fmt.Printf("An API error has returned: %s", err)
        return
    }
    // This is a direct failure instead of SDK exception. You can add other troubleshooting measures in the real code
    if err != nil {
        panic(err)
    }
    b, _ := json.Marshal(response.Response)
    // Print the returned JSON string
    fmt.Printf("%s", b)
}
```

## FAQs
<dx-accordion>
::: Proxy settings
If there is a proxy in your environment, you need to set the system environment variable `https_proxy`; otherwise, it may not be called normally, and a connection timeout exception will be thrown.
:::
::: Enabling \sDNS\s cache
Currently, the SDK for Go always requests the DNS server without using the cache of nscd. You can export the environment variable `GODEBUG=netdns=cgo` or specify the `-tags 'netcgo'` parameter when compiling `go build` so as to get the nscd cache.
:::
::: Ignoring server certificate verification
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
:::
::: Failure of package import with import\s
For example, if the error `imported and not used: "os"` is reported, it means that the package `os` is not used in the code. Therefore, simply remove it.
:::
</dx-accordion>
