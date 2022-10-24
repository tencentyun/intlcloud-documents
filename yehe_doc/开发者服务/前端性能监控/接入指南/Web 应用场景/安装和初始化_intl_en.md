You can install the SDK through CDN or npm.


## Installing and Initializing SDK Through CDN
1. Import the following code to the `<head></head>` tags on the HTML page:
<dx-codeblock>
:::  html
<script src="https://cdn-go.cn/aegis/aegis-sdk/latest/aegis.min.js"></script>
:::
</dx-codeblock>
As CDN uses the h3-Q050 protocol, `cache-control` is set to `max-age=666` by default. If you need to modify `cache-control`, add the `max_age` parameter. For example: 
<dx-codeblock>
:::  html
<script src="https://cdn-go.cn/aegis/aegis-sdk/latest/aegis.min.js?max_age=3600"></script>
:::
</dx-codeblock>

2. Create an Aegis instance and pass in the corresponding configuration in the following steps to initialize the SDK:
<dx-codeblock>
:::  javascript
const aegis = new Aegis({
    id: 'pGUVFTCZyewhxxxxxx', // Application ID, that is, reported ID
    uin: 'xxx', // User UIN (optional)
    reportApiSpeed: true, // API speed test
    reportAssetSpeed: true, // Static resource speed test
    spa: true // Enable PV calculation during SPA application page redirect
});
:::
</dx-codeblock>

## Installing and Initializing SDK Through npm
1. Run the following command to install `aegis-web-sdk` in your npm repository:
 <dx-codeblock>
::: Linux
$ npm install --save aegis-web-sdk
:::
</dx-codeblock>
2. Create an Aegis instance and pass in the corresponding configuration in the following steps to initialize the SDK:
<dx-codeblock>
:::  javascript
import Aegis from 'aegis-web-sdk';

const aegis = new Aegis({
    id: 'pGUVFTCZyewhxxxxxx', // Application ID, that is, reported ID
    uin: 'xxx', // User UIN (optional)
    reportApiSpeed: true, // API speed test
    reportAssetSpeed: true, // Static resource speed test
    spa: true // Enable PV calculation during SPA application page redirect
})
:::
</dx-codeblock>

>?To avoid missing any data, you should initialize the SDK as early as possible. After you install and initialize the SDK, you can use the following RUM features:
>
>- Error monitoring: Monitoring of JavaScript execution errors, Promise errors, Ajax request exceptions, resource loading failures, and return code exceptions, PV reporting, and allowlist detection.  
>- Speed test features: Speed tests for page performance, APIs, and static resources.
>- Statistics collection and analysis: You can analyze data in multiple dimensions in [Data Overview](https://console.cloud.tencent.com/rum/web).

> ?`aegis-sdk` uses `https://aegis.qq.com` as the domain name to be reported by default. You can use the `hostUrl` parameter to configure the domain name to be reported.
For regions in the Chinese mainland, you can choose `https://tamaegis.com` as the domain name to be reported.
For Singapore region, you can choose `https://rumt-sg.com` as the domain name to be reported.
