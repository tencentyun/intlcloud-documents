

## Overview

This document provides an overview of APIs and SDK code samples related to custom domains.

| API | Operation | Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting a custom domain | Sets a custom domain for a bucket |
| GET Bucket domain    | Querying a custom domain | Queries the custom domain of a bucket |

## Setting Custom Domains

#### Description

This API is used to set a custom domain for a bucket.

#### Method prototype

```c
cos_status_t *cos_put_bucket_domain(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_domain_params_t *domain_params,
                                      cos_table_t **resp_header);
```

#### Sample request

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// `endpoint` is the COS access domain name. For more information, visit https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                //your secret_id
static char *TEST_ACCESS_KEY_SECRET;            //your secret_key
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    //your appid
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

void test_put_bucket_domain()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_domain_params_t  *domain_params = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;
    
    // Create a memory pool
    cos_pool_create(&pool, NULL);
    
    // Initialize the request options
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    
    // Create domain parameters
    domain_params = cos_create_domain_params(options->pool);
    cos_str_set(&domain_params->status, "ENABLED");
    cos_str_set(&domain_params->name, "www.example.com");
    cos_str_set(&domain_params->type, "REST");
    cos_str_set(&domain_params->forced_replacement, "CNAME");
    
    status = cos_put_bucket_domain(options, &bucket, domain_params, &resp_headers);
    log_status(status);

    // Destroy the memory pool.
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

    //set log level, default COS_LOG_WARN
    cos_log_set_level(COS_LOG_WARN);

    //set log output, default stderr
    cos_log_set_output(NULL);

    test_put_bucket_domain();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for custom domain setting, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| domain_params      | Custom domain configuration for the bucket                                     | Struct |
| status                 | Domain status. Valid values: `ENABLED`, `DISABLED`             | String |
| name                   | Custom domain. Letters, digits, and dots (.) are supported.          | String |
| type                   | Type of the origin server to bind. Valid values: `REST`, `WEBSITE`                          | String |
| forced_replacement      | Replaces existing configurations. Valid values: `CNAME`, `TXT`. If this parameter is specified, configurations will only be delivered after the domain ownership is verified. | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Error codes

The following describes some common errors that may occur when you call this API:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict | The domain record already exists, and forced overwrite is not specified in the request; OR the domain record does not exist, and forced overwrite is specified in the request |
| HTTP 451 Unavailable For Legal Reasons | The domain does not have an ICP filing in the Chinese mainland                          |

## Querying a Custom Domain

#### Description

This API is used to query the custom domain set for a bucket.

#### Method prototype

```c
cos_status_t *cos_get_bucket_domain(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_domain_params_t *domain_params,
                                      cos_table_t **resp_header);
```

#### Sample request

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// `endpoint` is the COS access domain name. For more information, visit https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                //your secret_id
static char *TEST_ACCESS_KEY_SECRET;            //your secret_key
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    //your appid
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

void test_get_bucket_domain()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_domain_params_t  *domain_result = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;
    
    // Create a memory pool
    cos_pool_create(&pool, NULL);
    
    // Initialize the request options
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    
    // Query custom domain configuration
    domain_result = cos_create_domain_params(options->pool);
    status = cos_get_bucket_domain(options, &bucket, domain_result, &resp_headers);
    log_status(status);
    if (!cos_status_is_ok(status)) {
        cos_pool_destroy(pool);
        return;
    }
    
    // View results
    char *line = NULL;
    line = apr_psprintf(options->pool, "%.*s\n", domain_result->status.len, domain_result->status.data);
    printf("status: %s", line);
    line = apr_psprintf(options->pool, "%.*s\n", domain_result->name.len, domain_result->name.data);
    printf("name: %s", line);
    line = apr_psprintf(options->pool, "%.*s\n", domain_result->type.len, domain_result->type.data);
    printf("type: %s", line);
    line = apr_psprintf(options->pool, "%.*s\n", domain_result->forced_replacement.len, domain_result->forced_replacement.data);
    printf("forced_replacement: %s", line);

    // Destroy the memory pool.
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

    //set log level, default COS_LOG_WARN
    cos_log_set_level(COS_LOG_WARN);

    //set log output, default stderr
    cos_log_set_output(NULL);

    test_get_bucket_domain();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for custom domain query, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| domain_params      | Custom domain configuration for the bucket                                     | Struct |
| status                 | Domain status. Valid values: `ENABLED`, `DISABLED`             | String |
| name                   | Custom domain. Letters, digits, and dots (.) are supported.          | String |
| type                   | Type of the origin server to bind. Valid values: `REST`, `WEBSITE`                          | String |
| forced_replacement      | Replaces existing configurations. Valid values: `CNAME`, `TXT`. If this parameter is specified, configurations will only be delivered after the domain ownership is verified. | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |
