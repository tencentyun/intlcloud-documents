## Prerequisites
Before you can integrate TenDI Captcha into a client, you need to create a CAPTCHA and obtain its CaptchaAppId and AppSecretKey from the **CAPTCHA list**. Follow the steps below:

1. Log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical) and select **CAPTCHA** -> **Manage CAPTCHA** in the left navigation pane to enter the CAPTCHA management page.
2. Click **Create CAPTCHA** and set parameters such as CAPTCHA name according to your business requirements.
3. Click **OK** to complete the creation. You can view its CaptchaAppId and AppSecretKey in the CAPTCHA list.

## Sample code

The following sample code demonstrates a page where **Verify** is clicked to activate the CAPTCHA, and the verification result is displayed in a pop-up window.

>! This sample does not include the logic to call the ticket verification API. After TenDI Captcha is integrated into the business client, the business server needs to verify the CAPTCHA ticket (if ticket verification is not integrated, the black market can easily forge verification results, which defeats the purpose of human verification via CAPTCHAs). For more information, please see [Integration to Ticket Verification (Web and App)](https://intl.cloud.tencent.com/document/product/1159/49682).

```

  <!DOCTYPE html>
  <html lang="en">
  
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Web frontend access code sample</title>
    <!-- (Required) Dependency of the CAPTCHA program, which cannot be modified. If you use local caching or other methods to skip loading of the CAPTCHA, the CAPTCHA will not update and work properly, even triggering false positives. -->
    <script src="https://sg.captcha.qcloud.com/TCaptcha-global.js"></script>
  </head>
  
  <body>
    <button id="CaptchaId" type="button">Verify</button>
  </body>
  
  <script>
  
      // Define the callback function
      function callback(res) {
          // The callback output returned by the first passed parameter, which is as follows
          // ret         Int       Verification result. The value 0 indicates a successful verification. The value 2 indicates that the CAPTCHA is disabled by the user.
          // ticket      String    A verified ticket. The field value is not null only when ret = 0.
          // CaptchaAppId       String    ID of the CAPTCHA.
          // bizState    Any       The defined transparent transmission parameter.
          // randstr     String    The random string verified, which is required for subsequent ticket verification.
          console.log('callback:', res);
  
  
          // res（The user disables the CAPTCHA）= {ret: 2, ticket: null}
          // res（Verified） = {ret: 0, ticket: "String", randstr: "String"}
          // res（Return a disaster recovery ticket prefixed with "error_" when the verification request fails） = {ret: 0, ticket: "String", randstr: "String",  errorCode: Number, errorMessage: "String"}
          // Here is the code snippet of the verification result. Modify it based on the actual ticket and errorCode
          if (res.ret === 0) {
            // Copy result to clipboard
            var str = '【randstr】->【' + res.randstr + '】      【ticket】->【' + res.ticket + '】';
            var ipt = document.createElement('input');
            ipt.value = str;
            document.body.appendChild(ipt);
            ipt.select();
            document.execCommand("Copy");
            document.body.removeChild(ipt);
            alert('1. Return result（randstr、ticket）Copied successfully. You can press Ctrl+V to paste the result to view。2. Open the console from your browser and view the result returned。');
          }
      }
  
    // Define the function that handles TCaptcha-global.js loading errors
    function loadErrorCallback() {
      var appid = 'CaptchaAppId';
      // Generate a disaster recovery ticket or execute other operations
      var ticket = 'terror_1001_' + appid + '_' + Math.floor(new Date().getTime() / 1000);
      callback({
        ret: 0,
        randstr: '@'+ Math.random().toString(36).substr(2),
        ticket: ticket,
        errorCode: 1001,
        errorMessage: 'jsload_error',
      });
    }
  
      // Define the event that triggers CAPTCHA
      window.onload = function(){
        document.getElementById('CaptchaId').onclick = function(){
          try {
            // Generate a CAPTCHA object
            // CaptchaAppId：Log in to the Captcha console and enter the [Manage CAPTCHA] page. If no CAPTCHAs has been created, create one first.
            //callback：Defined callback function
            var captcha = new TencentCaptcha('CaptchaAppId', callback, {});
            // Call the method to display the CAPTCHA
            captcha.show(); 
          } catch (error) {
            // Load error. Please call the  load error handling function
            loadErrorCallback();
            }
          }
      }
  </script>
  
  </html>
  
```
## Integration steps

### Step 1: Dynamically introduce the CAPTCHA JS
You need to dynamically introduce the CAPTCHA JS into webpages to invoke CAPTCHAs when verification is needed.

```
<!-- Example of dynamically introducing the CAPTCHA JS -->
<script src="https://sg.captcha.qcloud.com/TCaptcha-global.js"></script>
```

>! You must dynamically introduce the CAPTCHA JS. If you use other methods to avoid dynamic loading, CAPTCHAs cannot be updated and consequently some legitimate requests rather than malicious requests might be blocked.

### Step 2: Create a CAPTCHA object
After the CAPTCHA JS is introduced, Captcha will globally register the class `TencentCaptcha`, which can be used to initialize CAPTCHAs, and show or hide CAPTCHAs.

>! Do not use `id="TencentCaptcha"` to trigger the CAPTCHA. TencentCaptcha is a default system id and cannot be used. 

#### Constructor function

```
new TencentCaptcha(CaptchaAppId, callback, options);
```

**Parameters**

<table>
<thead><tr>
<th>Parameter</th><th>Value type</th><th>Description</th></tr>
</thead>
<tbody><tr><td>CaptchaAppId</td><td>String</td>
<td>The CAPTCHA's CaptchaAppId: Log in to the <a href="https://console.cloud.tencent.com/captcha/graphical">Captcha console</a> to view it on the <strong>Manage CAPTCHA</strong> page. If no CAPTCHAs exist, create one first.</td></tr><tr><td> callback</td><td>Function</td><td>The CAPTCHA callback function. For more information, please see <a href="#hdhs">callback function</a>.</td>
</tr><tr><td>options</td><td>Object</td>
<td>The CAPTCHA appearance configuration parameter. For more information, please see <a href="#pzcs">options appearance configuration parameter</a>.</td>
</tr></tbody></table>


[](id:hdhs)

#### callback function

After verification is finished, the callback function passed by the business is called, and the callback result is passed in the first parameter. The callback fields are as follows:

| Field       | Value type | Description                                                         |
| ------------ | ------ | ------------------------------------------------------------ |
| ret          | Int    | Verification result. The possible values are 0 (Verification is successful) and 2 (CAPTCHA is closed by the user).               |
| ticket       | String | The ticket of a successful verification. ticket has a value only when ret is 0.            |
| CaptchaAppId | String | The CAPTCHA's app ID.                                              |
| bizState     | Any    | The custom pass-through parameter.                                             |
| randstr      | String | The random string for this verification. This parameter is required for ticket verification.               |
| errorCode    | Number | Error code. For more information, please see [Callback function errorCode values](#errorCode). |
| errorMessage | String | Error message.                                                     |

[](id:errorCode)
**Callback function errorCode values**

| errorCode | Description                       |
| --------- | -------------------------- |
| 1001      | TCaptcha-global.js load error |
| 1002      | Timeout when calling the show method         |
| 1003      | frame.js load timeout           |
| 1004      | frame.js load error           |
| 1005      | frame.js run error           |
| 1006      | Error/Timeout when pulling the CAPTCHA configuration    |
| 1007      | iframe load timeout            |
| 1008      | iframe load error            |
| 1009      | jquery load error            |
| 1010      | dy-ele.js load error           |
| 1011      | dy-ele.js run error           |
| 1012      | 3 consecutive failed attempts to pull a CAPTCHA after refreshing            |
| 1013      | 3 consecutive failed submissions for verification        |

[](id:pzcs)

#### options appearance configuration parameter

The options parameter sets the CAPTCHA appearance. It can be left empty by default.

>!
>- You cannot change the style and size within the CAPTCHA pop-up window. Instead, you can apply `transform:scale();` to the element with `class=tcaptcha-transform` at the outermost layer of the pop-up window. CAPTCHA updates may change element attributes, such as id and class. Do not use other attribute values of the CAPTCHA element to override the style.
>- Any horizontal swipe gesture set in your mobile app must be disabled before you call the CAPTCHA show method to prevent conflicts with CAPTCHA sliding events. The gesture can be enabled after verification is finished.


| Parameter         | Value type                | Description                                                         |
| :------------- | :-------------------- | :----------------------------------------------------------- |
| bizState       | Any                   | The custom pass-through parameter, which can be used to pass a small amount of data. The parameter value will be included in the callback object. |
| enableDarkMode | Boolean/String | Enables the adaptive dark mode or force dark mode.<li> Adaptive dark mode: {"enableDarkMode": true}</li><li> Force dark mode: {"enableDarkMode": 'force'}</li> |
| ready          | Function              | The CAPTCHA loading completion callback. The callback parameters are the actual CAPTCHA width and height:<br>{"sdkView": {<br>"width": number,<br>"height": number<br>}}<br>This parameter only displays the CAPTCHA width and height, and **cannot be used to set the width and height directly**. |
| needFeedBack   | String | Custom help link: {"needFeedBack": 'url' } |
|loading|Boolean| Indicates whether to display a loading overlay while the CAPTCHA is loading. If the parameter is not specified, a loading overlay is displayed by default.<li> Display a loading overlay: {"loading": true}</li><li> Don't display a loading overlay: {"loading": false}</li>|
| userLanguage   | String                | Specifies the language of CAPTCHA prompts. This configuration takes priority over the language of the console.<br/> You can pass the same value as the user's preferred language navigator.language. The value is non-case-sensitive.<br/> For more information, please see [userLanguage configuration parameters](#userLanguage). |

[](id:userLanguage)

**userLanguage configuration parameters**

| Parameter | Description                 |
| :----- | :------------------- |
| zh-cn  | Simplified Chinese             |
| zh-hk  | Traditional Chinese (Hong Kong, China) |
| zh-tw  | Traditional Chinese (Taiwan, China) |
| en     | English                 |
| ar     | Arabic             |
| my     | Burmese               |
| fr     | French                 |
| de     | German                 |
| he     | Hebrew             |
| hi     | Hindi               |
| id     | Indonesian               |
| it     | Italian             |
| ja     | Japanese                 |
| ko     | Korean               |
| lo     | Lao               |
| ms     | Malay               |
| pl     | Polish               |
| pt     | Portuguese             |
| ru     | Russian                 |
| es     | Spanish             |
| th     | Thai                 |
| tr     | Turkish             |
| vi     | Vietnamese               |

### Step 3: Call CAPTCHA instance methods

The TencentCaptcha instance provides some common methods for CAPTCHA operations:

| Method    | Description                       | Input parameter | Response content                                 |
| --------- | -------------------------- | -------- | ---------------------------------------- |
| show      | Shows the CAPTCHA. The method can be called multiple times. | None       | None                                       |
| destroy   | Hides the CAPTCHA. The method can be called multiple times. | None       | None                                       |
| getTicket | Obtains the ticket of a successful verification.   | None       | `Object:{"CaptchaAppId":"","ticket":""}` |

### Step 4: Handle disaster recovery

To ensure that customers' websites run normally in case of an exception in the Captcha server, we recommend the following integration steps.

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
	captcha.show() 
} catch (error) {
	// Load error. Call the CAPTCHA js load error handling function.
	loadErrorCallback();
}
```
3. Define the CAPTCHA callback function so the handling is based on ticket and errorCode (instead of ret). For errorCode definitions, please see "callback function errorCode values" in Step 2.
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

For more information on disaster recovery schemes, please see [Business Disaster Recovery Scheme](https://intl.cloud.tencent.com/document/product/1159/49688).

>! After TenDI Captcha is integrated into the business client, the business server needs to verify the CAPTCHA ticket (if ticket verification is not integrated, the black market can easily forge verification results, which defeats the purpose of human verification via CAPTCHAs). For more information, please see [Integration to Ticket Verification (Web and App)](https://intl.cloud.tencent.com/document/product/1159/49682).

## FAQs

For more information, please see [FAQs About Integration](https://intl.cloud.tencent.com/document/product/1159/49692).
