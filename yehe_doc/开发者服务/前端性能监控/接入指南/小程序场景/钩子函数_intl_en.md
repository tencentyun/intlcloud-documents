You can use a hook function to customize the configuration for resource speed test data reporting, and the system will calculate and collect the function execution duration. Then, you can use [custom speed test](https://console.cloud.tencent.com/rum/web/custom) to analyze the function execution duration in multiple dimensions.

## beforeReport

1. This hook will be executed before log reporting (by the `/collect?` API); for example:
<dx-codeblock>
:::  js
const aegis = new Aegis({
  id: 'pGUVFTCZyewxxxxx',
  beforeReport(log) {
  // Listen on the reported error below
    console.log(log); // {level: "4", msg: "An error occurred."}
    return log;
  }
});

throw new Error('An error occurred.');
:::
</dx-codeblock>
<dx-alert infotype="explain" title="">
The above `log` will have the following fields:  
1. `level`: log level. For example, `'4'` indicates error log.  
2. msg`: log content.
3. Below are all log levels:
- `{ level: '1', name: 'API request log (allowed log)' }`
- `{ level: '2', name: 'General log' }`
- `{ level: '4', name: 'JavaScript execution error' }`
- `{ level: '8', name: 'Promise error' }`
- `{ level: '16', name: 'Ajax request exception' }`
- `{ level: '32', name: 'JavaScript loading exception' }`
- `{ level: '64', name: 'Image loading exception' }`
- `{ level: '128', name: 'CSS loading exception' }`
- `{ level: '256', name: 'console.error (reserved)' }`
- `{ level: '512', name: 'Audio/Video resource exception' }`
- `{ level: '1024', name: 'retcode exception' }`
- `{ level: '2048', name: 'aegis report' `
</dx-alert>
2. If this hook returns `false`, the log won't be reported. This feature can be used to filter out errors that don't need to be reported; for example:
<dx-codeblock>
:::  js
const aegis = new Aegis({
  id: 'pGUVFTCZyewxxxxx',
  beforeReport(log) {
    if (log.level === '4' && log.msg && log.msg.indexOf('An error that doesn't need to be reported') !== -1) {
      return false
    }
  }
});
throw new Error('An error that doesn't need to be reported'); // This error will not be reported
:::
</dx-codeblock>
In the above sample code, if the error content contains the `An error that doesn't need to be reported` keywords, it won't be reported to the RUM backend.

## onReport

This hook is executed after a log is successfully reported, and its usage is similar to that of `beforeReport`. Their only difference is that all parameters received by this hook are of an already reported log, but the parameters received by `beforeReport` are of a log to be reported.

## beforeReportSpeed

1. This hook will be executed before the speed test data is reported; for example:
<dx-codeblock>
:::  js
const aegis = new Aegis({
  id: 'pGUVFTCZyewxxxxx',
  reportApiSpeed: true,
  reportAssetSpeed: true,
  beforeReportSpeed(msg) {
    console.log(msg); // {url: "https://localhost:3001/example.e31bb0bc.js", method: "get", duration: 7.4, status: 200, type: "static"}
    return msg
  }
});
:::
</dx-codeblock>
<dx-alert infotype="explain" title="">
The above `msg` will have the following fields:  
1. `url`: request address of this resource.  
2. `type`: resource type. Valid values: `fetch`: Aegis will report the resource as an API request; `static`: Aegis will report the resource as a static resource.  
3. `duration`: resource request duration.  
4. `method`: `http method` used when the resource is requested.  
5. `status`: status code returned by the server.  
</dx-alert>
In the above sample code, every time after Aegis collects the loading details of a resource, it will use such details (i.e., <code>msg</code> returned above) as parameters to call the <code>beforeReportSpeed</code> hook.  
2. If you have configured this hook, **the final content reported by Aegis is subject to the execution result of the hook**; for example:
<dx-codeblock>
:::  js
const aegis = new Aegis({
  id: 'pGUVFTCZyewxxxxx',
  reportApiSpeed: true,
  reportAssetSpeed: true,
  beforeReportSpeed(msg) {
    msg.type = 'static';
  }
});
:::
</dx-codeblock>
In the above sample code, all <code>msg.type</code> parameters are set to <code>static</code>, indicating that all resources, even API requests, will be reported as static resources.  
3. You can use this hook to correct the Aegis type and judge incorrect requests.  
#### Sample
You have an API `https://example.com/api` whose response header `Content-Type` is `text/html`. In normal case, RUM will report this API as a static resource; however, it must be reported as an API request in your business. Then, you can configure Aegis with following hook for correction:
<dx-codeblock>
:::  js
const aegis = new Aegis({
  id: 'pGUVFTCZyewxxxxx',
  reportApiSpeed: true,
  reportAssetSpeed: true,
  beforeReportSpeed(msg) {
    if (msg.url === 'https://example.com/api') {
      msg.type = 'fetch';
    }
  }
});
:::
</dx-codeblock>
4. You can also block the speed test data reporting of a resource as follows:
<dx-codeblock>
:::  js
const aegis = new Aegis({
  id: 'pGUVFTCZyewxxxxx',
  reportApiSpeed: true,
  reportAssetSpeed: true,
  beforeReportSpeed(msg) {
    // Speed test logs for resources whose address contains `https://example.com/api` will not be reported
    if (msg.url.indexOf('https://example.com/api') !== -1) {
      // If `false` is returned, the reporting of the speed test log will be blocked
      return false
    }
  }
});
:::
</dx-codeblock>

## beforeRequest

This hook will be executed before log reporting; for example:
<dx-alert infotype="notice" title="">
The SDK version must be 1.24.44 or above.
</dx-alert>
<dx-codeblock>
:::  js
const aegis = new Aegis({
  id: 'pGUVFTCZyewxxxxx',
  beforeRequest: function(msg) {
    if (msg.logs && msg.logs.level === '4' && msg.logs.msg && msg.logs.msg.indexOf('An error that doesn't need to be reported') !== -1) {
      return false
    }
    return msg;
  }
});
:::
</dx-codeblock>

Here, `msg` will have the following fields:

1. logType: log type. Valid values:
 - custom: custom speed test.
 - event: custom event.
 - log: log.
 - performance: page speed test.
 - pv: PV.
 - speed: API and static resource speed test.
 - vitals: Web Vitals.
2. logs: reported log content:
 - If `logType` is `'custom'`, `logs` will be in the format of `{name: "white screen time", duration: 3015.7000000178814, ext1: '', ext2: '', ext3: ''}`.
 - If `logType` is `'event'`, `logs` will be in the format of `{name: "ios", ext1: "", ext2: "", ext3: ""}`.
 - If `logType` is `'performance'`, `logs` will be in the format of `{contentDownload: 2, dnsLookup: 0, domParse: 501, firstScreenTiming: 2315, resourceDownload: 260, ssl: 4, tcp: 4, ttfb: 5}`.
 - If `logType` is `'speed'`, `logs` will be in the format of `{connectTime: 0, domainLookup: 0, duration: 508.2, isHttps: true, method: "get", status: 200, type: "tatic", url: "https://xxxxxx", urlQuery: "max_age=1296000"}`.
 - If `logType` is `'vitals'`, `logs` will be in the format of `{delta: 1100, entries: [PerformancePaintTiming], id: "v1-1629344653118-4916457684758", name: "CP", value: 1100}`.
 - If `logType` is `'log'`, `logs` will be in the format of `{msg: "log details", level: '4', ext1: '', ext2: '', ext3: '', trace: ''}`.
<dx-alert infotype="explain" title="">
Valid values of `level`:

- `{ level: '1', name: 'API request log (allowed log)' }`,
- `{ level: '2', name: 'General log' }`,
- `{ level: '4', name: 'JavaScript execution error' }`,
- `{ level: '8', name: 'Promise error' }`,
- `{ level: '16', name: 'Ajax request exception' }`,
- `{ level: '32', name: 'JavaScript loading exception' }`,
- `{ level: '64', name: 'Image loading exception' }`,
- `{ level: '128', name: 'CSS loading exception' }`,
- `{ level: '256', name: 'console.error (reserved)' }`,
- `{ level: '512', name: 'Audio/Video resource exception' }`,
- `{ level: '1024', name: 'retcode exception' }`,
- `{ level: '2048', name: 'aegis report' `}


If this hook returns `false`, the log won't be reported. This feature can be used to filter out errors and logs that don't need to be reported.
</dx-alert>

## afterRequest

This hook will be executed after speed test data reporting; for example:

<dx-alert infotype="notice" title="">
The SDK version must be 1.24.44 or above.
</dx-alert>


<dx-codeblock>
:::  js
const aegis = new Aegis({
  id: "pGUVFTCZyewxxxxx",
  afterRequest: function(msg) {
    // {isErr: false, result: Array(1), logType: "log", logs: Array(4)}
    console.log(msg);
  }
});
:::
</dx-codeblock>

Here, `msg` will have the following fields:
1. isErr: whether the request reporting API has an error.
2. result: response of the reporting API.
3. logs: reported log content.
4. logType: log type, which is the same as `logType` in `beforeRequest`.
