

## 简介

本文档提供关于日志管理的 API 概览以及 C SDK 示例代码。

| API                                                          | 操作名       | 操作描述                   |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | 设置日志管理 | 为源存储桶开启日志记录     |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | 查询日志管理 | 查询源存储桶的日志配置信息 |

## 设置日志管理

#### 功能说明

PUT Bucket logging 用于为源存储桶开启日志记录，将源存储桶的访问日志保存到指定的目标存储桶中。

#### 方法原型

```C
cos_status_t *cos_put_bucket_logging(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_logging_params_t *logging_params,
                                      cos_table_t **resp_headers);
```

#### 请求示例

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// endpoint 是 COS 访问域名信息，详情请参见 https://intl.cloud.tencent.com/document/product/436/6224 文档
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// 开发者拥有的项目身份ID/密钥，可在 https://console.cloud.tencent.com/cam/capi 页面获取
static char *TEST_ACCESS_KEY_ID;                //your secret_id
static char *TEST_ACCESS_KEY_SECRET;            //your secret_key
// 开发者访问 COS 服务时拥有的用户维度唯一资源标识，用以标识资源，可在 https://console.cloud.tencent.com/cam/capi 页面获取
static char TEST_APPID[] = "<APPID>";    //your appid
//the cos bucket name, syntax: [bucket]-[appid], for example: mybucket-1253666666，可在 https://console.cloud.tencent.com/cos5/bucket 查看
static char TEST_BUCKET_NAME[] = "<bucketname-appid>"; 

void log_status(cos_status_t *s)
{
    cos_warn_log("status->code: %d", s->code);
    if (s->error_code) cos_warn_log("status->error_code: %s", s->error_code);
    if (s->error_msg) cos_warn_log("status->error_msg: %s", s->error_msg);
    if (s->req_id) cos_warn_log("status->req_id: %s", s->req_id);
}

void init_test_config(cos_config_t *config, int is_cname)
{
    cos_str_set(&config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&config->appid, TEST_APPID);
    config->is_cname = is_cname;
}

void init_test_request_options(cos_request_options_t *options, int is_cname)
{
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    options->ctl = cos_http_controller_create(options->pool, 0);
}

void test_put_logging()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_logging_params_t  *params = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;

    //创建内存池
    cos_pool_create(&pool, NULL);

    //初始化请求选项
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //创建logging参数
    params = cos_create_logging_params(options->pool);
    cos_str_set(&params->target_bucket, TEST_BUCKET_NAME);
    cos_str_set(&params->target_prefix, "logging/");

    status = cos_put_bucket_logging(options, &bucket, params, &resp_headers);
    log_status(status);

    cos_pool_destroy(pool);
}

int main(int argc, char *argv[])
{
    // 通过环境变量获取 SECRETID 和 SECRETKEY
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    //set log level, default COS_LOG_WARN
    cos_log_set_level(COS_LOG_WARN);

    //set log output, default stderr
    cos_log_set_output(NULL);

    test_put_logging();

    cos_http_io_deinitialize();

    return 0;
}
```

#### 参数说明

| 参数名称       | 描述                                                         | 类型   |
| -------------- | ------------------------------------------------------------ | ------ |
| options        | COS 请求选项                                                 | Struct |
| bucket         | 开启日志功能的源存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| logging_params | 存储桶日志配置信息                                           | Struct |
| target_bucket  | 存放日志的目标存储桶，可以是同一个存储桶（但不推荐），或同一账户下、同一地域的存储桶 | String |
| target_prefix  | 日志存放在目标存储桶的指定路径                               | String |
| resp_headers   | 返回 HTTP 响应消息的头域                                     | Struct |

#### 返回结果说明

| 返回结果   | 描述        | 类型   |
| :--------- | :---------- | :----- |
| code       | 错误码      | Int    |
| error_code | 错误码内容  | String |
| error_msg  | 错误码描述  | String |
| req_id     | 请求消息 ID | String |

## 查询日志管理

#### 功能说明

GET Bucket logging 用于查询指定存储桶的日志配置信息。

#### 方法原型

```c
cos_status_t *cos_get_bucket_logging(const cos_request_options_t *options,  
                                      const cos_string_t *bucket,    
                                      cos_logging_params_t *logging_params,
                                      cos_table_t **resp_headers);
```

#### 请求示例

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// endpoint 是 COS 访问域名信息，详情请参见 https://intl.cloud.tencent.com/document/product/436/6224 文档
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// 开发者拥有的项目身份ID/密钥，可在 https://console.cloud.tencent.com/cam/capi 页面获取
static char *TEST_ACCESS_KEY_ID;                //your secret_id
static char *TEST_ACCESS_KEY_SECRET;            //your secret_key
// 开发者访问 COS 服务时拥有的用户维度唯一资源标识，用以标识资源，可在 https://console.cloud.tencent.com/cam/capi 页面获取
static char TEST_APPID[] = "<APPID>";    //your appid
//the cos bucket name, syntax: [bucket]-[appid], for example: mybucket-1253666666，可在 https://console.cloud.tencent.com/cos5/bucket 查看
static char TEST_BUCKET_NAME[] = "<bucketname-appid>"; 

void log_status(cos_status_t *s)
{
    cos_warn_log("status->code: %d", s->code);
    if (s->error_code) cos_warn_log("status->error_code: %s", s->error_code);
    if (s->error_msg) cos_warn_log("status->error_msg: %s", s->error_msg);
    if (s->req_id) cos_warn_log("status->req_id: %s", s->req_id);
}

void init_test_config(cos_config_t *config, int is_cname)
{
    cos_str_set(&config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&config->appid, TEST_APPID);
    config->is_cname = is_cname;
}

void init_test_request_options(cos_request_options_t *options, int is_cname)
{
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    options->ctl = cos_http_controller_create(options->pool, 0);
}

void test_get_logging()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_logging_params_t  *result = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;

    //创建内存池
    cos_pool_create(&pool, NULL);

    //初始化请求选项
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    result = cos_create_logging_params(options->pool);
    status = cos_get_bucket_logging(options, &bucket, result, &resp_headers);
    log_status(status);
    if (!cos_status_is_ok(status)) {
        cos_pool_destroy(pool);
        return;
    }

    //查看结果
    char *line = NULL;
    line = apr_psprintf(options->pool, "%.*s\n", result->target_bucket.len, result->target_bucket.data);
    printf("target bucket: %s", line);
    line = apr_psprintf(options->pool, "%.*s\n", result->target_prefix.len, result->target_prefix.data);
    printf("target prefix: %s", line);

    cos_pool_destroy(pool);
}

int main(int argc, char *argv[])
{
    // 通过环境变量获取 SECRETID 和 SECRETKEY
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    //set log level, default COS_LOG_WARN
    cos_log_set_level(COS_LOG_WARN);

    //set log output, default stderr
    cos_log_set_output(NULL);

    test_get_logging();

    cos_http_io_deinitialize();

    return 0;
}
```

#### 参数说明

| 参数名称       | 描述                                                         | 类型   |
| -------------- | ------------------------------------------------------------ | ------ |
| options        | COS 请求选项                                                 | Struct |
| bucket         | 存放日志的目标存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| logging_params | 存储桶日志配置信息                                           | Struct |
| target_bucket  | 存放日志的目标存储桶，可以是同一个存储桶（但不推荐），或同一账户下、同一地域的存储桶 | String |
| target_prefix  | 日志存放在目标存储桶的指定路径                               | String |
| resp_headers   | 返回 HTTP 响应消息的头域                                     | Struct |

#### 返回结果说明

| 返回结果   | 描述        | 类型   |
| :--------- | :---------- | :----- |
| code       | 错误码      | Int    |
| error_code | 错误码内容  | String |
| error_msg  | 错误码描述  | String |
| req_id     | 请求消息 ID | String |
