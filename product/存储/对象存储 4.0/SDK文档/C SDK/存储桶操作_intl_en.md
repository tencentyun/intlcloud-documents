## Overview

This document provides an overview of APIs related to basic bucket operations and access control list (ACL) and corresponding SDK sample code.

**Basic operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ---------- | -------------------------- |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for the specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a bucket |

## Basic Operations

### Creating a Bucket

#### Feature Description

This API is used to create a bucket under the specified account.

#### Method Prototype

```cpp
cos_status_t *cos_create_bucket(const cos_request_options_t *options, 
                                const cos_string_t *bucket, 
                                cos_acl_e cos_acl, 
                                cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| cos_acl | Allows user to customize permissions. <br>Value range: COS_ACL_PRIVATE(0), COS_ACL_PUBLIC_READ(1), COS_ACL_PUBLIC_READ_WRITE(2) <br>Default value: COS_ACL_PRIVATE(0) | Enum   |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Return Result Descriptions

| Return Result | Description | Type |
| ---------- | ---------- | ------ |
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
cos_acl_e cos_acl = COS_ACL_PRIVATE;
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

// Create a bucket
s = cos_create_bucket(options, &bucket, cos_acl, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("create bucket succeeded\n");
} else {
		printf("create bucket failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Deleting a Bucket

#### Feature Description

This API is used to delete an empty bucket under the specified account.

#### Method Prototype

```cpp
cos_status_t *cos_delete_bucket(const cos_request_options_t *options,
                                const cos_string_t *bucket, 
                                cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
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

// Delete a bucket
s = cos_delete_bucket(options, &bucket, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("create bucket succeeded\n");
} else {
		printf("create bucket failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Setting Bucket ACL

#### Feature Description

This API is used to set the access control list (ACL) for the specified bucket.

#### Method Prototype

```cpp
cos_status_t *cos_put_bucket_acl(const cos_request_options_t *options, 
                                 const cos_string_t *bucket, 
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
| cos_acl | Allows user to customize permissions. <br>Value range: COS_ACL_PRIVATE(0), COS_ACL_PUBLIC_READ(1), COS_ACL_PUBLIC_READ_WRITE(2) <br>Default value: COS_ACL_PRIVATE(0) | Enum   |
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

// Set the bucket ACL
cos_string_t read;
cos_str_set(&read, "id=\"qcs::cam::uin/100000000001:uin/100000000001\", id=\"qcs::cam::uin/100000000011:uin/100000000011\"");
s = cos_put_bucket_acl(options, &bucket, cos_acl, &read, NULL, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("put bucket acl succeeded\n");
} else {
		printf("put bucket acl failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Querying Bucket ACL

#### Feature Description

This API is used to query the access control list (ACL) of a bucket.

#### Method Prototype

```cpp
cos_status_t *cos_get_bucket_acl(const cos_request_options_t *options, 
                                 const cos_string_t *bucket, 
                                 cos_acl_params_t *acl_param, 
                                 cos_table_t **resp_headers)
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
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

// Get the bucket ACL
cos_acl_params_t *acl_params = NULL;
acl_params = cos_create_acl_params(p);
s = cos_get_bucket_acl(options, &bucket, acl_params, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("get bucket acl succeeded\n");
		printf("acl owner id:%s, name:%s\n", acl_params->owner_id.data, acl_params->owner_name.data);
		cos_acl_grantee_content_t *acl_content = NULL;
		cos_list_for_each_entry(cos_acl_grantee_content_t, acl_content, &acl_params->grantee_list, node) {
				printf("acl grantee type:%s, id:%s, name:%s, permission:%s\n", acl_content->type.data, acl_content->id.data, acl_content->name.data, acl_content->permission.data);
		}
} else {
		printf("get bucket acl failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```
