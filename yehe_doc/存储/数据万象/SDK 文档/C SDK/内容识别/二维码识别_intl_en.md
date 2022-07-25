## Overview

This document provides an overview of APIs and SDK code samples for image QR codes.

| API | Description |
| ------------------------------------------ | -------------------------- |
| [QR code recognition](https://intl.cloud.tencent.com/document/product/1045/47945) | Recognizes the location and content of valid QR codes in an image, outputs the text information (URL or text) contained in the QR codes, and pixelates the recognized QR codes. |

## QR Code Recognition

The QR code recognition feature recognizes the location and content of valid QR codes in an image, outputs the text information (URL or text) contained in the QR codes, and pixelates the recognized QR codes.

### Recognizing during upload


#### Method prototype

```c
cos_status_t *ci_put_object_from_file(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         const cos_string_t *object, 
                                         const cos_string_t *filename,
                                         cos_table_t *headers, 
                                         cos_table_t **resp_headers,
                                         ci_operation_result_t **results)
```

#### Feature description

The request for recognizing QR codes during image upload is the same as that used to simply upload a file to COS, except that you need to add the image processing parameter `Pic-Operations` to the request header.


#### Sample request

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, visit https://cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// CI endpoint. For more information, visit https://cloud.tencent.com/document/product/460/31066.
static char TEST_CI_ENDPOINT[] = "https://ci.ap-guangzhou.myqcloud.com";
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

void test_ci_image_qrcode()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t file;
    cos_table_t *resp_headers;
    cos_table_t *headers = NULL;
    ci_operation_result_t *results = NULL;
    ci_qrcode_info_t *content = NULL;

    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, "test.jpg");
    
    headers = cos_table_make(p, 1);
    apr_table_addn(headers, "pic-operations", "{\"is_pic_info\":1,\"rules\":[{\"fileid\":\"test.png\",\"rule\":\"QRcode/cover/1\"}]}");
    // Recognize during upload
    cos_str_set(&file, "test.jpg");
    cos_str_set(&object, "test.jpg");
    s = ci_put_object_from_file(options, &bucket, &object, &file, headers, &resp_headers, &results);
    log_status(s);
    if (!cos_status_is_ok(s)) {
        printf("put object failed\n");
    }
    printf("CodeStatus: %d\n", results->object.code_status);
    cos_list_for_each_entry(ci_qrcode_info_t, content, &results->object.qrcode_info, node) {
        printf("CodeUrl: %s\n", content->code_url.data);
        printf("Point: %s\n", content->point[0].data);
        printf("Point: %s\n", content->point[1].data);
        printf("Point: %s\n", content->point[2].data);
        printf("Point: %s\n", content->point[3].data);
    }

    // Terminate the memory pool
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

    test_ci_image_qrcode();

    cos_http_io_deinitialize();

    return 0;
}
```

#### Parameter description

| Parameter | Description | Type |
| :----------- | :----------------------------------------------------------- | :----- |
| options | COS request options | Struct |
| bucket             | Bucket name in the format of `BucketName-APPID` | String  |
| object             | Object name                                                  | String  |
| filename | Filename of the local object | String |
| headers            | COS request headers                                              | Struct |
| resp_headers       | Returned HTTP response headers                                       | Struct  |
| results      | Processing result of the in-cloud data  | Struct |



### Recognizing during download

#### Feature description

This feature recognizes QR codes during file download.

#### Method prototype
```c
cos_status_t *ci_get_qrcode(const cos_request_options_t *options,
                             const cos_string_t *bucket,
                             const cos_string_t *object,
                             int cover,
                             cos_table_t *headers,
                             cos_table_t *query_params, 
                             cos_table_t **resp_headers,
                             ci_qrcode_result_t **results)
```

#### Sample request

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// `endpoint` is the COS access domain name. For more information, visit https://cloud.tencent.com/document/product/436/6224.
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// CI endpoint. For more information, visit https://cloud.tencent.com/document/product/460/31066.
static char TEST_CI_ENDPOINT[] = "https://ci.ap-guangzhou.myqcloud.com";
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

void test_ci_get_image_qrcode()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers;
    ci_qrcode_info_t *content = NULL;
    ci_qrcode_result_t *result2 = NULL;

    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, "test.jpg");

    // Recognize during download
    s = ci_get_qrcode(options, &bucket, &object, 1, NULL, NULL, &resp_headers, &result2);
    log_status(s);
    if (!cos_status_is_ok(s)) {
        printf("get object failed\n");
    }
    printf("CodeStatus: %d\n", result2->code_status);
    cos_list_for_each_entry(ci_qrcode_info_t, content, &result2->qrcode_info, node) {
        printf("CodeUrl: %s\n", content->code_url.data);
        printf("Point: %s\n", content->point[0].data);
        printf("Point: %s\n", content->point[1].data);
        printf("Point: %s\n", content->point[2].data);
        printf("Point: %s\n", content->point[3].data);
    }
    printf("ImageResult: %s\n", result2->result_image.data);

    // Terminate the memory pool
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

    test_ci_get_image_qrcode();

    cos_http_io_deinitialize();

    return 0;
}
```


#### Parameter description


| Parameter | Description | Type |
| --------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID`. The bucket name entered here must be in this format.  | string |
| object | Object name | string |
| cover | Pixelates the recognized QR code. Valid values: 0 (no), 1 (yes). | int |
| headers            | COS request headers                                              | Struct |
| query_params | COS request operation parameters | Struct |
| resp_headers       | Returned HTTP response headers                                       | Struct  |
| results | Recognized QR code                                               | Struct |


