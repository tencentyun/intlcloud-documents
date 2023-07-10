## Overview

This document provides an overview of APIs and SDK code samples related to object copy and movement.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying attributes) | Copies an object to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes a specified object from a bucket. |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part. |


## Simple Copy

### Copying an object (modifying attributes)

#### Description

This API is used to copy an object to a destination path. You can also use this API to modify object attributes such as storage class.

#### Method prototype

```cpp
cos_status_t *cos_copy_object(const cos_request_options_t *options,
                              const cos_string_t *src_bucket,
                              const cos_string_t *src_object,
                              const cos_string_t *src_endpoint,
                              const cos_string_t *dest_bucket, 
                              const cos_string_t *dest_object,
                              cos_table_t *headers,
                              cos_copy_object_params_t *copy_object_param,
                              cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| src_bucket        | Source bucket                       | String |
| src_object        | Name of the source object                   | String |
| src_endpoint      | Endpoint of the source object          | String |
| dest_bucket | Name of the destination bucket name in the format of `BucketName-APPID` | String |
| dest_object | Name of the destination object | String |
| headers | Headers attached to the COS request | Struct |
| copy_object_param | Parameters of the `Put Object Copy` operation | Struct |
| etag | Returns the MD5 checksum of the file                                          | String |
| last_modify | Returns the time the file was last modified in GMT format | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample 1. Copying an object

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
static char TEST_OBJECT_NAME2[] = "test2.dat";

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

void test_copy()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t src_bucket;
    cos_string_t src_object;
    cos_string_t src_endpoint;
    cos_table_t *resp_headers = NULL;

    // Create a memory pool
    cos_pool_create(&p, NULL);

    // Initialize the request options
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Set object replication
    cos_str_set(&object, TEST_OBJECT_NAME2);
    cos_str_set(&src_bucket, TEST_BUCKET_NAME);
    cos_str_set(&src_endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&src_object, TEST_OBJECT_NAME1);

    cos_copy_object_params_t *params = NULL;
    params = cos_create_copy_object_params(p);
    s = cos_copy_object(options, &src_bucket, &src_object, &src_endpoint, &bucket, &object, NULL, params, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put object copy succeeded\n");
    } else {
        printf("put object copy failed\n");
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

    test_copy();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Sample 2. Modifying storage class

>!You can change STANDARD to STANDARD_IA, INTELLIGENT TIERING, ARCHIVE, or DEEP ARCHIVE. To modify ARCHIVE or DEEP ARCHIVE to other storage classes, you need to call `cos_post_object_restore()` to restore objects in ARCHIVE or DEEP ARCHIVE first before calling this API. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).


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

void test_modify_storage_class()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t src_bucket;
    cos_string_t src_object;
    cos_string_t src_endpoint;
    cos_table_t *resp_headers = NULL;
   
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, TEST_OBJECT_NAME1);
    cos_str_set(&src_bucket, TEST_BUCKET_NAME);
    cos_str_set(&src_endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&src_object, TEST_OBJECT_NAME1);

    // Set the `x-cos-metadata-directive` and `x-cos-storage-class` headers and replace the storage class with the desired storage class.
    cos_table_t *headers = cos_table_make(p, 2);
    apr_table_add(headers, "x-cos-metadata-directive", "Replaced");
    // Valid storage classes are NTELLIGENT_TIERING, MAZ_INTELLIGENT_TIERING, STANDARD_IA, ARCHIVE, and DEEP_ARCHIVE.
    apr_table_add(headers, "x-cos-storage-class", "ARCHIVE");

    cos_copy_object_params_t *params = NULL;
    params = cos_create_copy_object_params(p);
    s = cos_copy_object(options, &src_bucket, &src_object, &src_endpoint, &bucket, &object, headers, params, &resp_headers);
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

    test_modify_storage_class();

    cos_http_io_deinitialize();

    return 0;
}
```

## Multipart Copy

### Copying an object part

#### Description

This API is used to copy a part of an object.

#### Method prototype

```cpp
cos_status_t *cos_upload_part_copy(const cos_request_options_t *options,
                                   cos_upload_part_copy_params_t *params, 
                                   cos_table_t *headers, 
                                   cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| params | Parameters for the `Upload Part - Copy` operation | Struct |
| copy_source | Source file path | String |
| dest_bucket | Name of the destination bucket in the format of `BucketName-APPID` | String |
| dest_object | Name of the destination object                                            | String |
| upload_id | Upload task ID | String |
| part_num | Part number | Int |
| range_start | The starting offset of the source file | Int |
| range_end | The ending offset of the source file | Int |
| rsp_content  | The response of the `Upload Part - Copy` operation | Struct |
| etag | Returns the MD5 checksum of the file                                          | String |
| last_modify | Returns the time the file was last modified in GMT format | String |
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
#include <sys/stat.h>

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

void make_rand_string(cos_pool_t *p, int len, cos_string_t *data)
{
    char *str = NULL;
    int i = 0;
    str = (char *)cos_palloc(p, len + 1);
    for ( ; i < len; i++) {
        str[i] = 'a' + rand() % 32;
    }
    str[len] = '\0';
    cos_str_set(data, str);
}

unsigned long get_file_size(const char *file_path)
{
    unsigned long filesize = -1; 
    struct stat statbuff;

    if(stat(file_path, &statbuff) < 0){
        return filesize;
    } else {
        filesize = statbuff.st_size;
    }

    return filesize;
}

void test_part_copy()
{
    cos_pool_t *p = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t file;
    int is_cname = 0;
    cos_string_t upload_id;
    cos_list_upload_part_params_t *list_upload_part_params = NULL;
    cos_upload_part_copy_params_t *upload_part_copy_params1 = NULL;
    cos_upload_part_copy_params_t *upload_part_copy_params2 = NULL;
    cos_table_t *headers = NULL;
    cos_table_t *query_params = NULL;
    cos_table_t *resp_headers = NULL;
    cos_table_t *list_part_resp_headers = NULL;
    cos_list_t complete_part_list;
    cos_list_part_content_t *part_content = NULL;
    cos_complete_part_content_t *complete_content = NULL;
    cos_table_t *complete_resp_headers = NULL;
    cos_status_t *s = NULL;
    int part1 = 1;
    int part2 = 2;
    char *local_filename = "test_upload_part_copy.file";
    char *download_filename = "test_upload_part_copy.file.download";
    char *source_object_name = "cos_test_upload_part_copy_source_object";
    char *dest_object_name = "cos_test_upload_part_copy_dest_object";
    FILE *fd = NULL;
    cos_string_t download_file;
    cos_string_t dest_bucket;
    cos_string_t dest_object;
    int64_t range_start1 = 0;
    int64_t range_end1 = 6000000;
    int64_t range_start2 = 6000001;
    int64_t range_end2;
    cos_string_t data;

    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);

    // create multipart upload local file    
    make_rand_string(p, 10 * 1024 * 1024, &data);
    fd = fopen(local_filename, "w");
    fwrite(data.data, sizeof(data.data[0]), data.len, fd);
    fclose(fd);    

    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, source_object_name);
    cos_str_set(&file, local_filename);
    s = cos_put_object_from_file(options, &bucket, &object, &file, NULL, &resp_headers);
    log_status(s);

    // Initialize multipart upload
    cos_str_set(&object, dest_object_name);
    s = cos_init_multipart_upload(options, &bucket, &object, 
                                  &upload_id, NULL, &resp_headers);
    log_status(s);

    // Upload part copy 1
    upload_part_copy_params1 = cos_create_upload_part_copy_params(p);
    cos_str_set(&upload_part_copy_params1->copy_source, "bucket-appid.cn-south.myqcloud.com/cos_test_upload_part_copy_source_object");
    cos_str_set(&upload_part_copy_params1->dest_bucket, TEST_BUCKET_NAME);
    cos_str_set(&upload_part_copy_params1->dest_object, dest_object_name);
    cos_str_set(&upload_part_copy_params1->upload_id, upload_id.data);
    upload_part_copy_params1->part_num = part1;
    upload_part_copy_params1->range_start = range_start1;
    upload_part_copy_params1->range_end = range_end1;
    headers = cos_table_make(p, 0);
    s = cos_upload_part_copy(options, upload_part_copy_params1, headers, &resp_headers);
    log_status(s);
    printf("last modified:%s, etag:%s\n", upload_part_copy_params1->rsp_content->last_modify.data, upload_part_copy_params1->rsp_content->etag.data);

    // Upload part copy 2
    resp_headers = NULL;
    range_end2 = get_file_size(local_filename) - 1;
    upload_part_copy_params2 = cos_create_upload_part_copy_params(p);
    cos_str_set(&upload_part_copy_params2->copy_source, "bucket-appid.cn-south.myqcloud.com/cos_test_upload_part_copy_source_object");
    cos_str_set(&upload_part_copy_params2->dest_bucket, TEST_BUCKET_NAME);
    cos_str_set(&upload_part_copy_params2->dest_object, dest_object_name);
    cos_str_set(&upload_part_copy_params2->upload_id, upload_id.data);
    upload_part_copy_params2->part_num = part2;
    upload_part_copy_params2->range_start = range_start2;
    upload_part_copy_params2->range_end = range_end2;
    headers = cos_table_make(p, 0);
    s = cos_upload_part_copy(options, upload_part_copy_params2, headers, &resp_headers);
    log_status(s);
    printf("last modified:%s, etag:%s\n", upload_part_copy_params1->rsp_content->last_modify.data, upload_part_copy_params1->rsp_content->etag.data);

    // List parts
    list_upload_part_params = cos_create_list_upload_part_params(p);
    list_upload_part_params->max_ret = 10;
    cos_list_init(&complete_part_list);
        
    cos_str_set(&dest_bucket, TEST_BUCKET_NAME);
    cos_str_set(&dest_object, dest_object_name);
    s = cos_list_upload_part(options, &dest_bucket, &dest_object, &upload_id, 
                             list_upload_part_params, &list_part_resp_headers);
    log_status(s);
    cos_list_for_each_entry(cos_list_part_content_t, part_content, &list_upload_part_params->part_list, node) {
        complete_content = cos_create_complete_part_content(p);
        cos_str_set(&complete_content->part_number, part_content->part_number.data);
        cos_str_set(&complete_content->etag, part_content->etag.data);
        cos_list_add_tail(&complete_content->node, &complete_part_list);
    }
     
    // Complete multipart upload
    headers = cos_table_make(p, 0);
    s = cos_complete_multipart_upload(options, &dest_bucket, &dest_object, 
            &upload_id, &complete_part_list, headers, &complete_resp_headers);
    log_status(s);
    
    // Check whether the upload copy part content is equal to the local file
    headers = cos_table_make(p, 0);
    cos_str_set(&download_file, download_filename);
    s = cos_get_object_to_file(options, &dest_bucket, &dest_object, headers, 
                               query_params, &download_file, &resp_headers);
    log_status(s);
    printf("local file len = %"APR_INT64_T_FMT", download file len = %"APR_INT64_T_FMT, get_file_size(local_filename), get_file_size(download_filename));
    remove(download_filename);
    remove(local_filename);
    cos_pool_destroy(p);

    printf("test part copy ok\n");
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

    test_part_copy();

    cos_http_io_deinitialize();

    return 0;
}
```


## Moving an Object

### Moving an object

#### Description

Object movement involves copying the source object to the target location and deleting the source object.

Since COS uses the bucket name (`Bucket`) and object key (`ObjectKey`) to identify objects, moving an object will change the object identifier. Currently, COS’s C SDK does not provide a standalone API to change object identifiers. However, you can still move the object with a combination of basic operations (**object copy** and **object delete**).

- [Copying an object](#.E8.AE.BE.E7.BD.AE.E5.AF.B9.E8.B1.A1.E5.A4.8D.E5.88.B6.EF.BC.88.E4.BF.AE.E6.94.B9.E5.B1.9E.E6.80.A7.EF.BC.89)
- [Deleting an object](#.E5.88.A0.E9.99.A4.E5.8D.95.E4.B8.AA.E5.AF.B9.E8.B1.A1)

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
static char TEST_OBJECT_NAME2[] = "test2.dat";

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

void test_move()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t src_object;
    cos_string_t src_endpoint;
    cos_table_t *resp_headers = NULL;

    // Create a memory pool
    cos_pool_create(&p, NULL);
    
    // Initialize the request options
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    
    // Set object replication
    cos_str_set(&object, TEST_OBJECT_NAME1);
    cos_str_set(&src_endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&src_object, TEST_OBJECT_NAME2);
    
    cos_copy_object_params_t *params = NULL;
    params = cos_create_copy_object_params(p);
    s = cos_copy_object(options, &bucket, &src_object, &src_endpoint, &bucket, &object, NULL, params, &resp_headers);
    log_status(s);
    if (cos_status_is_ok(s)) {
        s = cos_delete_object(options, &bucket, &src_object, &resp_headers);
        log_status(s);
        printf("move object succeeded\n");
    } else {
        printf("move object failed\n");
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

    test_move();

    cos_http_io_deinitialize();

    return 0;
}
```