## Non-standard integration issues

### What issues will occur if the Captcha JS is not dynamically loaded?

1. Integration method: When the web or app integrates to Captcha, it uses a method other than dynamically loading TCaptcha-global.js.
2. Security risks: If the above methods are used, CAPTCHAs cannot be updated and consequently some legitimate requests rather than malicious requests might be blocked, and errors might be reported in the frontend.
3. Solution: Dynamically introduce the Captcha JS. For more information, please see [Web Integration](https://intl.cloud.tencent.com/document/product/1159/49680).

```html
<!-- Captcha program dependency (required). Do not modify the following program dependency. If you use other methods to avoid loading, CAPTCHAs cannot be updated and consequently some legitimate requests rather than malicious requests might be blocked. -->
<script src="https://sg.captcha.qcloud.com/TCaptcha-global.js"></script> 
```

### What issues will occur if ticket verification is not integrated?

1. Integration method: The client integrates to Captcha, but the server does not.
2. Security risks: If ticket verification is not integrated, the black market can easily forge verification results, which defeats the purpose of human verification via CAPTCHAs.
3. Solution: Integrate the server to ticket verification. For more information, please see [Integration to Ticket Verification (Web and App)](https://intl.cloud.tencent.com/document/product/1159/49682).

## Web and App integration issues

### During the test, the prompt "Too many attempts. Try again later." was displayed. How do I resolve this issue?
This is because the Captcha service blocks suspected malicious users. You may have frequently and intensively accessed the Captcha service of the same scenario in the same network environment, resulting in small-scale risk control blocking. Solutions:
- Perform the test again after 10-20 minutes.
- Change the IP or device and try again.
- Log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical), go to the **Security Configuration** page of the verification, and adjust the malicious request blocking level to **Loose**.

### Android uses the Web frontend HTML5 method for integration. During the debugging process, a blank background pops up first and then the CAPTCHA page. How do I change that?

- During the debugging process, normally, the webview is called first to load the webpage and then the CAPTCHA page pops up.
- If the blank background pops up first and then the Image CAPTCHA page, the reasons are as follows:
   - The time of loading the Captcha JS results in a white screen.
   - The page has no content, so the loaded webview is displayed. In this case, it is necessary to display the webview after the ready event is triggered.
- Therefore, Android needs to load the page without displaying it, wait for the ready callback, and then display the page after being notified to do so. For ready configuration instructions, see [Web Integration - Create Captcha Object](https://intl.cloud.tencent.com/document/product/1159/49680).
```
options={ready: function(size){
  // Communicate with Android
}}
new TencentCaptcha(appId, callback, options);
```

### What should I do when CAPTCHAs are not completely displayed on the app?
CAPTCHAs are displayed in the center based on the width and height of the container. CAPTCHAs may be truncated if the width of the container is too wide, causing the incomplete display of the CAPTCHAs. In this case, you need to adjust the pop-up window. In addition, random loading of other webviews may also cause truncation.
