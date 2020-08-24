## Overview

This document provides an overview of APIs and SDK code samples related to custom domain name.

| API | Operation Name | Operation Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting custom domain name | Sets custom domain name information for a bucket |
| GET Bucket domain | Querying custom domain name | Queries the custom domain name information of a bucket |

## Setting Custom Domain Name

#### Feature description

This API (PUT Bucket domain) is used to configure a custom domain name for a bucket.

#### Method prototype

```c
cos_status_t *cos_put_bucket_domain(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_domain_params_t *domain_params,
                                      cos_table_t **resp_header);
```

#### Sample request

```c
cos_pool_t *pool = NULL;
int is_cname = 0;
cos_status_t *status = NULL;
cos_request_options_t *options = NULL;
cos_domain_params_t  *domain_params = NULL;
cos_domain_params_t  *domain_result = NULL;
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
  
// Create a `domain` parameter
domain_params = cos_create_domain_params(options->pool);
cos_str_set(&domain_params->status, "ENABLED");
cos_str_set(&domain_params->name, "www.exmaple.com");
cos_str_set(&domain_params->type, "REST");
cos_str_set(&domain_params->forced_replacement, "CNAME");
  
status = cos_put_bucket_domain(options, &bucket, domain_params, &resp_headers);
log_status(status);
  
// Terminate the memory pool
cos_pool_destroy(pool);
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket            | Bucket for which to set a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| domain_params      | Custom domain name configuration information of bucket                                     | Struct |
| status                 | Domain name status. Valid values: ENABLED/DISABLED                   | String |
| name                   | Custom domain name. Valid values: letter, digit, dot                     | String |
| type                   | Type of bound origin server. Valid values: REST/WEBSITE                          | String |
| forced_replacement | Overwrites existing configuration. Valid values: CNAME/TXT. If this parameter is entered, the configuration will be distributed after the domain name ownership is forcibly verified | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Returned result description

| Return Result | Description | Type |
| :--------- | :---------- | :----- |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |

#### Returned error code description

Some frequent special errors that may occur with this request are listed below:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict                      | The domain name record already exists, and no forced overwriting is set in the request. Or, the domain name record does not exist, but forced overwriting is set in the request. |
| HTTP 451 Unavailable For Legal Reasons | The domain name is served in Mainland China but has no ICP filing.                          |

## Querying Custom Domain Name

#### Feature description

This API (GET Bucket domain) is used to query the custom domain name information of a bucket.

#### Method prototype

```c
cos_status_t *cos_get_bucket_domain(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_domain_params_t *domain_params,
                                      cos_table_t **resp_header);
```

#### Sample request

```c
cos_pool_t *pool = NULL;
int is_cname = 0;
cos_status_t *status = NULL;
cos_request_options_t *options = NULL;
cos_domain_params_t  *domain_params = NULL;
cos_domain_params_t  *domain_result = NULL;
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
  
// Query custom domain name configuration
domain_result = cos_create_domain_params(options->pool);
status = cos_get_bucket_domain(options, &bucket, domain_result, &resp_headers);
log_status(status);
if (!cos_status_is_ok(status)) {
 cos_pool_destroy(pool);
 return;
}
  
// View result
char *line = NULL;
line = apr_psprintf(options->pool, "%.*s\n", domain_result->status.len, domain_result->status.data);
printf("status: %s", line);
line = apr_psprintf(options->pool, "%.*s\n", domain_result->name.len, domain_result->name.data);
printf("name: %s", line);
line = apr_psprintf(options->pool, "%.*s\n", domain_result->type.len, domain_result->type.data);
printf("type: %s", line);
line = apr_psprintf(options->pool, "%.*s\n", domain_result->forced_replacement.len, domain_result->forced_replacement.data);
printf("forced_replacement: %s", line);
  
// Terminate the memory pool
cos_pool_destroy(pool);
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket            | Bucket for which to query a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |
| domain_params      | Custom domain name configuration information of bucket                                     | Struct |
| status                 | Domain name status. Valid values: ENABLED/DISABLED                   | String |
| name                   | Custom domain name. Valid values: letter, digit, dot                     | String |
| type                   | Type of bound origin server. Valid values: REST/WEBSITE                          | String |
| forced_replacement | Overwrites existing configuration. Valid values: CNAME/TXT. If this parameter is entered, the configuration will be distributed after the domain name ownership is forcibly verified | String |
| resp_headers | Header of the returned HTTP response message | Struct |

#### Returned result description

| Return Result | Description | Type |
| :--------- | :---------- | :----- |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg  | Error message | String |
| req_id | Request message ID | String |
