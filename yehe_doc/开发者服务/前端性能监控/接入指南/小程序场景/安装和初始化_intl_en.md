## Notes
- You can only use npm to install the SDK for mini program.
- The SDK supports WeChat Mini Program and QQ Mini Program.

> ?`aegis-sdk` uses `aegis.qq.com` as the reporting domain by default. You can also use `tamaegis.com` as the reporting domain.

>! To connect to a mini program in the production environment, you need to add the reporting domain as a secure domain.

## Installing SDK

Run the following command to install `aegis-mp-sdk` in your npm repository:
<dx-codeblock>
::: Linux
$ npm install --save aegis-mp-sdk
:::
</dx-codeblock>

## Initialization

Create an Aegis instance and pass in the corresponding configuration in the following steps to initialize the SDK:

<dx-codeblock>
::: Linux
import Aegis from 'aegis-mp-sdk';

const aegis = new Aegis({
  id: "pGUVFTCZyewxxxxx", // Project key
  uin: 'xxx', // User UIN (optional)
  reportApiSpeed: true, // API speed test
  spa: true, // Report the PV during page switch
});
:::
</dx-codeblock>

> ?To avoid missing any data, you should initialize the SDK as early as possible. If you use `miniprogram-api-promise` to encapsulate the `wx.request` request in your mini program project, you should note that Aegis rewrites `wx.request` for API monitoring. Therefore, you must initialize Aegis before importing `miniprogram-api-promise`; otherwise, Aegis may fail to collect the complete API information.
> After you install and initialize the SDK, you can use the following RUM features:
>
> 1. Error monitoring: JavaScript execution error monitoring.  
> 2. Speed test: API speed test.
> 3. Statistics collection and analysis: you can analyze data in multiple dimensions on the [**Data Overview**](https://console.cloud.tencent.com/rum/web) page in the RUM console.


