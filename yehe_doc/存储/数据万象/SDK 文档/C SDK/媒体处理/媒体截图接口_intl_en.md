## Overview

This document provides an overview of APIs and SDK code samples for media screenshot.

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
|   [GetSnapshot](https://intl.cloud.tencent.com/document/product/436/46912)     |  Querying screenshot |   Query the screenshot of media file at some time point     |

>! Before using this API, make sure that the media processing feature has been enabled in the data processing section in the console; otherwise, the error `media bucket unbinded, bucket's host is unavailable` will be reported. For more information, see [Enabling Media Processing](https://intl.cloud.tencent.com/document/product/436/46275).


## Querying Screenshot (Memory)

#### Feature description

This API is used to get a screenshot of a media file at some time point and put the screenshot information in the memory buffer.

#### Method prototype

```cpp
cos_status_t *ci_get_snapshot_to_buffer(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        const cos_string_t *object,
                                        const ci_get_snapshot_request_t *snapshot_request,
                                        cos_table_t *headers, 
                                        cos_list_t *buffer, 
                                        cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------- |
| options | COS request options. | Struct |
| bucket             | Bucket name in the format of `BucketName-APPID`. | String  |
| object             | Object name.                                                  | String  |
| snapshot_request   | Request parameters for getting media screenshot.                                           | Struct  |
| time               | Screenshot time point in seconds.                                          | Float  |
| width              | Screenshot width. Default value: 0.                                              | Int  |
| height | Screenshot height. Default value: 0<br/>If `width` and `height` are both `0`, the width and height of the video are used. If one of them is `0`, the other value is used to automatically adapt to the aspect ratio of the video. | Int |
| format | Screenshot format. Valid values: jpg; png. Default value: jpg. | String |
| rotate | Image rotation method<br/><li>auto: Rotate automatically according to the video rotation information.<br/><li>off: Do not rotate.<br/>Default value: auto. | String |
| mode | Frame capturing method<br/><li>keyframe: Capture the last keyframe before the specified time point.<br><li>exactframe: Capture the frame at a specified time point.<br/>Default value: exactframe. | String |
| headers            | COS request headers.                                              | Struct |
| buffer             | Returned screenshot content.                                            | Struct |
| resp_headers       | Returned HTTP response headers.                                       | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg | Error message | String |
| req_id | Request message ID | String |

#### Sample
For the complete code, see the `test_ci_media_process_snapshot()` function in `cos_demo.c`.

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

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

void test_ci_media_process_snapshot()
{
    cos_pool_t *p = NULL;
    int is_cname = 0; 
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers;
    cos_list_t download_buffer;
    cos_string_t object;
    ci_get_snapshot_request_t *snapshot_request;

    // Basic configuration
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);   
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, "test.mp4");

    // Use your own configuration. For more information, visit https://intl.cloud.tencent.com/document/product/436/46912.
    snapshot_request = ci_snapshot_request_create(p);
    snapshot_request->time = 7.5;
    snapshot_request->width = 0;
    snapshot_request->height = 0;
    cos_str_set(&snapshot_request->format, "jpg");
    cos_str_set(&snapshot_request->rotate, "auto");
    cos_str_set(&snapshot_request->mode, "exactframe");
    cos_list_init(&download_buffer);

    s = ci_get_snapshot_to_buffer(options, &bucket, &object, snapshot_request, NULL, &download_buffer, &resp_headers);
    log_status(s);

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

    test_ci_media_process_snapshot();

    cos_http_io_deinitialize();

    return 0;
}
```


## Querying Screenshot (File)

#### Feature description

This API is used to get a screenshot of a media file at some time point and put the screenshot information in a local file.

#### Method prototype

```cpp
cos_status_t *ci_get_snapshot_to_file(const cos_request_options_t *options,
                                      const cos_string_t *bucket, 
                                      const cos_string_t *object,
                                      const ci_get_snapshot_request_t *snapshot_request,
                                      cos_table_t *headers, 
                                      cos_string_t *filename, 
                                      cos_table_t **resp_headers);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------- |
| options | COS request options. | Struct |
| bucket             | Bucket name in the format of `BucketName-APPID`. | String  |
| object             | Object name.                                                  | String  |
| snapshot_request   | Request parameters for getting media screenshot.                                           | Struct  |
| time               | Screenshot time point in seconds.                                          | Float  |
| width              | Screenshot width. Default value: 0.                                              | Int  |
| height | Screenshot height. Default value: 0<br/>If `width` and `height` are both `0`, the width and height of the video are used. If one of them is `0`, the other value is used to automatically adapt to the aspect ratio of the video. | Int |
| format | Screenshot format. Valid values: jpg; png. Default value: jpg. | String |
| rotate | Image rotation method<br/><li>auto: Rotate automatically according to the video rotation information.<br/><li>off: Do not rotate.<br/>Default value: auto. | String |
| mode | Frame capturing method<br/><li>keyframe: Capture the last keyframe before the specified time point.<br><li>exactframe: Capture the frame at a specified time point.<br/>Default value: exactframe. | String |
| headers            | COS request headers.                                              | Struct |
| filename           | Name of the file for storing screenshot information.                                           | String |
| resp_headers       | Returned HTTP response headers.                                       | Struct  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg | Error message | String |
| req_id | Request message ID | String |

#### Sample
For the complete code, see the `test_ci_media_process_snapshot()` function in `cos_demo.c`.

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <sys/stat.h>

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

void test_ci_media_process_snapshot()
{
    cos_pool_t *p = NULL;
    int is_cname = 0; 
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers;
    cos_string_t object;
    ci_get_snapshot_request_t *snapshot_request;
    cos_string_t pic_file = cos_string("snapshot.jpg");

    // Basic configuration
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);   
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, "test.mp4");

    // Use your own configuration. For more information, visit https://intl.cloud.tencent.com/document/product/436/46912.
    snapshot_request = ci_snapshot_request_create(p);
    snapshot_request->time = 7.5;
    snapshot_request->width = 0;
    snapshot_request->height = 0;
    cos_str_set(&snapshot_request->format, "jpg");
    cos_str_set(&snapshot_request->rotate, "auto");
    cos_str_set(&snapshot_request->mode, "exactframe");

    s = ci_get_snapshot_to_file(options, &bucket, &object, snapshot_request, NULL, &pic_file, &resp_headers);
    log_status(s);

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

    test_ci_media_process_snapshot();

    cos_http_io_deinitialize();

    return 0;
}
```