

## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes the tags of a bucket |

## Setting Bucket Tags

#### Description

This API is used to set tags for an existing bucket.

#### Method prototype

```c
cos_status_t *cos_put_bucket_tagging(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_tagging_params_t *tagging_params,
                                      cos_table_t **resp_headers);
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

void test_put_bucket_tagging()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;
    cos_tagging_params_t *params = NULL;
    cos_tagging_tag_t *tag = NULL;

    // Create a memory pool
    cos_pool_create(&pool, NULL);

    // Initialize the request options
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Put tagging
    params = cos_create_tagging_params(pool);
    tag = cos_create_tagging_tag(pool);
    cos_str_set(&tag->key, "age");
    cos_str_set(&tag->value, "18");
    cos_list_add_tail(&tag->node, &params->node);

    tag = cos_create_tagging_tag(pool);
    cos_str_set(&tag->key, "name");
    cos_str_set(&tag->value, "xiaoming");
    cos_list_add_tail(&tag->node, &params->node);

    status = cos_put_bucket_tagging(options, &bucket, params, &resp_headers);
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

    test_put_bucket_tagging();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for tag setting, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| tagging_params | Bucket tagging parameters                                           | Struct |
| key | Tag key. A tag key must not exceed 128 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String |
| value | Tag value. A tag value must not exceed 256 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

## Querying Bucket Tags

#### Description

This API is used to query the existing tags of a specified bucket.

#### Method prototype

```c
cos_status_t *cos_get_bucket_tagging(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_tagging_params_t *tagging_params,
                                      cos_table_t **resp_headers);
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

void test_get_bucket_tagging()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;
    cos_tagging_params_t *result = NULL;
    cos_tagging_tag_t *tag = NULL;

    // Create a memory pool
    cos_pool_create(&pool, NULL);

    // Initialize the request options
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Get tagging
    result = cos_create_tagging_params(pool);
    status = cos_get_bucket_tagging(options, &bucket, result, &resp_headers);
    log_status(status);

    tag = NULL;
    cos_list_for_each_entry(cos_tagging_tag_t, tag, &result->node, node) {
        printf("taging key: %s\n", tag->key.data);
        printf("taging value: %s\n", tag->value.data);

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

    test_get_bucket_tagging();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for tag query, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| tagging_params | Bucket tagging parameters                                           | Struct |
| key | Tag key. A tag key must not exceed 128 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String |
| value | Tag value. A tag value must not exceed 256 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

## Deleting Bucket Tags

#### Description

This API is used to delete the existing tags from a bucket.

#### Method prototype

```c
cos_status_t *cos_delete_bucket_tagging(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_table_t **resp_headers);
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

void test_delete_bucket_tagging()
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

    // Delete tagging
    status = cos_delete_bucket_tagging(options, &bucket, &resp_headers);
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

    test_delete_bucket_tagging();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for tag deletion, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |
