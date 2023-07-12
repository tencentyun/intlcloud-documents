

## Overview

This document provides an overview of APIs and C SDK code samples related to logging.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting logging | Enables logging for a source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying logging configuration | Queries the logging configuration of a source bucket |

## Setting Logging Configuration

#### Description

This API is used to enable logging for a source bucket and store the access logs in a specified destination bucket.

#### Method prototype

```C
cos_status_t *cos_put_bucket_logging(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_logging_params_t *logging_params,
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

void test_put_logging()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_logging_params_t  *params = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;

    // Create a memory pool
    cos_pool_create(&pool, NULL);

    // Initialize the request options
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Set logging parameters
    params = cos_create_logging_params(options->pool);
    cos_str_set(&params->target_bucket, TEST_BUCKET_NAME);
    cos_str_set(&params->target_prefix, "logging/");

    status = cos_put_bucket_logging(options, &bucket, params, &resp_headers);
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

    test_put_logging();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Source bucket for which logging is to be enabled, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String                                      |
| logging_params | Bucket logging parameters                                           | Struct |
| target_bucket             | Destination bucket that stores logs. It can be the source bucket itself (although this is not recommended), or a bucket in the same account or region as the source bucket.                                           | String      |
| target_prefix             | The specified path prefix used to store logs in the destination bucket                                           | String      |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

## Querying Logging Configuration

#### Description

This API is used to query the logging configuration of a specified bucket.

#### Method prototype

```c
cos_status_t *cos_get_bucket_logging(const cos_request_options_t *options,  
                                      const cos_string_t *bucket,    
                                      cos_logging_params_t *logging_params,
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

void test_get_logging()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_logging_params_t  *result = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;

    // Create a memory pool
    cos_pool_create(&pool, NULL);

    // Initialize the request options
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

    // View results
    char *line = NULL;
    line = apr_psprintf(options->pool, "%.*s\n", result->target_bucket.len, result->target_bucket.data);
    printf("target bucket: %s", line);
    line = apr_psprintf(options->pool, "%.*s\n", result->target_prefix.len, result->target_prefix.data);
    printf("target prefix: %s", line);

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

    test_get_logging();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Destination bucket to store logs, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String                                      |
| logging_params | Bucket logging parameters                                           | Struct |
| target_bucket             | Destination bucket that stores logs. It can be the source bucket itself (although this is not recommended), or a bucket in the same account or region as the source bucket.                                           | String      |
| target_prefix             | The specified path prefix used to store logs in the destination bucket                                           | String      |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |
