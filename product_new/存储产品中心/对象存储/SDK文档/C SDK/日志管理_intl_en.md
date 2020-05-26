

## Overview

This document provides an overview of APIs and SDK code samples for C related to log management.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting log management | Enables logging for the source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying log management | Queries the logging configuration information of the source bucket |

## Setting Log Management

#### Feature description

This API (PUT Bucket logging) is used to enable logging for the source bucket and store its access logs in a specified destination bucket.

#### Method prototype

```C
cos_status_t *cos_put_bucket_logging(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_logging_params_t *logging_params,
                                      cos_table_t **resp_headers);
```

#### Sample request

```c
cos_pool_t *pool = NULL;
int is_cname = 0; 
cos_status_t *status = NULL;
cos_request_options_t *options = NULL;
cos_logging_params_t  *params = NULL;
cos_logging_params_t  *result = NULL;
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
  
// Create a `logging` parameter
params = cos_create_logging_params(options->pool);
cos_str_set(&params->target_bucket, TEST_BUCKET_NAME);
cos_str_set(&params->target_prefix, "logging/");
  
// Set log management
status = cos_put_bucket_logging(options, &bucket, params, &resp_headers);
log_status(status);
        
// Terminate the memory pool
cos_pool_destroy(pool); 
```

#### Parameter description

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket    | Source bucket for which to enable the logging feature in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |
| logging_params | Bucket log configuration information                                           | Struct |
| target_bucket  | The destination bucket for storing logs, which can be the source bucket (not recommended) or a bucket in the same region under the same account | String |
| target_prefix  | Specified path in the destination bucket for storing logs | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Returned result description

| Return Result | Description | Type |
| :--------- | :---------- | :----- |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

## Querying Log Management

#### Feature description

This API (GET Bucket logging) is used to query the log configuration information of a specified bucket.

#### Method prototype

```c
cos_status_t *cos_get_bucket_logging(const cos_request_options_t *options,  
                                      const cos_string_t *bucket,    
                                      cos_logging_params_t *logging_params,
                                      cos_table_t **resp_headers);
```

#### Sample request

```c
cos_pool_t *pool = NULL;
int is_cname = 0; 
cos_status_t *status = NULL;
cos_request_options_t *options = NULL;
cos_logging_params_t  *params = NULL;
cos_logging_params_t  *result = NULL;
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
  
// Query log configuration
result = cos_create_logging_params(options->pool);
status = cos_get_bucket_logging(options, &bucket, result, &resp_headers);
log_status(status);
  
if (!cos_status_is_ok(status)) {
	cos_pool_destroy(pool);
    return;
}    
  
// View result
char *line = NULL;
line = apr_psprintf(options->pool, "%.*s\n", result->target_bucket.len, result->target_bucket.data);
printf("target bucket: %s", line);
line = apr_psprintf(options->pool, "%.*s\n", result->target_prefix.len, result->target_prefix.data);
printf("target prefix: %s", line);
        
// Terminate the memory pool
cos_pool_destroy(pool); 
```

#### Parameter description

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Destination bucket where to store logs in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| logging_params | Bucket log configuration information                                           | Struct |
| target_bucket  | The destination bucket for storing logs, which can be the source bucket (not recommended) or a bucket in the same region under the same account | String |
| target_prefix  | Specified path in the destination bucket for storing logs | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Returned result description

| Return Result | Description | Type |
| :--------- | :---------- | :----- |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |
