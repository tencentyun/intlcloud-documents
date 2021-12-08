## Overview

The C SDK provides APIs to obtain pre-signed URLs. For detailed directions, see the description and examples below.

>?
> - You are advised to use a temporary key to generate pre-signed URLs for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
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
cos_pool_t *p = NULL;
int is_cname = 0;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t presigned_url;

//create memory pool
cos_pool_create(&p, NULL);

//init request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
/* You can use a temporary key by setting `sts_token`. When you use a temporary key, you need to set `access_key_id` and `access_key_secret` to its SecretId and SecretKey */
//cos_str_set(&options->config->sts_token, "MyTokenString");
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);

//generate presigned URL
cos_gen_presigned_url(options, &bucket, &object, 300, HTTP_GET, &presigned_url);
printf("presigned url: %s\n", presigned_url.data);

//destroy memory pool
cos_pool_destroy(p); 
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

#### Sample request of securely generating a pre-signed URL

You can obtain a pre-signed URL by setting a permanent or temporary key using the `options` parameter.

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t presigned_url;
cos_table_t *params;
cos_table_t *headers;

//create memory pool
cos_pool_create(&p, NULL);

//init request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
/* You can use a temporary key by setting `sts_token`. When you use a temporary key, you need to set `access_key_id` and `access_key_secret` to its SecretId and SecretKey */
//cos_str_set(&options->config->sts_token, "MyTokenString");
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);

// Add your “params” and “headers”.
params = cos_table_make(p, 0);
headers = cos_table_make(p, 0);

// You are strongly advised to set sign_host to 1. In this way, the host header will be added to the signature list forcibly to avoid unauthorized access.
cos_gen_presigned_url_safe(options, &bucket, &object, 300, HTTP_GET, headers, params, 1, &presigned_url);
printf("presigned_url_safe: %s\n", presigned_url.data);

//destroy memory pool
cos_pool_destroy(p); 
```
