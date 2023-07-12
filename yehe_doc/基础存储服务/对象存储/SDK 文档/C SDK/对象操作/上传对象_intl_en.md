## Overview

This document provides an overview of APIs and SDK code samples related to object uploads.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object (creating a directory) | Uploads an object to a bucket. |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | Appending parts  | Uploads an object by appending parts   |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads a file in parts. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |


## Advanced APIs (Recommended)

### Uploading an object (checkpoint restart)

#### Description

The upload API automatically divides your data into parts based on the size of your file. It's easier to use, eliminating the need to follow each step of the multipart upload process. The part size is 1,048,576 (1 MB) by default and can be adjusted via the `part_size` parameter. 

#### Method prototype

```cpp
cos_status_t *cos_resumable_upload_file(cos_request_options_t *options,
                                          cos_string_t *bucket,
                                          cos_string_t *object,
                                          cos_string_t *filepath,
                                          cos_table_t *headers,
                                          cos_table_t *params,
                                          cos_resumable_clt_params_t *clt_params,
                                          cos_progress_callback progress_callback,
                                          cos_table_t **resp_headers,
                                          cos_list_t *resp_body)
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
| clt_params | Control parameters for the upload operation | Struct |
| part_size | Part size in bytes. If you specify the part size to be below 1,048,576 (1 MB), the C SDK will divide your data based on the part size 1,048,576 (1 MB) by default. If the number of parts exceeds 10,000, the C SDK adjusts the part size according to the file size. | Int      |
| thread_num | Number of threads, that is, size of the thread pool. Default: 1 | Int |
| enable_checkpoint | Indicates whether to enable checkpoint restart | Int |
| checkpoint_path | Indicates the file path for which the upload progress is saved when checkpoint restart is enabled. Default: `<filepath>.cp`, where `filepath` is the local file name of the object | String   |
| progress_callback | Callback function for upload progress | Function |
| resp_headers | Returns the HTTP response headers | Struct |
| resp_body | Saves the data returned by the `Complete Multipart Upload` request                             | Struct   |

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
static char TEST_MULTIPART_FILE[] = "test.zip";
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

void test_resumable_upload_with_multi_threads()
{
    cos_pool_t *p = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t filename;
    cos_status_t *s = NULL;
    int is_cname = 0;
    cos_table_t *headers = NULL;
    cos_table_t *resp_headers = NULL;
    cos_request_options_t *options = NULL;
    cos_resumable_clt_params_t *clt_params;

    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    headers = cos_table_make(p, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, TEST_MULTIPART_OBJECT4);
    cos_str_set(&filename, TEST_MULTIPART_FILE);

    // upload
    clt_params = cos_create_resumable_clt_params_content(p, 1024 * 1024, 8, COS_FALSE, NULL);
    s = cos_resumable_upload_file(options, &bucket, &object, &filename, headers, NULL, 
        clt_params, NULL, &resp_headers, NULL);

    if (cos_status_is_ok(s)) {
        printf("upload succeeded\n");
    } else {
        printf("upload failed\n");
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

    test_resumable_upload_with_multi_threads();

    cos_http_io_deinitialize();

    return 0;
}
```


## Simple Operations

### Uploading an object (creating a directory) using simple upload

#### Description

This API is used to upload an object of up to 5 GB in size to a specified bucket. To upload objects larger than 5 GB, please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89).

#### Method prototype

```cpp
cos_status_t *cos_put_object_from_file(const cos_request_options_t *options,
                                       const cos_string_t *bucket, 
                                       const cos_string_t *object, 
                                       const cos_string_t *filename,
                                       cos_table_t *headers, 
                                       cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format: `BucketName-APPID` | String |
| object | Object name | String |
| filename | Filename of the local object before it is uploaded to COS | String |
| headers      | Additional headers of a COS request | Struct |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |


#### Sample 1. Uploading an object

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

void test_put_object_from_file()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers;
    cos_string_t file;
    int traffic_limit = 0;

    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_table_t *headers = NULL;
    if (traffic_limit) {
        // The speed range is 819200 to 838860800, that is 100 KB/s to 100 MB/s. If the value is not within this range, 400 will be returned.
        headers = cos_table_make(p, 1);
        cos_table_add_int(headers, "x-cos-traffic-limit", 819200);
    }
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&file, TEST_OBJECT_NAME1);
    cos_str_set(&object, TEST_OBJECT_NAME1);
    s = cos_put_object_from_file(options, &bucket, &object, &file, headers, &resp_headers);
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

    test_put_object_from_file();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Sample 2. Creating a folder

COS uses slashes (/) to separate object paths to simulate the effect of directories. Therefore, you can upload an empty stream and append a slash to its name to create an empty directory in COS.

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

void test_create_dir()
{
    cos_pool_t *p = NULL;
    int is_cname = 0; 
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers;
    cos_table_t *headers = NULL;
    cos_list_t buffer;
    
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, "folder/");

    // Upload a folder
    cos_list_init(&buffer);
    s = cos_put_object_from_buffer(options, &bucket, &object, 
            &buffer, headers, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put object succeeded\n");
    } else {
        printf("put object failed\n");
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

    test_create_dir();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Sample 3. Uploading an object to a COS directory

You can upload an object whose name is separated by slashes. In this way, the directory that contains this object will be created automatically. If you need to upload new objects to this COS directory, you can set the key’s prefix to the value of this directory.

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

void test_upload_file_to_dir()
{
    cos_pool_t *p = NULL;
    int is_cname = 0; 
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t file;
    cos_table_t *resp_headers;
    
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&file, "examplefile");
    cos_str_set(&object, "folder/exampleobject");
    s = cos_put_object_from_file(options, &bucket, &object, &file, NULL, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put object succeeded\n");
    } else {
        printf("put object failed\n");
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

    test_upload_file_to_dir();

    cos_http_io_deinitialize();

    return 0;
}
```

### Appending parts

#### Description

This API is used to upload an object by appending parts of the object. The default maximum size of each object part is 5 GB (no minimum size limit), and the size of the object uploaded using this API can be up to 5 GB. If the value of `position` is inconsistent with the object length, COS will return the 409 status code. If the object to append is of the "normal" type, COS will return "409 ObjectNotAppendable".

#### Method prototype

```cpp
cos_status_t *cos_append_object_from_file(const cos_request_options_t *options,
                                          const cos_string_t *bucket, 
                                          const cos_string_t *object, 
                                          int64_t position,
                                          const cos_string_t *append_file, 
                                          cos_table_t *headers, 
                                          cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format: `BucketName-APPID` | String |
| object | Object name | String |
| position     | Starting point for the append operation (in bytes). For the first append, the value of this parameter is 0. For subsequent appends, the value is the `content-length` of the current object.   | String |
| append_file | Filename of the local object before it is uploaded to COS | String |
| headers      | Additional headers of a COS request | Struct |
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
static char TEST_OBJECT_NAME3[] = "test3.dat";
static char *TEST_APPEND_NAMES[] = {"test.7z.001", "test.7z.002"};

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

void test_append_object()
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

    // Append parts
    cos_str_set(&object, TEST_OBJECT_NAME3);
    int32_t count = sizeof(TEST_APPEND_NAMES)/sizeof(char*);
    int32_t index = 0;
    int64_t position = 0;
    s = cos_head_object(options, &bucket, &object, NULL, &resp_headers);
    if(s->code == 200) {
        char *content_length_str = (char*)apr_table_get(resp_headers, COS_CONTENT_LENGTH);
        if (content_length_str != NULL) {
            position = atol(content_length_str);
        }
    }
    for (; index < count; index++)
    {
        cos_str_set(&file, TEST_APPEND_NAMES[index]);
        s = cos_append_object_from_file(options, &bucket, &object, 
                                        position, &file, NULL, &resp_headers);
        log_status(s);

        s = cos_head_object(options, &bucket, &object, NULL, &resp_headers);
        if(s->code == 200) {
            char *content_length_str = (char*)apr_table_get(resp_headers, COS_CONTENT_LENGTH);
            if (content_length_str != NULL) {
                position = atol(content_length_str);
            }
        }
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

    test_append_object();

    cos_http_io_deinitialize();

    return 0;
}
```

## Multipart Operations

### Querying multipart uploads

#### Description

This API is used to query in-progress multipart uploads. Up to 1,000 in-progress multipart uploads can be queried in a single request

#### Method prototype

```cpp
cos_status_t *cos_list_multipart_upload(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        cos_list_multipart_upload_params_t *params, 
                                        cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| options | COS request options | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| params | Parameters for the `List Multipart Uploads` operation | Struct |
| encoding_type | Specifies the encoding type of the returned value | String |
| prefix | Prefix to be matched, which is used to specify the prefix address of the files to be returned | String |
| delimiter | The delimiter is a symbol.<br><li>If a particular prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed.<br><li>If no prefix is specified, the list will start from the beginning of the path. | String |
| max_ret | The maximum number of returned entries per request; the default value is 1000 | String  |
| key_marker | Used together with `upload-id-marker`.<br><li>If `upload-id-marker` is not specified, only the multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed;<br><li>If `upload-id-marker` is specified, the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed, and any multipart upload whose `ObjectName` lexicographically equals `key-marker` and whose `UploadID` is greater than `upload-id-marker` will also be listed. | String |
| upload_id_marker | Used together with `key-marker`.<br><li>If `key-marker` is not specified, `upload-id-marker` will be ignored; <br><li>If `key-marker` is specified, the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed, and any multipart upload whose `ObjectName` lexicographically equals `key-marker` and whose `UploadID` is greater than `upload-id-marker` will also be listed | String |
| truncated  |  Indicates whether the returned entry is truncated. Valid value: `true` or `false` | Boolean |
| next_key_marker | If the returned list is truncated, the `NextKeyMarker` returned will be the starting point of the subsequent list. | String |
| next_upload_id_marker | If the returned list is truncated, the `UploadId` returned will be the starting point of the subsequent list. | String |
| upload_list | Lists all multipart uploads                                              | Struct  |
| key | Object name | String |
| upload_id | Identifies the ID of the current multipart upload | String |
| initiated | Indicates when the current multipart upload was initiated | String  |
| resp_headers | Returns the HTTP response headers | Struct |

```
typedef struct {
    cos_list_t node;
    cos_string_t key;
    cos_string_t upload_id;
    cos_string_t initiated;
} cos_list_multipart_upload_content_t;
```

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
static char TEST_MULTIPART_OBJECT[] = "multipart.dat";

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

void list_multipart()
{
    cos_pool_t *p = NULL;
    cos_string_t bucket;
    cos_string_t object;
    int is_cname = 0;
    cos_table_t *resp_headers = NULL;
    cos_request_options_t *options = NULL;
    cos_status_t *s = NULL;
    cos_list_multipart_upload_params_t *list_multipart_params = NULL;
    cos_list_upload_part_params_t *list_upload_param = NULL;

    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    
    list_multipart_params = cos_create_list_multipart_upload_params(p);
    list_multipart_params->max_ret = 999;
    s = cos_list_multipart_upload(options, &bucket, list_multipart_params, &resp_headers);
    log_status(s);

    list_upload_param = cos_create_list_upload_part_params(p);
    list_upload_param->max_ret = 1000;
    cos_string_t upload_id;
    cos_str_set(&upload_id,"149373379126aee264fecbf5fe8ddb8b9cd23b76c73ab1af0bcfd50683cc4254f81ebe2386");
    cos_str_set(&object, TEST_MULTIPART_OBJECT);
    s = cos_list_upload_part(options, &bucket, &object, &upload_id, 
                             list_upload_param, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("List upload part succeeded, upload_id::%.*s\n", 
               upload_id.len, upload_id.data);
        cos_list_part_content_t *part_content = NULL;
        cos_list_for_each_entry(cos_list_part_content_t, part_content, &list_upload_param->part_list, node) {
            printf("part_number = %s, size = %s, last_modified = %s, etag = %s\n",
                   part_content->part_number.data, 
                   part_content->size.data, 
                   part_content->last_modified.data, 
                   part_content->etag.data);
        }
    } else {
        printf("List upload part failed\n"); 
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

    list_multipart();

    cos_http_io_deinitialize();

    return 0;
}
```

### Initializing a multipart upload

#### Description

This API is used to initialize a multipart upload. After the request is executed successfully, the `Upload ID` is returned for the subsequent `Upload Part` requests.

#### Method prototype

```cpp
cos_status_t *cos_init_multipart_upload(const cos_request_options_t *options, 
                                        const cos_string_t *bucket, 
                                        const cos_string_t *object, 
                                        cos_string_t *upload_id, 
                                        cos_table_t *headers,
                                        cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format: `BucketName-APPID` | String |
| object | Object name | String |
| upload_id | Returns the ID of the multipart upload operation | String |
| headers      | Additional headers of a COS request | Struct |
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
static char TEST_MULTIPART_OBJECT[] = "multipart.dat";

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

void test_init_multipart_upload()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t upload_id;
    cos_table_t *resp_headers = NULL;

    // Create a memory pool
    cos_pool_create(&p, NULL);

    // Initialize the request options
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Initialize the multipart upload
    cos_str_set(&object, TEST_MULTIPART_OBJECT);
    s = cos_init_multipart_upload(options, &bucket, &object, 
                                &upload_id, NULL, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("init multipart upload succeeded\n");
    } else {
        printf("init multipart upload failed\n");
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

    test_init_multipart_upload();

    cos_http_io_deinitialize();

    return 0;
}
```



### Uploading parts

#### Description

This API is used to upload parts (possibly out of order) in an initiated multipart upload operation. This API supports the upload of between 1 to 10,000 parts, with each part ranging from 1 MB to 5 GB in size. The `Upload Part` request should include the `partNumber` and `uploadID`.

#### Method prototype

```cpp
cos_status_t *cos_upload_part_from_file(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        const cos_string_t *object,
                                        const cos_string_t *upload_id, 
                                        int part_num, 
                                        cos_upload_file_t *upload_file,
                                        cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format: `BucketName-APPID` | String |
| object | Object name | String |
| upload_id | Upload task ID | String |
| part_num | Part number | Int |
| upload_file | Information on the file to be uploaded | Struct |
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
static char TEST_MULTIPART_OBJECT[] = "multipart.dat";
static char TEST_MULTIPART_FILE[] = "test.zip";

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

void test_upload_part()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t upload_id = cos_string("xxxxxxxxxxxxxxxxxxx");  // Use your own `uploadid`
    cos_table_t *resp_headers = NULL;
    int part_num = 1;
    int64_t pos = 0;
    int64_t file_length = 0;

    // Create a memory pool
    cos_pool_create(&p, NULL);

    // Initialize the request options
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, TEST_MULTIPART_OBJECT);

    // Upload the parts
    int res = COSE_OK;
    cos_upload_file_t *upload_file = NULL;
    cos_file_buf_t *fb = cos_create_file_buf(p);
    res = cos_open_file_for_all_read(p, TEST_MULTIPART_FILE, fb);
    if (res != COSE_OK) {
        cos_error_log("Open read file fail, filename:%s\n", TEST_MULTIPART_FILE);
        return;
    }
    file_length = fb->file_last;
    apr_file_close(fb->file);
    while(pos < file_length) {
        upload_file = cos_create_upload_file(p);
        cos_str_set(&upload_file->filename, TEST_MULTIPART_FILE);
        upload_file->file_pos = pos;
        pos += 2 * 1024 * 1024;
        upload_file->file_last = pos < file_length ? pos : file_length; //2MB
        s = cos_upload_part_from_file(options, &bucket, &object, &upload_id,
                                    part_num++, upload_file, &resp_headers);

        if (cos_status_is_ok(s)) {
            printf("upload part succeeded\n");
        } else {
            printf("upload part failed\n");
        }
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

    test_upload_part();

    cos_http_io_deinitialize();

    return 0;
}
```

### Querying uploaded parts

#### Description

This API is used to query the uploaded parts of a specified multipart upload.

#### Method prototype

```cpp
cos_status_t *cos_list_upload_part(const cos_request_options_t *options,
                                   const cos_string_t *bucket, 
                                   const cos_string_t *object, 
                                   const cos_string_t *upload_id, 
                                   cos_list_upload_part_params_t *params,
                                   cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ----------------------- | ------------------------------------------------------------ | ------- |
| options | COS request options | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object | Object name | String |
| upload_id | Upload task ID | String |
| params | Parameters for the `List Parts` operation | Struct |
| part_number_marker | Marks the starting point of the list of parts; by default, entries are listed in UTF-8 binary order starting from this marker | String |
| encoding_type | Specifies the encoding type of the returned value | String |
| max_ret | The maximum number of returned entries per request; the default value is 1000 | String  |
| truncated  |  Indicates whether the returned entry is truncated. Valid value: `true` or `false` | Boolean|
| next_part_number_marker | Marks the starting point of the next entry if the returned entry is truncated | String |
| part_list | Lists all uploaded parts | Struct |
| part_number | Part number | String |
| size | Part size in bytes | String |
| etag | SHA-1 check value of the part | String |
| last_modified | The time the part was last modified | String |
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
static char TEST_MULTIPART_OBJECT[] = "multipart.dat";

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

void test_list_upload_part()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_list_upload_part_params_t *params = NULL;
    cos_list_t complete_part_list;
    cos_string_t upload_id = cos_string("xxxxxxxxxxxxxxxxxxx");  // Use your own `uploadid`
    cos_table_t *resp_headers = NULL;

    // Create a memory pool
    cos_pool_create(&p, NULL);

    // Initialize the request options
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, TEST_MULTIPART_OBJECT);

    // Query the uploaded parts
    params = cos_create_list_upload_part_params(p);
    params->max_ret = 1000;
    cos_list_init(&complete_part_list);
    s = cos_list_upload_part(options, &bucket, &object, &upload_id, 
                            params, &resp_headers);

    if (cos_status_is_ok(s)) {
        printf("List multipart succeeded\n");
    } else {
        printf("List multipart failed\n");
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

    test_list_upload_part();

    cos_http_io_deinitialize();

    return 0;
}
```

### Completing a multipart upload

#### Description

This API is used to complete the multipart upload of an entire file. You can use this API to complete the multipart upload when you have uploaded all the parts using the `Upload Parts` API. When using this API, you need to provide the `PartNumber` and `ETag` for every part in the body to verify the accuracy of the parts.

#### Method prototype

```cpp
cos_status_t *cos_complete_multipart_upload(const cos_request_options_t *options,
                                            const cos_string_t *bucket, 
                                            const cos_string_t *object, 
                                            const cos_string_t *upload_id, 
                                            cos_list_t *part_list, 
                                            cos_table_t *headers,
                                            cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format: `BucketName-APPID` | String |
| object | Object name | String |
| upload_id | Upload task ID | String |
| part_list | Parameters for the `Complete Multipart Upload` operation | Struct |
| part_number | Part number | String |
| etag | ETag of the part, which is the `sha1` checksum value. It must be enclosed in double quotes, such as: `"3a0f1fd698c235af9cf098cb74aa25bc"`. | String |
| headers      | Additional headers of a COS request | Struct |
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
static char TEST_MULTIPART_OBJECT[] = "multipart.dat";

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

void test_complete_multipart_upload()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_list_upload_part_params_t *params = NULL;
    cos_list_t complete_part_list;
    cos_string_t upload_id = cos_string("xxxxxxxxxxxxxxxxxxx");  // Use your own `uploadid`
    cos_table_t *resp_headers = NULL;
    cos_list_part_content_t *part_content = NULL;
    cos_complete_part_content_t *complete_part_content = NULL;

    // Create a memory pool
    cos_pool_create(&p, NULL);

    // Initialize the request options
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, TEST_MULTIPART_OBJECT);

    // Query the uploaded parts
    params = cos_create_list_upload_part_params(p);
    params->max_ret = 1000;
    cos_list_init(&complete_part_list);
    s = cos_list_upload_part(options, &bucket, &object, &upload_id, 
                            params, &resp_headers);

    if (cos_status_is_ok(s)) {
        printf("List multipart succeeded\n");
    } else {
        printf("List multipart failed\n");
        cos_pool_destroy(p);
        return;
    }

    cos_list_for_each_entry(cos_list_part_content_t, part_content, &params->part_list, node) {
        complete_part_content = cos_create_complete_part_content(p);
        cos_str_set(&complete_part_content->part_number, part_content->part_number.data);
        cos_str_set(&complete_part_content->etag, part_content->etag.data);
        cos_list_add_tail(&complete_part_content->node, &complete_part_list);
    }

    // Complete the multipart upload
    s = cos_complete_multipart_upload(options, &bucket, &object, &upload_id,
                                    &complete_part_list, NULL, &resp_headers);

    if (cos_status_is_ok(s)) {
        printf("Complete multipart upload from file succeeded, upload_id:%.*s\n", 
            upload_id.len, upload_id.data);
    } else {
        printf("Complete multipart upload from file failed\n");
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

    test_complete_multipart_upload();

    cos_http_io_deinitialize();

    return 0;
}
```

### Aborting a multipart upload

#### Description

This API is used to abort a multipart upload operation and delete the uploaded parts. When this API is called, a failure is returned for any request using the `Upload Parts` API.

#### Method prototype

```cpp
cos_status_t *cos_abort_multipart_upload(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         const cos_string_t *object, 
                                         cos_string_t *upload_id, 
                                         cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format: `BucketName-APPID` | String |
| object | Object name | String |
| upload_id | Upload task ID | String |
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
static char TEST_MULTIPART_OBJECT[] = "multipart.dat";

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

void abort_multipart_upload()
{
    cos_pool_t *p = NULL;
    cos_string_t bucket;
    cos_string_t object;
    int is_cname = 0;
    cos_table_t *headers = NULL;
    cos_table_t *resp_headers = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t upload_id;
    cos_status_t *s = NULL;

    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    headers = cos_table_make(p, 1);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, TEST_MULTIPART_OBJECT);

    s = cos_init_multipart_upload(options, &bucket, &object, 
                                  &upload_id, headers, &resp_headers);

    if (cos_status_is_ok(s)) {
        printf("Init multipart upload succeeded, upload_id:%.*s\n", 
               upload_id.len, upload_id.data);
    } else {
        printf("Init multipart upload failed\n"); 
        cos_pool_destroy(p);
        return;
    }
    
    s = cos_abort_multipart_upload(options, &bucket, &object, &upload_id, 
                                   &resp_headers);

    if (cos_status_is_ok(s)) {
        printf("Abort multipart upload succeeded, upload_id::%.*s\n", 
               upload_id.len, upload_id.data);
    } else {
        printf("Abort multipart upload failed\n"); 
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

    abort_multipart_upload();

    cos_http_io_deinitialize();

    return 0;
}
```