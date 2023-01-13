This document describes how to report the data of a Node.js application with the native Jaeger SDK.

## Directions

### Step 1. Get the endpoint and token

Log in to the [APM console](https://console.cloud.tencent.com/apm), enter the **Application monitoring** > **Application list** page, click **Access application**, and select the Node.js language and Jaeger data collection method. Then, get the endpoint and token in the step of access method selection.           

![](https://staticintl.cloudcachetci.com/yehe/backend-news/5rBD100_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A120230112-120043%402x.png)

### Step 2. Install dependencies
Install dependencies by using npm.
```
$ npm i jaeger-client
```

### Step 3. Import the SDK and report data
1. Import the SDK. Below is a sample:
```
const initTracer = require('jaeger-client').initTracer;

// Jaeger configuration
const config = {
    serviceName: 'service-name', // Customizable service name
    sampler: {
        type: 'const',
        param: 1,
    },
    reporter: {
        logSpans: true,
        collectorEndpoint: 'http://ap-guangzhou.apm.tencentcs.com:14268/api/traces', // Actual endpoint, which is the endpoint obtained in the APM console + `api/traces`.
    },
};

const options = {
    tags: {
        token: 'Vds************CrKck' // The requested token
    },
};
```

>? Node.js uses API to directly report data, so there is no need to start the Jaeger agent. Select the endpoint of your network environment and add the suffix `/api/traces` to form the actual endpoint.

2. Report data. Below is a sample:
```
// Initialize the tracer instance object
const tracer = initTracer(config, options);

// Initialize the span instance object
const span = tracer.startSpan('spanStart');

// Mark the current service as the server
span.setTag('span.kind', 'server');

// Set one or more tags (optional)
span.setTag('tagName', 'tagValue');

// Set one or more events (optional)
span.log({ event: 'timestamp', value: Date.now() });

// Mark the end of the span
span.finish();
```
