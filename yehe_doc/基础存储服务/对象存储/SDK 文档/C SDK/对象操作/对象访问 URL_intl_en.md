## Overview

This document provides an overview of the API and sample code for getting an object access URL.

## Getting an Object Access URL

#### Description
The API is used to get object access URLs for anonymous download or distribution.

#### Method prototype

```cpp
const char *cos_gen_object_url(const cos_request_options_t *options, 
                               const cos_string_t *bucket, 
                               const cos_string_t *object)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| options | COS request options | Struct | Yes |
| Bucket | Bucket name in the format of `BucketName-APPID` | Struct | Yes |
| object | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |

#### Response description

An object access URL is returned upon success.


#### Sample request

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

void test_gen_object_url()
{
    cos_pool_t *p = NULL;
    int is_cname = 0; 
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
        
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, TEST_OBJECT_NAME1);

    printf("url:%s\n", cos_gen_object_url(options, &bucket, &object));

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

    test_gen_object_url();

    cos_http_io_deinitialize();

    return 0;
}
```