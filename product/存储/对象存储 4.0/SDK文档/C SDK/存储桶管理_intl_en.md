## Overview

This document provides an overview of APIs related to cross-origin access, lifecycle, versioning, and cross-region replication and corresponding SDK sample code.

**Cross-origin access**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permission of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration information of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

**Lifecycle**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning feature of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rule of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rule of a bucket |

## Cross-origin Access

### Setting Cross-origin Access Configuration

#### Feature Description

This API is used to set the cross-origin access permission to a bucket.

#### Method Prototype

```cpp
cos_status_t *cos_put_bucket_cors(const cos_request_options_t *options,
                                  const cos_string_t *bucket, 
                                  cos_list_t *cors_rule_list, 
                                  cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| --------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| cors_rule_list | Bucket cross-origin access configuration information | Struct |
| id | Configures the rule ID | String |
| allowed_origin | Allowed origin. Wildcard `*` is supported | String |
| allowed_method | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | String |
| allowed_header | Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard `*` is supported | String |
| expose_header | Sets custom header information from the server that the browser can receive | String |
| max_age_seconds | Sets the validity period of the result of the OPTIONS request | Int |
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

// Set the cross-origin access configuration
cos_list_t rule_list;
cos_list_init(&rule_list);
cos_cors_rule_content_t *rule_content = NULL;

rule_content = cos_create_cors_rule_content(p);
cos_str_set(&rule_content->id, "testrule1");
cos_str_set(&rule_content->allowed_origin, "http://www.test1.com");
cos_str_set(&rule_content->allowed_method, "GET");
cos_str_set(&rule_content->allowed_header, "*");
cos_str_set(&rule_content->expose_header, "xxx");
rule_content->max_age_seconds = 3600;
cos_list_add_tail(&rule_content->node, &rule_list);

rule_content = cos_create_cors_rule_content(p);
cos_str_set(&rule_content->id, "testrule2");
cos_str_set(&rule_content->allowed_origin, "http://www.test2.com");
cos_str_set(&rule_content->allowed_method, "GET");
cos_str_set(&rule_content->allowed_header, "*");
cos_str_set(&rule_content->expose_header, "yyy");
rule_content->max_age_seconds = 7200;
cos_list_add_tail(&rule_content->node, &rule_list);

rule_content = cos_create_cors_rule_content(p);
cos_str_set(&rule_content->id, "testrule3");
cos_str_set(&rule_content->allowed_origin, "http://www.test3.com");
cos_str_set(&rule_content->allowed_method, "GET");
cos_str_set(&rule_content->allowed_header, "*");
cos_str_set(&rule_content->expose_header, "zzz");
rule_content->max_age_seconds = 60;
cos_list_add_tail(&rule_content->node, &rule_list);

// Set the cross-origin access configuration
s = cos_put_bucket_cors(options, &bucket, &rule_list, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("put bucket cors succeeded\n");
} else {
		printf("put bucket cors failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Querying Cross-origin Access Configuration

#### Feature Description

This API is used to query the cross-origin access configuration information of a bucket.

#### Method Prototype

```cpp
cos_status_t *cos_get_bucket_cors(const cos_request_options_t *options,
                                  const cos_string_t *bucket, 
                                  cos_list_t *cors_rule_list, 
                                  cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| --------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| cors_rule_list | Bucket cross-origin access configuration information | Struct |
| id | Configures the rule ID | String |
| allowed_origin | Allowed origin. Wildcard `*` is supported | String |
| allowed_method | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | String |
| allowed_header | Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard `*` is supported | String |
| expose_header | Sets custom header information from the server that the browser can receive | String |
| max_age_seconds | Sets the validity period of the result of the OPTIONS request | Int |
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

// Get the cross-origin access configuration
cos_list_t rule_list_ret;
cos_list_init(&rule_list_ret);
s = cos_get_bucket_cors(options, &bucket, &rule_list_ret, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("get bucket cors succeeded\n");
		cos_cors_rule_content_t *content = NULL;
		cos_list_for_each_entry(cos_cors_rule_content_t, content, &rule_list_ret, node) {
				printf("cors id:%s, allowed_origin:%s, allowed_method:%s, allowed_header:%s, expose_header:%s, max_age_seconds:%d\n",
						content->id.data, content->allowed_origin.data, content->allowed_method.data, content->allowed_header.data, content->expose_header.data, content->max_age_seconds);
		}
} else {
		printf("get bucket cors failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Deleting Cross-origin Access Configuration

#### Feature Description

This API is used to delete the cross-origin access configuration information of a bucket.

#### Method Prototype

```cpp
cos_status_t *cos_delete_bucket_cors(const cos_request_options_t *options,
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

// Delete the cross-origin access configuration
s = cos_delete_bucket_cors(options, &bucket, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("delete bucket cors succeeded\n");
} else {
		printf("delete bucket cors failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

## Lifecycle

### Setting Lifecycle

#### Feature Description

This API is used to set the lifecycle management configuration for a bucket.

#### Method Prototype

```cpp
cos_status_t *cos_put_bucket_lifecycle(const cos_request_options_t *options,
                                       const cos_string_t *bucket, 
                                       cos_list_t *lifecycle_rule_list, 
                                       cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| lifecycle_rule_list | Lifecycle rule information | Struct |
| id | Lifecycle rule ID | String |
| prefix | Specifies the prefix to which the rule applies | String |
| status | Indicates whether the rule is enabled. Enumerated values: Enabled, Disabled | String |
| expire | Rule expiration attribute | Struct |
| days | Indicates in how many days a deletion or transition operation should be performed or a multipart upload has to be completed once started | Int |
| date | Indicates when the deletion or transition operation is performed | String |
| transition | Transition rule attribute, indicating when an object should be transitioned to Standard_IA or Archive storage class | Struct |
| storage_class | Specifies the transitioned storage class of an object. Enumerated values: Standard_IA, Archive | String |
| abort | Sets the maximum amount of time allowed for a multipart upload to keep running | Struct |
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

// Set the lifecycle information
cos_list_t rule_list;
cos_list_init(&rule_list);
cos_lifecycle_rule_content_t *rule_content = NULL;

rule_content = cos_create_lifecycle_rule_content(p);
cos_str_set(&rule_content->id, "testrule1");
cos_str_set(&rule_content->prefix, "abc/");
cos_str_set(&rule_content->status, "Enabled");
rule_content->expire.days = 60;
cos_list_add_tail(&rule_content->node, &rule_list);

rule_content = cos_create_lifecycle_rule_content(p);
cos_str_set(&rule_content->id, "testrule2");
cos_str_set(&rule_content->prefix, "efg/");
cos_str_set(&rule_content->status, "Disabled");
cos_str_set(&rule_content->transition.storage_class, "Standard_IA");
rule_content->transition.days = 30;
cos_list_add_tail(&rule_content->node, &rule_list);

rule_content = cos_create_lifecycle_rule_content(p);
cos_str_set(&rule_content->id, "testrule3");
cos_str_set(&rule_content->prefix, "xxx/");
cos_str_set(&rule_content->status, "Enabled");
rule_content->abort.days = 1;
cos_list_add_tail(&rule_content->node, &rule_list);

// Set the lifecycle
s = cos_put_bucket_lifecycle(options, &bucket, &rule_list, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("put bucket lifecycle succeeded\n");
} else {
		printf("put bucket lifecycle failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Querying Lifecycle

#### Feature Description

This API is used to query the lifecycle management configuration for a bucket.

#### Method Prototype

```cpp
cos_status_t *cos_get_bucket_lifecycle(const cos_request_options_t *options,
                                       const cos_string_t *bucket, 
                                       cos_list_t *lifecycle_rule_list, 
                                       cos_table_t **resp_headers);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| lifecycle_rule_list | Lifecycle rule information | Struct |
| id | Lifecycle rule ID | String |
| prefix | The prefix to which the rule applies | String |
| status | Whether the rule is enabled. Enumerated values: Enabled, Disabled | String |
| expire | Rule expiration attribute | Struct |
| days | Indicates in how many days a deletion operation should be performed | Int |
| date | Indicates when the deletion operation is performed | String |
| transition | Transition rule attribute, indicating when an object should be transitioned to Standard_IA or Archive storage class | Struct |
| days | Indicates in how many days a transition operation should be performed | Int |
| date | Indicates when the transition operation is performed | String |
| storage_class | Specifies the transitioned storage class of an object. Enumerated values: Standard_IA, Archive | String |
| abort | Sets the maximum amount of time allowed for a multipart upload to keep running | Struct |
| days | Indicates in how many days a multipart upload has to be completed once started | Int |
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

// Query the lifecycle
cos_list_t rule_list_ret;
cos_list_init(&rule_list_ret);
s = cos_get_bucket_lifecycle(options, &bucket, &rule_list_ret, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("get bucket lifecycle succeeded\n");
} else {
		printf("get bucket lifecycle failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Deleting Lifecycle

#### Feature Description

This API is used to delete the lifecycle rule of a bucket.

#### Method Prototype

```cpp
cos_status_t *cos_delete_bucket_lifecycle(const cos_request_options_t *options,
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

// Delete the lifecycle
s = cos_delete_bucket_lifecycle(options, &bucket, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("delete bucket lifecycle succeeded\n");
} else {
		printf("delete bucket lifecycle failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

## Versioning
### Setting Versioning

#### Feature Description

This API is used to set the versioning feature of the specified bucket.

#### Method Prototype
```cpp
cos_status_t *cos_put_bucket_versioning(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        cos_versioning_content_t *versioning, 
                                        cos_table_t **resp_headers);
```

#### Parameter Descriptions
| Parameter Name | Description | Type | 
|---------|---------|---------|
| options | COS request options | Struct |  
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |  
| versioning | Versioning request operation parameter | Struct |  
| status | Whether versioning is enabled. Enumerated values: Suspended, Enabled | String |  
| resp_headers | Header of the returned HTTP response message | Struct |  

#### Return Result Descriptions
| Return Result | Description | Type | 
|---------|---------|---------|
| code | Error code | Int |        
| error_code | Error code | String |   
| error_msg  | Error message | String |   
| req_id | Request message ID | String | 

#### Examples

**Enable versioning**

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

//put bucket versioning
cos_versioning_content_t *versioning = NULL;
versioning = cos_create_versioning_content(p);
cos_str_set(&versioning->status, "Enabled");
s = cos_put_bucket_versioning(options, &bucket, versioning, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("put bucket versioning succeeded\n");
} else {
		printf("put bucket versioning failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

**Suspend versioning**

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

//put bucket versioning
cos_versioning_content_t *versioning = NULL;
versioning = cos_create_versioning_content(p);
cos_str_set(&versioning->status, "Suspended");
s = cos_put_bucket_versioning(options, &bucket, versioning, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("put bucket versioning succeeded\n");
} else {
		printf("put bucket versioning failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Querying Versioning

#### Feature Description

This API is used to query the versioning information of the specified bucket.

#### Method Prototype
```cpp
cos_status_t *cos_get_bucket_versioning(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        cos_versioning_content_t *versioning, 
                                        cos_table_t **resp_headers);
```

#### Parameter Descriptions
| Parameter Name | Description | Type | 
|---------|---------|---------|
| options | COS request options | Struct |  
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |  
| versioning | Versioning request operation parameter | Struct |  
| status | Whether versioning is enabled. Enumerated values: Suspended, Enabled | String |  
| resp_headers | Header of the returned HTTP response message | Struct |  

#### Return Result Descriptions
| Return Result | Description | Type | 
|---------|---------|---------|
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

//get bucket versioning
cos_versioning_content_t *versioning = NULL;
versioning = cos_create_versioning_content(p);
s = cos_get_bucket_versioning(options, &bucket, versioning, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("put bucket versioning succeeded\n");
		printf("bucket versioning status: %s\n", versioning->status.data);
} else {
		printf("put bucket versioning failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

## Cross-region Replication
### Setting Cross-region Replication

#### Feature Description

This API is used to set the cross-region replication rule of the specified bucket.

#### Method Prototype
```cpp
cos_status_t *cos_put_bucket_replication(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         cos_replication_params_t *replication_param, 
                                         cos_table_t **resp_headers);
```

#### Parameter Descriptions
| Parameter Name | Description | Type | 
|---------|---------|---------|
| options | COS request options | Struct |  
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |  
| replication_param | Cross-region replication request operation parameter | Struct |  
| role | Operator account information | String |  
| rule_list | Cross-region replication rule configuration information | Struct |  
| id | Identifies the name of a specific rule | String |  
| status | Identifies whether the rule is in effect. Enumerated values: Enabled, Disabled | String |  
| prefix | Matching prefix. Prefixes cannot overlap; otherwise, an error will be returned | String |  
| dst_bucket | Destination bucket ID in the format of resource ID `qcs::cos:[region]::[bucketname-AppId]`|String|  
| storage_class | Storage class; enumerated values: Standard, Standard_IA <br>Default value: class of the source bucket | String |  
| resp_headers | Header of the returned HTTP response message | Struct |  

#### Return Result Descriptions
| Return Result | Description | Type | 
|---------|---------|---------|
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

// Set the cross-region replication rule
cos_replication_params_t *replication_param = NULL;
replication_param = cos_create_replication_params(p);
cos_str_set(&replication_param->role, "qcs::cam::uin/100000616666:uin/100000616666");

cos_replication_rule_content_t *rule = NULL;
rule = cos_create_replication_rule_content(p);
cos_str_set(&rule->id, "Rule_01");
cos_str_set(&rule->status, "Enabled");
cos_str_set(&rule->prefix, "test1");
cos_str_set(&rule->dst_bucket, "qcs::cos:ap-shanghai::replicationtest-1253686666");
cos_list_add_tail(&rule->node, &replication_param->rule_list);

rule = cos_create_replication_rule_content(p);
cos_str_set(&rule->id, "Rule_02");
cos_str_set(&rule->status, "Disabled");
cos_str_set(&rule->prefix, "test2");
cos_str_set(&rule->storage_class, "Standard_IA");
cos_str_set(&rule->dst_bucket, "qcs::cos:ap-shanghai::replicationtest-1253686666");
cos_list_add_tail(&rule->node, &replication_param->rule_list);

rule = cos_create_replication_rule_content(p);
cos_str_set(&rule->id, "Rule_03");
cos_str_set(&rule->status, "Enabled");
cos_str_set(&rule->prefix, "test3");
cos_str_set(&rule->storage_class, "Standard_IA");
cos_str_set(&rule->dst_bucket, "qcs::cos:ap-shanghai::replicationtest-1253686666");
cos_list_add_tail(&rule->node, &replication_param->rule_list);

s = cos_put_bucket_replication(options, &bucket, replication_param, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("put bucket replication succeeded\n");
} else {
		printf("put bucket replication failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

### Querying Cross-region Replication

#### Feature Description

This API is used to query the cross-region replication rule of the specified bucket.

#### Method Prototype
```cpp
cos_status_t *cos_get_bucket_replication(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         cos_replication_params_t *replication_param, 
                                         cos_table_t **resp_headers);
```

#### Parameter Descriptions
| Parameter Name | Description | Type | 
|---------|---------|---------|
| options | COS request options | Struct |  
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |  
| replication_param | Cross-region replication request operation parameter | Struct |  
| role | Operator account information | String |  
| rule_list | Cross-region replication rule configuration information | Struct |  
| id | Identifies the name of a specific rule | String |  
| status | Identifies whether the rule is in effect. Enumerated values: Enabled, Disabled | String |  
| prefix | Matching prefix. Prefixes cannot overlap; otherwise, an error will be returned | String |  
| dst_bucket | Destination bucket ID in the format of resource ID `qcs::cos:[region]::[bucketname-AppId]`|String|  
| storage_class | Storage class; enumerated values: Standard, Standard_IA <br>Default value: class of the source bucket | String |  
| resp_headers | Header of the returned HTTP response message | Struct |  

#### Return Result Descriptions
| Return Result | Description | Type | 
|---------|---------|---------|
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

// Query the cross-region replication rule
cos_replication_params_t *replication_param2 = NULL;
replication_param2 = cos_create_replication_params(p);
s = cos_get_bucket_replication(options, &bucket, replication_param2, &resp_headers);

if (cos_status_is_ok(s)) {
		printf("get bucket replication succeeded\n");
		printf("ReplicationConfiguration role: %s\n", replication_param2->role.data);
cos_replication_rule_content_t *content = NULL;
		cos_list_for_each_entry(cos_replication_rule_content_t, content, &replication_param2->rule_list, node) {
		printf("ReplicationConfiguration rule, id:%s, status:%s, prefix:%s, dst_bucket:%s, storage_class:%s\n",
						content->id.data, content->status.data, content->prefix.data, content->dst_bucket.data, content->storage_class.data);
		}
} else {
		printf("get bucket replication failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```

## Deleting Cross-region Replication

#### Feature Description

This API is used to delete the cross-region replication rule of the specified bucket.

#### Method Prototype
```cpp
cos_status_t *cos_delete_bucket_replication(const cos_request_options_t *options,
                                            const cos_string_t *bucket, 
                                            cos_table_t **resp_headers);
```

#### Parameter Descriptions
| Parameter Name | Description | Type | 
|---------|---------|---------|
| options | COS request options | Struct |  
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |  
| resp_headers | Header of the returned HTTP response message | Struct |  

#### Return Result Descriptions
| Return Result | Description | Type | 
|---------|---------|---------|
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

// Delete the cross-region replication rule
s = cos_delete_bucket_replication(options, &bucket, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("delete bucket replication succeeded\n");
} else {
		printf("delete bucket replication failed\n");
}

// Terminate the memory pool
cos_pool_destroy(p); 
```
