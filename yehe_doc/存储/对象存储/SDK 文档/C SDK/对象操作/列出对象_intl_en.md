## Overview

This document provides an overview of APIs and SDK code samples related to object listing.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying objects | Queries some or all the objects in a bucket. |


## Querying an Object List

#### Description

This API is used to query some or all the objects in a bucket.

#### Method prototype

```cpp
cos_status_t *cos_list_object(const cos_request_options_t *options,
                              const cos_string_t *bucket, 
                              cos_list_object_params_t *params, 
                              cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------- |
| options | COS request options | Struct |
| Bucket | Bucket name in the format of `BucketName-APPID` | String |
| params | Parameters for the list operation | Struct |
| encoding_type | Specifies the encoding type of the returned value | String |
| prefix | Prefix to be matched, which is used to specify the prefix address of the files to be returned | String |
| marker  | Marks the starting point of the object list; by default, entries are listed in UTF-8 binary order starting from this marker | String |
| delimiter | A query separator, used to group object keys                             | String  |
| max_ret | The maximum number of returned entries per request; the default value is 1000 | Struct  |
| truncated  |  Indicates whether the returned entry is truncated. Valid value: `true` or `false` | Boolean|
| next_marker        | Marks the starting point of the next entry if the returned entry is truncated  | String  |
| object_list | Object list returned by the `Get Bucket` operation | Struct |
| key | Name (key) of the object returned by the `Get Bucket` operation | Struct |
| last_modified      | The last modified time of the object returned by the `Get Bucket` operation | Struct  |
| etag | SHA-1 check value of the object returned by the `Get Bucket` operation                | Struct  |
| size | The size in bytes of the object returned by the `Get Bucket` operation | Struct  |
| owner_id           | UID of the owner of the object returned by the `Get Bucket` operation                      | Struct  |
| storage_class      | The storage class of the object returned by the `Get Bucket` operation                            | Struct  |
| common_prefix_list | The identical paths between a particular prefix and the delimiter are grouped together and defined as a common prefix | Struct |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample 1. Listing objects on the first page

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

void test_list_objects()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    // Create a memory pool
    cos_pool_create(&p, NULL);

    // Initialize the request options
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Get the object list
    cos_list_object_params_t *list_params = NULL;
    cos_list_object_content_t *content = NULL;
    list_params = cos_create_list_object_params(p);
    s = cos_list_object(options, &bucket, list_params, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("list object succeeded\n");
        cos_list_for_each_entry(cos_list_object_content_t, content, &list_params->object_list, node) {
           printf("object: %.*s\n", content->key.len, content->key.data);
        }
    } else {
        printf("list object failed\n");
    }

    // Destroy the memory pool.
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

    test_list_objects();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Sample 2. Listing the objects in a directory

COS does not have the concept of folder, but you can use slashes (/) as the delimiter to stimulate folders.

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

void test_list_directory()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers;
    int is_truncated = 1;
    cos_string_t marker;
    
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    
    //list object (get bucket)
    cos_list_object_params_t *list_params = NULL;
    list_params = cos_create_list_object_params(p);
    // The prefix indicates that the key of the object to be listed must start with this value
    cos_str_set(&list_params->prefix, "folder/");
    // Set the delimiter to "/" to list objects in the current directory. To list all objects, leave it empty.
    cos_str_set(&list_params->delimiter, "/");
    // Set the maximum number of traversed objects (up to 1,000 per listobject request)
    list_params->max_ret = 1000;
    cos_str_set(&marker, "");
    while (is_truncated) {
        list_params->marker = marker;
        s = cos_list_object(options, &bucket, list_params, &resp_headers);
        if (!cos_status_is_ok(s)) {
            printf("list object failed, req_id:%s\n", s->req_id);
            break;
        }
        // `list_params->object_list` returns the following objects
        cos_list_object_content_t *content = NULL;
        cos_list_for_each_entry(cos_list_object_content_t, content, &list_params->object_list, node) {
            printf("object: %s\n", content->key.data);
        }
        // `list_params->common_prefix_list` indicates paths that end with the delimiter. If the delimiter is set to "/", the common prefix indicates the paths of all subdirectories.
        cos_list_object_common_prefix_t *common_prefix = NULL;
        cos_list_for_each_entry(cos_list_object_common_prefix_t, common_prefix, &list_params->common_prefix_list, node) {
            printf("common prefix: %s\n", common_prefix->prefix.data);
        }

        is_truncated = list_params->truncated;
        marker = list_params->next_marker;
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

    test_list_directory();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Sample 3. Listing all objects in a bucket

A maximum of 1,000 objects can be listed at a time. When the number of objects in a bucket exceeds 1,000, you need to list all objects in the bucket repeatedly.

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

void test_list_all_objects()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers;
    int is_truncated = 1;
    cos_string_t marker;
    
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    
    //list object (get bucket)
    cos_list_object_params_t *list_params = NULL;
    list_params = cos_create_list_object_params(p);
    // Set the maximum number of traversed objects (up to 1,000 per listobject request)
    list_params->max_ret = 1000;
    cos_str_set(&marker, "");
    while (is_truncated) {
        list_params->marker = marker;
        cos_list_init(&list_params->object_list);
        s = cos_list_object(options, &bucket, list_params, &resp_headers);
        if (!cos_status_is_ok(s)) {
            printf("list object failed, req_id:%s\n", s->req_id);
            break;
        }
        // `list_params->object_list` returns the following objects
        cos_list_object_content_t *content = NULL;
        cos_list_for_each_entry(cos_list_object_content_t, content, &list_params->object_list, node) {
            printf("object: %s\n", content->key.data);
        }

        is_truncated = list_params->truncated;
        marker = list_params->next_marker;
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

    test_list_all_objects();

    cos_http_io_deinitialize();

    return 0;
}
```