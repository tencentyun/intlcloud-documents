## Overview

The SDK for C provides an API to get pre-signed request URLs. For more information, see the directions and examples in this document.



## Getting a Pre-signed Request URL 

#### Generating a Pre-signed Request URL

#### Feature Description

This API is used to generate a pre-signed request URL.

#### Method Prototype

```cpp
int cos_gen_presigned_url(const cos_request_options_t *options,
                          const cos_string_t *bucket, 
                          const cos_string_t *object,
                          const int64_t expire,
                          http_method_e method,
                          cos_string_t *presigned_url);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| object | Object name | String |
| expire | Signature validity period in seconds | Int |
| method | HTTP request method in enumeration type, including HTTP_GET, HTTP_HEAD, HTTP_PUT, HTTP_POST, and HTTP_DELETE | Enum |
| presigned_url | The pre-signed request URL generated | String |

#### Return Result Descriptions

| Return Result | Description | Type |
| -------- | ------ | ---- |
| code | Error code | Int |

## Example of Pre-signing a Request

A pre-signed URL can be obtained by setting a permanent or temporary key in the options parameter.

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
/* You can use a temporary key by setting sts_token. When the temporary key is used, access_key_id and access_key_secret need to be set to its SecretId and SecretKey */
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
