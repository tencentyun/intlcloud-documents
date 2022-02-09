
The Aegis instance of RUM automatically monitors exceptions such as JavaScript and Promise execution errors and Ajax (fetch) request exceptions. This document describes the monitoring logic of each error type and how to handle them.

<dx-alert infotype="notice" title="">
 The Aegis instance monitors such exceptions. It will not report any data If you merely import the Aegis SDK and don't instantiate it.
</dx-alert>

## JavaScript Execution Error

Aegis listens on the `onerror` event in the `wx` object to capture project errors. Then, it parses errors and analyze the heaps and stacks to automatically report the error information to the backend service. In this case, the report level is `error`; therefore, when the number of automatically reported errors reaches the threshold, Aegis will automatically trigger an alarm to help you find the exceptions promptly. As the report level is `error`, automatic reporting will also affect the project score.

## Request Exception

Aegis will rewrite `wx.request`/`qq.request` and listen on each API request. If `statusCode` does not exist or is greater than 400, the request will be considered a failure, timeout, or abortion.

If you use a library that will also rewrite `wx.request`/`qq.request`, such as `miniprogram-api-promise`, in your project, or you also perform encapsulation, you must initialize Aegis before importing the library; otherwise, API failures cannot be listened on.

>! When an error occurs, the Aegis SDK doesn't actively collect API request and response parameters. You can configure the `apiDetail` parameter in the API calling to enable reporting of such information.

<dx-codeblock>
:::  js
new Aegis({
  api: {
    apiDetail: true,
  },
});
:::
</dx-codeblock>

## `retcode` Exception

Aegis rewrites `wx.request`/`qq.request` to get the API response. It also tries to get the `retcode` of the request in the response. If the `retcode` doesn't meet the expectation, the request will be considered exceptional and will be reported.

<dx-alert infotype="explain" title="">
You can get `retcode` and judge which `retcode` values are normal as instructed in [Configuration Guide](https://intl.cloud.tencent.com/document/product/1131/44539).
</dx-alert>
