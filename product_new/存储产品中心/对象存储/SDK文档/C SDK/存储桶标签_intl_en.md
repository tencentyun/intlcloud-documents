

## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting a bucket tag | Sets a tag for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting a bucket tag | Deletes a specified bucket tag |

## Setting Bucket Tag

#### Feature description

This API (PUT Bucket tagging) is used to set a tag for an existing bucket.

#### Method prototype

```c
cos_status_t *cos_put_bucket_tagging(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_tagging_params_t *tagging_params,
                                      cos_table_t **resp_headers);
```

#### Sample request

```c
cos_pool_t *pool = NULL;
int is_cname = 0;
cos_status_t *status = NULL;
cos_request_options_t *options = NULL;
cos_table_t *resp_headers = NULL;
cos_string_t bucket;
cos_tagging_params_t *params = NULL;
cos_tagging_params_t *result = NULL;
cos_tagging_tag_t *tag = NULL;
  
// Create a memory pool
cos_pool_create(&pool, NULL);
  
// Initialize the request options
options = cos_request_options_create(pool);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
  
// put tagging
params = cos_create_tagging_params(pool);
tag = cos_create_tagging_tag(pool);
cos_str_set(&tag->key, "age");
cos_str_set(&tag->value, "18");
cos_list_add_tail(&tag->node, &params->node);
  
tag = cos_create_tagging_tag(pool);
cos_str_set(&tag->key, "name");
cos_str_set(&tag->value, "xiaoming");
cos_list_add_tail(&tag->node, &params->node);
  
// Set bucket tag
status = cos_put_bucket_tagging(options, &bucket, params, &resp_headers);
log_status(status);
  
// Terminate the memory pool
cos_pool_destroy(pool);
```

#### Parameter description

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for which to set a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| tagging_params | Bucket tag configuration information                                           | Struct |
| key | Tag key, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 128 bytes | String |
| value | Tag value, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 256 bytes | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Returned result description

| Return Result | Description | Type |
| :--------- | :---------- | :----- |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

## Querying Bucket Tag

#### Feature description

This API (GET Bucket tagging) is used to query the existing tags of a specified bucket.

#### Method prototype

```c
cos_status_t *cos_get_bucket_tagging(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_tagging_params_t *tagging_params,
                                      cos_table_t **resp_headers);
```

#### Sample request

```c
cos_pool_t *pool = NULL;
int is_cname = 0;
cos_status_t *status = NULL;
cos_request_options_t *options = NULL;
cos_table_t *resp_headers = NULL;
cos_string_t bucket;
cos_tagging_params_t *params = NULL;
cos_tagging_params_t *result = NULL;
cos_tagging_tag_t *tag = NULL;
  
// Create a memory pool
cos_pool_create(&pool, NULL);
  
// Initialize the request options
options = cos_request_options_create(pool);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
  
// get tagging
result = cos_create_tagging_params(pool);
status = cos_get_bucket_tagging(options, &bucket, result, &resp_headers);
log_status(status);
 
// View the result
tag = NULL;
cos_list_for_each_entry(cos_tagging_tag_t, tag, &result->node, node) {
	printf("taging key: %s\n", tag->key.data);
    printf("taging value: %s\n", tag->value.data);
} 
  
// Terminate the memory pool
cos_pool_destroy(pool);
```

#### Parameter description

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for which to query a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| tagging_params | Bucket tag configuration information                                           | Struct |
| key | Tag key, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 128 bytes | String |
| value | Tag value, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 256 bytes | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Returned result description

| Return Result | Description | Type |
| :--------- | :---------- | :----- |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

## Deleting Bucket Tag

#### Feature description

This API (DELETE Bucket tagging) is used to delete an existing tag of a specified bucket.

#### Method prototype

```c
cos_status_t *cos_delete_bucket_tagging(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_table_t **resp_headers);
```

#### Sample request

```c
cos_pool_t *pool = NULL;
int is_cname = 0;
cos_status_t *status = NULL;
cos_request_options_t *options = NULL;
cos_table_t *resp_headers = NULL;
cos_string_t bucket;
cos_tagging_params_t *params = NULL;
cos_tagging_params_t *result = NULL;
cos_tagging_tag_t *tag = NULL;
  
// Create a memory pool
cos_pool_create(&pool, NULL);
  
// Initialize the request options
options = cos_request_options_create(pool);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
  
// delete tagging
status = cos_delete_bucket_tagging(options, &bucket, &resp_headers);
log_status(status);
  
// Terminate the memory pool
cos_pool_destroy(pool);
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for which to delete a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Returned result description

| Return Result | Description | Type |
| :--------- | :---------- | :----- |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |
