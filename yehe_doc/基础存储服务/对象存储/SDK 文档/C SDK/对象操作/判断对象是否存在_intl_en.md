## Overview

This document provides an overview of the API and sample code for quickly checking whether an object exists in a bucket. 

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |


## Checking Whether an Object Exists

#### Description

This API is used to check whether an object exists in a bucket. It actually calls the `HEAD Object` API to perform the action.

#### Method prototype

```cpp
cos_status_t *cos_check_object_exist(const cos_request_options_t *options, 
                                     const cos_string_t *bucket, 
                                     const cos_string_t *object,
                                     cos_table_t *headers, 
                                     cos_object_exist_status_e *object_exist,
                                     cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| --------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object | Object name | String |
| headers      | Additional headers of a COS request | Struct |
| object_exist    | Whether an object exists. Enumerated values: `exist`, `non exist`, `unknown` (no explicit state is obtained)   | Enum   |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample

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
// A unique identifier of an object stored in COS. For more information about objects and object keys, please see https://intl.cloud.tencent.com/document/product/436/13324.
static char TEST_OBJECT_NAME1[] = "1.txt";

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

void test_check_object_exist()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers;
    cos_table_t *headers = NULL;
    cos_object_exist_status_e object_exist;

    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, TEST_OBJECT_NAME1);

    // Check whether an object exists
    s = cos_check_object_exist(options, &bucket, &object, headers, &object_exist, &resp_headers);
    if (object_exist == COS_OBJECT_NON_EXIST) {
        printf("object: %.*s non exist.\n", object.len, object.data);
    } else if (object_exist == COS_OBJECT_EXIST) {
        printf("object: %.*s exist.\n", object.len, object.data);
    } else {
        printf("object: %.*s unknown status.\n", object.len, object.data);
        log_status(s);
    }

    cos_pool_destroy(p);
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

    test_check_object_exist();

    cos_http_io_deinitialize();

    return 0;
}
```
