

## Overview

This document provides an overview of APIs and SDK code samples related to COS inventory.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Setting an inventory job | Sets an inventory job in a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries inventory jobs for a bucket |
|  [List Bucket Inventory Configurations](https://intl.cloud.tencent.com/document/product/436/30627)  | Querying all inventories | Queries all inventory jobs of a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job of a bucket |

## Creating Inventory Job

#### Feature description

This API is used to create an inventory job for a bucket.

#### Method prototype

```c
cos_status_t *cos_put_bucket_inventory(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_inventory_params_t *inventory_params,
                                      cos_table_t **resp_headers
```

#### Sample request

```c
cos_pool_t *pool = NULL;
int is_cname = 0;
int inum = 3, i, len;
char buf[inum][32];
char dest_bucket[128];
cos_status_t *status = NULL;
cos_request_options_t *options = NULL;
cos_table_t *resp_headers = NULL;
cos_string_t bucket;
cos_inventory_params_t *get_params = NULL;
cos_inventory_optional_t *optional = NULL;
cos_list_inventory_params_t *list_params = NULL;
  
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
  
// put bucket inventory 
len = snprintf(dest_bucket, 128, "qcs::cos:%s::%s", TEST_REGION, TEST_BUCKET_NAME);
dest_bucket[len] = 0;
// Set multiple inventories
for (i = 0; i < inum; i++) {
	cos_inventory_params_t *params = cos_create_inventory_params(pool);
	cos_inventory_optional_t *optional;
	len = snprintf(buf[i], 32, "id%d", i);
	buf[i][len] = 0;
	cos_str_set(&params->id, buf[i]);
	cos_str_set(&params->is_enabled, "true");
	cos_str_set(&params->frequency, "Daily");
	cos_str_set(&params->filter_prefix, "myPrefix");
	cos_str_set(&params->included_object_versions, "All");
	cos_str_set(&params->destination.format, "CSV");
	cos_str_set(&params->destination.account_id, TEST_UIN);
	cos_str_set(&params->destination.bucket, dest_bucket);
	cos_str_set(&params->destination.prefix, "invent");
	params->destination.encryption = 1;
	optional = cos_create_inventory_optional(pool);
	cos_str_set(&optional->field, "Size");
	cos_list_add_tail(&optional->node, &params->fields);
	optional = cos_create_inventory_optional(pool);
	cos_str_set(&optional->field, "LastModifiedDate");
	cos_list_add_tail(&optional->node, &params->fields);
	optional = cos_create_inventory_optional(pool);
	cos_str_set(&optional->field, "ETag");
	cos_list_add_tail(&optional->node, &params->fields);
	optional = cos_create_inventory_optional(pool);
	cos_str_set(&optional->field, "StorageClass");
	cos_list_add_tail(&optional->node, &params->fields);
	optional = cos_create_inventory_optional(pool);
	cos_str_set(&optional->field, "ReplicationStatus");
	cos_list_add_tail(&optional->node, &params->fields);
  
  	// Set bucket inventory
	status = cos_put_bucket_inventory(options, &bucket, params, &resp_headers);
	log_status(status);
}

// Terminate the memory pool
cos_pool_destroy(pool);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket  | Bucket for which to set an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| inventory_params | Inventory configuration information of bucket                                           | Struct   |
| node                     | Used to link inventory configuration to the `list inventory` API                           | List   |
| id                       | Inventory name, corresponding to the ID in the request parameter                           | String |
| is_enabled              | Inventory status flag: <br><li>If this is set to `true`, the inventory is enabled; <br><li>if `false`, no inventories will be generated | Struct        |
| frequency | Inventory job frequency. Enumerated values: Daily, Weekly | String |
| filter_prefix            | Prefix of the objects to be analyzed                                         | String |
| included_object_versions | Whether to include object versions in the inventory <br><li>If this is set to `All`, the inventory will include all object versions and add `VersionId`, `IsLatest`, and `DeleteMarker` fields <br><li>If `Current`, no object version information will be included in the inventory | String |
| destination              | Destination to store the inventory result                                       | Struct |
| format | File format of the inventory result. CSV is available | String |
| account_id               | Bucket owner ID, such as 100000000001 | String |
| bucket | Name of the bucket where the inventory result is stored | String |
| prefix | Prefix of the inventory result | String |
| encryption               | Option to provide server-side encryption for the inventory result                               | Int    |
| fields                   | Sets the analysis items that should be included in the inventory result                               | Struct |
| field                    | Name of the analysis items that can be optionally included in the inventory result. Valid values: Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, ReplicationStatus | String |
| resp_headers | Returns the HTTP response headers | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int |
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Error code description

The following describes some common errors that may occur when you make requests using this API.

| Error Code | Description | Status Code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied          | Unauthorized access. You most likely do not have access permission for the bucket | HTTP 403 Forbidden   |

## Querying Inventory Jobs

#### Feature description

This API (GET Bucket inventory) is used to query the inventory job information in a bucket.

#### Method prototype

```c
cos_status_t *cos_get_bucket_inventory(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_inventory_params_t *inventory_params,
                                      cos_table_t **resp_headers);
```

#### Sample request

```c
cos_pool_t *pool = NULL;
int is_cname = 0;
int inum = 3, i, len;
char buf[inum][32];
char dest_bucket[128];
cos_status_t *status = NULL;
cos_request_options_t *options = NULL;
cos_table_t *resp_headers = NULL;
cos_string_t bucket;
cos_inventory_params_t *get_params = NULL;
cos_inventory_optional_t *optional = NULL;
cos_list_inventory_params_t *list_params = NULL;
  
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
  
// get inventory 
get_params = cos_create_inventory_params(pool);
cos_str_set(&get_params->id, buf[inum/2]);
status = cos_get_bucket_inventory(options, &bucket, get_params, &resp_headers);
log_status(status); 

// Terminate the memory pool
cos_pool_destroy(pool);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for which to query an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| inventory_params         | Used to link inventory configuration to the `list inventory` API                         | Struct |
| node                     | Links inventory configuration                                                 | List   |
| id                       | Inventory name, corresponding to the ID in the request parameter                           | String |
| is_enabled              | Inventory status flag: <br><li>If this is set to `true`, the inventory is enabled; <br><li>if `false`, no inventories will be generated | Struct        |
| frequency | Inventory job frequency. Enumerated values: Daily, Weekly | String |
| filter_prefix            | Prefix of the objects to be analyzed                                         | String |
| included_object_versions | Whether to include object versions in the inventory <br><li>If this is set to `All`, the inventory will include all object versions and add `VersionId`, `IsLatest`, and `DeleteMarker` fields <br><li>If `Current`, no object version information will be included in the inventory | String |
| destination              | Destination to store the inventory result                                       | Struct |
| format | File format of the inventory result. CSV is available | String |
| account_id               | Bucket owner ID, such as 100000000001 | String |
| bucket | Name of the bucket where the inventory result is stored | String |
| prefix | Prefix of the inventory result | String |
| encryption               | Option to provide server-side encryption for the inventory result                               | Int    |
| fields                   | Sets the analysis items that should be included in the inventory result                               | Struct |
| field                    | Name of the analysis items that can be optionally included in the inventory result. Valid values: Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, ReplicationStatus | String |
| resp_headers | Returns the HTTP response headers | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int |
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

## Querying All Inventories

#### Feature description

This API (List Bucket Inventory Configurations) is used to request that all inventory jobs in a bucket be returned. Up to 1,000 inventory jobs can be configured in one bucket.

#### Method prototype

```c
cos_status_t *cos_list_bucket_inventory(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_list_inventory_params_t *inventory_params,
                                      cos_table_t **resp_headers);
```

#### Sample request

```c
cos_pool_t *pool = NULL;
int is_cname = 0;
int inum = 3, i, len;
char buf[inum][32];
char dest_bucket[128];
cos_status_t *status = NULL;
cos_request_options_t *options = NULL;
cos_table_t *resp_headers = NULL;
cos_string_t bucket;
cos_inventory_params_t *get_params = NULL;
cos_inventory_optional_t *optional = NULL;
cos_list_inventory_params_t *list_params = NULL;
  
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
  
// list inventory
list_params = cos_create_list_inventory_params(pool); 
status = cos_list_bucket_inventory(options, &bucket, list_params, &resp_headers);
log_status(status);

// View the result
get_params = NULL;
cos_list_for_each_entry(cos_inventory_params_t, get_params, &list_params->inventorys, node) {
	printf("id: %s\nis_enabled: %s\nfrequency: %s\nfilter_prefix: %s\nincluded_object_versions: %s\n",  get_params->id.data, get_params->is_enabled.data, get_params->frequency.data, get_params->filter_prefix.data, get_params->included_object_versions.data);
	printf("destination:\n");
	printf("\tencryption: %d\n", get_params->destination.encryption);
	printf("\tformat: %s\n", get_params->destination.format.data);
	printf("\taccount_id: %s\n", get_params->destination.account_id.data);
	printf("\tbucket: %s\n", get_params->destination.bucket.data);
	printf("\tprefix: %s\n", get_params->destination.prefix.data);
	cos_list_for_each_entry(cos_inventory_optional_t, optional, &get_params->fields, node) {
		printf("field: %s\n", optional->field.data);
	}
}

// Terminate the memory pool
cos_pool_destroy(pool);
```

#### Parameter description

| Parameter | Description | Type |
| ----------------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Destination bucket to store inventory results in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |
| inventory_params        | All inventory configuration information of bucket                                       | Struct |
| inventorys              | Links node members of `cos_inventory_params_t`                     | List   |
| is_truncated            | Flag about whether all inventory jobs have been listed. If yes, it is `false`; otherwise, it is `true` | Struct |
| continuation_token      | Flag of the inventory list on the current page, which can be understood as the page number. It corresponds to the `continuation-token` parameter in the request | String |
| next_continuation_token | Flag of the next page of inventory list. If there is a value in this parameter, the value can be used as the `continuation-token` parameter to initiate a GET request to get the inventory job information of the next page | String |
| resp_headers | Returns the HTTP response headers | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int |
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

## Deleting Inventory Job

#### Feature description

This API (DELETE Bucket inventory) is used to delete a specified inventory job of a bucket.

#### Method prototype

```c
cos_status_t *cos_delete_bucket_inventory(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      const cos_string_t *id,
                                      cos_table_t **resp_headers);
```

#### Sample request

```c
cos_pool_t *pool = NULL;
int is_cname = 0;
int inum = 3, i, len;
char buf[inum][32];
char dest_bucket[128];
cos_status_t *status = NULL;
cos_request_options_t *options = NULL;
cos_table_t *resp_headers = NULL;
cos_string_t bucket;
cos_inventory_params_t *get_params = NULL;
cos_inventory_optional_t *optional = NULL;
cos_list_inventory_params_t *list_params = NULL;
  
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
  
// delete inventory
for (i = 0; i < inum; i++) {
	cos_string_t id;
	cos_str_set(&id, buf[i]);
	status = cos_delete_bucket_inventory(options, &bucket, &id, &resp_headers);
	log_status(status);
}

// Terminate the memory pool
cos_pool_destroy(pool);
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for which to delete an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| id           | Inventory name                                                   | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int |
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |
