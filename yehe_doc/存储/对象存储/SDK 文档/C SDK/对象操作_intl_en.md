## Overview

This document provides an overview of APIs and SDK sample codes related to simple, multipart, and other operations on objects.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/7734) | Querying object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies a file to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects in a single request |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload task |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple Operations

### Querying object list

#### Feature

This API (GET Bucket (List Object)) is used to query some or all objects in a bucket.

#### Method prototype

```cpp
cos_status_t *cos_list_object(const cos_request_options_t *options,
                              const cos_string_t *bucket, 
                              cos_list_object_params_t *params, 
                              cos_table_t **resp_headers);
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------- |
| options            | COS request options                                               | Struct  |
| Bucket | Bucket name in the format of `BucketName-APPID` | String |
| params             | Parameters for the List Objects operation                                          | Struct  |
| encoding_type | Specifies the encoding type of the returned value | String |
| prefix | Prefix to be matched, which specifies the address prefix of the files to be returned | String |
| marker  | By default, entries are listed in UTF-8 binary order starting from this `marker` | String |
| delimiter          | A separator for query, used to group object keys                             | String  |
| max_ret            | The maximum number of returned entries per request. Default: 1000                             | Struct  |
| truncated  |  Indicates whether the returned entry is truncated. Valid value: `true` or `false` | Boolean|
| next_marker        | Marks the start of the next entry if the returned entry is truncated  | String  |
| object_list        | The object list returned by Get Bucket                             | Struct  |
| key                | The key of the object returned by Get Bucket                           | Struct  |
| last_modified      | The last modified time of the object returned by Get Bucket                     | Struct  |
| etag               | SHA-1 check value of the object returned by Get Bucket                 | Struct  |
| size               | The size in bytes of the object returned by Get Bucket                      | Struct  |
| owner_id           | UID of the object owner returned by Get Bucket                      | Struct  |
| storage_class      | The storage class of the object returned by Get Bucket                             | Struct  |
| common_prefix_list | The identical paths between `Prefix` and `delimiter` are grouped together and defined as Common Prefix | Struct |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_table_t *resp_headers = NULL;

// Create a memory pool
cos_pool_create(&p, NULL);

// Initialize request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
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

// Destroy the memory pool
cos_pool_destroy(p); 
```

### Uploading an object using simple upload

#### Feature

This API (PUT Object) is used to upload an object up to 5 GB to a specified bucket. To upload objects larger than 5 GB, please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89).

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

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options            | COS request options                                               | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object       | Object name                                                  | String |
| filename     | The local filename of the object before being uploaded to COS    | String |
| headers      | Headers attached to the COS request                                             | Struct |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

// Initialize request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
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

//Destroy the memory pool
cos_pool_destroy(p); 
```

### Querying object metadata

#### Feature

This API (HEAD Object) is used to query object metadata.

#### Method prototype

```cpp
cos_status_t *cos_head_object(const cos_request_options_t *options, 
                              const cos_string_t *bucket, 
                              const cos_string_t *object,
                              cos_table_t *headers, 
                              cos_table_t **resp_headers);
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options            | COS request options                                               | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object       | Object name                                                  | String |
| headers      | Headers attached to the COS request                                             | Struct |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

// Initialize request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Get object metadata
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_head_object(options, &bucket, &object, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("put object succeeded\n");
} else {
    printf("put object failed\n");
}

//Destroy the memory pool
cos_pool_destroy(p); 
```

### Downloading an object

#### Feature

This API (GET Object) is used to download an object from COS. This operation requires that you have write access to the object, or the object open read access to all (public read).

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

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options            | COS request options                                               | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object       | Object name                                                  | String |
| headers      | Headers attached to the COS request                                             | Struct |
| params       | Parameters for a COS request operation                                             | Struct |
| filename     | The local filename of the object before being uploaded to COS    | String |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

// Initialize request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//Get an object
cos_str_set(&file, TEST_DOWNLOAD_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_get_object_to_file(options, &bucket, &object, NULL, NULL, &file, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("get object succeeded\n");
} else {
    printf("get object failed\n");
}

//Destroy the memory pool
cos_pool_destroy(p); 
```

### Setting object replication

#### Feature

This API (PUT Object - Copy) is used to copy a file to the destination path.

#### Method prototype

```cpp
cos_status_t *cos_copy_object(const cos_request_options_t *options,
                              const cos_string_t *copy_source, 
                              const cos_string_t *dest_bucket, 
                              const cos_string_t *dest_object,
                              cos_table_t *headers,
                              cos_copy_object_params_t *copy_object_param,
                              cos_table_t **resp_headers);
```

#### Parameter description

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| options            | COS request options                                               | Struct  |
| copy_source       | Source file path                                                  | String |
| dest_bucket | Name of the destination bucket. Format: `BucketName-APPID` | String |
| dest_object       | Name of the destination object                                            | String |
| headers      | Headers attached to the COS request                                             | Struct |
| copy_object_param | Parameters for Put Object Copy                                     | Struct |
| etag                                | Returns MD5 checksum of the file                                          | String      |
| last_modify| Returns the time in GMT when the file is last modified | String |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

// Initialize request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//Set object replication
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

//Destroy the memory pool
cos_pool_destroy(p);  
```

### Deleting a single object

#### Feature

This API (DELETE Object) deletes a specified object from the bucket.

#### Method prototype

```cpp
cos_status_t *cos_delete_object(const cos_request_options_t *options,
                                const cos_string_t *bucket, 
                                const cos_string_t *object, 
                                cos_table_t **resp_headers);
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options            | COS request options                                               | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object       | Object name                                                  | String |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

// Initialize request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//Delete a single object
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_delete_object(options, &bucket, &object, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("delete object succeeded\n");
} else {
    printf("delete object failed\n");
}

//Destroy the memory pool
cos_pool_destroy(p); 

```

### Deleting multiple objects

#### Feature

This API (DELETE Multiple Objects) is used to delete objects from a bucket in batches. It can delete up to 1,000 objects in a single request. For the response result, COS provides two modes: Verbose and Quiet. Verbose mode returns the deletion result for each object, while Quiet mode only returns the information of objects for which errors are reported.

#### Method prototype

```cpp
cos_status_t *cos_delete_objects(const cos_request_options_t *options,
                                 const cos_string_t *bucket, 
                                 cos_list_t *object_list, 
                                 int is_quiet,
                                 cos_table_t **resp_headers, 
                                 cos_list_t *deleted_object_list);
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------------- | ------------------------------------------------------------ | ------- |
| options            | COS request options                                               | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object_list         | The list of objects to delete                                         | Struct  |
| key | Name of the object to delete | String |
| is_quiet | Indicate whether the Quiet mode is enabled.<br>True(1): Quiet mode is enabled; False(0): Verbose mode is enabled. Default is False(0). | Boolean |
| resp_headers       | Returns HTTP response headers                                     | Struct  |
| deleted_object_list | The list of deleted objects                                          | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

// Initialize request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//Set multiple objects to delete
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

//Delete the multiple objects
int is_quiet = COS_TRUE;
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_delete_objects(options, &bucket, &object_list, is_quiet, &resp_headers, &deleted_object_list);
if (cos_status_is_ok(s)) {
    printf("delete objects succeeded\n");
} else {
    printf("delete objects failed\n");
}

//Destroy the memory pool
cos_pool_destroy(p); 

```

## Multipart Operations

### Querying multipart upload

#### Feature

This API (List Multipart Uploads) is used to query in-progress multipart uploads, which are up to 1,000 in a single request.

#### Method prototype

```cpp
cos_status_t *cos_list_multipart_upload(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        cos_list_multipart_upload_params_t *params, 
                                        cos_table_t **resp_headers);
```

#### Parameter description

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| options               | COS request options                                                 | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| params                | Parameters for List Multipart Uploads                              | Struct  |
| encoding_type | Specifies the encoding type of the returned value | String |
| prefix | Prefix to be matched, which specifies the address prefix of the files to be returned | String |
| next_marker | Marks the start of the next entry if the returned entry is truncated  | String  |
| delimiter | Delimiter is a sign.<br><li>If `Prefix` is provided, the same paths between `Prefix` and `delimiter` are grouped together and defined as Common Prefix, and then all common prefixes get listed.<br><li>If `Prefix` is not provided, the listing starts from the beginning of the path. | String |
| max_ret            | The maximum number of returned entries per request. Default: 1000                             | String  |
| key_marker | Used together with `upload-id-marker`.<br><li>If `upload-id-marker` is not specified, only the multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed;<br><li>If `upload-id-marker` is specified, the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed, and any multipart upload whose `ObjectName` lexicographically equals `key-marker` and whose `UploadID` is greater than `upload-id-marker` will also be listed. | String |
| upload_id_marker | Used together with `key-marker`.<br><li>If `key-marker` is not specified, `upload-id-marker` will be ignored; <br><li>If `key-marker` is specified, the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed, and any multipart upload whose `ObjectName` lexicographically equals `key-marker` and whose `UploadID` is greater than `upload-id-marker` will also be listed | String |
| truncated  |  Indicates whether the returned entry is truncated. Valid value: `true` or `false` | Boolean|
| next_key_marker       | Marks the start of the next entry if the returned entry is truncated   | String  |
| next_upload_id_marker | Marks the start of the next entry if the returned entry is truncated  | String  |
| upload_list           | Lists all multipart uploads                                              | Struct  |
| key | Object name | String |
| upload_id | Identifies the ID of this multipart upload | String |
| initiated             | Indicates when this multipart upload was initiated                               | String  |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

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

#### Samples

```cpp
cos_pool_t *p = NULL;
cos_string_t bucket;
int is_cname = 0;
cos_table_t *resp_headers = NULL;
cos_request_options_t *options = NULL;
cos_status_t *s = NULL;
cos_list_multipart_upload_params_t *list_multipart_params = NULL;

//Create a memory pool, and initialize request options
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
cos_str_set(&bucket, TEST_BUCKET_NAME);

//Query multipart uploads
list_multipart_params = cos_create_list_multipart_upload_params(p);
list_multipart_params->max_ret = 999;
s = cos_list_multipart_upload(options, &bucket, list_multipart_params, &resp_headers);
log_status(s);

//Destroy the memory pool
cos_pool_destroy(p);

```

### Initializing multipart upload

#### Feature

This API (Initiate Multipart Upload) is used to initialize multipart upload. After the request is executed successfully, Upload ID is returned for the subsequent Upload Part requests.

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

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options            | COS request options                                               | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object       | Object name                                                  | String |
| upload_id    | Returns ID of the multipart upload                                       | String |
| headers      | Headers attached to the COS request                                             | Struct |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

// Initialize request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//Initialize the multipart upload
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_init_multipart_upload(options, &bucket, &object, 
                              &upload_id, headers, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("init multipart upload succeeded\n");
} else {
    printf("init multipart upload failed\n");
}

//Destroy the memory pool
cos_pool_destroy(p); 
```



### Uploading parts

#### Feature

This API (Upload Part) is used to upload parts (possibly out of order) in an initiated multipart upload, with the number of parts between 1 to 10,000, and the size of each part between 1 MB and 5 GB. Each Upload Part request should include partNumber (number of the part) and uploadID.

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

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options            | COS request options                                               | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object       | Object name                                                  | String |
| upload_id | ID of the upload task | String |
| part_num     | Number of the part                                                     | Int    |
| upload_file  | Information about the file to upload                                           | Struct |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

// Initialize request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//Upload parts
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

//Destroy the memory pool
cos_pool_destroy(p); 
```

### Copying a part

#### Feature

This API (Upload Part - Copy) is used to copy an object as a part.

#### Method prototype

```cpp
cos_status_t *cos_upload_part_copy(const cos_request_options_t *options,
                                   cos_upload_part_copy_params_t *params, 
                                   cos_table_t *headers, 
                                   cos_table_t **resp_headers);
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options            | COS request options                                               | Struct  |
| params       | Parameters for Upload Part - Copy                                            | Struct |
| copy_source       | Source file path                                                  | String |
| dest_bucket | Name of the destination bucket. Format: `BucketName-APPID` | String |
| dest_object       | Name of the destination object                                            | String |
| upload_id | ID of the upload task | String |
| part_num     | Number of the part                                                     | Int    |
| range_start  | The starting offset of source file                                               | Int    |
| range_end    | The ending offset of source file                                                | Int    |
| rsp_content  | The response to Upload Part - Copy                                            | Struct |
| etag                                | Returns MD5 checksum of the file                                          | String      |
| last_modify| Returns the time in GMT when the file is last modified | String |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

//Create a random local file of 10 MB    
make_rand_string(p, 10 * 1024 * 1024, &data);
fd = fopen(local_filename, "w");
fwrite(data.data, sizeof(data.data[0]), data.len, fd);
fclose(fd);    

//Upload the local file as an object
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
cos_str_set(&bucket, "source-1253666666");
cos_str_set(&object, "cos_test_upload_part_copy_source_object");
cos_str_set(&file, local_filename);
s = cos_put_object_from_file(options, &bucket, &object, &file, NULL, &resp_headers);
log_status(s);

//Initialize the multipart upload
cos_str_set(&object, dest_object_name);
s = cos_init_multipart_upload(options, &bucket, &object, 
                              &upload_id, NULL, &resp_headers);
log_status(s);

//Copy an uploaded object as Part 1
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

//Copy an uploaded object as Part 2
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

//List the uploaded parts
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

//Complete the multipart upload
headers = cos_table_make(p, 0);
s = cos_complete_multipart_upload(options, &dest_bucket, &dest_object, 
                                  &upload_id, &complete_part_list, headers, &complete_resp_headers);
log_status(s);

//Check if the object uploaded using Upload Part - Copy matches the local file
headers = cos_table_make(p, 0);
cos_str_set(&download_file, download_filename);
s = cos_get_object_to_file(options, &dest_bucket, &dest_object, headers, 
                           query_params, &download_file, &resp_headers);
log_status(s);
printf("local file len = %"APR_INT64_T_FMT", download file len = %"APR_INT64_T_FMT, get_file_size(local_filename), get_file_size(download_filename));
remove(download_filename);
remove(local_filename);

//Destroy the memory pool
cos_pool_destroy(p);    
```



### Querying uploaded parts

#### Feature

This API (List Parts) is used to query the uploaded parts in a specified multipart upload.

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

| Parameter Name | Description | Type |
| ----------------------- | ------------------------------------------------------------ | ------- |
| options                 | COS request options                                                 | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object                  | Object name                                                | String  |
| upload_id | Upload task ID | String |
| params                  | Parameters for List Parts                                         | Struct  |
| part_number_marker | By default, entries are listed in UTF-8 binary order starting from this marker | String |
| encoding_type | Specifies the encoding type of the returned value | String |
| max_ret            | The maximum number of returned entries per request. Default: 1000                             | String  |
| truncated  |  Indicates whether the returned entry is truncated. Valid value: `true` or `false` | Boolean|
| next_part_number_marker        | Marks the start of the next entry if the returned entry is truncated  | String  |
| part_list               | Lists all uploaded parts                                             | Struct  |
| part_number   | Part number                                                    | String      |
| size          | Part size in bytes                                            | String      |
| etag                    | SHA-1 check value of the part                                     | String  |
| last_modified                  | Last modified time of the part                                           | String      |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

// Initialize request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//Query uploaded parts
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

//Complete the multipart upload
s = cos_complete_multipart_upload(options, &bucket, &object, &upload_id,
                                  &complete_part_list, complete_headers, &resp_headers);

if (cos_status_is_ok(s)) {
    printf("Complete multipart upload from file succeeded, upload_id:%.*s\n", 
           upload_id.len, upload_id.data);
} else {
    printf("Complete multipart upload from file failed\n");
}

//Destroy the memory pool
cos_pool_destroy(p); 
```






### Completing a multipart upload

#### Feature

This API (Complete Multipart Upload) is used to complete the multipart upload of an entire file. You can use this API to complete the multipart upload when you have uploaded all parts using Upload Parts. When using this API, you need to provide the PartNumber and ETag for every part in Body, to verify the accuracy of parts.

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

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options            | COS request options                                               | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object       | Object name                                                  | String |
| upload_id | ID of the upload task | String |
| part_list    | Parameters for Complete Multipart Upload                                           | Struct |
| part_number   | Part number                                                    | String      |
| etag | ETag of the part, which is SHA1 check value. It must be enclosed in double quotes, such as: "3a0f1fd698c235af9cf098cb74aa25bc". | String |
| headers      | Headers attached to the COS request                                             | Struct |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

// Initialize request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//Query uploaded parts
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

//Complete the multipart upload
s = cos_complete_multipart_upload(options, &bucket, &object, &upload_id,
                                  &complete_part_list, complete_headers, &resp_headers);

if (cos_status_is_ok(s)) {
    printf("Complete multipart upload from file succeeded, upload_id:%.*s\n", 
           upload_id.len, upload_id.data);
} else {
    printf("Complete multipart upload from file failed\n");
}

//Destroy the memory pool
cos_pool_destroy(p); 
```

### Aborting a multipart upload

#### Feature

This API (Abort Multipart Upload) is used to abort a multipart upload, and delete uploaded parts in it. When Abort Multipart Upload is called, a failure is returned for any request that is using Upload Parts.

#### Method prototype

```cpp
cos_status_t *cos_abort_multipart_upload(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         const cos_string_t *object, 
                                         cos_string_t *upload_id, 
                                         cos_table_t **resp_headers);
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options            | COS request options                                               | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object       | Object name                                                  | String |
| upload_id | ID of the upload task | String |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

//Create a memory pool, and initialize request options
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
headers = cos_table_make(p, 1);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, TEST_MULTIPART_OBJECT);

//Initialize the multipart upload
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

//Abort the multipart upload
s = cos_abort_multipart_upload(options, &bucket, &object, &upload_id, 
                               &resp_headers);

if (cos_status_is_ok(s)) {
    printf("Abort multipart upload succeeded, upload_id::%.*s\n", 
           upload_id.len, upload_id.data);
} else {
    printf("Abort multipart upload failed\n"); 
}    

//Destroy the memory pool
cos_pool_destroy(p);
```

##Other Operations

### Restoring an archived object

#### Feature

This API (POST Object restore) is used to restore an archived object for access.

#### Method prototype

```cpp
cos_status_t *cos_post_object_restore(const cos_request_options_t *options,
                                      const cos_string_t *bucket, 
                                      const cos_string_t *object,
                                      cos_object_restore_params_t *restore_params,
                                      cos_table_t *headers,
                                      cos_table_t *params,
                                      cos_table_t **resp_headers);
```

#### Parameter description

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| options                 | COS request options                                                 | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object                  | Object name                                                | String  |
| restore_params | Parameters for Post Object Restore                                 | Struct |
| days           | The number of days before a temporary copy restored using Post Object Restore expires                | Int    |
| tier           | Specifies one of the three CAS restoration modes for Post Object Restore: Expedited, Standard, Bulk | String |
| headers      | Headers attached to the COS request                                             | Struct |
| params       | Parameters for a COS request operation                                             | Struct |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

// Initialize request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);

//Restore an archived object
cos_object_restore_params_t *restore_params = cos_create_object_restore_params(p);
restore_params->days = 30;
cos_str_set(&restore_params->tier, "Standard");
s = cos_post_object_restore(options, &bucket, &object, restore_params, NULL, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("post object restore succeeded\n");
} else {
    printf("post object restore failed\n");
}

//Destroy the memory pool
cos_pool_destroy(p); 
```

### Setting object ACL

#### Feature

This API (PUT Object acl) is used to set an ACL for the specified object in a bucket.

#### Method prototype

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

#### Parameter description

| Parameter Name | Description | Type |
| --------------- | ------------------------------------------------------------ | ------ |
| options         | COS request options                                                | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object          | Object name                                                  | String |
| cos_acl         | Allows user-defined permission. Valid values: COS_ACL_PRIVATE(0), COS_ACL_PUBLIC_READ(1)<br>Default: COS_ACL_PRIVATE(0) | Enum   |
| grant_read      | Read access grantee                                                | String |
| grant_write     | Write access grantee                                              | String |
| grant_full_ctrl | Read/Write access grantee                                            | String |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

// Initialize request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//Set object ACL
cos_str_set(&object, TEST_OBJECT_NAME);
cos_string_t read;
cos_str_set(&read, "id=\"qcs::cam::uin/12345:uin/12345\", id=\"qcs::cam::uin/45678:uin/45678\"");
s = cos_put_object_acl(options, &bucket, &object, cos_acl, &read, NULL, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("put object acl succeeded\n");
} else {
    printf("put object acl failed\n");
}

//Destroy the memory pool
cos_pool_destroy(p);  
```

### Querying object ACL

#### Feature

This API (GET Object acl) is used to query the ACL of an object.

#### Method prototype

```cpp
cos_status_t *cos_get_object_acl(const cos_request_options_t *options, 
                                 const cos_string_t *bucket,
                                 const cos_string_t *object,
                                 cos_acl_params_t *acl_param, 
                                 cos_table_t **resp_headers)
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options            | COS request options                                               | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object       | Object name                                                  | String |
| acl_param    | Parameters for the request                                                 | Struct |
| owner_id     | ID of the bucket owner                             | String |
| owner_id     | Name of the bucket owner                             | String |
| object_list  | Information about the grantee and permission                         | Struct |
| type         | Type of the grantee account                             | String |
| id           | ID of the grantee                             | String |
| name         | Name of the grantee                        | String |
| permission   | Permission granted to the grantee                              | String |
| resp_headers       | Returns HTTP response headers                                     | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

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

// Initialize request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//Get the object ACL
cos_acl_params_t *acl_params2 = NULL;
acl_params2 = cos_create_acl_params(p);
s = cos_get_object_acl(options, &bucket, &object, acl_params2, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("get object succeeded\n");
    printf("acl owner id:%s, name:%s\n", acl_params2->owner_id.data, acl_params2->owner_name.data);
    acl_content = NULL;
    cos_list_for_each_entry(cos_acl_grantee_content_t, acl_content, &acl_params2->grantee_list, node) {
        printf("acl grantee id:%s, name:%s, permission:%s\n", acl_content->id.data, acl_content->name.data, acl_content->permission.data);
    }
} else {
    printf("get object acl failed\n");
}

//Destroy the memory pool
cos_pool_destroy(p); 
```

## Advanced APIs (recommended)

### Uploading objects (checkpoint restart)

#### Feature

This API (Upload) is used to automatically divide your data and lowers your usage threshold based on the size of your file when uploading, and perform checkpoint restart for unfinished multipart uploads. 

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

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | -------- |
| options           | COS request options                                                 | Struct   |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object          | Object name                                                  | String |
| filepath          | The local file name of the object                                          | String   |
| headers      | Headers attached to the COS request                                             | Struct |
| params            | Parameters for the COS request                                           | Struct   |
| clt_params        | Control parameters for the Upload operation                                             | Struct   |
| part_size         | Part size in bytes. If it is specified as below 1048576 (1 MB),  the C SDK will divide your data automatically.  | Int      |
| thread_num        | Number of the threads. Default: 1                                          | Int      |
| enable_checkpoint | Indicates whether to enable checkpoint restart                                             | Int      |
| checkpoint_path   | Indicates the file path for which the upload progress is saved when checkpoint restart is enabled. Default: `<filepath>.cp`, where `filepath` is the local file name of the object | String   |
| progress_callback | Callback function for upload progress                                            | Function |
| resp_headers       | Returns HTTP response headers                                     | Struct  |
| resp_body         | Saves the data returned by the Complete Multipart Upload request                             | Struct   |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Samples

```cpp
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
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
headers = cos_table_make(p, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, TEST_MULTIPART_OBJECT);
cos_str_set(&filename, TEST_MULTIPART_FILE);

// Set upload control parameters
clt_params = cos_create_resumable_clt_params_content(p, 0, 1, COS_FALSE, NULL);
// upload
s = cos_resumable_upload_file(options, &bucket, &object, &filename, headers, NULL,
						clt_params, NULL, &resp_headers, NULL);

if (cos_status_is_ok(s)) {
	printf("upload succeeded\n");
} else {
	printf("upload failed\n");
}

cos_pool_destroy(p);
```

