## Overview

This document describes how to use a non-default domain to request COS.

### Default CDN acceleration domain name

#### Description

After enabling a default CDN acceleration domain name for a bucket through the COS console, you can set the domain name in the SDK code for acceleration.
For more information, please see [Enabling Default CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31505).


#### Sample request

```cpp
cos_pool_t *p = NULL;
cos_request_options_t *options = NULL;
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
// The request domain format is <bucketname-appid>.file.myqcloud.com.
cos_str_set(&options->config->endpoint, "<bucketname-appid>.file.myqcloud.com");
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ---------------------------- | -------------- |
| endpoint     | Set the domain suffix to use the CDN acceleration domain name | String         |



### Custom CDN acceleration domain name

#### Description

After setting a custom CDN acceleration domain name for a bucket through the COS console, you can set the domain name in the SDK code to implement acceleration for the custom domain. For more information, please see [Enabling Custom Accelerated Domain Name](https://intl.cloud.tencent.com/document/product/436/31506).

#### Sample request

```cpp
cos_pool_t *p = NULL;
cos_request_options_t *options = NULL;
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
// Set the requested endpoint to `your.domain.com`
cos_str_set(&options->config->endpoint, "your.domain.com"); // Custom CDN domain
// Set `is_cname` to `1`
options->config->is_cname = 1;
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ---------------------------- | -------------- |
| endpoint     | Set the domain suffix to use a custom CDN endpoint  | String         |
| is_cname           | Set this parameter to `1` to use the custom CDN endpoint mode | Int         |



### Custom origin server domain name

#### Description

After setting a custom origin server domain for a bucket through the COS console, you can set the domain in the SDK code to access COS resources. For more information, please see [Enabling Custom Endpoints](https://intl.cloud.tencent.com/document/product/436/31507).

#### Sample code

```cpp
cos_pool_t *p = NULL;
cos_request_options_t *options = NULL;
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
// Set the requested endpoint to `your.domain.com`
cos_str_set(&options->config->endpoint, "your.domain.com"); // Custom endpoint
// Set `is_cname` to `1`
options->config->is_cname = 1;
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ---------------------------- | -------------- |
| endpoint     | Set the domain suffix to use a custom origin server endpoint  | String         |
| is_cname           | Set this parameter to `1` to use the custom origin server endpoint mode | Int         |


### Global acceleration endpoint

#### Description

After enabling a global acceleration endpoint for a bucket through the COS console, you can set the domain name in the SDK code for global acceleration. For more information, please see [Global Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/33409).

#### Sample code

```cpp
cos_pool_t *p = NULL;
cos_request_options_t *options = NULL;
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
// Set the requested endpoint to `cos.accelerate.myqcloud.com`
cos_str_set(&options->config->endpoint, "cos.accelerate.myqcloud.com");
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ---------------------------- | -------------- |
| endpoint     | Set the domain suffix to use a global acceleration endpoint | String         |
