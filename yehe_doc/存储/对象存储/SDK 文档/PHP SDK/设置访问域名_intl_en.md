## Overview

This document describes how to use a non-default domain to request COS.

## Parameter Description

You can use the initialization parameters below to control the request domain:

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Domain | The custom request domain name used to call a bucket or object API. You can use a template, such as `"{$Bucket}.cos.{$Region}.myqcloud.com"` which will use the bucket and region passed in the replacement parameters when an API is called. | String | No |
| Protocol | The protocol used when the request is made. Valid values: `https:`, `http:`. By default, `http:` is used when the current page is determined to be in `http:` format; otherwise, `https:` is used | String | No |

## Default CDN Acceleration Domain Name

For more information, see [Enabling Default CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31505).

The sample code below shows how to access a COS service using a default CDN acceleration domain name.

```php
$bucket = "examplebucket-1250000000";

$cosClient = new Qcloud\Cos\Client(
    array(
        'domain' => $bucket . '.file.myqcloud.com', // Default acceleration domain name
        'schema' => 'https', // Protocol, http by default
        'credentials'=> array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey
        )
    )
);
```

## Custom CDN Acceleration Domain Name

For more information, see [Enabling Custom CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31506).

The sample code below shows how to access a COS service using a custom CDN acceleration domain name.

```php
$cosClient = new Qcloud\Cos\Client(
    array(
        'domain' => 'example-cdn-domain.com', // Default acceleration domain name
        'schema' => 'https', // Protocol, http by default
        'credentials'=> array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey
        )
    )
);
```

## Custom Origin Server Domain Name

For more information, see [Enabling Custom Origin Domain](https://intl.cloud.tencent.com/document/product/436/31507).

The sample code below shows how to access a COS service using a custom origin server domain name.

```php
$cosClient = new Qcloud\Cos\Client(
    array(
        'domain' => 'example-cos-domain.com', // Default acceleration domain name
        'schema' => 'https', // Protocol, http by default
        'credentials'=> array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey
        )
    )
);
```

## Global Acceleration Domain Name

For more information on global acceleration, see [Overview](https://intl.cloud.tencent.com/document/product/436/33409).

The sample code below shows how to access a COS service using a global acceleration endpoint.

```php
// Change {$bucket}.cos.{$region}.myqcloud.com/key to the one below:
//{$bucket}.cos.accelerate.myqcloud.com/key
$cosClient = new Qcloud\Cos\Client(
    array(
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey
        ),
        'allow_accelerate' => true // Set this parameter to “true” to use a global acceleration domain.
    )
);
```
