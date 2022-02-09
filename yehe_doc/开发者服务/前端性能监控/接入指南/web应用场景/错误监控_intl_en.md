
The Aegis instance of RUM automatically monitors exceptions such as JavaScript and Promise execution errors and Ajax (fetch) request exceptions. This document describes the monitoring logic of each error type and how to handle them.

<dx-alert infotype="notice" title="">
 The Aegis instance monitors such exceptions. If you only import the Aegis SDK but don't instantiate it, it won't report any data.
</dx-alert>

## JavaScript Execution Error

Aegis listens on the `onerror` event in the `window` object to capture project errors. Then, it parses errors and analyze the heaps and stacks to automatically report the error information to the backend service. In this case, the report level is `error`; therefore, when the number of automatically reported errors reaches the threshold, Aegis will automatically trigger an alarm to help you find the exceptions promptly. As the report level is `error`, automatic reporting will also affect the project score.


- If a cross-origin JavaScript script is imported on the page, you need to add the `crossorigin` attribute to the `script` tag; otherwise, Aegis cannot get the error details.
- If the user uses the Vue framework, import the following code to get and actively report errors:
<dx-codeblock>
:::  js
Vue.config.errorHandler = function(err, vm, info) {
  console.log(`Error: ${err.toString()}\nStack: ${err.stack}\nInfo: ${info}`);
  aegis.error(`Error: ${err.toString()}\nStack: ${err.stack}\nInfo: ${info}`);
};
:::
</dx-codeblock>


## Promise Execution Error

RUM listens on the `unhandledrejection` event to capture Promise errors that are not caught through `catch`. To ensure page stability, we recommend you `catch` all Promise errors.

## Ajax (`fetch`) Request Exception

Aegis rewrites the `XMLHttpRequest` object to listen on each API request and will consider the following cases an exception:  

- `http status` is greater than or equal to 400.
- A request times out or is aborted, cross-origin, or canceled.
- `http status` is still 0 when a request ends, which usually occurs when the request fails.

>! When an error occurs, the Aegis SDK doesn't actively collect API request and response parameters. If you want such API information to be reported, you can use the `apiDetail` API parameter to enable reporting.

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

Aegis rewrites the `XMLHttpRequest` object to get the API response. It also tries to get the `retcode` of the request in the response. If the `retcode` doesn't meet the expectation, the request will be considered exceptional and will be reported.

<dx-alert infotype="explain" title="">
You can get `retcode` and judge which `retcode` values are normal as instructed in [Configuration Guide](https://intl.cloud.tencent.com/document/product/1131/44529).
</dx-alert>

## Resource Loading Failure

If a request sent by a page element fails, it will be captured by the `window.onerror` event. Aegis uses this feature to listen on the loading failures of following resources:  

- CSS and font requested by the `<link>` tag.
- Scripts requested by the `<script>` tag.
- Multimedia resources requested by the `<audio>` and `<video>` tags.
