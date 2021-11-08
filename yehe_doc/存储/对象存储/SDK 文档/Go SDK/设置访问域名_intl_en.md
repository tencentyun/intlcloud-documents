## Overview

This document describes how to use a non-default domain to request COS.

### Setting the default COS domain

#### Sample request
```go
// Replace examplebucket-1250000000 and COS_REGION with the actual information.
u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
// The following calls the `Get Service` API. By default, all regions (service.cos.myqcloud.com) will be queried.
su, _ := url.Parse("https://cos.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: u, ServiceURL: su}
// 1. Permanent key
client := cos.NewClient(b, &http.Client{
   Transport: &cos.AuthorizationTransport{
       SecretID:  "SECRETID",
       SecretKey: "SECRETKEY",
   },
})
```

### Default CDN acceleration domain name

#### Description

After enabling a default CDN acceleration domain name for a bucket through the COS console, you can set the domain name in the SDK code for acceleration.
For more information, please see [Enabling Default CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31505).

#### Sample request

```go
// Replace examplebucket-1250000000 with the actual information.
u, _ := url.Parse("https://examplebucket-1250000000.file.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
// Use a CDN acceleration domain. COS verification information does not need to be sent.
client := cos.NewClient(b, &http.Client{})
```

### Custom CDN acceleration domain name

#### Description

After setting a custom CDN acceleration domain name for a bucket through the COS console, you can set the domain name in the SDK code to implement acceleration for the custom domain. For more information, please see [Enabling Custom Accelerated Domain Name](https://intl.cloud.tencent.com/document/product/436/31506).

#### Sample request

```go
// Set the custom CDN acceleration domain.
u, _ := url.Parse("https://xxx.xxx.com")
b := &cos.BaseURL{BucketURL: u}
// Use a CDN acceleration domain. COS verification information does not need to be sent.
client := cos.NewClient(b, &http.Client{})
```

### Custom origin server domain name

#### Sample request

```go
// Custom origin server domain
u, _ := url.Parse("https://xxx.xxx.com")
b := &cos.BaseURL{BucketURL: u}
client := cos.NewClient(b, &http.Client{
   Transport: &cos.AuthorizationTransport{
       SecretID:  "SECRETID",
       SecretKey: "SECRETKEY",
   },
})
```

### Global acceleration endpoint

#### Sample request

```go
// Global acceleration domain
// Replace examplebucket-1250000000 with the actual information.
u, _ := url.Parse("https://examplebucket-1250000000.cos.accelerate.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
client := cos.NewClient(b, &http.Client{
   Transport: &cos.AuthorizationTransport{
       SecretID:  "SECRETID",
       SecretKey: "SECRETKEY",
   },
})
```
