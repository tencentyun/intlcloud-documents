

## Overview

This document provides an overview of APIs and SDK code samples related to static website.

| API | Operation | Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website configuration | Configures a static website for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying a static website configuration | Queries the static website configuration of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting a static website configuration | Deletes the static website configuration of a bucket |

## Setting Static Website Configuration

#### Description

This API is used to configure a static website for a bucket.

#### Method prototype

```c
cos_status_t *cos_put_bucket_website(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_website_params_t *website_params,
                                      cos_table_t **resp_header);
```

#### Sample request

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
// COS bucket name, in the format of [bucket]-[appid], for example `mybucket-1253666666`. It can be obtained at https://console.cloud.tencent.com/cos5/bucket.
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

    // Create a memory pool
    cos_pool_create(&pool, NULL);

    // Initialize the request options
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Set website parameters
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
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_put_website();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| --------------------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct  |
| bucket                      | Bucket for which a static website is configured, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| website_params              | Static website parameters of the bucket                                       | Struct |
| index                    | Index document                                                 | String |
| redirect_protocol                    | Site-wide redirect protocol. Only HTTPS is supported.                       | String   |
| error_document              | Common error response                                             | String |
| rule_list                   | Multiple redirect rules. Up to 100 redirect rules can be set.                    | list   |
| condition_errcode       | Redirect error code. Only 4xx status codes are supported. This has a higher priority than `error_document`.   | String |
| condition_prefix          | Redirect path prefix to replace with the specified "folder/" for the redirect.                     | String |
| redirect_protocol         | Redirect protocol. Only HTTPS is supported.                       | String |
| redirect_replace_key       | Content that is used to replace the entire key.                                    | String |
| redirect_replace_key_prefix | Content that is used to replace the key prefix. The replacement is allowed only when `Condition` is `KeyPrefixEquals`. | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

## Querying Static Website Configuration

#### Description

This API is used to query the static website configuration associated with a bucket.

#### Method prototype

```c
cos_status_t *cos_get_bucket_website(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_website_params_t *website_params,
                                      cos_table_t **resp_header);
```

#### Sample request

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
// COS bucket name, in the format of [bucket]-[appid], for example `mybucket-1253666666`. It can be obtained at https://console.cloud.tencent.com/cos5/bucket.
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

    // Create a memory pool
    cos_pool_create(&pool, NULL);

    // Initialize the request options
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

    // View results
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
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_get_website();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| --------------------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct  |
| bucket | Bucket for which static website configuration is queried, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| website_params              | Static website parameters of the bucket                                       | Struct |
| index                    | Index document                                                 | String |
| redirect_protocol                    | Site-wide redirect protocol. Only HTTPS is supported.                       | String   |
| error_document              | Common error response                                             | String |
| rule_list                   | Multiple redirect rules. Up to 100 redirect rules can be set.                    | list   |
| condition_errcode       | Redirect error code. Only 4xx status codes are supported. This has a higher priority than `error_document`.   | String |
| condition_prefix          | Redirect path prefix to replace with the specified "folder/" for the redirect.                     | String |
| redirect_protocol         | Redirect protocol. Only HTTPS is supported.                       | String |
| redirect_replace_key       | Content that is used to replace the entire key.                                    | String |
| redirect_replace_key_prefix | Content that is used to replace the key prefix. The replacement is allowed only when `Condition` is `KeyPrefixEquals`. | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

## Deleting Static Website Configuration

#### Description

This API is used to delete the static website configuration of a bucket.

#### Method prototype

```c
cos_status_t *cos_delete_bucket_website(const cos_request_options_t *options,
                                          const cos_string_t *bucket,
                                          cos_table_t **resp_header);
```

#### Sample request

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
// COS bucket name, in the format of [bucket]-[appid], for example `mybucket-1253666666`. It can be obtained at https://console.cloud.tencent.com/cos5/bucket.
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

    // Create a memory pool
    cos_pool_create(&pool, NULL);

    // Initialize the request options
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    status = cos_delete_bucket_website(options, &bucket, &resp_headers);
    log_status(status); 

    cos_pool_destroy(pool);
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_delete_website();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket from which static website configuration is deleted, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |
