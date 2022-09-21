## Business request process
The CAPTCHA request process involves the interaction between the business client (frontend), business server (backend), and Captcha server. The sequence diagram of calls is shown as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/123b3a67dd614c0226e1ea45873d62fc.png)

To ensure that customers' business processes run normally in case of an exception in the Captcha server, we provide the following business disaster recovery schemes.

>! No billing is incurred when verifying any disaster recovery tickets generated in the disaster recovery schemes.

## Business client (frontend) disaster recovery
1. Define the JS load error handling function.

``` javascript
// The error handling function ensures that event processes run normally in case of JS load or initialization errors.
// Define the function before the script loads
function loadErrorCallback() {
	var appid = ''
	// Generate a disaster recovery ticket or use another handling technique
	var ticket = 'terror_1001_' + appid + Math.floor(new Date().getTime() / 1000);
	callback({
		ret: 0,
        randstr: '@'+ Math.random().toString(36).substr(2),
        ticket,
        errorCode: 1001,
        errorMessage: 'jsload_error',
	});
}
```

2. Call the JS load error handling function if an error is caught during the CAPTCHA instance call.

```javascript
try {
	// Generate a CAPTCHA object
	var captcha = new TencentCaptcha('Your CAPTCHA's CaptchaAppId', callback, {});
	// Call the method to show the CAPTCHA
	captcha.show(); 
} catch (error) {
	// Load error. Call the CAPTCHA js load error handling function.
	loadErrorCallback();
}
```

3. Define the CAPTCHA callback function so the handling is based on ticket and errorCode (instead of ret). For errorCode definitions, please see [Web Frontend Integration](https://console.cloud.tencent.com/captcha/graphical).

```javascript
function callback(res) {
	// res (CAPTCHA is closed by the user) = {ret: 2, ticket: null}
	// res (Verification is successful) = {ret: 0, ticket: "String", randstr: "String"}
	// res (Request error. A disaster recovery ticket with the prefix terror_ is returned.) = {ret: 0, ticket: "String", randstr: "String",  errorCode: Number, errorMessage: "String"}
	if (res.ticket){
		// Handle based on errorCode
        if(res.errorCode === xxxxx){
           // Customize the disaster recovery logic (for example, skip this verification)
        }
      }
}
```


## Business server (backend) disaster recovery
In case of an exception when requesting the **ticket verification API**, the business server needs to handle the exception (for example, skip this verification) to avoid affecting business processes due to abnormal API responses, request timeouts, or the service not responding. **The following are some abnormal responses that require disaster recovery on the business side.**
- Request timeout or service not responding.
- Exception returned. Code is InternalError. Example:
```php
{
    "Response": {
        "Error": {
            "Code": "InternalError",
            "Message": "An internal error has occurred. Retry your request. If the problem persists, contact us."
        },
        "RequestId": "xxxxxxxxxxx"
    }
}
```
- Service internal error. CaptchaCode is 26. Example:
``` 
{
    "Response": {
        "CaptchaCode": 26,
        "CaptchaMsg": "System busy. For more information, please see the TenDI Captcha documentation. Search for the keyword "DescribeCaptchaResult", and check the description of the CaptchaCode field in the output parameters",
        "EvilLevel": 0,
        "GetCaptchaTime": 0,
        "RequestId": "xxxxxxxxxxx"
    },
    "retcode": 0,
    "retmsg": "ok"
}
```

## More information
You can log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical), and click **Quick Consulting** in the upper right corner to learn more.
