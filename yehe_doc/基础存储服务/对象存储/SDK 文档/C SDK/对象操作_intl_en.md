## Overview

This document provides an overview of APIs and SDK code samples related to simple operations, multipart operations, and other object operations.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying objects | Queries some or all the objects in a bucket. |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object (creating a directory) | Uploads an object to a bucket. |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system. |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying attributes) | Copies an object to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes a specified object from a bucket. |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket. |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads a file in parts. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying an object part | Copies a part of an object. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets an ACL for an object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object |

## Simple Operations

### Querying objects

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

#### Sample 1. Querying an object list

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

// Destroy the memory pool.
cos_pool_destroy(p); 
```

#### Sample 2. Listing the objects in a directory

COS does not have the concept of folder, but you can use slashes (/) as the delimiter to stimulate folders.

```c
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
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
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
```

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
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Upload an object
cos_str_set(&file, TEST_DOWNLOAD_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_put_object_from_file(options, &bucket, &object, &file, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("put object succeeded\n");
} else {
    printf("put object failed\n");
}

// Destroy the memory pool.
cos_pool_destroy(p); 
```

#### Sample 2. Creating a folder

COS uses slashes (/) to separate object paths to simulate the effect of directories. Therefore, you can upload an empty stream and append a slash to its name to create an empty directory in COS.

```c
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
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, "folder/");
cos_list_init(&buffer);
s = cos_put_object_from_buffer(options, &bucket, &object, 
		&buffer, headers, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("put object succeeded\n");
} else {
    printf("put object failed\n");
}
cos_pool_destroy(p);
```

#### Sample 3. Uploading an object to a COS directory

You can upload an object whose name is separated by slashes. In this way, the directory that contains this object will be created automatically. If you need to upload new objects to this COS directory, you can set the key’s prefix to the value of this directory.

```c
cos_pool_t *p = NULL;
int is_cname = 0; 
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers;
cos_table_t *headers = NULL;
cos_list_t buffer;
  
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
```

#### Sample 4. Uploading an object (limiting single-URL speed)

>? For more information about the speed limits on object uploads and downloads, please see [Single-URL Speed Limits](https://intl.cloud.tencent.com/document/product/436/34072).

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;
cos_table_t *headers = NULL;

// Create a memory pool
cos_pool_create(&p, NULL);

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// The speed range is 819200 to 838860800, that is 100 KB/s to 100 MB/s. If the value is not within this range, 400 will be returned.
headers = cos_table_make(p, 1);
cos_table_add_int(headers, "x-cos-traffic-limit", 819200);

// Upload an object
cos_str_set(&file, TEST_DOWNLOAD_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_put_object_from_file(options, &bucket, &object, &file, headers, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("put object succeeded\n");
} else {
    printf("put object failed\n");
}

// Destroy the memory pool.
cos_pool_destroy(p); 
```


### Querying object metadata

#### Description

This API is used to query the metadata of an object.

#### Method prototype

```cpp
cos_status_t *cos_head_object(const cos_request_options_t *options, 
                              const cos_string_t *bucket, 
                              const cos_string_t *object,
                              cos_table_t *headers, 
                              cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format: `BucketName-APPID` | String |
| object | Object name | String |
| headers      | Additional headers of a COS request | Struct |
| resp_headers | Returns the HTTP response headers | Struct |

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

// Initialize the request options
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
    printf("head object succeeded\n");
} else {
    printf("head object failed\n");
}

// Destroy the memory pool.
cos_pool_destroy(p); 
```

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

#### Sample 1. Simple download

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
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Get the object
cos_str_set(&file, TEST_DOWNLOAD_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_get_object_to_file(options, &bucket, &object, NULL, NULL, &file, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("get object succeeded\n");
} else {
    printf("get object failed\n");
}

// Destroy the memory pool.
cos_pool_destroy(p); 
```

#### Sample 2. Downloading an object (limiting single-URL speed)

>? For more information about the speed limits on object uploads and downloads, please see [Single-URL Speed Limits](https://intl.cloud.tencent.com/document/product/436/34072).

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *headers = NULL;
cos_table_t *resp_headers = NULL;

// Create a memory pool
cos_pool_create(&p, NULL);

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// The speed range is 819200 to 838860800, that is 100 KB/s to 100 MB/s. If the value is not within this range, 400 will be returned.
headers = cos_table_make(p, 1);
cos_table_add_int(headers, "x-cos-traffic-limit", 819200);

// Get the object
cos_str_set(&file, TEST_DOWNLOAD_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_get_object_to_file(options, &bucket, &object, headers, NULL, &file, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("get object succeeded\n");
} else {
    printf("get object failed\n");
}

// Destroy the memory pool.
cos_pool_destroy(p); 
```



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
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Set object replication
cos_str_set(&object, TEST_OBJECT_NAME);
cos_str_set(&src_bucket, TEST_BUCKET_NAME);
cos_str_set(&src_endpoint, "ap-guangzhou.myqcloud.com");
cos_str_set(&src_object, "test.txt");

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
```

#### Sample 2:. Modifying storage class

>!You can change STANDARD to STANDARD_IA, INTELLIGENT TIERING, ARCHIVE, or DEEP ARCHIVE. To modify ARCHIVE or DEEP ARCHIVE to other storage classes, you need to call `cos_post_object_restore()` to restore objects in ARCHIVE or DEEP ARCHIVE first before calling this API. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).


```cpp
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
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
// The source and destination objects are the same.
cos_str_set(&object, "test.txt");
cos_str_set(&src_object, "test.txt");
cos_str_set(&src_bucket, TEST_BUCKET_NAME);
cos_str_set(&src_endpoint, TEST_COS_ENDPOINT);

// Set the x-cos-metadata-directive and x-cos-storage-class headers and replace it with the desired storage class.
cos_table_t *headers = cos_table_make(p, 2);
apr_table_add(headers, "x-cos-metadata-directive", "Replaced");
// Valid storage classes are NTELLIGENT_TIERING, MAZ_INTELLIGENT_TIERING, STANDARD_IA, ARCHIVE, and DEEP_ARCHIVE.
apr_table_add(headers, "x-cos-storage-class", "ARCHIVE");

// Copy the object and set the storage class.
cos_copy_object_params_t *params = NULL;
params = cos_create_copy_object_params(p);
s = cos_copy_object(options, &src_bucket, &src_object, &src_endpoint, & bucket, &object, headers, params, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("copy object succeeded\n");
} else {
    printf("copy object failed\n");
}

// Destroy the memory pool.
cos_pool_destroy(p); 
```



### Deleting an object

#### Description

This API is used to delete a specified object from a bucket.

#### Method prototype

```cpp
cos_status_t *cos_delete_object(const cos_request_options_t *options,
                                const cos_string_t *bucket, 
                                const cos_string_t *object, 
                                cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format: `BucketName-APPID` | String |
| object | Object name | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |


#### Sample 1. Deleting an object

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
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Delete the single object
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_delete_object(options, &bucket, &object, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("delete object succeeded\n");
} else {
    printf("delete object failed\n");
}

// Destroy the memory pool.
cos_pool_destroy(p); 

```

#### Sample 2. Deleting a folder

This request does not delete objects in the folder but only the specified key.

```
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
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Delete the directory object
cos_str_set(&object, "folder/");
s = cos_delete_object(options, &bucket, &object, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("delete object succeeded\n");
} else {
    printf("delete object failed\n");
}

// Destroy the memory pool.
cos_pool_destroy(p); 
```



### Deleting multiple objects

#### Description

This API is used to delete multiple objects from a bucket in a single request. It can delete up to 1,000 objects in a single request. This API supports two response modes: Verbose and Quiet. Verbose mode returns the information on the deletion of each object, whereas Quiet mode only returns the information on the objects for which deletion errors were reported.

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

| Parameter | Description | Type |
| ------------------- | ------------------------------------------------------------ | ------- |
| options | COS request options | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object_list | The list of objects to be deleted                                         | Struct  |
| key | Name of the object to be deleted | String |
| is_quiet | Indicates whether Quiet mode is enabled.<br>True(1): Quiet mode is enabled; False(0): Verbose mode is enabled. The default value is False(0). | Boolean |
| resp_headers | Returns the HTTP response headers | Struct |
| deleted_object_list | The list of deleted objects                                          | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |



#### Sample 1. Deleting multiple objects

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
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Set multiple objects to be deleted
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

// Delete the objects
int is_quiet = COS_TRUE;
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_delete_objects(options, &bucket, &object_list, is_quiet, &resp_headers, &deleted_object_list);
if (cos_status_is_ok(s)) {
    printf("delete objects succeeded\n");
} else {
    printf("delete objects failed\n");
}

// Destroy the memory pool.
cos_pool_destroy(p); 

```

#### Sample 2. Deleting a folder and the objects contained

COS does not have the concept of folder, but you can use slashes (/) as the delimiter to stimulate folders.

In COS, deleting a folder and the objects contained actually means deleting objects that have the same specified prefix. Currently, COS’s C SDK does not provide a standalone API to perform this operation. However, you can still do so with a combination of basic operations (**query object list** and **batch delete objects**).

```c
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
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
  
//list object (get bucket)
cos_list_object_params_t *list_params = NULL;
list_params = cos_create_list_object_params(p);
cos_str_set(&list_params->encoding_type, "url");
cos_str_set(&list_params->prefix, "folder/");
cos_str_set(&marker, "");
while (is_truncated) {
	list_params->marker = marker;
	s = cos_list_object(options, &bucket, list_params, &resp_headers);
	if (!cos_status_is_ok(s)) {
		printf("list object failed, req_id:%s\n", s->req_id);
		break;
	}
	cos_list_object_content_t *content = NULL;
	cos_list_for_each_entry(cos_list_object_content_t, content, &list_params->object_list, node) {
        s = cos_delete_object(options, &bucket, &content->key, &resp_headers);
        if (!cos_status_is_ok(s)) {
            printf("delete object[%s] failed, req_id:%s\n", content->key.data, s->req_id);
        }
	}
	is_truncated = list_params->truncated;
	marker = list_params->next_marker;
}    
cos_pool_destroy(p);
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

#### Samples

```cpp
cos_pool_t *p = NULL;
cos_string_t bucket;
int is_cname = 0;
cos_table_t *resp_headers = NULL;
cos_request_options_t *options = NULL;
cos_status_t *s = NULL;
cos_list_multipart_upload_params_t *list_multipart_params = NULL;

// Create a memory pool and initialize request options
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Query the multipart uploads
list_multipart_params = cos_create_list_multipart_upload_params(p);
list_multipart_params->max_ret = 999;
s = cos_list_multipart_upload(options, &bucket, list_multipart_params, &resp_headers);
log_status(s);

// Destroy the memory pool.
cos_pool_destroy(p);

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

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Initialize the multipart upload
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_init_multipart_upload(options, &bucket, &object, 
                              &upload_id, headers, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("init multipart upload succeeded\n");
} else {
    printf("init multipart upload failed\n");
}

// Destroy the memory pool.
cos_pool_destroy(p); 
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

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

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
```

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

// Create a random local file of 10 MB    
make_rand_string(p, 10 * 1024 * 1024, &data);
fd = fopen(local_filename, "w");
fwrite(data.data, sizeof(data.data[0]), data.len, fd);
fclose(fd);    

// Upload the local file as an object
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

// Initialize the multipart upload
cos_str_set(&object, dest_object_name);
s = cos_init_multipart_upload(options, &bucket, &object, 
                              &upload_id, NULL, &resp_headers);
log_status(s);

// Copy the uploaded object as Part 1
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

// Copy the uploaded object as Part 2
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

// List the uploaded parts
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

// Check if the object uploaded using Upload Part - Copy matches the local file
headers = cos_table_make(p, 0);
cos_str_set(&download_file, download_filename);
s = cos_get_object_to_file(options, &dest_bucket, &dest_object, headers, 
                           query_params, &download_file, &resp_headers);
log_status(s);
printf("local file len = %"APR_INT64_T_FMT", download file len = %"APR_INT64_T_FMT, get_file_size(local_filename), get_file_size(download_filename));
remove(download_filename);
remove(local_filename);

// Destroy the memory pool.
cos_pool_destroy(p);    
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

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

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
                                  &complete_part_list, complete_headers, &resp_headers);

if (cos_status_is_ok(s)) {
    printf("Complete multipart upload from file succeeded, upload_id:%.*s\n", 
           upload_id.len, upload_id.data);
} else {
    printf("Complete multipart upload from file failed\n");
}

// Destroy the memory pool.
cos_pool_destroy(p); 
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

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

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
                                  &complete_part_list, complete_headers, &resp_headers);

if (cos_status_is_ok(s)) {
    printf("Complete multipart upload from file succeeded, upload_id:%.*s\n", 
           upload_id.len, upload_id.data);
} else {
    printf("Complete multipart upload from file failed\n");
}

// Destroy the memory pool.
cos_pool_destroy(p); 
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

// Create a memory pool and initialize request options
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

// Initialize the multipart upload
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

// Abort the multipart upload
s = cos_abort_multipart_upload(options, &bucket, &object, &upload_id, 
                               &resp_headers);

if (cos_status_is_ok(s)) {
    printf("Abort multipart upload succeeded, upload_id::%.*s\n", 
           upload_id.len, upload_id.data);
} else {
    printf("Abort multipart upload failed\n"); 
}    

// Destroy the memory pool.
cos_pool_destroy(p);
```

## Other Operations

### Restoring an archived object

#### Description

This API is used to restore an archived object for access.

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

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object | Object name | String |
| restore_params | Parameters for the `Post Object Restore` operation | Struct |
| days | The number of days before a temporary copy restored using `Post Object Restore` expires | Int |
| tier | Specifies one of the three CAS restoration modes for Post Object Restore: `Expedited`, `Standard`, `Bulk` | String |
| headers | Headers attached to the COS request | Struct |
| params | Parameters for the COS request operation | Struct |
| resp_headers | Returns the HTTP response headers | Struct |

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

// Initialize the request options
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

// Restore the archived object
cos_object_restore_params_t *restore_params = cos_create_object_restore_params(p);
restore_params->days = 30;
cos_str_set(&restore_params->tier, "Standard");
s = cos_post_object_restore(options, &bucket, &object, restore_params, NULL, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("post object restore succeeded\n");
} else {
    printf("post object restore failed\n");
}

// Destroy the memory pool.
cos_pool_destroy(p); 
```

### Setting an object ACL

#### Description

This API is used to set an ACL for an object in a bucket.

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

| Parameter | Description | Type |
| --------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object | Object name | String |
| cos_acl | Allow users to customize permissions. Valid values: COS_ACL_PRIVATE(0) (default), COS_ACL_PUBLIC_READ(1), COS_ACL_PUBLIC_READ_WRITE(2)  | Enum |
| grant_read | Grants a user permission to read an object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | String |
| grant_write | Grants a user permission to write to an object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | String |
| grant_full_ctrl | Grants a user full permission to operate on an object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | String |
| resp_headers | Returns the HTTP response headers | Struct |

>?For more information, please see [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) and [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583).

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

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
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

// Destroy the memory pool.
cos_pool_destroy(p);  
```

### Querying an object ACL

#### Description

This API is used to query the ACL of an object.

#### Method prototype

```cpp
cos_status_t *cos_get_object_acl(const cos_request_options_t *options, 
                                 const cos_string_t *bucket,
                                 const cos_string_t *object,
                                 cos_acl_params_t *acl_param, 
                                 cos_table_t **resp_headers)
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format: `BucketName-APPID` | String |
| object | Object name | String |
| acl_param | Parameters for the request | Struct |
| owner_id | ID of the bucket owner | String |
| owner_id | Name of the bucket owner | String |
| object_list  | Information on the authorized user and granted permission | Struct |
| type | Authorized user account type | String |
| id | ID of the authorized user | String |
| name | Name of the authorized user | String |
| permission | Permission granted to the authorized user | String |
| resp_headers | Returns the HTTP response headers | Struct |

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

// Initialize the request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
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

// Destroy the memory pool.
cos_pool_destroy(p); 
```

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

#### Samples

```c
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
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);

headers = cos_table_make(p, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, TEST_MULTIPART_OBJECT);
cos_str_set(&filename, TEST_MULTIPART_FILE);

// Set the upload control parameters
clt_params = cos_create_resumable_clt_params_content(p, 0, 1, COS_TRUE, NULL);
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

#### Samples

```c
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
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);

cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, TEST_MULTIPART_OBJECT);
cos_str_set(&filepath, TEST_DOWNLOAD_NAME);

clt_params = cos_create_resumable_clt_params_content(p, 5*1024*1024, 3, COS_FALSE, NULL);
s = cos_resumable_download_file(options, &bucket, &object, &filepath, NULL, NULL, clt_params, NULL);
if (cos_status_is_ok(s)) {
	printf("download succeeded\n");
} else {
	printf("download failed\n");
}
cos_pool_destroy(p);
```

### Moving an object

#### Description

Object movement involves copying the source object to the target location and deleting the source object.

Since COS uses the bucket name (`Bucket`) and object key (`ObjectKey`) to identify objects, moving an object will change the object identifier. Currently, COS’s C SDK does not provide a standalone API to change object identifiers. However, you can still move the object with a combination of basic operations (**object copy** and **object delete**).

- [Copying an object](#.E8.AE.BE.E7.BD.AE.E5.AF.B9.E8.B1.A1.E5.A4.8D.E5.88.B6.EF.BC.88.E4.BF.AE.E6.94.B9.E5.B1.9E.E6.80.A7.EF.BC.89)
- [Deleting an object](#.E5.88.A0.E9.99.A4.E5.8D.95.E4.B8.AA.E5.AF.B9.E8.B1.A1)

#### Samples
```c
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
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Set object replication
cos_str_set(&object, TEST_OBJECT_NAME1);
cos_str_set(&src_endpoint, "ap-guangzhou.myqcloud.com");
cos_str_set(&src_object, "example");
cos_copy_object_params_t *params = NULL;
params = cos_create_copy_object_params(p);
s = cos_copy_object(options, &bucket, &src_object, &src_endpoint, &bucket, &object, NULL, params, &resp_headers);
if (cos_status_is_ok(s)) {
	s = cos_delete_object(options, &bucket, &src_object, &resp_headers);
} else {
	printf("move object failed\n");
}
// Destroy the memory pool.
cos_pool_destroy(p);
```
	
	
