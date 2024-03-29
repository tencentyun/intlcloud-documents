## 简介

本文档提供关于如何使用非默认域名请求对象存储（Cloud Object Storage，COS）服务。

### 默认 CDN 加速域名

#### 功能说明

在 COS 控制台为存储桶开启默认 CDN 加速域名后，可在 SDK 代码中设置对应的域名，以便实现默认加速功能。
关于如何开启默认加速域名请参见 [开启默认 CDN 加速域名](https://intl.cloud.tencent.com/document/product/436/31505)。


#### 请求示例

```cpp
cos_pool_t *p = NULL;
cos_request_options_t *options = NULL;
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
//请求域名格式为 <bucketname-appid>.file.myqcloud.com
cos_str_set(&options->config->endpoint, "<bucketname-appid>.file.myqcloud.com");
```

#### 参数说明

| 参数名称            | 描述                          | 类型           |
| ------------------ | ---------------------------- | -------------- |
| endpoint           | 通过设置域名后缀，使用 CDN 加速域名 | String         |



### 自定义 CDN 加速域名

#### 功能说明

在 COS 控制台为存储桶设置自定义 CDN 加速域名后，可在 SDK 代码中设置对应的域名，以便实现自定义域名的加速功能。关于如何开启自定义 CDN 加速域名，请参见 [开启自定义 CDN 加速域名](https://intl.cloud.tencent.com/document/product/436/31506)。

#### 请求示例

```cpp
cos_pool_t *p = NULL;
cos_request_options_t *options = NULL;
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
//请求域名为 your.domain.com
cos_str_set(&options->config->endpoint, "your.domain.com"); //自定义CDN域名
// is_cname设置为1
options->config->is_cname = 1；
```

#### 参数说明

| 参数名称            | 描述                          | 类型           |
| ------------------ | ---------------------------- | -------------- |
| endpoint           | 通过设置域名后缀，使用自定义 CDN 域名 | String         |
| is_cname           | 设置为1，设置为自定义 CDN 域名模式  | Int         |



### 自定义源站域名

#### 功能说明

在 COS 控制台为存储桶设置自定义源站域名后，可在 SDK 代码中设置对应的域名，以便实现访问 COS 资源。关于如何设置自定义源站域名请参见 [自定义源站域名](https://intl.cloud.tencent.com/document/product/436/31507)。

#### 示例代码

```cpp
cos_pool_t *p = NULL;
cos_request_options_t *options = NULL;
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
//请求域名为 your.domain.com
cos_str_set(&options->config->endpoint, "your.domain.com"); //自定义域名
// is_cname设置为1
options->config->is_cname = 1；
```

#### 参数说明

| 参数名称            | 描述                          | 类型           |
| ------------------ | ---------------------------- | -------------- |
| endpoint           | 通过设置域名后缀，使用自定义源站域名 | String         |
| is_cname           | 设置为1，设置为自定义源站域名模式 | Int         |


### 全球加速域名

#### 功能说明

在 COS 控制台为存储桶开启全球加速域名后，可在 SDK 代码中设置对应的域名，以便实现全球加速功能。关于全球加速的功能介绍，请参见 [全球加速功能概述](https://intl.cloud.tencent.com/document/product/436/33409)。

#### 示例代码

```cpp
cos_pool_t *p = NULL;
cos_request_options_t *options = NULL;
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
//请求域名为 cos.accelerate.myqcloud.com
cos_str_set(&options->config->endpoint, "cos.accelerate.myqcloud.com");
```

#### 参数说明

| 参数名称            | 描述                          | 类型           |
| ------------------ | ---------------------------- | -------------- |
| endpoint           | 通过设置域名后缀，使用全球加速域名 | String         |
