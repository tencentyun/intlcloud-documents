## Overview

This document provides an overview of APIs and SDK code samples related to bucket referer allowlist or blocklist.


| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Setting bucket referer configuration | Sets a bucket referer allowlist or blocklist |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Querying bucket referer configuration | Queries a bucket referer allowlist or blocklist |

## Setting Bucket Referer Configuration

#### Description

This API (PUT Bucket referer) is used to set a referer allowlist/blocklist for a bucket.

#### Method prototype

```cpp
cos_status_t *cos_put_bucket_referer(const cos_request_options_t *options,
                                     const cos_string_t *bucket,
                                     cos_referer_params_t *referer_params,
                                     cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------------------------------------------------------ | ------- |
| options | COS request options | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| referer_params   | Referer parameters                                              | Struct  |
| status   | Whether hotlink protection is enabled. Enumerated values: `Enabled, `Disabled` | String                                   |
| referer_type    | Hotlink protection type. Enumerated values: `Black-List`, `White-List`          | String |
| empty_refer_config | Whether to allow access with an empty referer. Enumerated values: `Allow`, `Deny` (default) | String |
| domain_list   | List of domain names in the blocklist/allowlist. Using a prefix to specify multiple domains is supported. Domain names and IPs with ports are supported. A wildcard (*) is supported for second-level or multi-level domains.   | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample

For the complete code, see the `test_referer()` function in `cos_demo.c`.

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

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

void test_put_referer()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;
    cos_referer_params_t *params = NULL;
    cos_referer_domain_t *domain = NULL;

    // Create a memory pool
    cos_pool_create(&pool, NULL);

    // Initialize the request options
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Use your own configuration. For more information, see https://intl.cloud.tencent.com/document/product/436/31423.
    params = cos_create_referer_params(pool);
    cos_str_set(&params->status, "Enabled");
    cos_str_set(&params->referer_type, "White-List");
    cos_str_set(&params->empty_refer_config, "Allow");
    domain = cos_create_referer_domain(pool);
    cos_str_set(&domain->domain, "www.qq.com");
    cos_list_add_tail(&domain->node, &params->domain_list);
    domain = cos_create_referer_domain(pool);
    cos_str_set(&domain->domain, "*.tencent.com");
    cos_list_add_tail(&domain->node, &params->domain_list);

    // Put referer
    status = cos_put_bucket_referer(options, &bucket, params, &resp_headers);
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

    test_put_referer();

    cos_http_io_deinitialize();

    return 0;
}
```

## Querying Bucket Referer Configuration

#### Description

This API (GET Bucket referer) is used to query the referer allowlist/blocklist of a bucket.

#### Method prototype

```cpp
cos_status_t *cos_get_bucket_referer(const cos_request_options_t *options,
                                     const cos_string_t *bucket,
                                     cos_referer_params_t *referer_params,
                                     cos_table_t **resp_headers);
```
#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------------------------------------------------------ | ------- |
| options | COS request options | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| referer_params   | Referer parameters                                              | Struct  |
| status   | Whether hotlink protection is enabled. Enumerated values: `Enabled, `Disabled` | String                                   |
| referer_type    | Hotlink protection type. Enumerated values: `Black-List`, `White-List`          | String |
| empty_refer_config | Whether to allow access with an empty referer. Enumerated values: `Allow`, `Deny` (default) | String |
| domain_list   | List of domain names in the blocklist/allowlist. Using a prefix to specify multiple domains is supported. Domain names and IPs with ports are supported. A wildcard (*) is supported for second-level or multi-level domains.   | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample request

For the complete code, see the `test_referer()` function in `cos_demo.c`.

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

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

static void log_get_referer(cos_referer_params_t *result)
{
    int index = 0;
    cos_referer_domain_t *domain;

    cos_warn_log("status: %s", result->status.data);
    cos_warn_log("referer_type: %s", result->referer_type.data);
    cos_warn_log("empty_refer_config: %s", result->empty_refer_config.data);

    cos_list_for_each_entry(cos_referer_domain_t, domain, &result->domain_list, node) {
        cos_warn_log("domain index:%d", ++index);
        cos_warn_log("domain: %s", domain->domain.data);
    }
}

void test_get_referer()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;
    cos_referer_params_t *result = NULL;

    // Create a memory pool
    cos_pool_create(&pool, NULL);

    // Initialize the request options
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Get referer
    result = cos_create_referer_params(pool);
    status = cos_get_bucket_referer(options, &bucket, result, &resp_headers);
    log_status(status);
    if (status->code == 200) {
        log_get_referer(result);
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

    test_get_referer();

    cos_http_io_deinitialize();

    return 0;
}
```
