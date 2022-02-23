

## Overview

This document provides an overview of APIs and SDK code samples related to COS inventory.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Creating an inventory job | Creates an inventory job for a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries the inventory jobs of a bucket |
|  [List Bucket Inventory Configurations](https://intl.cloud.tencent.com/document/product/436/30627) | Querying the list of inventory configurations | Queries the list of inventory configurations for a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job from a bucket |

## Creating an Inventory Job

#### Description

This API (PUT Bucket inventory) is used to create an inventory job for a bucket.

#### Method prototype

```c
cos_status_t *cos_put_bucket_inventory(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_inventory_params_t *inventory_params,
                                      cos_table_t **resp_headers
```

#### Sample request

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                //your secret_id
static char *TEST_ACCESS_KEY_SECRET;            //your secret_key
// The only user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    //your appid
// Region information. For more information about the enumerated values (such as ap-beijing, ap-hongkong, and eu-frankfurtplease), please visit https://cloud.tencent.com/document/product/436/6224.
static char TEST_REGION[] = "ap-guangzhou";    //region in endpoint
// Object owner, e.g., user UIN: 100000000001
static char TEST_UIN[] = "<Uin>";    //your uin
// COS bucket name, in the format of [bucket]-[appid], for example `mybucket-1253666666`. It can be obtained at https://console.cloud.tencent.com/cos5/bucket.
static char TEST_BUCKET_NAME[] = "<bucketname-appid>";

void log_status(cos_status_t *s)
{
    cos_warn_log("status->code: %d", s->code);
    if (s->error_code) cos_warn_log("status->error_code: %s", s->error_code);
    if (s->error_msg) cos_warn_log("status->error_msg: %s", s->error_msg);
    if (s->req_id) cos_warn_log("status->req_id: %s", s->req_id);
}

void init_test_config(cos_config_t *config, int is_cname)
{
    cos_str_set(&config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&config->appid, TEST_APPID);
    config->is_cname = is_cname;
}

void init_test_request_options(cos_request_options_t *options, int is_cname)
{
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    options->ctl = cos_http_controller_create(options->pool, 0);
}

void test_put_bucket_inventory()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    int inum = 3, i, len;
    char buf[inum][32];
    char dest_bucket[128];
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;
    
    // Create a memory pool
    cos_pool_create(&pool, NULL);
    
    // Initialize the request options
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
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

    // Destroy the memory pool
    cos_pool_destroy(pool);
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    //set log level, default COS_LOG_WARN
    cos_log_set_level(COS_LOG_WARN);

    //set log output, default stderr
    cos_log_set_output(NULL);

    test_put_bucket_inventory();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| ------------------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for inventory job setting, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| inventory_params | Inventory configuration information of bucket | Struct   |
| node | Used to link inventory configuration to the `list inventory` API | List |
| id | Inventory name, corresponding to the ID in the request parameter | String |
| is_enabled | Indicates whether to enable inventory<br><li>`true`: enable<br><li>`false`: no inventory will be generated. | Struct |
| frequency | Frequency of the inventory job. Enumerated values: `Daily`, `Weekly` | String |
| filter_prefix | Prefix of the objects to analyze | String |
| included_object_versions | Indicates whether to include object versions in the inventory<br><li>If this is set to `All`, the inventory will include all object versions and the additional fields `VersionId`, `IsLatest`, and `DeleteMarker`.<br><li>If this is set to `Current`, no object versions will be included in the inventory. | String |
| destination              | Destination to store the inventory result                                       | Struct |
| format             | Format of the inventory results. Valid value: `CSV`                                           | String      |
| account_id             | ID of the bucket owner, e.g., 100000000001                                           | String      |
| bucket             | Name of the bucket that stores the inventory results                                           | String      |
| prefix | Prefix of the inventory result | String |
| encryption                | Option of enabling server-side encryption for inventory results                               | Int   |
| fields                   | Sets the analysis items to be included in the inventory results                               | Struct |
| field | Optional analysis dimensions, including `Size`, `LastModifiedDate`, `StorageClass`, `ETag`, `IsMultipartUploaded`, and `ReplicationStatus` | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Error codes

The following describes some common errors that may occur when you call this API:

| Error Code | Description | Status Code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied          | Unauthorized access. You most likely do not have access permission for the bucket | HTTP 403 Forbidden   |

## Querying Inventory Jobs

#### Description

This API is used to query the inventory jobs of a bucket.

#### Method prototype

```c
cos_status_t *cos_get_bucket_inventory(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_inventory_params_t *inventory_params,
                                      cos_table_t **resp_headers);
```

#### Sample request

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                //your secret_id
static char *TEST_ACCESS_KEY_SECRET;            //your secret_key
// The only user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    //your appid
// COS bucket name, in the format of [bucket]-[appid], for example `mybucket-1253666666`. It can be obtained at https://console.cloud.tencent.com/cos5/bucket.
static char TEST_BUCKET_NAME[] = "<bucketname-appid>";

void log_status(cos_status_t *s)
{
    cos_warn_log("status->code: %d", s->code);
    if (s->error_code) cos_warn_log("status->error_code: %s", s->error_code);
    if (s->error_msg) cos_warn_log("status->error_msg: %s", s->error_msg);
    if (s->req_id) cos_warn_log("status->req_id: %s", s->req_id);
}

void init_test_config(cos_config_t *config, int is_cname)
{
    cos_str_set(&config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&config->appid, TEST_APPID);
    config->is_cname = is_cname;
}

void init_test_request_options(cos_request_options_t *options, int is_cname)
{
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    options->ctl = cos_http_controller_create(options->pool, 0);
}

void test_get_bucket_inventory()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    int inum = 3;
    char buf[inum][32];
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;
    cos_inventory_params_t *get_params = NULL;
    cos_inventory_optional_t *optional = NULL;
    
    // Create a memory pool
    cos_pool_create(&pool, NULL);
    
    // Initialize the request options
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    
    // get inventory 
    get_params = cos_create_inventory_params(pool);
    cos_str_set(&get_params->id, buf[inum/2]);
    status = cos_get_bucket_inventory(options, &bucket, get_params, &resp_headers);
    log_status(status); 

    printf("id: %s\nis_enabled: %s\nfrequency: %s\nfilter_prefix: %s\nincluded_object_versions: %s\n", 
            get_params->id.data, get_params->is_enabled.data, get_params->frequency.data, get_params->filter_prefix.data, get_params->included_object_versions.data);
    printf("destination:\n");
    printf("\tencryption: %d\n", get_params->destination.encryption);
    printf("\tformat: %s\n", get_params->destination.format.data);
    printf("\taccount_id: %s\n", get_params->destination.account_id.data);
    printf("\tbucket: %s\n", get_params->destination.bucket.data);
    printf("\tprefix: %s\n", get_params->destination.prefix.data);
    cos_list_for_each_entry(cos_inventory_optional_t, optional, &get_params->fields, node) {
        printf("field: %s\n", optional->field.data);
    }

    // Destroy the memory pool
    cos_pool_destroy(pool);
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    //set log level, default COS_LOG_WARN
    cos_log_set_level(COS_LOG_WARN);

    //set log output, default stderr
    cos_log_set_output(NULL);

    test_get_bucket_inventory();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| ------------------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for inventory job query, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| inventory_params         | Used to link inventory configuration to the `list inventory` API                         | Struct |
| node                     | Links inventory configuration                                                 | List   |
| id                       | Inventory name, corresponding to the ID in the request parameter                           | String |
| is_enabled | Indicates whether to enable inventory.<br><li>`true`: enable<br><li>`false`: no inventory will be generated. | Struct |
| frequency | Frequency of the inventory job. Enumerated values: `Daily`, `Weekly` | String |
| filter_prefix | Prefix of the objects to analyze | String |
| included_object_versions | Indicates whether to include object versions in the inventory<br><li>If this is set to `All`, the inventory will include all object versions and the additional fields `VersionId`, `IsLatest`, and `DeleteMarker`.<br><li>If this is set to `Current`, no object versions will be included in the inventory. | String |
| destination              | Destination to store the inventory result                                       | Struct |
| format             | Format of the inventory results. Valid value: `CSV`                                           | String      |
| account_id             | ID of the bucket owner, e.g., 100000000001                                           | String      |
| bucket             | Name of the bucket that stores the inventory results                                           | String      |
| prefix | Prefix of the inventory result | String |
| encryption                | Option of enabling server-side encryption for inventory results                               | Int   |
| fields                   | Sets the analysis items to be included in the inventory results                               | Struct |
| field | Optional analysis dimensions, including `Size`, `LastModifiedDate`, `StorageClass`, `ETag`, `IsMultipartUploaded`, and `ReplicationStatus` | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

## Querying All Inventories

#### Description

This API is used to query all inventory jobs set for a bucket. You can configure up to 1,000 inventory jobs for a bucket.

#### Method prototype

```c
cos_status_t *cos_list_bucket_inventory(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_list_inventory_params_t *inventory_params,
                                      cos_table_t **resp_headers);
```

#### Sample request

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                //your secret_id
static char *TEST_ACCESS_KEY_SECRET;            //your secret_key
// The only user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    //your appid
// COS bucket name, in the format of [bucket]-[appid], for example `mybucket-1253666666`. It can be obtained at https://console.cloud.tencent.com/cos5/bucket.
static char TEST_BUCKET_NAME[] = "<bucketname-appid>";

void log_status(cos_status_t *s)
{
    cos_warn_log("status->code: %d", s->code);
    if (s->error_code) cos_warn_log("status->error_code: %s", s->error_code);
    if (s->error_msg) cos_warn_log("status->error_msg: %s", s->error_msg);
    if (s->req_id) cos_warn_log("status->req_id: %s", s->req_id);
}

void init_test_config(cos_config_t *config, int is_cname)
{
    cos_str_set(&config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&config->appid, TEST_APPID);
    config->is_cname = is_cname;
}

void init_test_request_options(cos_request_options_t *options, int is_cname)
{
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    options->ctl = cos_http_controller_create(options->pool, 0);
}

void test_list_bucket_inventory()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
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
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    
    // list inventory
    list_params = cos_create_list_inventory_params(pool); 
    status = cos_list_bucket_inventory(options, &bucket, list_params, &resp_headers);
    log_status(status);

    // View results
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

    // Destroy the memory pool
    cos_pool_destroy(pool);
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    //set log level, default COS_LOG_WARN
    cos_log_set_level(COS_LOG_WARN);

    //set log output, default stderr
    cos_log_set_output(NULL);

    test_list_bucket_inventory();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| ----------------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct  |
| bucket | Destination bucket to store inventory results in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |
| inventory_params        | All inventory configuration information of bucket                                       | Struct |
| inventorys              | Links node members of `cos_inventory_params_t`                     | List   |
| is_truncated            | Flag about whether all inventory jobs have been listed. If yes, it is `false`; otherwise, it is `true` | Struct |
| continuation_token      | Flag of the inventory list on the current page, which can be understood as the page number. It corresponds to the `continuation-token` parameter in the request | String |
| next_continuation_token | Identifier of the next response. You can pass the value of this parameter to `continuation-token` and initiate a GET request to obtain the inventory jobs from the next response | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

## Deleting an Inventory Job

#### Description

This API is used to delete a specified inventory job from a bucket.

#### Method prototype

```c
cos_status_t *cos_delete_bucket_inventory(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      const cos_string_t *id,
                                      cos_table_t **resp_headers);
```

#### Sample request

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                //your secret_id
static char *TEST_ACCESS_KEY_SECRET;            //your secret_key
// The only user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    //your appid
// COS bucket name, in the format of [bucket]-[appid], for example `mybucket-1253666666`. It can be obtained at https://console.cloud.tencent.com/cos5/bucket.
static char TEST_BUCKET_NAME[] = "<bucketname-appid>";

void log_status(cos_status_t *s)
{
    cos_warn_log("status->code: %d", s->code);
    if (s->error_code) cos_warn_log("status->error_code: %s", s->error_code);
    if (s->error_msg) cos_warn_log("status->error_msg: %s", s->error_msg);
    if (s->req_id) cos_warn_log("status->req_id: %s", s->req_id);
}

void init_test_config(cos_config_t *config, int is_cname)
{
    cos_str_set(&config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&config->appid, TEST_APPID);
    config->is_cname = is_cname;
}

void init_test_request_options(cos_request_options_t *options, int is_cname)
{
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    options->ctl = cos_http_controller_create(options->pool, 0);
}

void test_delete_bucket_inventory()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;
    int inum = 3, i;
    char buf[inum][32];
    
    // Create a memory pool
    cos_pool_create(&pool, NULL);
    
    // Initialize the request options
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    
    // delete inventory
    for (i = 0; i < inum; i++) {
        cos_string_t id;
        cos_str_set(&id, buf[i]);
        status = cos_delete_bucket_inventory(options, &bucket, &id, &resp_headers);
        log_status(status);
    }

    // Destroy the memory pool
    cos_pool_destroy(pool);
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    //set log level, default COS_LOG_WARN
    cos_log_set_level(COS_LOG_WARN);

    //set log output, default stderr
    cos_log_set_output(NULL);

    test_delete_bucket_inventory();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket for inventory job deletion, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| id           | Inventory name                                                   | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| :--------- | :---------- | :----- |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |
