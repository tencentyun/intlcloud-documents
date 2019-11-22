## Overview

This document provides an overview of APIs related to simple object operations, multipart upload, and other operations and corresponding SDK sample code.

**Simple operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/30614) | Querying object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Simply uploading an object | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies a file to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes the specified object in a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes objects in a bucket in batches |

**Multipart upload operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload task |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Retrieves an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple Operations

### Querying Object List

#### Feature Description

This API is used to query some or all objects in a bucket.

#### Method Prototype

```cpp
cos_status_t *cos_list_object(const cos_request_options_t *options,
                              const cos_string_t *bucket, 
                              cos_list_object_params_t *params, 
                              cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------- |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| params | Listing operation parameter information | Struct  |
| encoding_type | Specifies the encoding method of the return value | String |
| prefix | Prefix match, used to specify the prefix address of the file returned | String |
| marker | By default, entries are listed in UTF-8 binary order, and the entry list starts at marker | String |
| delimiter | Query delimiter used to group object keys | String |
| max_ret | Maximum number of entries returned at a time; 1,000 by default | Struct |
| truncated | Whether returned entries are truncated; value range: true, false | Boolean |
| next_marker | If the returned entries are truncated, then NextMarker is the starting point of the next entry | String |
| object_list | Object information list returned by the GET Bucket operation | Struct |
| key | Name of the object returned by the GET Bucket operation | Struct |
| last_modified | Last modified time of the object returned by the GET Bucket operation | Struct |
| etag | SHA-1 checksum of the object returned by the GET Bucket operation | Struct |
| size | Size of the object returned by the GET Bucket operation in bytes | Struct |
| owner_id | Owner UID of the object returned by the GET Bucket operation | Struct |
| storage_class | Storage class of the object returned by the GET Bucket operation | Struct |
| common_prefix_list | The identical paths between prefix and delimiter are grouped into one class and defined as a common prefix | Struct |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
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
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Get the object list
cos_list_object_params_t *list_params = NULL;
cos_list_object_content_t *content = NULL;
list_params = cos_create_list_object_params(p);
s = cos_list_object(options, &bucket, list_params, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("list object succeeded\n");
    cos_list_for_each_entry(cos_list_object_content_t, content, &list_params->object_list, node) {
        key = printf("%.*s\n", content->key.len, content->key.data);
    }
} else {
    printf("list object failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Simply Uploading an Object

#### Feature Description

This API is used to upload an object to a bucket.

#### Method Prototype

```cpp
cos_status_t *cos_put_object_from_file(const cos_request_options_t *options,
                                       const cos_string_t *bucket, 
                                       const cos_string_t *object, 
                                       const cos_string_t *filename,
                                       cos_table_t *headers, 
                                       cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Object name | String |
| filename | Local filename of the object | String |
| headers | Additional headers of the COS request | Struct |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
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
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Upload the object
cos_str_set(&file, TEST_DOWNLOAD_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_put_object_from_file(options, &bucket, &object, &file, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("put object succeeded\n");
} else {
    printf("put object failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Querying Object Metadata

#### Feature Description

This API is used to query object metadata.

#### Method Prototype

```cpp
cos_status_t *cos_head_object(const cos_request_options_t *options, 
                              const cos_string_t *bucket, 
                              const cos_string_t *object,
                              cos_table_t *headers, 
                              cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Object name | String |
| headers | Additional headers of the COS request | Struct |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

// Create a memory pool
cos_pool_create(&p, NULL);

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Get the object metadata
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_head_object(options, &bucket, &object, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("head object succeeded\n");
} else {
    printf("head object failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Downloading an Object

#### Feature Description

This API is used to download an object to the local file system. This operation requires you to have permission to read the target object or the target object to be public-read.

#### Method Prototype

```cpp
cos_status_t *cos_get_object_to_file(const cos_request_options_t *options,
                                     const cos_string_t *bucket, 
                                     const cos_string_t *object,
                                     cos_table_t *headers, 
                                     cos_table_t *params,
                                     cos_string_t *filename, 
                                     cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Object name | String |
| headers | Additional headers of the COS request | Struct |
| params | Operation parameters of the COS request | Struct |
| filename | Local filename of the object | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
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
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Get an object
cos_str_set(&file, TEST_DOWNLOAD_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_get_object_to_file(options, &bucket, &object, NULL, NULL, &file, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("get object succeeded\n");
} else {
    printf("get object failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Setting Object Replication

#### Feature Description

This API is used to copy a file to the destination path.

#### Method Prototype

```cpp
cos_status_t *cos_copy_object(const cos_request_options_t *options,
                              const cos_string_t *copy_source, 
                              const cos_string_t *dest_bucket, 
                              const cos_string_t *dest_object,
                              cos_table_t *headers,
                              cos_copy_object_params_t *copy_object_param,
                              cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| copy_source | Path to the source file | String |
| dest_bucket | Name of the destination bucket, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Name of the destination object | String |
| headers | Additional headers of the COS request | Struct |
| copy_object_param | Parameters of the Put Object Copy operation | Struct |
| etag | MD5 checksum of the returned file | String |
| last_modify | Returns the last modified time of the file in GMT time | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

// Create a memory pool
cos_pool_create(&p, NULL);

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Set object replication
cos_str_set(&object, TEST_OBJECT_NAME);
cos_string_t copy_source;
cos_str_set(&copy_source, TEST_COPY_SRC);
cos_copy_object_params_t *params = NULL;
params = cos_create_copy_object_params(p);
s = cos_copy_object(options, &copy_source, &bucket, &object, NULL, params, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("put object copy succeeded\n");
} else {
    printf("put object copy failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p);  
```

### Deleting a Single Object

#### Feature Description

This API is used to delete the specified object in a bucket.

#### Method Prototype

```cpp
cos_status_t *cos_delete_object(const cos_request_options_t *options,
                                const cos_string_t *bucket, 
                                const cos_string_t *object, 
                                cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Object name | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

// Create a memory pool
cos_pool_create(&p, NULL);

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Deleting a single object
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_delete_object(options, &bucket, &object, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("delete object succeeded\n");
} else {
    printf("delete object failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 

```

### Deleting Multiple Objects

#### Feature Description

This API is used to delete objects in a bucket in batches. It can delete up to 1,000 objects in a single operation. For the return result, COS provides two result modes: Verbose and Quiet. Verbose mode returns the deletion result for each object; while Quiet mode only returns the information of objects for which errors are reported.

#### Method Prototype

```cpp
cos_status_t *cos_delete_objects(const cos_request_options_t *options,
                                 const cos_string_t *bucket, 
                                 cos_list_t *object_list, 
                                 int is_quiet,
                                 cos_table_t **resp_headers, 
                                 cos_list_t *deleted_object_list);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------------- | ------------------------------------------------------------ | ------- |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object_list | List of objects to be deleted | Struct |
| key | Name of the object to be deleted | String |
| is_quiet | Specifies whether to enable Quiet mode <br>True(1): Enable Quiet mode; False(0): Enable Verbose mode. The default value is False(0) | Boolean |
| resp_headers | Header of the returned HTTP response message | Struct |
| deleted_object_list | Information list of deleted objects | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

// Create a memory pool
cos_pool_create(&p, NULL);

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Set batch object deletion
char *object_name1 = TEST_OBJECT_NAME1;
char *object_name2 = TEST_OBJECT_NAME2;
cos_object_key_t *content1 = NULL;
cos_object_key_t *content2 = NULL;
cos_list_t object_list;
cos_list_t deleted_object_list;
cos_list_init(&object_list);
cos_list_init(&deleted_object_list);
content1 = cos_create_cos_object_key(p);
cos_str_set(&content1->key, object_name1);
cos_list_add_tail(&content1->node, &object_list);
content2 = cos_create_cos_object_key(p);
cos_str_set(&content2->key, object_name2);
cos_list_add_tail(&content2->node, &object_list);

// Delete objects in batches
int is_quiet = COS_TRUE;
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_delete_objects(options, &bucket, &object_list, is_quiet, &resp_headers, &deleted_object_list);
if (cos_status_is_ok(s)) {
    printf("delete objects succeeded\n");
} else {
    printf("delete objects failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 

```

## Multipart Upload Operations

### Querying a Multipart Upload

#### Feature Description

This API is used to query the multipart uploads in progress. Up to 1,000 ones can be listed in one single operation.

#### Method Prototype

```cpp
cos_status_t *cos_list_multipart_upload(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        cos_list_multipart_upload_params_t *params, 
                                        cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| params | List Multipart Uploads operation parameters | Struct |
| encoding_type | Specifies the encoding method of the return value | String |
| prefix | Prefix match, used to specify the prefix address of the file returned | String |
| upload_id_marker | If the returned entries are truncated, then NextMarker is the starting point of the next entry | String |
| delimiter | The delimiter is a symbol. <br>If there is a prefix, the identical paths between prefix and delimiter are grouped into one class and defined as a common prefix, and then all common prefixes are listed. <br>If there is no prefix, it starts at the beginning of the path | String |
| max_ret | Maximum number of entries returned at a time; 1,000 by default | String |
| key_marker | Used together with upload-id-marker. <br>If upload-id-marker is not specified, only the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included in the list; <br>otherwise, the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included, and any multipart uploads with ObjectNames equal to the key-marker will also be included, provided that they have UploadIDs lexicographically greater than the specified upload-id-marker | String |
| upload_id_marker | Used together with key-marker. <br>If key-marker is not specified, upload-id-marker will be ignored; <br>otherwise, the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included in the list, and any multipart uploads with ObjectNames equal to the key-marker will also be included, provided that they have UploadIDs lexicographically greater than the specified upload-id-marker | String |
| truncated | Whether returned entries are truncated; value range: true, false | Boolean |
| next_key_marker | If the returned entries are truncated, then NextMarker is the starting point of the next entry | String |
| next_upload_id_marker | If the returned entries are truncated, then NextMarker is the starting point of the next entry | String |
| upload_list | Multipart upload information | Struct  |
| key | Object name | String |
| upload_id | Identifies the ID of this multipart upload | String |
| initiated | Indicates the start time of this multipart upload task | String |
| resp_headers | Header of the returned HTTP response message | Struct |

```
typedef struct {
    cos_list_t node;
    cos_string_t key;
    cos_string_t upload_id;
    cos_string_t initiated;
} cos_list_multipart_upload_content_t;
```

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
cos_pool_t *p = NULL;
cos_string_t bucket;
int is_cname = 0;
cos_table_t *resp_headers = NULL;
cos_request_options_t *options = NULL;
cos_status_t *s = NULL;
cos_list_multipart_upload_params_t *list_multipart_params = NULL;

// Create a memory pool and initialize the request options
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
init_test_request_options(options, is_cname);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Query multipart uploads
list_multipart_params = cos_create_list_multipart_upload_params(p);
list_multipart_params->max_ret = 999;
s = cos_list_multipart_upload(options, &bucket, list_multipart_params, &resp_headers);
log_status(s);

// Terminate the memory pool
cos_pool_destroy(p);

```

### Initializing a Multipart Upload

#### Feature Description

This API (Initiate Multipart Upload) is used to initialize a multipart upload. After the execution of this request, Upload ID will be returned for the subsequent Upload Part requests.

#### Method Prototype

```cpp
cos_status_t *cos_init_multipart_upload(const cos_request_options_t *options, 
                                        const cos_string_t *bucket, 
                                        const cos_string_t *object, 
                                        cos_string_t *upload_id, 
                                        cos_table_t *headers,
                                        cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Object name | String |
| upload_id | Upload ID returned by the operation | String |
| headers | Additional headers of the COS request | Struct |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
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
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Initialize a multipart upload
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_init_multipart_upload(options, &bucket, &object, 
                              &upload_id, headers, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("init multipart upload succeeded\n");
} else {
    printf("init multipart upload failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 

```

### Querying Uploaded Parts

#### Feature Description

This API is used to query uploaded parts in the specified multipart upload operation.

#### Method Prototype

```cpp
cos_status_t *cos_list_upload_part(const cos_request_options_t *options,
                                   const cos_string_t *bucket, 
                                   const cos_string_t *object, 
                                   const cos_string_t *upload_id, 
                                   cos_list_upload_part_params_t *params,
                                   cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ----------------------- | ------------------------------------------------------------ | ------- |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Object name | String |
| upload_id | Upload task number | String |
| params | List Parts operation parameters | Struct |
| part_number_marker | By default, entries are listed in UTF-8 binary order, and the entry list starts at marker | String |
| encoding_type | Specifies the encoding method of the return value | String |
| max_ret | Maximum number of entries returned at a time; 1,000 by default | String |
| truncated | Whether returned entries are truncated; value range: true, false | Boolean |
| next_part_number_marker | If the returned entries are truncated, then NextMarker is the starting point of the next entry | String |
| part_list | Information of completed parts | Struct  |
| part_number | Part number | String |
| size | Part size in bytes | String |
| etag | SHA-1 checksum of the part | String |
| last_modified | Last modified time of the part | String  |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;
cos_list_part_content_t *part_content = NULL;
cos_complete_part_content_t *complete_part_content = NULL;
int part_num = 1;
int64_t pos = 0;
int64_t file_length = 0;

// Create a memory pool
cos_pool_create(&p, NULL);

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Query uploaded parts
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
                                  &complete_part_list, complete_headers, &resp_headers);

if (cos_status_is_ok(s)) {
    printf("Complete multipart upload from file succeeded, upload_id:%.*s\n", 
           upload_id.len, upload_id.data);
} else {
    printf("Complete multipart upload from file failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Uploading Parts

#### Feature Description

This API is used to upload parts after a multipart upload is initialized. It can upload 1-10,000 parts of 1 MB to 5 GB in size. Each time you request the Upload Part API, you need to pass in the partNumber (which is the part number) and uploadId parameters. Out-of-order uploading is supported.

#### Method Prototype

```cpp
cos_status_t *cos_upload_part_from_file(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        const cos_string_t *object,
                                        const cos_string_t *upload_id, 
                                        int part_num, 
                                        cos_upload_file_t *upload_file,
                                        cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Object name | String |
| upload_id | Upload task number | String |
| part_num | Part number | Int |
| upload_file | Information of the local file to be uploaded | Struct |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;
int part_num = 1;
int64_t pos = 0;
int64_t file_length = 0;

// Create a memory pool
cos_pool_create(&p, NULL);

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Upload parts
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

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Copying Parts

#### Feature Description

This API is used to copy an object as a part.

#### Method Prototype

```cpp
cos_status_t *cos_upload_part_copy(const cos_request_options_t *options,
                                   cos_upload_part_copy_params_t *params, 
                                   cos_table_t *headers, 
                                   cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| params | Parameter information of the copied parts | Struct  |
| copy_source | Path to the source file | String |
| dest_bucket | Name of the destination bucket, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Name of the destination object | String |
| upload_id | Upload task number | String |
| part_num | Part number | Int |
| range_start | Source file start offset | Int |
| range_end | Source file end offset | Int |
| rsp_content | Result information of the multipart copy | Struct |
| etag | MD5 checksum of the returned file | String |
| last_modify | Returns the last modified time of the file in GMT time | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
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

// Create a random local file of 10 MB    
make_rand_string(p, 10 * 1024 * 1024, &data);
fd = fopen(local_filename, "w");
fwrite(data.data, sizeof(data.data[0]), data.len, fd);
fclose(fd);    

// Use a local file to upload an object
init_test_request_options(options, is_cname);
cos_str_set(&bucket, "source-1253666666");
cos_str_set(&object, "cos_test_upload_part_copy_source_object");
cos_str_set(&file, local_filename);
s = cos_put_object_from_file(options, &bucket, &object, &file, NULL, &resp_headers);
log_status(s);

// Initialize a multipart upload
cos_str_set(&object, dest_object_name);
s = cos_init_multipart_upload(options, &bucket, &object, 
                              &upload_id, NULL, &resp_headers);
log_status(s);

// Use an uploaded object to copy part 1
upload_part_copy_params1 = cos_create_upload_part_copy_params(p);
cos_str_set(&upload_part_copy_params1->copy_source, "mybucket-1253666666.cn-south.myqcloud.com/cos_test_upload_part_copy_source_object");
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

// Use an uploaded object to copy part 2
resp_headers = NULL;
range_end2 = get_file_size(local_filename) - 1;
upload_part_copy_params2 = cos_create_upload_part_copy_params(p);
cos_str_set(&upload_part_copy_params2->copy_source, "mybucket-1253666666.cn-south.myqcloud.com/cos_test_upload_part_copy_source_object");
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

// List the uploaded objects
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

// Complete the multipart upload
headers = cos_table_make(p, 0);
s = cos_complete_multipart_upload(options, &dest_bucket, &dest_object, 
                                  &upload_id, &complete_part_list, headers, &complete_resp_headers);
log_status(s);

// Check whether the object generated by the multipart copy matches the local file
headers = cos_table_make(p, 0);
cos_str_set(&download_file, download_filename);
s = cos_get_object_to_file(options, &dest_bucket, &dest_object, headers, 
                           query_params, &download_file, &resp_headers);
log_status(s);
printf("local file len = %"APR_INT64_T_FMT", download file len = %"APR_INT64_T_FMT, get_file_size(local_filename), get_file_size(download_filename));
remove(download_filename);
remove(local_filename);

// Terminate the memory pool
cos_pool_destroy(p);    

```

### Completing a Multipart Upload

#### Feature Description

This API is used to complete the entire multipart upload. After all parts are uploaded using the Upload Parts API, this API can be called to complete the upload. When using this API, you must specify the PartNumber and ETag of each part in the request body to verify the accuracy of parts.

#### Method Prototype

```cpp
cos_status_t *cos_complete_multipart_upload(const cos_request_options_t *options,
                                            const cos_string_t *bucket, 
                                            const cos_string_t *object, 
                                            const cos_string_t *upload_id, 
                                            cos_list_t *part_list, 
                                            cos_table_t *headers,
                                            cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Object name | String |
| upload_id | Upload task number | String |
| part_list | Parameter of the completed multipart upload | Struct  |
| part_number | Part number | String |
| etag | ETag value of a part, which is an SHA1 checksum. You need to add double quotation marks before and after the checksum, such as "3a0f1fd698c235af9cf098cb74aa25bc" | String |
| headers | Additional headers of the COS request | Struct |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;
cos_list_part_content_t *part_content = NULL;
cos_complete_part_content_t *complete_part_content = NULL;
int part_num = 1;
int64_t pos = 0;
int64_t file_length = 0;

// Create a memory pool
cos_pool_create(&p, NULL);

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Query uploaded parts
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
                                  &complete_part_list, complete_headers, &resp_headers);

if (cos_status_is_ok(s)) {
    printf("Complete multipart upload from file succeeded, upload_id:%.*s\n", 
           upload_id.len, upload_id.data);
} else {
    printf("Complete multipart upload from file failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Aborting a Multipart Upload

#### Feature Description

This API is used to abort a multipart upload operation and delete the uploaded parts. When you call this API, if there is a request that is uploading a part using the Upload Parts API, the request will fail.

#### Method Prototype

```cpp
cos_status_t *cos_abort_multipart_upload(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         const cos_string_t *object, 
                                         cos_string_t *upload_id, 
                                         cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Object name | String |
| upload_id | Upload task number | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
cos_pool_t *p = NULL;
cos_string_t bucket;
cos_string_t object;
int is_cname = 0;
cos_table_t *headers = NULL;
cos_table_t *resp_headers = NULL;
cos_request_options_t *options = NULL;
cos_string_t upload_id;
cos_status_t *s = NULL;

// Create a memory pool and initialize the request options
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
init_test_request_options(options, is_cname);
headers = cos_table_make(p, 1);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, TEST_MULTIPART_OBJECT);

// Initialize a multipart upload
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

// Abort a multipart upload
s = cos_abort_multipart_upload(options, &bucket, &object, &upload_id, 
                               &resp_headers);

if (cos_status_is_ok(s)) {
    printf("Abort multipart upload succeeded, upload_id::%.*s\n", 
           upload_id.len, upload_id.data);
} else {
    printf("Abort multipart upload failed\n"); 
}    

// Terminate the memory pool
cos_pool_destroy(p);
```

## Other Operations

### Restoring an Archived Object

#### Feature Description

This API is used to retrieve an archived object for access.

#### Method Prototype

```cpp
cos_status_t *cos_post_object_restore(const cos_request_options_t *options,
                                      const cos_string_t *bucket, 
                                      const cos_string_t *object,
                                      cos_object_restore_params_t *restore_params,
                                      cos_table_t *headers,
                                      cos_table_t *params,
                                      cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Object name | String |
| restore_params | Post Object Restore operation parameters | Struct |
| days | The temporary copy expiration time set by the Post Object Restore operation | Int |
| tier | SetTier | The restoration type supported by CAS specified by the Post Object Restore operation, including Expedited, Standard, and Bulk | String |
| headers | Additional headers of the COS request | Struct |
| params | Operation parameters of the COS request | Struct |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

// Create a memory pool
cos_pool_create(&p, NULL);

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);

// Restore an archived object
cos_object_restore_params_t *restore_params = cos_create_object_restore_params(p);
restore_params->days = 30;
cos_str_set(&restore_params->tier, "Standard");
s = cos_post_object_restore(options, &bucket, &object, restore_params, NULL, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("post object restore succeeded\n");
} else {
    printf("post object restore failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Setting Object ACL

#### Feature Description

This API is used to set the ACL for the specified object in a bucket.

#### Method Prototype

```cpp
cos_status_t *cos_put_object_acl(const cos_request_options_t *options, 
                                 const cos_string_t *bucket,
                                 const cos_string_t *object,  
                                 cos_acl_e cos_acl,
                                 const cos_string_t *grant_read,
                                 const cos_string_t *grant_write,
                                 const cos_string_t *grant_full_ctrl,
                                 cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| --------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Object name | String |
| cos_acl | Allows user to customize permissions. Value range: COS_ACL_PRIVATE(0), COS_ACL_PUBLIC_READ(1) <br>Default value: COS_ACL_PRIVATE(0) | Enum   |
| grant_read | Grants read permission | String |
| grant_write | Grants write permission | String |
| grant_full_ctrl | Grants read/write permission | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

// Create a memory pool
cos_pool_create(&p, NULL);

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Set the object ACL
cos_str_set(&object, TEST_OBJECT_NAME);
cos_string_t read;
cos_str_set(&read, "id=\"qcs::cam::uin/12345:uin/12345\", id=\"qcs::cam::uin/45678:uin/45678\"");
s = cos_put_object_acl(options, &bucket, &object, cos_acl, &read, NULL, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("put object acl succeeded\n");
} else {
    printf("put object acl failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p);  
```

### Querying Object ACL

#### Feature Description

This API is used to query the ACL of an object.

#### Method Prototype

```cpp
cos_status_t *cos_get_object_acl(const cos_request_options_t *options, 
                                 const cos_string_t *bucket,
                                 const cos_string_t *object,
                                 cos_acl_params_t *acl_param, 
                                 cos_table_t **resp_headers)
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Object name | String |
| acl_param | Request operation parameter | Struct |
| owner_id | Bucket owner ID returned by the request operation | String |
| owner_name | Bucket owner name returned by the request operation | String |
| object_list | Information of the grantee and permission returned by the request operation | Struct |
| type | Grantee account type returned by the request operation | String |
| id | Grantee ID returned by the request operation | String |
| name | Grantee name returned by the request operation | String |
| permission | Information of the grantee permission returned by the request operation | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Examples

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

// Create a memory pool
cos_pool_create(&p, NULL);

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Get the object ACL
cos_acl_params_t *acl_params2 = NULL;
acl_params2 = cos_create_acl_params(p);
s = cos_get_object_acl(options, &bucket, &object, acl_params2, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("get object acl succeeded\n");
    printf("acl owner id:%s, name:%s\n", acl_params2->owner_id.data, acl_params2->owner_name.data);
    acl_content = NULL;
    cos_list_for_each_entry(cos_acl_grantee_content_t, acl_content, &acl_params2->grantee_list, node) {
        printf("acl grantee id:%s, name:%s, permission:%s\n", acl_content->id.data, acl_content->name.data, acl_content->permission.data);
    }
} else {
    printf("get object acl failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```
