## Overview

The C SDK provides APIs to obtain pre-signed URLs. For detailed directions, see the description and examples below.

>?
> - You are advised to use a temporary key to generate a pre-signed URL for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> 


## Getting a Pre-signed Request URL 

#### Generating pre-signed URL

#### Description

This API is used to generate a pre-signed URL.

#### Method prototype

```cpp
int cos_gen_presigned_url(const cos_request_options_t *options,
                          const cos_string_t *bucket, 
                          const cos_string_t *object,
                          const int64_t expire,
                          http_method_e method,
                          cos_string_t *presigned_url);
```

#### Parameter description

| Parameter | Description | Type |
| ------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object | Object name | String |
| expire        | Validity time of the signature, in seconds                      | Int    |
| method        | HTTP request method. Enumerated values: `HTTP_GET`, `HTTP_HEAD`, `HTTP_PUT`, `HTTP_POST`, `HTTP_DELETE` | Enum   |
| presigned_url | The generated pre-signed URL                  | String                      | 

#### Response description

| Response | Description | Type |
| -------- | ------ | ---- |
| code | Error code | Int | 

#### Pre-signed request samples

You can obtain a pre-signed URL by setting a permanent or temporary key using the `options` parameter.

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
// COS bucket name, in the format of [bucket]-[appid], for example `mybucket-1253666666`. It can be obtained at https://console.cloud.tencent.com/cos5/bucket.
static char TEST_BUCKET_NAME[] = "<bucketname-appid>";
// A unique identifier of an object stored in COS. For more information about objects and object keys, please see https://intl.cloud.tencent.com/document/product/436/13324.
static char TEST_OBJECT_NAME1[] = "1.txt";

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

void test_presigned_url()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t presigned_url;
    
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, TEST_OBJECT_NAME1);

    cos_gen_presigned_url(options, &bucket, &object, 300, HTTP_GET, &presigned_url);
    printf("presigned_url: %s\n", presigned_url.data);

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

    test_presigned_url();

    cos_http_io_deinitialize();

    return 0;
}
```

## Securely Getting a Pre-signed Request URL 

#### Securely generating a pre-signed URL

#### Description

This API is used to securely generate a pre-signed URL.

#### Method prototype

```cpp
int cos_gen_presigned_url_safe(const cos_request_options_t *options,
                          const cos_string_t *bucket, 
                          const cos_string_t *object,
                          const int64_t expire,
                          http_method_e method,
                          cos_table_t *headers,
                          cos_table_t *params,
                          int sign_host,
                          cos_string_t *presigned_url);
```

#### Parameter description

| Parameter | Description | Type |
| ------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct  |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object | Object name | String |
| expire        | Validity time of the signature, in seconds                      | Int    |
| method        | HTTP request method. Enumerated values: `HTTP_GET`, `HTTP_HEAD`, `HTTP_PUT`, `HTTP_POST`, `HTTP_DELETE` | Enum   |
| headers      | Additional headers of a COS request | Struct |
| params | Parameters for the COS request                                           | Struct |
| sign_host     | Whether to sign the signature to the host header. You are strongly advised to enable it for security’s sake.      | Int    |
| presigned_url | The generated pre-signed URL                  | String                      | 

#### Response description

| Response | Description | Type |
| -------- | ------ | ---- |
| code | Error code | Int | 

#### Sample request 1. Generate a pre-signed URL with `host` in the signature

You can obtain a pre-signed URL by setting a permanent or temporary key using the `options` parameter.

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
// COS bucket name, in the format of [bucket]-[appid], for example `mybucket-1253666666`. It can be obtained at https://console.cloud.tencent.com/cos5/bucket.
static char TEST_BUCKET_NAME[] = "<bucketname-appid>";
// A unique identifier of an object stored in COS. For more information about objects and object keys, please see https://intl.cloud.tencent.com/document/product/436/13324.
static char TEST_OBJECT_NAME1[] = "1.txt";

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

void test_safe_presigned_url()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t presigned_url;
    cos_table_t *params = NULL;
    cos_table_t *headers = NULL;
    int sign_host = 1;
    
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    /* You can use a temporary key by setting `sts_token`. When you use a temporary key, you need to set `access_key_id` and `access_key_secret` to its SecretId and SecretKey */
    //cos_str_set(&options->config->sts_token, "MyTokenString");
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, TEST_OBJECT_NAME1);

    // You are strongly advised to set `sign_host` to `1` to add the `host` header to the signature list by force to prevent unauthorized access.
    cos_gen_presigned_url_safe(options, &bucket, &object, 300, HTTP_GET, headers, params, sign_host, &presigned_url);
    printf("presigned_url_safe: %s\n", presigned_url.data);

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

    test_safe_presigned_url();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Sample request 2. Generate the pre-signed URL with the signature containing `request param` and `request header`

You can obtain a pre-signed URL by setting a permanent or temporary key using the `options` parameter.

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// `endpoint` is the COS access domain name. For more information, see https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                // Your SecretId
static char *TEST_ACCESS_KEY_SECRET;            // Your SecretKey
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    // Your APPID
// COS bucket name, in the format of [bucket]-[appid], for example `mybucket-1253666666`. It can be obtained at https://console.cloud.tencent.com/cos5/bucket.
static char TEST_BUCKET_NAME[] = "<bucketname-appid>";
// A unique identifier of an object stored in COS. For more information about objects and object keys, please see https://intl.cloud.tencent.com/document/product/436/13324.
static char TEST_OBJECT_NAME1[] = "1.txt";

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

void test_safe_presigned_url()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t presigned_url;
    cos_table_t *params = NULL;
    cos_table_t *headers = NULL;
    int sign_host = 1;
    
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    /* You can use a temporary key by setting `sts_token`. When you use a temporary key, you need to set `access_key_id` and `access_key_secret` to its SecretId and SecretKey */
    //cos_str_set(&options->config->sts_token, "MyTokenString");
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, TEST_OBJECT_NAME1);

    // Add your `params` and `headers`
    params = cos_table_make(options->pool, 0);
    //cos_table_add(params, "param1", "value");
    headers = cos_table_make(options->pool, 0);
    //cos_table_add(headers, "header1", "value");

    // You are strongly advised to set `sign_host` to `1` to add the `host` header to the signature list by force to prevent unauthorized access.
    cos_gen_presigned_url_safe(options, &bucket, &object, 300, HTTP_GET, headers, params, sign_host, &presigned_url);
    printf("presigned_url_safe: %s\n", presigned_url.data);

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

    test_safe_presigned_url();

    cos_http_io_deinitialize();

    return 0;
}
```
