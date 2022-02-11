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
- You have prepared the dependent environment: Node.js 7.10.1 or above.
- You have obtained the `SecretID` and `SecretKey` on the **[API Key Management](https://console.cloud.tencent.com/cam/capi)** page in the CAM console.
 - `SecretID` is used to identify the API caller.
 - `SecretKey` is used to encrypt the string to sign that can be verified on the server. **You should keep it private and avoid disclosure.**
- The endpoint of the SMS service is `sms.tencentcloudapi.com`.

## Relevant Documents
- For more information on the APIs and their parameters, please see [API Documentation](https://intl.cloud.tencent.com/document/product/382/40463).
- You can download the SDK source code [here](https://github.com/TencentCloud/tencentcloud-sdk-nodejs).

## Installing SDK
### Installing through npm (recommended)
[npm](https://www.npmjs.com/) is a package management tool for Node.js.

1. Run the following installation command:
```
npm install tencentcloud-sdk-nodejs --save
```
2. Refer to the corresponding module code in your code. For more information, please see the [sample code](#example).

### Installing through source package
1. Go to the [GitHub code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-nodejs) or [quick download address](https://tencentcloud-sdk-1253896243.file.myqcloud.com/tencentcloud-sdk-nodejs/tencentcloud-sdk-nodejs.zip) to download the source code package.
2. Decompress the source package to an appropriate location in your project.
3. Refer to the corresponding module code in your code. For more information, please see the [sample code](#example).


## Sample Code[](id:example)
>?All samples are for reference only and cannot be directly compiled and executed. You need to modify them based on your actual needs. You can also use [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sms&Version=2021-01-11&Action=SendSms) to automatically generate the demo code as needed.

Each API has a corresponding request structure and a response structure. This document only lists the sample code of several common features as shown below: 

### Sending SMS message

```
const tencentcloud = require("tencentcloud-sdk-nodejs")

// Import the client models of the corresponding product module
const smsClient = tencentcloud.sms.v20210111.Client

/* Instantiate the client object of the requested product (with SMS as an example) */
const client = new smsClient({
  credential: {
  // Required: `secretId` and `secretKey` of Tencent Cloud account.
   * The example here uses the way to read from the environment variable, so you need to set these two values in the environment variable first.
   * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others;
   * otherwise, the key pair may be leaked, causing damage to your properties.
   * Query the CAM key: https://console.cloud.tencent.com/cam/capi */
    secretId: process.env.secretId,
    secretKey: process.env.secretKey,
  },
  /* Required: region information. The parameter is the information on the region you select in Tencent Cloud International. If you select Singapore, you should enter the string `ap-singapore`. Click https://intl.cloud.tencent.com/document/api/382/40466?lang=en#region-list to view the region list. */
  region: "ap-singapore",
  /* Optional:
   * Client configuration object. You can specify the timeout period and other configuration items */
  profile: {
    /* The SDK uses `TC3-HMAC-SHA256` to sign by default. Do not modify this field unless absolutely necessary */
    signMethod: "HmacSHA256",
    httpProfile: {
      /* The SDK uses the POST method by default
       * If you have to use the GET method, you can set it here, but the GET method cannot handle some large requests */
      reqMethod: "POST",
      /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
       * If needed, check in the code to get the latest default value */
      reqTimeout: 30,
      /**
       * The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance zone,
       * you need to manually specify the domain name. For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com`
       */
      endpoint: "sms.tencentcloudapi.com"
    },
  },
})

/* Request parameter. You can further set the request parameters according to the API called and actual conditions
 * An attribute may be of a basic type or import another data structure
 * We recommend you use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
const params = {
  /* SMS application ID, which is the `SmsSdkAppId` generated after an application is added in the [SMS console], such as 1400006666 */
  SmsSdkAppId: "1400787878",
  /* SMS signature content, which should be encoded in UTF-8. You must enter an approved signature, which can be viewed in the [SMS console] */
  SignName: "xxx",
  /* SMS code number extension, which is not activated by default. If you need to activate it, please contact [SMS Helper] */
  ExtendCode: "",
  /* `senderid` for Global SMS, which is not activated by default. If you need to activate it, please contact [SMS Helper] for assistance. This parameter should be left empty for Mainland China SMS */
  SenderId: "",
  /* User session content, which can carry context information such as user-side ID and will be returned as-is by the server */
  SessionContext: "",
  /* Target mobile number in the e.164 standard (+[country/region code][mobile number])
   * Example: +8613711112222, which has a + sign followed by 86 (country/region code) and then by 13711112222 (mobile number). Up to 200 mobile numbers are supported */
  PhoneNumberSet: ["+8613711112222"],
  /* Template ID. You must enter the ID of an approved template, which can be viewed in the [SMS console] */
  TemplateId: "449739",
  /* Template parameters. If there are no template parameters, leave it empty */
  TemplateParamSet: ["666"],
}
// Call the API you want to access through the client object; you need to pass in the request object and the response callback function
client.SendSms(params, function (err, response) {
  // The request returns an exception and the exception information is printed
  if (err) {
    console.log(err)
    return
  }
  // The request is returned normally, and the `response` object is printed
  console.log(response)
})
```

### Pulling receipt status

```
const tencentcloud = require("tencentcloud-sdk-nodejs")

// Import the client models of the corresponding product module
const smsClient = tencentcloud.sms.v20210111.Client

/* Instantiate the client object of the requested product (with SMS as an example) */
const client = new smsClient({
  credential: {
  // Required: `secretId` and `secretKey` of Tencent Cloud account.
   * The example here uses the way to read from the environment variable, so you need to set these two values in the environment variable first.
   * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others;
   * otherwise, the key pair may be leaked, causing damage to your properties.
   * Query the CAM key: https://console.cloud.tencent.com/cam/capi */
    secretId: process.env.secretId,
    secretKey: process.env.secretKey,
  },
  /* Required: region information. The parameter is the information on the region you select in Tencent Cloud International. If you select Singapore, you should enter the string `ap-singapore`. Click https://intl.cloud.tencent.com/document/api/382/40466?lang=en#region-list to view the region list. */
  region: "ap-singapore",
  /* Optional:
   * Client configuration object. You can specify the timeout period and other configuration items */
  profile: {
    /* The SDK uses `TC3-HMAC-SHA256` to sign by default. Do not modify this field unless absolutely necessary */
    signMethod: "HmacSHA256",
    httpProfile: {
      /* The SDK uses the POST method by default
       * If you have to use the GET method, you can set it here, but the GET method cannot handle some large requests */
      reqMethod: "POST",
      /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
       * If needed, check in the code to get the latest default value */
      reqTimeout: 30,
      /**
       * The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance zone,
        * you need to manually specify the domain name. For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com`
       */
      endpoint: "sms.tencentcloudapi.com"
    },
  },
})

/* Request parameter. You can further set the request parameters according to the API called and actual conditions
 * An attribute may be of a basic type or import another data structure
 * We recommend you use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
const params = {
  // SMS application ID, which is the `SdkAppId` generated after an application is added in the [SMS console], such as 1400006666
  SmsSdkAppId: "1400787878",
  // Maximum number of pulled entries. Maximum value: 100
  Limit: 10,
}
// Call the API you want to access through the client object; you need to pass in the request object and the response callback function
client.PullSmsSendStatus(params, function (err, response) {
  // The request returns an exception and the exception information is printed
  if (err) {
    console.log(err)
    return
  }
  // The request is returned normally, and the `response` object is printed
  console.log(response)
})
```

### Collecting SMS message sending data

```
const tencentcloud = require("tencentcloud-sdk-nodejs")

// Import the client models of the corresponding product module
const smsClient = tencentcloud.sms.v20210111.Client

/* Instantiate the client object of the requested product (with SMS as an example) */
const client = new smsClient({
  credential: {
  // Required: `secretId` and `secretKey` of Tencent Cloud account.
   * The example here uses the way to read from the environment variable, so you need to set these two values in the environment variable first.
   * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others;
   * otherwise, the key pair may be leaked, causing damage to your properties.
   * Query the CAM key: https://console.cloud.tencent.com/cam/capi */
    secretId: process.env.secretId,
    secretKey: process.env.secretKey,
  },
  /* Required: region information. The parameter is the information on the region you select in Tencent Cloud International. If you select Singapore, you should enter the string `ap-singapore`. Click https://intl.cloud.tencent.com/document/api/382/40466?lang=en#region-list to view the region list. */
  region: "ap-singapore",
  /* Optional:
   * Client configuration object. You can specify the timeout period and other configuration items */
  profile: {
    /* The SDK uses `TC3-HMAC-SHA256` to sign by default. Do not modify this field unless absolutely necessary */
    signMethod: "HmacSHA256",
    httpProfile: {
      /* The SDK uses the POST method by default
       * If you have to use the GET method, you can set it here, but the GET method cannot handle some large requests */
      reqMethod: "POST",
      /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
       * If needed, check in the code to get the latest default value */
      reqTimeout: 30,
      /**
       * The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance zone,
        * you need to manually specify the domain name. For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com`
       */
      endpoint: "sms.tencentcloudapi.com"
    },
  },
})

/* Request parameter. You can further set the request parameters according to the API called and actual conditions
 * An attribute may be of a basic type or import another data structure
 * We recommend you use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
const params = {
    // SMS application ID, which is the `SdkAppId` generated after an application is added in the [SMS console], such as 1400006666
    SmsSdkAppId: "1400787878",
    // Maximum number of pulled entries. Maximum value: 100
    Limit: 10,
    // Offset. Note: this parameter is currently fixed at 0
    Offset: 0,
    // Start time of pull in the format of `yyyymmddhh` accurate to the hour
    BeginTime: "2019122400",
    // End time of pull in the format of `yyyymmddhh` accurate to the hour
    // Note: `EndTime` must be after `BeginTime`
    EndTime: "2019122523",
}
// Call the API you want to access through the client object; you need to pass in the request object and the response callback function
client.SendStatusStatistics(params, function (err, response) {
  // The request returns an exception and the exception information is printed
  if (err) {
    console.log(err)
    return
  }
  // The request is returned normally, and the `response` object is printed
  console.log(response)
})
```

### Applying for SMS template
```
const tencentcloud = require("tencentcloud-sdk-nodejs")

// Import the client models of the corresponding product module
const smsClient = tencentcloud.sms.v20210111.Client

/* Instantiate the client object of the requested product (with SMS as an example) */
const client = new smsClient({
  credential: {
  // Required: `secretId` and `secretKey` of Tencent Cloud account.
   * The example here uses the way to read from the environment variable, so you need to set these two values in the environment variable first.
   * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others;
   * otherwise, the key pair may be leaked, causing damage to your properties.
   * Query the CAM key: https://console.cloud.tencent.com/cam/capi */
    secretId: process.env.secretId,
    secretKey: process.env.secretKey,
  },
  /* Required: region information. The parameter is the information on the region you select in Tencent Cloud International. If you select Singapore, you should enter the string `ap-singapore`. Click https://intl.cloud.tencent.com/document/api/382/40466?lang=en#region-list to view the region list. */
  region: "ap-singapore",
  /* Optional:
   * Client configuration object. You can specify the timeout period and other configuration items */
  profile: {
    /* The SDK uses `TC3-HMAC-SHA256` to sign by default. Do not modify this field unless absolutely necessary */
    signMethod: "HmacSHA256",
    httpProfile: {
      /* The SDK uses the POST method by default
       * If you have to use the GET method, you can set it here, but the GET method cannot handle some large requests */
      reqMethod: "POST",
      /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
       * If needed, check in the code to get the latest default value */
      reqTimeout: 30,
      /**
       * The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance zone,
       * you need to manually specify the domain name. For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com`
       */
      endpoint: "sms.tencentcloudapi.com"
    },
  },
})

/* Request parameter. You can further set the request parameters according to the API called and actual conditions
 * An attribute may be of a basic type or import another data structure
 * We recommend you use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
const params = {
  /* Template name */
  TemplateName: "Tencent Cloud",
  /* Template content */
  TemplateContent: "Your login verification code is {1}. Please enter it within {2} minutes. If the login was not initiated by you, please ignore this message.",
  /* SMS type. 0: regular SMS; 1: marketing SMS */
  SmsType: 0,
  /* Whether it is Global SMS. 0: Mainland China SMS; 1: Global SMS */
  International: 0,
  /* Template remarks, such as reason for application and use case */
  Remark: "xxx",
}
// Call the API you want to access through the client object; you need to pass in the request object and the response callback function
client.AddSmsTemplate(params, function (err, response) {
  // The request returns an exception and the exception information is printed
  if (err) {
    console.log(err)
    return
  }
  // The request is returned normally, and the `response` object is printed
  console.log(response)
})
```

## FAQs
<dx-accordion>
::: Proxy settings
If there is a proxy in your environment, you need to set the system environment variable `https_proxy`; otherwise, it may not be called normally, and a connection timeout exception will be thrown.
:::
</dx-accordion>
