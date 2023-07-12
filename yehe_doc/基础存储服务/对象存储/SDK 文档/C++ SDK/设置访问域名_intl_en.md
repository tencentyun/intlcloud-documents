## Overview

This document describes how to use a non-default domain to request COS.

### Default CDN acceleration domain name

#### Description

To use a default CDN acceleration endpoint to access COS, you need to enable the default CDN acceleration endpoint feature for your bucket in the COS console. For operation details, see [Enabling Default CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31505).

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
// Replace `examplebucket-1250000000` with your bucket name.
CosSysConfig::SetDomainSameToHost(true);
CosSysConfig::SetDestDomain("examplebucket-1250000000.file.myqcloud.com");
```

Or you can modify `config.json` as follows:

```
"IsDomainSameToHost":true,
"DestDomain":"examplebucket-1250000000.file.myqcloud.com",
```

### Custom CDN acceleration domain name

#### Description

To use a custom CDN acceleration domain name to access COS, you need to enable the custom CDN acceleration domain name feature for your bucket in the COS console. For operation details, see [Enabling Custom CDN Accelerated Domain Name](https://intl.cloud.tencent.com/document/product/436/31506).

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
// Replace `mycdndomain.com` with your CDN domain name.
CosSysConfig::SetDomainSameToHost(true);
CosSysConfig::SetDestDomain("mycdndomain.com");
```

Or you can modify `config.json` as follows:

```
"IsDomainSameToHost":true,
"DestDomain":"emycdndomain.com",
```

### Custom origin server domain name

#### Description

To use a custom origin server domain name to access COS, you need to enable the custom origin server domain name feature for your bucket in the COS console. For operation details, see [Enabling Custom Origin Server Domains](https://intl.cloud.tencent.com/document/product/436/31507).

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
// Replace `mydomain.com` with your custom domain name.
CosSysConfig::SetDomainSameToHost(true);
CosSysConfig::SetDestDomain("mydomain.com");
```

Or you can modify `config.json` as follows:

```
"IsDomainSameToHost":true,
"DestDomain":"mydomain.com",
```

#### Global Acceleration Domain Name

#### Description

To use a global acceleration domain name to access COS, you need to enable the global acceleration domain name feature for your bucket in the COS console. For operation details, see [Enabling Global Acceleration](https://intl.cloud.tencent.com/document/product/436/33406).

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
config.SetRegion("accelerate")
qcloud_cos::CosAPI cos(config);
```

Or you can modify `config.json` as follows:

```
"Region":"accelerate",   
```
