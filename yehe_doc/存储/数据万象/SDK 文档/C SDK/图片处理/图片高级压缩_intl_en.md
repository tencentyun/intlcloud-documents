## Overview

This document provides an overview of APIs and SDK code samples for image advanced compression.


| API | Description |
| :--------------- |  :--------------------- |
| [Image advanced compression](https://intl.cloud.tencent.com/document/product/1045/40108) | Allows you to easily convert images into formats that provide a high compression ratio, such as TPG and HEIF. This effectively reduces the transfer time, loading time, and the use of bandwidth and traffic. |

#### Method prototype

Image compression is implemented via [object download](https://intl.cloud.tencent.com/document/product/436/43553). All you need to do is to add the request parameters in the following syntax:

```c
imageMogr2/format/<Format>
```
| Parameter | Description |
| :--------- | :--------------------------------------------- |
| format | Target compression format, which can be TPG or HEIF for thumbnails. |



#### Sample request

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, visit https://intl.cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                //your secret_id
static char *TEST_ACCESS_KEY_SECRET;            //your secret_key
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    //your appid
// COS bucket name in the format of [bucket]-[appid], for example, `mybucket-1253666666`. It can be obtained at https://console.cloud.tencent.com/cos5/bucket.
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

void test_image_compress()
{
    cos_pool_t *p = NULL;
    int is_cname = 0; 
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t file;
    cos_table_t *resp_headers;
    cos_table_t *params = NULL;
    
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    params = cos_table_make(p, 1);
    apr_table_addn(params, "imageMogr2/format/tpg", "");
    cos_str_set(&object, "test.jpg");
    cos_str_set(&file, "test.tpg");
    s = cos_get_object_to_file(options, &bucket, &object, NULL, params, &file, &resp_headers);
    log_status(s);
    if (!cos_status_is_ok(s)) {
        printf("cos_get_object_to_file fail, req_id:%s\n", s->req_id);
    }

    params = cos_table_make(p, 1);
    apr_table_addn(params, "imageMogr2/format/heif", "");
    cos_str_set(&file, "test.heif");
    s = cos_get_object_to_file(options, &bucket, &object, NULL, params, &file, &resp_headers);
    log_status(s);
    if (!cos_status_is_ok(s)) {
        printf("cos_get_object_to_file fail, req_id:%s\n", s->req_id);
    }

    cos_pool_destroy(p);
}

int main(int argc, char *argv[])
{
    // Get `SECRETID` and `SECRETKEY` from environment variables
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    //set log level, default COS_LOG_WARN
    cos_log_set_level(COS_LOG_WARN);

    //set log output, default stderr
    cos_log_set_output(NULL);

    test_image_compress();

    cos_http_io_deinitialize();

    return 0;
}
```
