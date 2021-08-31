SDK 3.0 is a companion tool for the TencentCloud API 3.0 platform. You can use all [SMS APIs](https://intl.cloud.tencent.com/document/product/382/34689) through the SDK. The new SDK version is unified and features the same SDK usage, API call methods, error codes, and returned packet formats for different programming languages.

>!
>
>- SMS sending APIs
>  One message can be sent to up to 200 numbers at a time.
>- Signature and body template APIs
>  Individual users have no permission to use signature and body template APIs and can [manage SMS signatures](https://intl.cloud.tencent.com/document/product/382/35456) and [SMS body templates](https://intl.cloud.tencent.com/document/product/382/35457) only in the SMS console. To use the APIs, change "Individual Identity" to "Organizational Identity".



## Prerequisites

- You have activated SMS. For detailed directions, please see [Getting Started with Mainland China SMS](https://intl.cloud.tencent.com/document/product/382/35449).
- If you need to send Mainland China SMS messages, you need to purchase a Mainland China SMS package first.
- You have prepared the dependent environment: JDK 7 or above.
- You have obtained the `SecretID` and `SecretKey` on the **[API Key Management](https://console.cloud.tencent.com/cam/capi)** page in the CAM console.
 - `SecretID` is used to identify the API caller.
 - `SecretKey` is used to encrypt the string to sign that can be verified on the server. **You should keep it private and avoid disclosure.**
- The endpoint of the SMS service is `sms.tencentcloudapi.com`.

## Relevant Documents

- For more information on the APIs and their parameters, please see [API Documentation](https://intl.cloud.tencent.com/document/product/382/34689).
- You can download the SDK source code [here](https://github.com/TencentCloud/tencentcloud-sdk-java).


## Installing SDK

### Installing through Maven (recommended)

[Maven](https://maven.apache.org) is a dependency management tool for Java that supports the dependencies your project requires and installs them into your project.

1. Go to [Maven's official website](https://maven.apache.org/) to download the corresponding Maven installation package for your system and install it.
2. Add Maven dependencies by adding the following dependencies in Maven's pom.xml:

 >!The version number here is for demonstration only. Please get the latest version number in [Maven Repository](https://search.maven.org/search?q=tencentcloud-sdk-java) for replacement.

<pre><code class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">dependency</span>&gt;</span>
        <span class="hljs-tag">&lt;<span class="hljs-name">groupId</span>&gt;</span>com.tencentcloudapi<span class="hljs-tag">&lt;/<span class="hljs-name">groupId</span>&gt;</span>
        <span class="hljs-tag">&lt;<span class="hljs-name">artifactId</span>&gt;</span>tencentcloud-sdk-java<span class="hljs-tag">&lt;/<span class="hljs-name">artifactId</span>&gt;</span>
        <span class="hljs-tag">&lt;<span class="hljs-name">version</span>&gt;</span>3.1.270<span class="hljs-tag">&lt;/<span class="hljs-name">version</span>&gt;</span><span class="hljs-comment">&lt;!-- Note: the version number here is for demonstration only. Please get the <a href="https://mvnrepository.com/artifact/com.tencentcloudapi/tencentcloud-sdk-java">latest version number</a> for replacement --&gt;</span>
<span class="hljs-tag">&lt;/<span class="hljs-name">dependency</span>&gt;</span></code></pre>

3. For importing methods, please see the [sample code](#example).

### Installing through source package

1. [Download](https://github.com/tencentcloud/tencentcloud-sdk-java) the source code package.
2. Decompress the source package to an appropriate location in your project.
3. Put the jar package under the `vendor` directory in a path that can be found by Java.
4. For importing methods, please see the [sample code](#example).

## Sample Code[](id:example)

>?All samples are for reference only and cannot be directly compiled and executed. You need to modify them based on your actual needs. You can also use [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sms&Version=2021-01-11&Action=SendSms) to automatically generate the demo code as needed.

Each API has a corresponding request structure and a response structure. This document only lists the sample code of several common features as shown below:

### Sending SMS message

```
import com.tencentcloudapi.common.Credential;
import com.tencentcloudapi.common.exception.TencentCloudSDKException;

// Import the optional configuration classes
import com.tencentcloudapi.common.profile.ClientProfile;
import com.tencentcloudapi.common.profile.HttpProfile;

// Import the client of the corresponding SMS module
import com.tencentcloudapi.sms.v20210111.SmsClient;

// Import the request response class corresponding to the request API
import com.tencentcloudapi.sms.v20210111.models.SendSmsRequest;
import com.tencentcloudapi.sms.v20210111.models.SendSmsResponse;

/**
 * Tencent Cloud Sms Sendsms
 *
 */
public class SendSms
{
    public static void main(String[] args)
    {
        try {
            /* Required steps:
             * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters.
             * The example here uses the way to read from the environment variable, so you need to set these two values in the environment variable first.
             * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others;
             * otherwise, the key pair may be leaked, causing damage to your properties.
             * Query the CAM key: https://console.cloud.tencent.com/cam/capi*/
            Credential cred = new Credential("secretId", "secretKey");

            // (Optional) Instantiate an HTTP option
            HttpProfile httpProfile = new HttpProfile();
            // Set the proxy
            httpProfile.setProxyHost("host");
            httpProfile.setProxyPort(port);
            /* The SDK uses the POST method by default
             * If you have to use the GET method, you can set it here, but the GET method cannot handle some large requests */
            httpProfile.setReqMethod("POST");
            /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
             * If needed, check in the code to get the latest default value */
            httpProfile.setConnTimeout(60);
            /* The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance zone,
             * you have to manually specify the domain name. For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com` */
            httpProfile.setEndpoint("sms.tencentcloudapi.com");

            /* Optional steps:
             * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
            ClientProfile clientProfile = new ClientProfile();
            /* The SDK uses `TC3-HMAC-SHA256` to sign by default
             * Do not modify this field unless absolutely necessary */
            clientProfile.setSignMethod("HmacSHA256");
            clientProfile.setHttpProfile(httpProfile);
            /* Instantiate the client object of the requested product (with SMS as an example)
             * The second parameter is the region information. You can directly enter the string `ap-guangzhou` or import the preset constant */
            SmsClient client = new SmsClient(cred, "ap-guangzhou",clientProfile);
            /* Instantiate a request object. You can further set the request parameters according to the API called and actual conditions
             * You can directly check the SDK source code to determine which attributes of the API can be set
             * An attribute may be of a basic type or import another data structure
             * We recommend you use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
            SendSmsRequest req = new SendSmsRequest();

            /* Populate the request parameters. Here, the member variables of the request object are the input parameters of the corresponding API
             * You can view the definition of the request parameters in the API documentation at the official website or by redirecting to the definition of the request object
             * Settings of a basic parameter:
             * Help link:
             * SMS console: https://console.cloud.tencent.com/smsv2
             * SMS Helper: https://cloud.tencent.com/document/product/382/3773 */

            /* SMS application ID, which is the `SdkAppId` generated after an application is added in the [SMS console], such as 1400006666 */
            String sdkAppId = "1400009099";
            req.setSmsSdkAppId(sdkAppId);

            /* SMS signature content, which should be encoded in UTF-8. You must enter an approved signature, which can be viewed in the [SMS console] */
            String signName = "Signature content";
            req.setSignName(signName);

            /* `SenderId` for Global SMS, which is not activated by default. If you need to activate it, please contact [SMS Helper] for assistance. This parameter should be left empty for Mainland China SMS */
            String senderid = "xxx";
            req.setSenderId(senderid);

            /* User session content, which can carry context information such as user-side ID and will be returned as-is by the server */
            String sessionContext = "xxx";
            req.setSessionContext(sessionContext);

            /* SMS code number extension, which is not activated by default. If you need to activate it, please contact [SMS Helper] */
            String extendCode = "xxx";
            req.setExtendCode(extendCode);

            /* Template ID. You must enter the ID of an approved template, which can be viewed in the [SMS console] */
            String templateId = "400000";
            req.setTemplateId(templateId);

            /* Target mobile number in the E.164 standard (+[country/region code][mobile number])
             * Example: +8613711112222, which has a + sign followed by 86 (country/region code) and then by 13711112222 (mobile number). Up to 200 mobile numbers are supported */
            String[] phoneNumberSet = {"+8621212313123", "+8612345678902", "+8612345678903"};
            req.setPhoneNumberSet(phoneNumberSet);

            /* Template parameters. If there are no template parameters, leave it empty */
            String[] templateParamSet = {"5678"};
            req.setTemplateParamSet(templateParamSet);

            /* Initialize the request by calling the `SendSms` method on the client object. Note: the request method name corresponds to the request object
             * The returned `res` is an instance of the `SendSmsResponse` class which corresponds to the request object */
            SendSmsResponse res = client.SendSms(req);

            // A string return packet in JSON format is output
            System.out.println(SendSmsResponse.toJsonString(res));

            // You can also take a single value. You can view the definition of the return field in the API documentation at the official website or by redirecting to the definition of the response object
            System.out.println(res.getRequestId());

        } catch (TencentCloudSDKException e) {
            e.printStackTrace();
        }
    }
}
```



### Pulling receipt status

```
import com.tencentcloudapi.common.Credential;
import com.tencentcloudapi.common.exception.TencentCloudSDKException;

// Import the optional configuration classes
import com.tencentcloudapi.common.profile.ClientProfile;
import com.tencentcloudapi.common.profile.HttpProfile;

// Import the client of the corresponding SMS module
import com.tencentcloudapi.sms.v20210111.SmsClient;

// Import the request response class corresponding to the request API
import com.tencentcloudapi.sms.v20210111.models.PullSmsReplyStatusRequest;
import com.tencentcloudapi.sms.v20210111.models.PullSmsReplyStatusResponse;

/**
 * Tencent Cloud Sms PullSmsSendStatus
 *
 */
public class PullSmsSendStatus {
    public static void main(String[] args) {
        try {
            /* Required steps:
             * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters.
             * The example here uses the way to read from the environment variable, so you need to set these two values in the environment variable first.
             * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others;
             * otherwise, the key pair may be leaked, causing damage to your properties.
             * Query the CAM key: https://console.cloud.tencent.com/cam/capi*/
            Credential cred = new Credential("secretId", "secretKey");

            // (Optional) Instantiate an HTTP option
            HttpProfile httpProfile = new HttpProfile();
            // Set the proxy
            httpProfile.setProxyHost("host");
            httpProfile.setProxyPort(port);
            /* The SDK uses the POST method by default
             * If you have to use the GET method, you can set it here, but the GET method cannot handle some large requests */
            httpProfile.setReqMethod("POST");
            /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
             * If needed, check in the code to get the latest default value */
            httpProfile.setConnTimeout(60);
            /* The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance zone,
             * you have to manually specify the domain name. For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com` */
            httpProfile.setEndpoint("sms.tencentcloudapi.com");

            /* Optional steps:
             * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
            ClientProfile clientProfile = new ClientProfile();
            /* The SDK uses `TC3-HMAC-SHA256` to sign by default
             * Do not modify this field unless absolutely necessary */
            clientProfile.setSignMethod("HmacSHA256");
            clientProfile.setHttpProfile(httpProfile);

            /* Instantiate the client object of the requested product (with SMS as an example)
             * The second parameter is the region information. You can directly enter the string `ap-guangzhou` or import the preset constant */
            SmsClient client = new SmsClient(cred, "ap-guangzhou", clientProfile);

            /* Instantiate a request object. You can further set the request parameters according to the API called and actual conditions
             * You can directly check the SDK source code to determine which attributes of the API can be set
             * An attribute may be of a basic type or import another data structure
             * We recommend you use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
            PullSmsSendStatusRequest req = new PullSmsSendStatusRequest();

            /* Populate the request parameters. Here, the member variables of the request object are the input parameters of the corresponding API
             * You can view the definition of the request parameters in the API documentation at the official website or by redirecting to the definition of the request object
             * Settings of a basic parameter:
             * Help link:
             * SMS console: https://console.cloud.tencent.com/smsv2
             * SMS Helper: https://cloud.tencent.com/document/product/382/3773 */

            /* SMS application ID, which is the `SdkAppId` generated after an application is added in the [SMS console], such as 1400006666 */
            String sdkAppId = "1400009099";
            req.setSmsSdkAppId(sdkAppId);

            // Set the maximum number of pulled entries. Maximum value: 100
            Long limit = 5L;
            req.setLimit(limit);

            /* Initialize the request by calling the `PullSmsSendStatus` method on the client object. Note: the request method name corresponds to the request object
             * The returned `res` is an instance of the `PullSmsSendStatusResponse` class which corresponds to the request object */
            PullSmsSendStatusResponse res = client.PullSmsSendStatus(req);

            // A string return packet in JSON format is output
            System.out.println(PullSmsSendStatusResponse.toJsonString(res));

        } catch (TencentCloudSDKException e) {
            e.printStackTrace();
        }
    }
}
```


### Collecting SMS message sending data

```
import com.tencentcloudapi.common.Credential;
import com.tencentcloudapi.common.exception.TencentCloudSDKException;

// Import the optional configuration classes
import com.tencentcloudapi.common.profile.ClientProfile;
import com.tencentcloudapi.common.profile.HttpProfile;

// Import the client of the corresponding SMS module
import com.tencentcloudapi.sms.v20210111.SmsClient;

// Import the request response class corresponding to the request API
import com.tencentcloudapi.sms.v20210111.models.SendStatusStatisticsRequest;
import com.tencentcloudapi.sms.v20210111.models.SendStatusStatisticsResponse;

/**
 * Tencent Cloud Sms SendStatusStatistics
 *
 */
public class SendStatusStatistics {
    public static void main(String[] args) {
        try {
            /* Required steps:
             * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters.
             * The example here uses the way to read from the environment variable, so you need to set these two values in the environment variable first.
             * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others;
             * otherwise, the key pair may be leaked, causing damage to your properties.
             * Query the CAM key: https://console.cloud.tencent.com/cam/capi*/
            Credential cred = new Credential("secretId", "secretKey");

            // (Optional) Instantiate an HTTP option
            HttpProfile httpProfile = new HttpProfile();
            // Set the proxy
            httpProfile.setProxyHost("host");
            httpProfile.setProxyPort(port);
            /* The SDK uses the POST method by default
             * If you have to use the GET method, you can set it here, but the GET method cannot handle some large requests */
            httpProfile.setReqMethod("POST");
            /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
             * If needed, check in the code to get the latest default value */
            httpProfile.setConnTimeout(60);
            /* The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance zone,
             * you have to manually specify the domain name. For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com` */
            httpProfile.setEndpoint("sms.tencentcloudapi.com");

            /* Optional steps:
             * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
            ClientProfile clientProfile = new ClientProfile();
            /* The SDK uses `TC3-HMAC-SHA256` to sign by default
             * Do not modify this field unless absolutely necessary */
            clientProfile.setSignMethod("HmacSHA256");
            clientProfile.setHttpProfile(httpProfile);

            /* Instantiate the client object of the requested product (with SMS as an example)
             * The second parameter is the region information. You can directly enter the string `ap-guangzhou` or import the preset constant */
            SmsClient client = new SmsClient(cred, "ap-guangzhou",clientProfile);

            /* Instantiate a request object. You can further set the request parameters according to the API called and actual conditions
             * You can directly check the SDK source code to determine which attributes of the API can be set
             * An attribute may be of a basic type or import another data structure
             * We recommend you use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
            SendStatusStatisticsRequest req = new SendStatusStatisticsRequest();

            /* Populate the request parameters. Here, the member variables of the request object are the input parameters of the corresponding API
             * You can view the definition of the request parameters in the API documentation at the official website or by redirecting to the definition of the request object
             * Settings of a basic parameter:
             * Help link:
             * SMS console: https://console.cloud.tencent.com/smsv2
             * SMS Helper: https://cloud.tencent.com/document/product/382/3773 */

            /* SMS application ID, which is the `SdkAppId` generated after an application is added in the [SMS console], such as 1400006666 */
            String sdkAppId = "1400009099";
            req.setSmsSdkAppId(sdkAppId);

            // Set the maximum number of pulled entries. Maximum value: 100
            Long limit = 5L;
            req.setLimit(limit);
            /* Offset. Note: this parameter is currently fixed at 0 */
            Long offset = 0L;
            req.setOffset(offset);
            /* Start time of pull in the format of `yyyymmddhh` accurate to the hour */
            String beginTime = "2019071100";
            req.setBeginTime(beginTime);
            /* End time of pull in the format of `yyyymmddhh` accurate to the hour
             * Note: `EndTime` must be after `beginTime` */
            String endTime = "2019071123";
            req.setEndTime(endTime);

            /* Initialize the request by calling the `SendStatusStatistics` method on the client object. Note: the request method name corresponds to the request object
             * The returned `res` is an instance of the `SendStatusStatisticsResponse` class which corresponds to the request object */
            SendStatusStatisticsResponse res = client.SendStatusStatisticsStatus(req);

            // A string return packet in JSON format is output
            System.out.println(SendStatusStatisticsStatusResponse.toJsonString(res));

        } catch (TencentCloudSDKException e) {
            e.printStackTrace();
        }
    }
}
```

### Applying for SMS template

```
import com.tencentcloudapi.common.Credential;
import com.tencentcloudapi.common.exception.TencentCloudSDKException;
// Import the optional configuration classes
import com.tencentcloudapi.common.profile.ClientProfile;
import com.tencentcloudapi.common.profile.HttpProfile;
// Import the client of the SMS module
import com.tencentcloudapi.sms.v20210111.SmsClient;
// Import the request response class corresponding to the request API
import com.tencentcloudapi.sms.v20210111.models.AddSmsTemplateRequest;
import com.tencentcloudapi.sms.v20210111.models.AddSmsTemplateResponse;
/**
* Tencent Cloud Sms AddSmsTemplate
*
*/
public class AddSmsTemplate
{
  public static void main( String[] args )
  {
      try {
          /* Required steps:
           * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters
           * This example uses the way to read from the environment variable, so you need to set these two values in the environment variable in advance
           * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others
           * Query the CAM key: https://console.cloud.tencent.com/cam/capi
           */
          Credential cred = new Credential("secretId", "secretKey");
           // Instantiate an HTTP option (optional; skip if there are no special requirements)
          HttpProfile httpProfile = new HttpProfile();
          // Set the proxy
          httpProfile.setProxyHost("host");
          httpProfile.setProxyPort(port);
          /* The SDK uses the POST method by default
           * If you need to use the GET method, you can set it here, but the GET method cannot handle some large requests */
          httpProfile.setReqMethod("POST");
          /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
           * If needed, check in the code to get the latest default value */
          httpProfile.setConnTimeout(60);
          /* The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance AZ, you must manually specify the domain name
           * For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com` */
          httpProfile.setEndpoint("sms.tencentcloudapi.com");
           /* Optional steps:
           * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
          ClientProfile clientProfile = new ClientProfile();
          /* The SDK uses `TC3-HMAC-SHA256` to sign by default
           * Do not modify this field unless absolutely necessary */
          clientProfile.setSignMethod("HmacSHA256");
          clientProfile.setHttpProfile(httpProfile);
          /* Instantiate an SMS client object
           * The second parameter is the region information. You can directly enter the string `ap-guangzhou` or import the preset constant */
          SmsClient client = new SmsClient(cred, "ap-guangzhou", clientProfile);
          /* Instantiate a request object. You can further set the request parameters according to the API called and actual conditions
           * You can directly check the SDK source code to determine which attributes of the API can be set
           * An attribute may be of a basic type or import another data structure
           * We recommend you use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
          AddSmsTemplateRequest req = new AddSmsTemplateRequest();
           /* Populate the request parameters. Here, the member variables of the request object are the input parameters of the corresponding API
           * You can view the definition of the request parameters in the API documentation at the official website or by redirecting to the definition of the request object
           * Settings of a basic parameter:
           * Help link:
           * SMS console: https://console.cloud.tencent.com/smsv2
           * SMS Helper: https://cloud.tencent.com/document/product/382/3773 */
           /* Template name */
          String templatename = "Tencent Cloud";
          req.setTemplateName(templatename);
           /* Template content */
          String templatecontent = "Your login verification code is {1}. Please enter it within {2} minutes. If the login was not initiated by you, please ignore this message.";
          req.setTemplateContent(templatecontent);
           /* SMS type. 0: regular SMS; 1: marketing SMS */
          long smstype = 0;
          req.setSmsType(smstype);
           /* Whether it is Global SMS. 0: Mainland China SMS; 1: Global SMS */
          long international = 0;
          req.setInternational(international);
           /* Template remarks, such as reason for application and use case */
          String remark = "xxx";
          req.setRemark(remark);
           /* Initialize the request by calling the `AddSmsTemplate` method on the client object. Note: the request method name corresponds to the request object
           * The returned `res` is an instance of the `AddSmsTemplateResponse` class which corresponds to the request object */
          AddSmsTemplateResponse res = client.AddSmsTemplate(req);
           // A string return packet in JSON format is output
          System.out.println(AddSmsTemplateResponse.toJsonString(res));
           // You can take a single value. You can view the definition of the return field in the API documentation at the official website or by redirecting to the definition of the response object
          System.out.println(res.getRequestId());
       } catch (TencentCloudSDKException e) {
          e.printStackTrace();
      }
  }
}
```

