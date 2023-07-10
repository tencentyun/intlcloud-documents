## Overview

This document provides an overview of APIs and SDK code samples related to cross-origin resource sharing (CORS), lifecycle, versioning, and cross-region replication.

**CORS**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting CORS | Sets CORS permissions for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying CORS configuration | Queries the CORS configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting CORS configuration | Deletes the CORS configuration of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle configuration | Sets lifecycle for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying a lifecycle configuration | Queries the lifecycle configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting a lifecycle configuration | Deletes the lifecycle configuration of a bucket |

**Versioning**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting a cross-region replication rule | Sets a cross-region replication rule for a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying a cross-region replication rule | Queries the cross-region replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting a cross-region replication rule | Deletes the cross-region replication rule from a bucket |

## CORS

### Setting CORS

#### Description

This API is used to configure the cross-origin resource sharing (CORS) permission of a bucket.

#### Method prototype

```cpp
cos_status_t *cos_put_bucket_cors(const cos_request_options_t *options,
                                  const cos_string_t *bucket, 
                                  cos_list_t *cors_rule_list, 
                                  cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| --------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| cors_rule_list  | Bucket CORS configuration                                           | Struct |
| id              | Rule ID                                                  | String |
| allowed_origin  | Allowed access sources. The wildcard `*` is supported.                                | String |
| allowed_method  | Allowed HTTP operations. Enumerated values: `GET`, `PUT`, `HEAD`, `POST`, `DELETE`       | String |
| allowed_header | Custom HTTP request headers that can be included in subsequent `OPTIONS` requests sent. The wildcard `*` is supported. | String |
| expose_header | Custom header information that can be received by the browser from the server | String |
| max_age_seconds | Validity period of the `OPTIONS` request result | Int |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
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

void test_put_cors()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;
   
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

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

    // Set CORS
    s = cos_put_bucket_cors(options, &bucket, &rule_list, &resp_headers);
    log_status(s);
    
    cos_pool_destroy(p);
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_put_cors();

    cos_http_io_deinitialize();

    return 0;
}
```

### Querying a CORS configuration

#### Description

This API is used to query the CORS configuration of a bucket.

#### Method prototype

```cpp
cos_status_t *cos_get_bucket_cors(const cos_request_options_t *options,
                                  const cos_string_t *bucket, 
                                  cos_list_t *cors_rule_list, 
                                  cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| --------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| cors_rule_list  | Bucket CORS configuration                                           | Struct |
| id              | Rule ID                                                  | String |
| allowed_origin  | Allowed access sources. The wildcard `*` is supported.                                | String |
| allowed_method  | Allowed HTTP operations. Enumerated values: `GET`, `PUT`, `HEAD`, `POST`, `DELETE`       | String |
| allowed_header | Custom HTTP request headers that can be included in subsequent `OPTIONS` requests sent. The wildcard `*` is supported. | String |
| expose_header | Custom header information that can be received by the browser from the server | String |
| max_age_seconds | Validity period of the `OPTIONS` request result | Int |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
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

void test_get_cors()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;
   
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

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

    // Query CORS configuration
    cos_list_t rule_list_ret;
    cos_list_init(&rule_list_ret);
    s = cos_get_bucket_cors(options, &bucket, &rule_list_ret, &resp_headers);
    log_status(s);
    cos_cors_rule_content_t *content = NULL;
    cos_list_for_each_entry(cos_cors_rule_content_t, content, &rule_list_ret, node) {
        printf("cors id:%s, allowed_origin:%s, allowed_method:%s, allowed_header:%s, expose_header:%s, max_age_seconds:%d\n",
                content->id.data, content->allowed_origin.data, content->allowed_method.data, content->allowed_header.data, content->expose_header.data, content->max_age_seconds);
    }
    
    cos_pool_destroy(p);
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_get_cors();

    cos_http_io_deinitialize();

    return 0;
}
```

### Deleting CORS configuration

#### Description

This API is used to delete the CORS configuration of a bucket.

#### Method prototype

```cpp
cos_status_t *cos_delete_bucket_cors(const cos_request_options_t *options,
                                     const cos_string_t *bucket, 
                                     cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
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

void test_delete_cors()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;
   
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

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

    // Delete CORS configuration
    cos_delete_bucket_cors(options, &bucket, &resp_headers);
    log_status(s);
    
    cos_pool_destroy(p);
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_delete_cors();

    cos_http_io_deinitialize();

    return 0;
}
```

## Lifecycle

### Setting lifecycle configuration

#### Description

This API is used to set the lifecycle configuration of a bucket.

#### Method prototype

```cpp
cos_status_t *cos_put_bucket_lifecycle(const cos_request_options_t *options,
                                       const cos_string_t *bucket, 
                                       cos_list_t *lifecycle_rule_list, 
                                       cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| lifecycle_rule_list | Lifecycle rule information                                             | Struct |
| id                  | Lifecycle rule ID                                              | String |
| prefix              | Prefix to which the rule applies                                         | String |
| status              | Whether to enable the rule. Enumerated values: `Enabled`, `Disabled`                  | String |
| expire              | Rule expiration attribute                                                 | Struct |
| days                | Number of days before the deletion or transition operation is performed; number of days within which the multipart upload must be completed after it starts | Int    |
| date                | Date when the deletion or transition operation is performed                             | String |
| transition | Rule transition attribute, which indicates when the object is transited to Standard_IA or Archive | Struct |
| storage_class | Target storage class to which the object is transited. Enumerated values: `Standard_IA`, `Archive` | String |
| abort               | Maximum time length allowed for a multipart upload                           | Struct |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
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

void test_put_bucket_lifecycle()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;
   
    // Initialize the request options
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Set lifecycle information
    cos_list_t rule_list;
    cos_list_init(&rule_list);
    cos_lifecycle_rule_content_t *rule_content = NULL;

    rule_content = cos_create_lifecycle_rule_content(p);
    cos_str_set(&rule_content->id, "testrule1");
    cos_str_set(&rule_content->prefix, "abc/");
    cos_str_set(&rule_content->status, "Enabled");
    rule_content->expire.days = 365;
    cos_list_add_tail(&rule_content->node, &rule_list);

    rule_content = cos_create_lifecycle_rule_content(p);
    cos_str_set(&rule_content->id, "testrule2");
    cos_str_set(&rule_content->prefix, "efg/");
    cos_str_set(&rule_content->status, "Disabled");
    cos_str_set(&rule_content->transition.storage_class, "Standard_IA");
    rule_content->transition.days = 999;
    cos_list_add_tail(&rule_content->node, &rule_list);

    rule_content = cos_create_lifecycle_rule_content(p);
    cos_str_set(&rule_content->id, "testrule3");
    cos_str_set(&rule_content->prefix, "xxx/");
    cos_str_set(&rule_content->status, "Enabled");
    rule_content->abort.days = 1;
    cos_list_add_tail(&rule_content->node, &rule_list);
    
    // Configure the lifecycle
    s = cos_put_bucket_lifecycle(options, &bucket, &rule_list, &resp_headers);
    log_status(s);
    
    cos_pool_destroy(p);    
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_put_bucket_lifecycle();

    cos_http_io_deinitialize();

    return 0;
}
```

### Querying a lifecycle configuration

#### Description

This API is used to query the lifecycle management configuration of a bucket.

#### Method prototype

```cpp
cos_status_t *cos_get_bucket_lifecycle(const cos_request_options_t *options,
                                       const cos_string_t *bucket, 
                                       cos_list_t *lifecycle_rule_list, 
                                       cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| lifecycle_rule_list | Lifecycle rule information                                             | Struct |
| id                  | Lifecycle rule ID                                              | String |
| prefix              | Prefix to which the rule applies                                         | String |
| status              | Whether to enable the rule. Enumerated values: `Enabled`, `Disabled`                  | String |
| expire              | Rule expiration attribute                                                 | Struct |
| days                | Number of days before the deletion operation is performed                                     | Int    |
| date                | Date when the deletion operation is performed                                       | String |
| transition | Rule transition attribute, which indicates when the object is transited to Standard_IA or Archive | Struct |
| days                | Number of days before the transition operation is performed                                     | Int    |
| date                | Date when the transition operation is performed                                       | String |
| storage_class | Target storage class to which the object is transited. Enumerated values: `Standard_IA`, `Archive` | String |
| abort               | Maximum time length allowed for a multipart upload                           | Struct |
| days                | Number of days within which the multipart upload must be completed after it starts                       | Int    |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
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

void test_get_bucket_lifecycle()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;
   
    // Initialize the request options
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Query a lifecycle configuration
    cos_list_t rule_list_ret;
    cos_list_init(&rule_list_ret);
    s = cos_get_bucket_lifecycle(options, &bucket, &rule_list_ret, &resp_headers);
    if (cos_status_is_ok(s)) {
            printf("get bucket lifecycle succeeded\n");
    } else {
            printf("get bucket lifecycle failed\n");
    }
    
    cos_pool_destroy(p);    
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_get_bucket_lifecycle();

    cos_http_io_deinitialize();

    return 0;
}
```

### Deleting a lifecycle configuration

#### Description

This API is used to delete the lifecycle configuration of a bucket.

#### Method prototype

```cpp
cos_status_t *cos_delete_bucket_lifecycle(const cos_request_options_t *options,
                                          const cos_string_t *bucket, 
                                          cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
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

void test_delete_bucket_lifecycle()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;
   
    // Initialize the request options
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Delete a lifecycle configuration
    s = cos_delete_bucket_lifecycle(options, &bucket, &resp_headers);
    if (cos_status_is_ok(s)) {
            printf("delete bucket lifecycle succeeded\n");
    } else {
            printf("delete bucket lifecycle failed\n");
    }
    
    cos_pool_destroy(p);    
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_delete_bucket_lifecycle();

    cos_http_io_deinitialize();

    return 0;
}
```

## Versioning
### Setting versioning

#### Description

This API is used to set the versioning configuration for a bucket.

#### Method prototype
```cpp
cos_status_t *cos_put_bucket_versioning(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        cos_versioning_content_t *versioning, 
                                        cos_table_t **resp_headers);
```

#### Parameter description
| Parameter | Description | Type |
|---------|---------|---------|
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| versioning | Versioning request operation parameters |Struct|
| status | Whether to enable versioning. Enumerated values: `Suspended`, `Enabled` | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description
| Response | Description | Type |
|---------|---------|---------|
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample

**Enabling versioning**

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
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

void test_put_versioning()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;
   
   // Initialize the request options
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Put bucket versioning
    cos_versioning_content_t *versioning = NULL;
    versioning = cos_create_versioning_content(p);
    cos_str_set(&versioning->status, "Enabled");
    s = cos_put_bucket_versioning(options, &bucket, versioning, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put bucket versioning succeeded\n");
    } else {
        printf("put bucket versioning failed\n");
    }
    
    cos_pool_destroy(p);
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_put_versioning();

    cos_http_io_deinitialize();

    return 0;
}
```

**Suspending Versioning**

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
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

void test_put_versioning()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;
   
   // Initialize the request options
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Put bucket versioning
    cos_versioning_content_t *versioning = NULL;
    versioning = cos_create_versioning_content(p);
    cos_str_set(&versioning->status, "Suspended");
    s = cos_put_bucket_versioning(options, &bucket, versioning, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put bucket versioning succeeded\n");
    } else {
        printf("put bucket versioning failed\n");
    }
    
    cos_pool_destroy(p);
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_put_versioning();

    cos_http_io_deinitialize();

    return 0;
}
```

### Querying versioning

#### Description

This API is used to query the versioning configuration of a specified bucket.

#### Method prototype
```cpp
cos_status_t *cos_get_bucket_versioning(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        cos_versioning_content_t *versioning, 
                                        cos_table_t **resp_headers);
```

#### Parameter description
| Parameter | Description | Type |
|---------|---------|---------|
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| versioning | Versioning request operation parameters |Struct|
| status | Whether to enable versioning. Enumerated values: `Suspended`, `Enabled` | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description
| Response | Description | Type |
|---------|---------|---------|
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample
```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
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

void test_get_versioning()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;
   
   // Initialize the request options
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Get bucket versioning
    cos_versioning_content_t *versioning = NULL;
    versioning = cos_create_versioning_content(p);
    s = cos_get_bucket_versioning(options, &bucket, versioning, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put bucket versioning succeeded\n");
        printf("bucket versioning status: %s\n", versioning->status.data);
    } else {
        printf("put bucket versioning failed\n");
    }
    
    cos_pool_destroy(p);
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_get_versioning();

    cos_http_io_deinitialize();

    return 0;
}
```

## Cross-Region Replication
### Setting a cross-region replication rule

#### Description

This API is used to set the cross-region replication rules of a specified bucket.

#### Method prototype
```cpp
cos_status_t *cos_put_bucket_replication(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         cos_replication_params_t *replication_param, 
                                         cos_table_t **resp_headers);
```

#### Parameter description
| Parameter | Description | Type |
|---------|---------|---------|
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| replication_param | Cross-region replication request operation parameters |Struct|
| role | Operator's account information | String |
| rule_list | Cross-region replication rule configuration | Struct |
| id | Name of a specific rule | String |
| status | Rule status identifier. Enumerated values: `Enabled`, `Disabled` | String |
| prefix | Prefix match. Prefixes cannot overlap; otherwise, an error is returned | String |
| dst_bucket | Destination bucket ID. Format: `qcs::cos:[region]::[bucketname-AppId]` | String |
| storage_class | Storage class. Enumerated values: `Standard`, `Standard_IA`<br>Defaults to the storage class of the source bucket. | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description
| Response | Description | Type |
|---------|---------|---------|
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample
```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
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

void test_put_replication()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_request_options_t *dst_options = NULL;
    cos_string_t bucket;
    cos_string_t dst_bucket;
    cos_table_t *resp_headers = NULL;
   
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&dst_bucket, "replicationtest");

    dst_options = cos_request_options_create(p);
    init_test_request_options(dst_options, is_cname);
    cos_str_set(&dst_options->config->endpoint, "cn-east.myqcloud.com");

    cos_replication_params_t *replication_param = NULL;
    replication_param = cos_create_replication_params(p);
    cos_str_set(&replication_param->role, "qcs::cam::uin/100000616666:uin/100000616666");
    
    cos_replication_rule_content_t *rule = NULL;
    rule = cos_create_replication_rule_content(p);
    cos_str_set(&rule->id, "Rule_01");
    cos_str_set(&rule->status, "Enabled");
    cos_str_set(&rule->prefix, "test1");
    cos_str_set(&rule->dst_bucket, "qcs:id/0:cos:cn-east:appid/1253686666:replicationtest");
    cos_list_add_tail(&rule->node, &replication_param->rule_list);

    rule = cos_create_replication_rule_content(p);
    cos_str_set(&rule->id, "Rule_02");
    cos_str_set(&rule->status, "Disabled");
    cos_str_set(&rule->prefix, "test2");
    cos_str_set(&rule->storage_class, "Standard_IA");
    cos_str_set(&rule->dst_bucket, "qcs:id/0:cos:cn-east:appid/1253686666:replicationtest");
    cos_list_add_tail(&rule->node, &replication_param->rule_list);

    rule = cos_create_replication_rule_content(p);
    cos_str_set(&rule->id, "Rule_03");
    cos_str_set(&rule->status, "Enabled");
    cos_str_set(&rule->prefix, "test3");
    cos_str_set(&rule->storage_class, "Standard_IA");
    cos_str_set(&rule->dst_bucket, "qcs:id/0:cos:cn-east:appid/1253686666:replicationtest");
    cos_list_add_tail(&rule->node, &replication_param->rule_list);
    
    //put bucket replication
    s = cos_put_bucket_replication(options, &bucket, replication_param, &resp_headers);
    log_status(s);
    
    cos_pool_destroy(p);
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_put_replication();

    cos_http_io_deinitialize();

    return 0;
}
```

### Querying a cross-region replication rule

#### Description

This API is used to query the cross-region replication rules of a specified bucket.

#### Method prototype
```cpp
cos_status_t *cos_get_bucket_replication(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         cos_replication_params_t *replication_param, 
                                         cos_table_t **resp_headers);
```

#### Parameter description
| Parameter | Description | Type |
|---------|---------|---------|
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| replication_param | Cross-region replication request operation parameters |Struct|
| role | Operator's account information | String |
| rule_list | Cross-region replication rule configuration | Struct |
| id | Name of a specific rule | String |
| status | Rule status identifier. Enumerated values: `Enabled`, `Disabled` | String |
| prefix | Prefix match. Prefixes cannot overlap; otherwise, an error is returned | String |
| dst_bucket | Destination bucket ID. Format: `qcs::cos:[region]::[bucketname-AppId]` | String |
| storage_class | Storage class. Enumerated values: `Standard`, `Standard_IA`<br>Defaults to the storage class of the source bucket. | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description
| Response | Description | Type |
|---------|---------|---------|
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample
```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
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

void test_get_replication()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;
   
    // Initialize the request options
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Query a cross-region replication rule
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
    
    cos_pool_destroy(p);
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_get_replication();

    cos_http_io_deinitialize();

    return 0;
}
```

### Deleting a cross-region replication rule

#### Description

This API is used to delete the cross-region replication rules of a specified bucket.

#### Method prototype
```cpp
cos_status_t *cos_delete_bucket_replication(const cos_request_options_t *options,
                                            const cos_string_t *bucket, 
                                            cos_table_t **resp_headers);
```

#### Parameter description
| Parameter | Description | Type |
|---------|---------|---------|
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| resp_headers | Returns the HTTP response headers | Struct |

#### Response description
| Response | Description | Type |
|---------|---------|---------|
| code | Error code | Int | 
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |

#### Sample
```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
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

void test_delete_replication()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;
   
    // Initialize the request options
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Delete a cross-region replication rule
    s = cos_delete_bucket_replication(options, &bucket, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("delete bucket replication succeeded\n");
    } else {
        printf("delete bucket replication failed\n");
    }
    
    cos_pool_destroy(p);
}

int main(int argc, char *argv[])
{
    // Get SecretId and SecretKey from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    // Set the log level. Default value: `COS_LOG_WARN`
    cos_log_set_level(COS_LOG_WARN);

    // Set log output. Default value: `stderr`
    cos_log_set_output(NULL);

    test_delete_replication();

    cos_http_io_deinitialize();

    return 0;
}
```
