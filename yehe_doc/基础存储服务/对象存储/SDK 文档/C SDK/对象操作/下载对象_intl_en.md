## Overview

This document provides an overview of APIs and SDK code samples related to object downloads.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system. |


## Advanced APIs (Recommended)

### Downloading an object (checkpoint restart)

#### Description

The multipart download API automatically downloads data concurrently with `Range` according to the object size. The part size is 1,048,576 (1 MB) by default and can be adjusted via the `part_size` parameter.

#### Method prototype

```cpp
cos_status_t *cos_resumable_download_file(cos_request_options_t *options,
                                          cos_string_t *bucket,
                                          cos_string_t *object,
                                          cos_string_t *filepath,
                                          cos_table_t *headers,
                                          cos_table_t *params,
                                          cos_resumable_clt_params_t *clt_params,
                                          cos_progress_callback progress_callback);
```

#### Parameter description

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | -------- |
| options | COS request options | Struct |
| bucket | Bucket name in the format: `BucketName-APPID` | String |
| object | Object name | String |
| filepath | The local file name of the object                                          | String |
| headers | Headers attached to the COS request | Struct |
| params | Parameters for the COS request                                           | Struct |
| clt_params | Control parameters for the download operation | Struct |
| part_size | Part size in bytes. If you specify the part size to be below 4,194,304 (4 MB), the system will divide your data based on the part size 4,194,304 (4 MB). | Int      |
| thread_num | Number of threads, that is, size of the thread pool. Default: 1 | Int |
| enable_checkpoint | Indicates whether to enable checkpoint restart | Int |
| checkpoint_path | Indicates the file path for which the upload progress is saved when checkpoint restart is enabled. Default: `<filepath>.cp`, where `filepath` is the local file name of the object | String   |
| progress_callback | Callback function for the download progress | Function |

#### Response

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
static char TEST_DOWNLOAD_NAME4[] = "multipart_download.dat";
static char TEST_MULTIPART_OBJECT4[] = "multipart4.dat";

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

void test_resumable()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t filepath;
    cos_resumable_clt_params_t *clt_params;
    
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, TEST_MULTIPART_OBJECT4);
    cos_str_set(&filepath, TEST_DOWNLOAD_NAME4);

    clt_params = cos_create_resumable_clt_params_content(p, 5*1024*1024, 3, COS_FALSE, NULL);
    s = cos_resumable_download_file(options, &bucket, &object, &filepath, NULL, NULL, clt_params, NULL);
    log_status(s);

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

    test_resumable();

    cos_http_io_deinitialize();

    return 0;
}
```

### Batch downloading files (downloading a COS directory)

#### Description

This API is used to download a COS directory and the files in it to the local disk.

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

void test_download_directory()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t file_name;
    cos_string_t suffix = cos_string("/");
    cos_table_t *resp_headers;
    cos_table_t *headers = NULL;
    cos_table_t *params = NULL;
    int is_truncated = 1;
    cos_string_t marker;
    apr_status_t status;

    // Initialize the request options
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //list object (get bucket)
    cos_list_object_params_t *list_params = NULL;
    list_params = cos_create_list_object_params(p);
    cos_str_set(&list_params->prefix, "folder/");   // Use your own directory name
    cos_str_set(&marker, "");
    while (is_truncated) {
        list_params->marker = marker;
        s = cos_list_object(options, &bucket, list_params, &resp_headers);
        log_status(s);
        if (!cos_status_is_ok(s)) {
            printf("list object failed, req_id:%s\n", s->req_id);
            break;
        }
        cos_list_object_content_t *content = NULL;
        cos_list_for_each_entry(cos_list_object_content_t, content, &list_params->object_list, node) {
            cos_str_set(&file_name, content->key.data);
            if (cos_ends_with(&content->key, &suffix)) {
                // If you need to create the directory first, you can modify the 0x0755 permission as desired. For details, see the definition in `apr_file_info.h`.
                status = apr_dir_make(content->key.data, 0x0755, options->pool);
                if (status != APR_SUCCESS && !APR_STATUS_IS_EEXIST(status)) {
                    printf("mkdir: %s failed, status: %d\n", content->key.data, status);
                }
            } else {
                // Download the object to a local directory, which is the current program running directory by default
                s = cos_get_object_to_file(options, &bucket, &content->key, headers, params, &file_name, &resp_headers);
                if (!cos_status_is_ok(s)) {
                    printf("get object[%s] failed, req_id:%s\n", content->key.data, s->req_id);
                }
            }
        }
        is_truncated = list_params->truncated;
        marker = list_params->next_marker;
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

    test_download_directory();

    cos_http_io_deinitialize();

    return 0;
}
```


## Simple Operations

### Downloading an object

#### Description

This API is used to download an object to the local file system. This operation requires that you have read permission for the object, or that the object has public read permission enabled.

#### Method prototype

```cpp
cos_status_t *cos_get_object_to_file(const cos_request_options_t *options,
                                     const cos_string_t *bucket, 
                                     const cos_string_t *object,
                                     cos_table_t *headers, 
                                     cos_table_t *params,
                                     cos_string_t *filename, 
                                     cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format: `BucketName-APPID` | String |
| object | Object name | String |
| headers      | Additional headers of a COS request | Struct |
| params | Parameters for the COS request operation | Struct |
| filename | Filename of the local object before it is uploaded to COS | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample: simple download

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
static char TEST_DOWNLOAD_NAME[] = "download_test3.dat";

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

void test_download_object()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t file;
    cos_table_t *resp_headers = NULL;

    // Create a memory pool
    cos_pool_create(&p, NULL);

    // Initialize the request options
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Get the object
    cos_str_set(&file, TEST_DOWNLOAD_NAME);
    cos_str_set(&object, TEST_OBJECT_NAME1);
    s = cos_get_object_to_file(options, &bucket, &object, NULL, NULL, &file, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("get object succeeded\n");
    } else {
        printf("get object failed\n");
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

    test_download_object();

    cos_http_io_deinitialize();

    return 0;
}
```