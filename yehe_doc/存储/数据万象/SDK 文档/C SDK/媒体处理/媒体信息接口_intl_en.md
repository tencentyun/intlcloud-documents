## Overview

This document provides an overview of APIs and SDK code samples for media information.

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
|  [GetMediaInfo](https://intl.cloud.tencent.com/document/product/436/46915)    |   Querying file information | Queries media file information      |

>! Before using this API, make sure that the media processing feature has been enabled in the data processing section in the console; otherwise, the error `media bucket unbinded, bucket's host is unavailable` will be reported. For more information, see [Enabling Media Processing](https://intl.cloud.tencent.com/document/product/436/46275).

## Querying File Information

#### Feature description

This API is used to get media file information.

#### Method prototype

```cpp
cos_status_t *ci_get_media_info(const cos_request_options_t *options,
                                const cos_string_t *bucket, 
                                const cos_string_t *object,
                                cos_table_t *headers, 
                                cos_table_t **resp_headers,
                                ci_media_info_result_t **media_result);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------- |
| options | COS request options. | Struct |
| bucket             | Bucket name in the format of `BucketName-APPID`. | String  |
| object             | Object name.                                                  | String  |
| headers            | COS request headers.                                              | Struct |
| resp_headers       | Returned HTTP response headers.                                       | Struct  |
| media_result       | Returned media file information.                                              | Struct  |
| format             | Format information.                                                      | Struct  |
| num_stream         | Number of streams (including videos, audios, and subtitles).                     | Int  |
| num_program        | Number of programs.                                                     | Int  |
| format_name        | Container format name.                                                    | String  |
| format_long_name   | Detailed name of the container format.                                               | String  |
| start_time         | Start time in seconds.                                               | Float  |
| duration           | Duration in seconds.                                                  | Float  |
| bit_rate           | Bitrate in Kbps.                                             | Int  |
| size               | Size in bytes.                                               | Int  |
| stream             | Stream information.                                                        | Struct  |
| video              | Video information.                                                      | Struct  |
| audio              | Audio information.                                                      | Struct  |
| subtitle           | Subtitles information.                                                      | Struct  |

#### `video` structure description
| Parameter | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------- |
| index              | Stream number.                                                   | Int  |
| codec_name         | Codec format name.                                                | String  |
| codec_long_name    | Detailed name of the codec format.                                           | String  |
| codec_time_base    | Codec timebase.                                                     | String |
| codec_tag_string   | Codec tag name.                                                    | String  |
| codec_tag          | Codec tag.                                                      | String  |
| profile            | Video codec profile.                                                   | String  |
| height             | Video height in px.                                                | Int  |
| width              | Video width in px.                                                | Int  |
| has_b_frame        | Whether B-frames exist. 1: yes; 0: no.                                      | Int  |
| ref_frames         | Number of reference frames for video codec.                                             | Int  |
| sar                | Sample aspect ratio.                                                     | String |
| dar                | Display aspect ratio.                                                    | String  |
| pix_format         | Pixel format.                                                      | String  |
| field_order        | Field order.                                                      | String  |
| level              | Video codec level.                                                   | Int  |
| fps                | Video frame rate.                                                       | Int  |
| avg_fps            | Average frame rate.                                                      | String  |
| timebase           | Timebase.                                                          | String  |
| start_time         | Video start time in seconds.                                           | Float  |
| duration           | Video duration in seconds.                                              | Float  |
| bit_rate           | Bitrate in Kbps.                                             | Float  |
| num_frames         | Total number of frames.                                                        | Int  |
| language           | Language.                                                           | String |

#### `audio` structure description
| Parameter | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------- |
| index              | Stream number.                                                   | Int  |
| codec_name         | Codec format name.                                                | String  |
| codec_long_name    | Detailed name of the codec format.                                           | String  |
| codec_time_base    | Codec timebase.                                                     | String |
| codec_tag_string   | Codec tag name.                                                    | String  |
| codec_tag          | Codec tag.                                                      | String  |
| sample_fmt         | Sample format.                                                      | String  |
| sample_rate        | Sample rate.                                                        | Int  |
| channel            | Number of channels.                                                       | Int  |
| channel_layout     | Channel layout.                                                      | String |
| timebase           | Timebase.                                                          | String  |
| start_time         | Audio start time in seconds.                                           | Float  |
| duration           | Audio duration in seconds.                                              | Float  |
| bit_rate           | Bitrate in Kbps.                                             | Float  |
| language           | Language.                                                           | String |

#### `subtitle` structure description
| Parameter | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------- |
| index              | Stream number.                                                   | Int  |
| language           | Language. `und` indicates no query result.                                       | String |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg | Error message | String |
| req_id | Request message ID | String |

#### Sample
For the complete code, see the `test_ci_media_process_media_info()` function in `cos_demo.c`.

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

static void log_media_info_result(ci_media_info_result_t *result)
{
    // format
    cos_warn_log("format.num_stream: %d", result->format.num_stream);
    cos_warn_log("format.num_program: %d", result->format.num_program);
    cos_warn_log("format.format_name: %s", result->format.format_name.data);
    cos_warn_log("format.format_long_name: %s", result->format.format_long_name.data);
    cos_warn_log("format.start_time: %f", result->format.start_time);
    cos_warn_log("format.duration: %f", result->format.duration);
    cos_warn_log("format.bit_rate: %d", result->format.bit_rate);
    cos_warn_log("format.size: %d", result->format.size);

    // stream.video
    cos_warn_log("stream.video.index: %d", result->stream.video.index);
    cos_warn_log("stream.video.codec_name: %s", result->stream.video.codec_name.data);
    cos_warn_log("stream.video.codec_long_name: %s", result->stream.video.codec_long_name.data);
    cos_warn_log("stream.video.codec_time_base: %s", result->stream.video.codec_time_base.data);
    cos_warn_log("stream.video.codec_tag_string: %s", result->stream.video.codec_tag_string.data);
    cos_warn_log("stream.video.codec_tag: %s", result->stream.video.codec_tag.data);
    cos_warn_log("stream.video.profile: %s", result->stream.video.profile.data);
    cos_warn_log("stream.video.height: %d", result->stream.video.height);
    cos_warn_log("stream.video.width: %d", result->stream.video.width);
    cos_warn_log("stream.video.has_b_frame: %d", result->stream.video.has_b_frame);
    cos_warn_log("stream.video.ref_frames: %d", result->stream.video.ref_frames);
    cos_warn_log("stream.video.sar: %s", result->stream.video.sar.data);
    cos_warn_log("stream.video.dar: %s", result->stream.video.dar.data);
    cos_warn_log("stream.video.pix_format: %s", result->stream.video.pix_format.data);
    cos_warn_log("stream.video.field_order: %s", result->stream.video.field_order.data);
    cos_warn_log("stream.video.level: %d", result->stream.video.level);
    cos_warn_log("stream.video.fps: %d", result->stream.video.fps);
    cos_warn_log("stream.video.avg_fps: %s", result->stream.video.avg_fps.data);
    cos_warn_log("stream.video.timebase: %s", result->stream.video.timebase.data);
    cos_warn_log("stream.video.start_time: %f", result->stream.video.start_time);
    cos_warn_log("stream.video.duration: %f", result->stream.video.duration);
    cos_warn_log("stream.video.bit_rate: %f", result->stream.video.bit_rate);
    cos_warn_log("stream.video.num_frames: %d", result->stream.video.num_frames);
    cos_warn_log("stream.video.language: %s", result->stream.video.language.data);

    // stream.audio
    cos_warn_log("stream.audio.index: %d", result->stream.audio.index);
    cos_warn_log("stream.audio.codec_name: %s", result->stream.audio.codec_name.data);
    cos_warn_log("stream.audio.codec_long_name: %s", result->stream.audio.codec_long_name.data);
    cos_warn_log("stream.audio.codec_time_base: %s", result->stream.audio.codec_time_base.data);
    cos_warn_log("stream.audio.codec_tag_string: %s", result->stream.audio.codec_tag_string.data);
    cos_warn_log("stream.audio.codec_tag: %s", result->stream.audio.codec_tag.data);
    cos_warn_log("stream.audio.sample_fmt: %s", result->stream.audio.sample_fmt.data);
    cos_warn_log("stream.audio.sample_rate: %d", result->stream.audio.sample_rate);
    cos_warn_log("stream.audio.channel: %d", result->stream.audio.channel);
    cos_warn_log("stream.audio.channel_layout: %s", result->stream.audio.channel_layout.data);
    cos_warn_log("stream.audio.timebase: %s", result->stream.audio.timebase.data);
    cos_warn_log("stream.audio.start_time: %f", result->stream.audio.start_time);
    cos_warn_log("stream.audio.duration: %f", result->stream.audio.duration);
    cos_warn_log("stream.audio.bit_rate: %f", result->stream.audio.bit_rate);
    cos_warn_log("stream.audio.language: %s", result->stream.audio.language.data);

    // stream.subtitle
    cos_warn_log("stream.subtitle.index: %d", result->stream.subtitle.index);
    cos_warn_log("stream.subtitle.language: %s", result->stream.subtitle.language.data);
}

void test_ci_media_process_media_info()
{
    cos_pool_t *p = NULL;
    int is_cname = 0; 
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers;
    ci_media_info_result_t *media_info;
    cos_string_t object;

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

    // Use your own configuration. For more information, visit https://intl.cloud.tencent.com/document/product/436/46915.
    s = ci_get_media_info(options, &bucket, &object, NULL, &resp_headers, &media_info);
    log_status(s);
    if (s->code == 200) {
        log_media_info_result(media_info);
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

    test_ci_media_process_media_info();

    cos_http_io_deinitialize();

    return 0;
}
```