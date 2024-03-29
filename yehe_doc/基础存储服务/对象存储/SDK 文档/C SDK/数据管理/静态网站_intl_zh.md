

## 简介

本文档提供关于静态网站的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名           | 操作描述                 |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | 设置静态网站     | 设置存储桶的静态网站配置 |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | 查询静态网站配置 | 查询存储桶的静态网站配置 |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | 删除静态网站配置 | 删除存储桶的静态网站配置 |

## 设置静态网站

#### 功能说明

PUT Bucket website 用于为存储桶配置静态网站。

#### 方法原型

```c
cos_status_t *cos_put_bucket_website(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_website_params_t *website_params,
                                      cos_table_t **resp_header);
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

void test_put_website()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_website_params_t  *website_params = NULL;
    cos_website_rule_content_t *website_content = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;

    //创建内存池
    cos_pool_create(&pool, NULL);

    //初始化请求选项
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //创建website参数
    website_params = cos_create_website_params(options->pool);
    cos_str_set(&website_params->index, "index.html");
    cos_str_set(&website_params->redirect_protocol, "https");
    cos_str_set(&website_params->error_document, "Error.html");

    website_content = cos_create_website_rule_content(options->pool);
    cos_str_set(&website_content->condition_errcode, "404");
    cos_str_set(&website_content->redirect_protocol, "https");
    cos_str_set(&website_content->redirect_replace_key, "404.html");
    cos_list_add_tail(&website_content->node, &website_params->rule_list);

    website_content = cos_create_website_rule_content(options->pool);
    cos_str_set(&website_content->condition_prefix, "docs/");
    cos_str_set(&website_content->redirect_protocol, "https");
    cos_str_set(&website_content->redirect_replace_key_prefix, "documents/");
    cos_list_add_tail(&website_content->node, &website_params->rule_list);

    website_content = cos_create_website_rule_content(options->pool);
    cos_str_set(&website_content->condition_prefix, "img/");
    cos_str_set(&website_content->redirect_protocol, "https");
    cos_str_set(&website_content->redirect_replace_key, "demo.jpg");
    cos_list_add_tail(&website_content->node, &website_params->rule_list);

    status = cos_put_bucket_website(options, &bucket, website_params, &resp_headers);
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

    test_put_website();

    cos_http_io_deinitialize();

    return 0;
}
```

#### 参数说明

| 参数名称                    | 描述                                                         | 类型   |
| --------------------------- | ------------------------------------------------------------ | ------ |
| options                     | COS 请求选项                                                 | Struct |
| bucket                      | 设置静态网站的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| website_params              | 存储桶静态网站配置信息                                       | Struct |
| index                       | 指定索引文档                                                 | String |
| redirect_protocol           | 指定全站重定向的协议，只能设置为 https                       | String |
| error_document              | 指定通用错误返回                                             | String |
| rule_list                   | 设置重定向规则，最多设置100条 RoutingRule                    | list   |
| condition_errcode           | 指定重定向错误码，只支持配置4XX返回码，优先级高于 error_document | String |
| condition_prefix            | 指定前缀重定向的路径，替换指定的 folder/                     | String |
| redirect_protocol           | 指定重定向规定的协议，只能设置为 https                       | String |
| redirect_replace_key        | 替换整个 Key 为指定的内容                                    | String |
| redirect_replace_key_prefix | 替换匹配到的前缀为指定的内容，Conditon 为 KeyPrefixEquals 才可设置 | String |
| resp_headers                | 返回 HTTP 响应消息的头域                                     | Struct |

#### 返回结果说明

| 返回结果   | 描述        | 类型   |
| :--------- | :---------- | :----- |
| code       | 错误码      | Int    |
| error_code | 错误码内容  | String |
| error_msg  | 错误码描述  | String |
| req_id     | 请求消息 ID | String |

## 查询静态网站配置

#### 功能说明

GET Bucket website 用于查询与存储桶关联的静态网站配置信息。

#### 方法原型

```c
cos_status_t *cos_get_bucket_website(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_website_params_t *website_params,
                                      cos_table_t **resp_header);
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

void test_get_website()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_website_params_t  *website_result = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;

    //创建内存池
    cos_pool_create(&pool, NULL);

    //初始化请求选项
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    website_result = cos_create_website_params(options->pool);
    status = cos_get_bucket_website(options, &bucket, website_result, &resp_headers);
    log_status(status);
    if (!cos_status_is_ok(status)) {
        cos_pool_destroy(pool);
        return;
    }

    //查看结果
    cos_website_rule_content_t *content = NULL;
    char *line = NULL;
    line = apr_psprintf(options->pool, "%.*s\n", website_result->index.len, website_result->index.data);
    printf("index: %s", line);
    line = apr_psprintf(options->pool, "%.*s\n", website_result->redirect_protocol.len, website_result->redirect_protocol.data);
    printf("redirect protocol: %s", line);
    line = apr_psprintf(options->pool, "%.*s\n", website_result->error_document.len, website_result->error_document.data);
    printf("error document: %s", line);
    cos_list_for_each_entry(cos_website_rule_content_t, content, &website_result->rule_list, node) {
        line = apr_psprintf(options->pool, "%.*s\t%.*s\t%.*s\t%.*s\t%.*s\n", content->condition_errcode.len, content->condition_errcode.data, content->condition_prefix.len, content->condition_prefix.data, content->redirect_protocol.len, content->redirect_protocol.data, content->redirect_replace_key.len, content->redirect_replace_key.data, content->redirect_replace_key_prefix.len, content->redirect_replace_key_prefix.data);
        printf("%s", line);
    }

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

    test_get_website();

    cos_http_io_deinitialize();

    return 0;
}
```

#### 参数说明

| 参数名称                    | 描述                                                         | 类型   |
| --------------------------- | ------------------------------------------------------------ | ------ |
| options                     | COS 请求选项                                                 | Struct |
| bucket                      | 查询静态网站配置的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| website_params              | 存储桶静态网站配置信息                                       | Struct |
| index                       | 指定索引文档                                                 | String |
| redirect_protocol           | 指定全站重定向的协议，只能设置为 https                       | String |
| error_document              | 指定通用错误返回                                             | String |
| rule_list                   | 设置重定向规则，最多设置100条 RoutingRule                    | list   |
| condition_errcode           | 指定重定向错误码，只支持配置4XX返回码，优先级高于 error_document | String |
| condition_prefix            | 指定前缀重定向的路径，替换指定的 folder/                     | String |
| redirect_protocol           | 指定重定向规定的协议，只能设置为 https                       | String |
| redirect_replace_key        | 替换整个 Key 为指定的内容                                    | String |
| redirect_replace_key_prefix | 替换匹配到的前缀为指定的内容，Conditon 为 KeyPrefixEquals 才可设置 | String |
| resp_headers                | 返回 HTTP 响应消息的头域                                     | Struct |

#### 返回结果说明

| 返回结果   | 描述        | 类型   |
| :--------- | :---------- | :----- |
| code       | 错误码      | Int    |
| error_code | 错误码内容  | String |
| error_msg  | 错误码描述  | String |
| req_id     | 请求消息 ID | String |

## 删除静态网站配置

#### 功能说明

DELETE Bucket website 用于删除存储桶中的静态网站配置。

#### 方法原型

```c
cos_status_t *cos_delete_bucket_website(const cos_request_options_t *options,
                                          const cos_string_t *bucket,
                                          cos_table_t **resp_header);
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

void test_delete_website()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;

    //创建内存池
    cos_pool_create(&pool, NULL);

    //初始化请求选项
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    status = cos_delete_bucket_website(options, &bucket, &resp_headers);
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

    test_delete_website();

    cos_http_io_deinitialize();

    return 0;
}
```

#### 参数说明

| 参数名称     | 描述                                                         | 类型   |
| ------------ | ------------------------------------------------------------ | ------ |
| options      | COS 请求选项                                                 | Struct |
| bucket       | 被删除静态网站配置的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| resp_headers | 返回 HTTP 响应消息的头域                                     | Struct |

#### 返回结果说明

| 返回结果   | 描述        | 类型   |
| :--------- | :---------- | :----- |
| code       | 错误码      | Int    |
| error_code | 错误码内容  | String |
| error_msg  | 错误码描述  | String |
| req_id     | 请求消息 ID | String |
