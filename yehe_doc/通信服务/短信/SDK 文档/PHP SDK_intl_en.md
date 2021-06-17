
SDK 3.0 is a companion tool for the TencentCloud API 3.0 platform. You can use all [SMS APIs](https://intl.cloud.tencent.com/document/product/382/34689) through the SDK. The new SDK version is unified and features the same SDK usage, API call methods, error codes, and returned packet formats for different programming languages.
>!
>- SMS sending APIs
>One message can be sent to up to 200 numbers at a time.
>- Signature and body template APIs
>Individual users have no permission to use signature and body template APIs and can [manage SMS signatures](https://intl.cloud.tencent.com/document/product/382/35456) and [SMS body templates](https://intl.cloud.tencent.com/document/product/382/35457) only in the SMS console. To use the APIs, change "Individual Identity" to "Organizational Identity".


## Prerequisites

- You have activated SMS. For detailed directions, please see [Getting Started with Mainland China SMS](https://intl.cloud.tencent.com/document/product/382/35449).
- If you need to send Mainland China SMS messages, you need to purchase a Mainland China SMS package first.
- You have prepared the dependent environment: PHP 5.6.33 or above.
- You have obtained the `SecretID` and `SecretKey` on the **[API Key Management](https://console.cloud.tencent.com/cam/capi)** page in the CAM console.
 - `SecretID` is used to identify the API caller.
 - `SecretKey` is used to encrypt the string to sign that can be verified on the server. **You should keep it private and avoid disclosure.**
- The endpoint of the SMS service is `sms.tencentcloudapi.com`.

## Relevant Documents
- For more information on the APIs and their parameters, please see [API Documentation](https://intl.cloud.tencent.com/document/product/382/34689).
- You can download the SDK source code [here](https://github.com/TencentCloud/tencentcloud-sdk-php).

## Installing SDK


[Composer](https://www.phpcomposer.com) is a dependency management tool for PHP that supports the dependencies your project requires and installs them into your project.
1. Install Composer.
 - For Windows, go to [Composer official website](https://getcomposer.org/download/) to download the installation package and install it.
 - For Unix, run the following command to install Composer:
```
curl -sS https://getcomposer.org/installer | php
```
2. Add dependencies.
```
composer require tencentcloud/tencentcloud-sdk-php
```
3. Add the following reference code in the code.
>!This example is for reference only. Composer will generate a `vendor` directory in the project root directory, whose actual absolute path is `/path/to/`. If the operation is executed in the project root directory, you can omit the absolute path.
>
```
require '/path/to/vendor/autoload.php';
```

## Sample Code[](id:example)
>?All samples are for reference only and cannot be directly compiled and executed. You need to modify them based on your actual needs. You can also use [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sms&Version=2019-07-11&Action=SendSms) to automatically generate the demo code as needed.

Each API has a corresponding request structure and a response structure. This document only lists the sample code of several common features. For more samples, please see [SDK for PHP Samples](https://github.com/TencentCloud/tencentcloud-sdk-php/tree/master/examples/sms).


### Applying for SMS template

```
<?php
require_once '../../../TCloudAutoLoader.php';
// Import the client of the SMS module
use TencentCloud\Sms\V20190711\SmsClient;
// Import the `Request` class corresponding to the API to be requested
use TencentCloud\Sms\V20190711\Models\AddSmsTemplateRequest;
use TencentCloud\Common\Exception\TencentCloudSDKException;
use TencentCloud\Common\Credential;
// Import the optional configuration classes
use TencentCloud\Common\Profile\ClientProfile;
use TencentCloud\Common\Profile\HttpProfile;

try {
    /* Required steps:
	 * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters
	 * This example uses the way to read from the environment variable, so you need to set these two values in the environment variable in advance
	 * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others
	 * Query the CAM key: https://console.cloud.tencent.com/cam/capi
	 */
    
		$cred = new Credential("xxx", "xxx");
    //$cred = new Credential(getenv("TENCENTCLOUD_SECRET_ID"), getenv("TENCENTCLOUD_SECRET_KEY"));

    // Instantiate an HTTP option (optional; skip if there are no special requirements)
    $httpProfile = new HttpProfile();
    $httpProfile->setReqMethod("GET");  // POST request (POST request by default)
    $httpProfile->setReqTimeout(30);    // Request timeout period in seconds (60 seconds by default)
    $httpProfile->setEndpoint("sms.tencentcloudapi.com");  // Specify the access region domain name (nearby access by default)

    // Instantiate a client option (optional; skip if no special requirements are present)
    $clientProfile = new ClientProfile();
    $clientProfile->setSignMethod("TC3-HMAC-SHA256");  // Specify the signature algorithm (`HmacSHA256` by default)
    $clientProfile->setHttpProfile($httpProfile);

    // Instantiate an SMS client object. `clientProfile` is optional
    $client = new SmsClient($cred, "ap-shanghai", $clientProfile);

    // Instantiate an `AddSmsTemplateRequest` request object. Each API corresponds to a request object
    $req = new AddSmsTemplateRequest();

    /* Populate the request parameters. Here, the member variables of the request object are the input parameters of the corresponding API
     * You can view the definition of the request parameters in the API documentation at the official website or by redirecting to the definition of the request object
     * Settings of a basic parameter:
	   * Help link:
	   * SMS console: https://console.cloud.tencent.com/smsv2
  	 * SMS Helper: https://cloud.tencent.com/document/product/382/3773
  	*/
	
	/* Template name */
	$req->TemplateName = "Tencent Cloud";
	/* Template content */
	$req->TemplateContent = "Your login verification code is {1}. Please enter it within {2} minutes. If the login was not initiated by you, please ignore this message.";
	/* SMS type. 0: regular SMS; 1: marketing SMS */
	$req->SmsType = 0;
	/* Whether it is Global SMS:
		0: Mainland China SMS
		1: Global SMS */
	$req->International = 0;
	/* Template remarks, such as reason for application and use case */
	$req->Remark = "xxx";

    // Initialize the request by calling the `AddSmsTemplate` method on the client object. Note: the request method name corresponds to the request object
    $resp = $client->AddSmsTemplate($req);

    // A string return packet in JSON format is output
    print_r($resp->toJsonString());

    // You can take a single value. You can view the definition of the return field in the API documentation at the official website or by redirecting to the definition of the response object
    print_r($resp->TotalCount);
}
catch(TencentCloudSDKException $e) {
    echo $e;
}
```

### Sending SMS message

```
<?php
require_once '../../../TCloudAutoLoader.php';
// Import the SMS client
use TencentCloud\Sms\V20190711\SmsClient;
// Import the `Request` class corresponding to the API to be requested
use TencentCloud\Sms\V20190711\Models\SendSmsRequest;
use TencentCloud\Common\Exception\TencentCloudSDKException;
use TencentCloud\Common\Credential;
// Import the optional configuration classes
use TencentCloud\Common\Profile\ClientProfile;
use TencentCloud\Common\Profile\HttpProfile;

try {
    /* Required steps:
     * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters
     * This example uses the way to read from the environment variable, so you need to set these two values in the environment variable in advance
     * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others
     * Query the CAM key: https://console.cloud.tencent.com/cam/capi
     */

    $cred = new Credential("xxx", "xxx");
    //$cred = new Credential(getenv("TENCENTCLOUD_SECRET_ID"), getenv("TENCENTCLOUD_SECRET_KEY"));

    // Instantiate an HTTP option (optional; skip if there are no special requirements)
    $httpProfile = new HttpProfile();
    $httpProfile->setReqMethod("GET");  // POST request (POST request by default)
    $httpProfile->setReqTimeout(30);    // Request timeout period in seconds (60 seconds by default)
    $httpProfile->setEndpoint("sms.tencentcloudapi.com");  // Specify the access region domain name (nearby access by default)

    // Instantiate a client option (optional; skip if no special requirements are present)
    $clientProfile = new ClientProfile();
    $clientProfile->setSignMethod("TC3-HMAC-SHA256");  // Specify the signature algorithm (`HmacSHA256` by default)
    $clientProfile->setHttpProfile($httpProfile);

    // Instantiate an SMS client object. `clientProfile` is optional
    $client = new SmsClient($cred, "ap-shanghai", $clientProfile);

    // Instantiate an SMS message sending request object. Each API corresponds to a request object
    $req = new SendSmsRequest();

    /* Populate the request parameters. Here, the member variables of the request object are the input parameters of the corresponding API
     * You can view the definition of the request parameters in the API documentation at the official website or by redirecting to the definition of the request object
     * Settings of a basic parameter:
       * Help link:
       * SMS console: https://console.cloud.tencent.com/smsv2
       * SMS Helper: https://cloud.tencent.com/document/product/382/3773 */

    /* SMS application ID, which is the `SDKAppID` generated after an application is added in the [SMS console], such as 1400006666 */
    $req->SmsSdkAppid = "1400787878";
    /* SMS signature content, which should be encoded in UTF-8. You must enter an approved signature, which can be viewed in the [SMS console] */
    $req->Sign = "xxx";
    /* SMS code number extension, which is not activated by default. If you need to activate it, please contact [SMS Helper] */
    $req->ExtendCode = "0";
    /* Target mobile number in the E.164 standard (+[country/region code][mobile number])
	   * Example: +8613711112222, which has a + sign followed by 86 (country/region code) and then by 13711112222 (mobile number). Up to 200 mobile numbers are supported */
    $req->PhoneNumberSet = array("+8613711112222", "+8613711333222", "+8613711144422");
    /* `senderid` for Global SMS, which is not activated by default. If you need to activate it, please contact [SMS Helper] for assistance. This parameter should be left empty for Mainland China SMS */
    $req->SenderId = "xxx";
    /* User session content, which can carry context information such as user-side ID and will be returned as-is by the server */
    $req->SessionContext = "xxx";
    /* Template ID. You must enter the ID of an approved template, which can be viewed in the [SMS console] */
    $req->TemplateID = "449739";
    /* Template parameters. If there are no template parameters, leave it empty */
    $req->TemplateParamSet = array("0");


    // Initialize the request by calling the `SendSms` method on the client object. Note: the request method name corresponds to the request object
    $resp = $client->SendSms($req);

    // A string return packet in JSON format is output
    print_r($resp->toJsonString());

    // You can take a single value. You can view the definition of the return field in the API documentation at the official website or by redirecting to the definition of the response object
    print_r($resp->TotalCount);
}
catch(TencentCloudSDKException $e) {
    echo $e;
}
```

### Pulling receipt status


```
<?php
require_once '../../../TCloudAutoLoader.php';
// Import the client of the SMS module
use TencentCloud\Sms\V20190711\SmsClient;
// Import the `Request` class corresponding to the API to be requested
use TencentCloud\Sms\V20190711\Models\PullSmsSendStatusRequest;
use TencentCloud\Common\Exception\TencentCloudSDKException;
use TencentCloud\Common\Credential;
// Import the optional configuration classes
use TencentCloud\Common\Profile\ClientProfile;
use TencentCloud\Common\Profile\HttpProfile;

try {
    /* Required steps:
     * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters
     * This example uses the way to read from the environment variable, so you need to set these two values in the environment variable in advance
     * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others
     * Query the CAM key: https://console.cloud.tencent.com/cam/capi
     */

    $cred = new Credential("xxx", "xxx");
    //$cred = new Credential(getenv("TENCENTCLOUD_SECRET_ID"), getenv("TENCENTCLOUD_SECRET_KEY"));

    // Instantiate an HTTP option (optional; skip if there are no special requirements)
    $httpProfile = new HttpProfile();
    $httpProfile->setReqMethod("GET");  // POST request (POST request by default)
    $httpProfile->setReqTimeout(30);    // Request timeout period in seconds (60 seconds by default)
    $httpProfile->setEndpoint("sms.tencentcloudapi.com");  // Specify the access region domain name (nearby access by default)

    // Instantiate a client option (optional; skip if no special requirements are present)
    $clientProfile = new ClientProfile();
    $clientProfile->setSignMethod("TC3-HMAC-SHA256");  // Specify the signature algorithm (`HmacSHA256` by default)
    $clientProfile->setHttpProfile($httpProfile);

    // Instantiate an SMS client object. `clientProfile` is optional
    $client = new SmsClient($cred, "ap-shanghai", $clientProfile);

    // Instantiate an SMS message sending request object. Each API corresponds to a request object
    $req = new PullSmsSendStatusRequest();

    /* Populate the request parameters. Here, the member variables of the request object are the input parameters of the corresponding API
     * You can view the definition of the request parameters in the API documentation at the official website or by redirecting to the definition of the request object
     * Settings of a basic parameter:
       * Help link:
       * SMS console: https://console.cloud.tencent.com/smsv2
       * SMS Helper: https://cloud.tencent.com/document/product/382/3773 */

    /* SMS application ID, which is the `SDKAppID` generated after an application is added in the [SMS console], such as 1400006666 */
    $req->SmsSdkAppid = "1400787878";
    /* Maximum number of pulled entries. Maximum value: 100 */
    $req->Limit = 10;


    // Initialize the request by calling the `PullSmsSendStatus` method on the client object. Note: the request method name corresponds to the request object
    $resp = $client->PullSmsSendStatus($req);

    // A string return packet in JSON format is output
    print_r($resp->toJsonString());

    // You can take a single value. You can view the definition of the return field in the API documentation at the official website or by redirecting to the definition of the response object
    print_r($resp->TotalCount);
}
catch(TencentCloudSDKException $e) {
    echo $e;
}
```


### Collecting SMS message sending data

```
<?php
require_once '../../../TCloudAutoLoader.php';
// Import the client of the SMS module
use TencentCloud\Sms\V20190711\SmsClient;
// Import the `Request` class corresponding to the API to be requested
use TencentCloud\Sms\V20190711\Models\SendStatusStatisticsRequest;
use TencentCloud\Common\Exception\TencentCloudSDKException;
use TencentCloud\Common\Credential;
// Import the optional configuration classes
use TencentCloud\Common\Profile\ClientProfile;
use TencentCloud\Common\Profile\HttpProfile;

try {
    /* Required steps:
     * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters
     * This example uses the way to read from the environment variable, so you need to set these two values in the environment variable in advance
     * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others
     * Query the CAM key: https://console.cloud.tencent.com/cam/capi
     */

    $cred = new Credential("xxx", "xxx");
    //$cred = new Credential(getenv("TENCENTCLOUD_SECRET_ID"), getenv("TENCENTCLOUD_SECRET_KEY"));

    // Instantiate an HTTP option (optional; skip if there are no special requirements)
    $httpProfile = new HttpProfile();
    $httpProfile->setReqMethod("GET");  // POST request (POST request by default)
    $httpProfile->setReqTimeout(30);    // Request timeout period in seconds (60 seconds by default)
    $httpProfile->setEndpoint("sms.tencentcloudapi.com");  // Specify the access region domain name (nearby access by default)

    // Instantiate a client option (optional; skip if no special requirements are present)
    $clientProfile = new ClientProfile();
    $clientProfile->setSignMethod("TC3-HMAC-SHA256");  // Specify the signature algorithm (`HmacSHA256` by default)
    $clientProfile->setHttpProfile($httpProfile);

    // Instantiate an SMS client object. `clientProfile` is optional
    $client = new SmsClient($cred, "ap-shanghai", $clientProfile);

    // Instantiate an SMS message sending request object. Each API corresponds to a request object
    $req = new SendStatusStatisticsRequest();

    /* Populate the request parameters. Here, the member variables of the request object are the input parameters of the corresponding API
     * You can view the definition of the request parameters in the API documentation at the official website or by redirecting to the definition of the request object
     * Settings of a basic parameter:
       * Help link:
       * SMS console: https://console.cloud.tencent.com/smsv2
       * SMS Helper: https://cloud.tencent.com/document/product/382/3773 */

    /* SMS application ID, which is the `SDKAppID` generated after an application is added in the [SMS console], such as 1400006666 */
    $req->SmsSdkAppid = "1400787878";
    /* Maximum number of pulled entries. Maximum value: 100 */
    $req->Limit = 10;
    /* Offset. Note: this parameter is currently fixed at 0 */
    $req->Offset = 0;
    /* Start time of pull in the format of `yyyymmddhh` accurate to the hour */
    $req->StartDateTime = "2019122500";
    /* End time of pull in the format of `yyyymmddhh` accurate to the hour
	 * Note: `EndDataTime` must be after `StartDateTime` */
    $req->EndDataTime = "2019122523";

    // Initialize the request by calling the `SendStatusStatistics` method on the client object. Note: the request method name corresponds to the request object
    $resp = $client->SendStatusStatistics($req);

    // A string return packet in JSON format is output
    print_r($resp->toJsonString());

    // You can take a single value. You can view the definition of the return field in the API documentation at the official website or by redirecting to the definition of the response object
    print_r($resp->TotalCount);
}
catch(TencentCloudSDKException $e) {
    echo $e;
}
```

## FAQs[](id:point)
### Proxy
If there is a proxy in your environment, you need to set the system environment variable `https_proxy`; otherwise, it may not be called normally, and a connection timeout exception will be thrown.
You can also use `GuzzleHttp` to configure the proxy:
```php
$cred = new Credential("secretId", "secretKey");

$httpProfile = new HttpProfile();
$httpProfile->setProxy('https://ip:port');

$clientProfile = new ClientProfile();
$clientProfile->setHttpProfile($httpProfile);

$client = new OcrClient($cred, 'ap-beijing', $this->clientProfile);
```

### Certificate issue
If there is a problem with your PHP environment certificate, errors similar to `cURL error 60: See http://curl.haxx.se/libcurl/c/libcurl-errors.html` will occur, which can be solved as follows:
1. Download the certificate file [cacert.pem](https://curl.haxx.se/ca/cacert.pem) and save it to the PHP installation path.
2. Edit the `php.ini` file: delete the semicolon comment (;) before the `curl.cainfo` configuration item and set the value to the absolute path of the saved certificate file `cacert.pem`.
3. Restart the services that depend on PHP.

### php_curl extension
`GuzzleHttp`, which this SDK depends on, needs to have the `php_curl` extension enabled. Check whether the `php.ini` environment in your environment is enabled.
For example, on Linux with PHP 7.1, for services hosted under Apache, you can open `/etc/php/7.1/apache2/php.ini` to see whether the `extension=php_curl.dll` configuration item has been commented. Please delete the comment before it and restart Apache.

### Exceptional web access
Access is normal on the command line, but the following error is reported when access is performed on a web server: cURL error 0: The cURL request was retried 3 times and did not succeed. The most likely reason for the failure is that cURL was unable to rewind the body of the request and subsequent retries resulted in the same error. Turn on the debug option to see what went wrong. See https://bugs.php.net/bug.php?id=47204 for more information. (see http://curl.haxx.se/libcurl/c/libcurl-errors.html).
This error may occur in different cases. You can run `php -r "echo sys_get_temp_dir();"` to print the absolute path of the default system temporary directory and set `sys_temp_dir` in `php.ini` to the printed path, and then check whether this error is fixed.
