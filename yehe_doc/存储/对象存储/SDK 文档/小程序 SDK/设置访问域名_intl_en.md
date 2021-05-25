## Overview

This document describes how to request a COS service using a non-default COS endpoint.

### Parameter description

You can use initialization parameters to configure the request domain name. Parameters involved are described as follows. For more initialization parameters, please see **Configuration items** in [Getting Started](https://intl.cloud.tencent.com/document/product/436/30609).

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Domain | The custom request domain name used to call a bucket or object API. You can use a template, such as `"{Bucket}.cos.{Region}.myqcloud.com"` which will use the bucket and region passed in the replacement parameters when an API is called. | String | No |
| Protocol | The protocol used when the request is made. Valid values: `https:`, `http:`. By default, `http:` is used when the current page is determined to be in `http:` format; otherwise, `https:` is used | String | No |

### Default CDN acceleration domain name

For more information, see [Enabling Default CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31505).

The sample code below shows how to access a COS service using a default CDN acceleration domain name.

```javascript
var cos = new COS({
    Domain: '{Bucket}.file.myqcloud.com', // Custom acceleration domain name (supports using a template). In this sample, the value of {Bucket} will be replaced by the value passed in the request.
    Protocol: 'https:', // Request protocol, which can be 'https:' or 'http:'
});
```

### Custom CDN Acceleration Domain Name

For more information, see [Enabling Custom CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31506).

The sample code below shows how to access a COS service using a custom CDN acceleration domain name.

```js
var cos = new COS({
    Domain: 'example-cdn-domain.com', // Custom acceleration domain name
    Protocol: 'https:', // Request protocol, which can be 'https:' or 'http:'
});
```

### Custom origin server domain name

For more information, see [Enabling Custom Origin Domain](https://intl.cloud.tencent.com/document/product/436/31507).

The sample code below shows how to access a COS service using a custom origin server domain name.

```js
var cos = new COS({
    Domain: 'example-cos-domain.com', // Custom origin server domain
    Protocol: 'https:', // Request protocol, which can be 'https:' or 'http:'
});
```

### Global acceleration endpoint

For more information on global acceleration, see [Overview](https://intl.cloud.tencent.com/document/product/436/33409).

The sample code below shows how to access a COS service using a global acceleration endpoint.

```js
var cos = new COS({
    UseAccelerate: true, // Set this parameter to “true” to use a global acceleration domain.
    Protocol: 'https:', // Request protocol, which can be 'https:' or 'http:'
});
```
