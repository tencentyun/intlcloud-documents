

## Overview

This document provides an overview of APIs and SDK code samples related to static website.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website | Sets static website configuration for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying static website configuration | Queries the static website configuration information of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting static website configuration | Deletes the static website configuration of a bucket |

## Setting Static Website

#### Feature description

This API (PUT Bucket website) is used to configure a static website for a bucket.

#### Method prototype

```c
cos_status_t *cos_put_bucket_website(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_website_params_t *website_params,
                                      cos_table_t **resp_header);
```

#### Sample request

```c
cos_pool_t *pool = NULL;
int is_cname = 0;
cos_status_t *status = NULL;
cos_request_options_t *options = NULL;
cos_website_params_t  *website_params = NULL;
cos_website_params_t  *website_result = NULL;
cos_website_rule_content_t *website_content = NULL;
cos_table_t *resp_headers = NULL;
cos_string_t bucket;
  
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
  
// Create a `website` parameter
website_params = cos_create_website_params(options->pool);
cos_str_set(&website_params->index, "index.html");
cos_str_set(&website_params->redirect_protocol, "https");
cos_str_set(&website_params->error_document, "Error.html");
  
website_content = cos_create_website_rule_content(options->pool);
cos_str_set(&website_content->condition_errcode, "404");
cos_str_set(&website_content->redirect_protocol, "https");
cos_str_set(&website_content->redirect_replace_key, "404.html");
cos_list_add_tail(&website_content->node, &website_params->rule_list);
  
website_content = cos_create_website_rule_content(options->pool);
cos_str_set(&website_content->condition_prefix, "docs/");
cos_str_set(&website_content->redirect_protocol, "https");
cos_str_set(&website_content->redirect_replace_key_prefix, "documents/");
cos_list_add_tail(&website_content->node, &website_params->rule_list);
  
website_content = cos_create_website_rule_content(options->pool);
cos_str_set(&website_content->condition_prefix, "img/");
cos_str_set(&website_content->redirect_protocol, "https");
cos_str_set(&website_content->redirect_replace_key, "demo.jpg");
cos_list_add_tail(&website_content->node, &website_params->rule_list);

// Set static website configuration
status = cos_put_bucket_website(options, &bucket, website_params, &resp_headers);
log_status(status);

// Terminate the memory pool
cos_pool_destroy(pool);
```

#### Parameter description

| Parameter Name | Description | Type |
| --------------------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for which to set a static website in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| website_params              | Static website configuration information of bucket                                       | Struct |
| index                       | Specifies index document                                                 | String |
| redirect_protocol           | Specifies the protocol for global redirect, which can only be `https`                       | String |
| error_document              | Specifies the common return for errors                                             | String |
| rule_list                   | Sets redirect rules. Up to 100 `RoutingRule` can be set                    | list   |
| condition_errcode           | Specifies the error code triggering redirect, which can only be 4XX and has a higher priority than `error_document` | String |
| condition_prefix            | Specifies the path for prefix-triggered redirect, which replaces the specified `folder/`                     | String |
| redirect_protocol           | Specifies the protocol for redirect, which can only be `https`                       | String |
| redirect_replace_key        | Replaces the entire `Key` with the specified content                                    | String |
| redirect_replace_key_prefix | Replaces the matched prefix with the specified content, which can be set only if `Condition` is `KeyPrefixEquals` | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Returned result description

| Return Result | Description | Type |
| :--------- | :---------- | :----- |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

## Querying Static Website Configuration

#### Feature description

This API (GET Bucket website) is used to query the configuration information of a static website associated with a bucket.

#### Method prototype

```c
cos_status_t *cos_get_bucket_website(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_website_params_t *website_params,
                                      cos_table_t **resp_header);
```

#### Sample request

```c
cos_pool_t *pool = NULL;
int is_cname = 0;
cos_status_t *status = NULL;
cos_request_options_t *options = NULL;
cos_website_params_t  *website_params = NULL;
cos_website_params_t  *website_result = NULL;
cos_website_rule_content_t *website_content = NULL;
cos_table_t *resp_headers = NULL;
cos_string_t bucket;
  
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
 
// Query static website configuration
website_result = cos_create_website_params(options->pool);
status = cos_get_bucket_website(options, &bucket, website_result, &resp_headers);
log_status(status);

// Terminate the memory pool
cos_pool_destroy(pool);
```

#### Parameter description

| Parameter Name | Description | Type |
| --------------------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for which to query static website configuration in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| website_params              | Static website configuration information of bucket                                       | Struct |
| index                       | Specifies index document                                                 | String |
| redirect_protocol           | Specifies the protocol for global redirect, which can only be `https`                       | String |
| error_document              | Specifies the common return for errors                                             | String |
| rule_list                   | Sets redirect rules. Up to 100 `RoutingRule` can be set                    | list   |
| condition_errcode           | Specifies the error code triggering redirect, which can only be 4XX and has a higher priority than `error_document` | String |
| condition_prefix            | Specifies the path for prefix-triggered redirect, which replaces the specified `folder/`                     | String |
| redirect_protocol           | Specifies the protocol for redirect, which can only be `https`                       | String |
| redirect_replace_key        | Replaces the entire `Key` with the specified content                                    | String |
| redirect_replace_key_prefix | Replaces the matched prefix with the specified content, which can be set only if `Condition` is `KeyPrefixEquals` | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Returned result description

| Return Result | Description | Type |
| :--------- | :---------- | :----- |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

## Deleting Static Website Configuration

#### Feature description

This API (DELETE Bucket website) is used to delete the static website configuration of a bucket.

#### Method prototype

```c
cos_status_t *cos_delete_bucket_website(const cos_request_options_t *options,
                                          const cos_string_t *bucket,
                                          cos_table_t **resp_header);
```

#### Sample request

```c
cos_pool_t *pool = NULL;
int is_cname = 0;
cos_status_t *status = NULL;
cos_request_options_t *options = NULL;
cos_website_params_t  *website_params = NULL;
cos_website_params_t  *website_result = NULL;
cos_website_rule_content_t *website_content = NULL;
cos_table_t *resp_headers = NULL;
cos_string_t bucket;
  
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
 
// Delete static website configuration
status = cos_delete_bucket_website(options, &bucket, &resp_headers);
log_status(status); 

// Terminate the memory pool
cos_pool_destroy(pool);
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for which to delete static website configuration in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Returned result description

| Return Result | Description | Type |
| :--------- | :---------- | :----- |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |
