## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for video moderation.

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
| [Submitting video moderation job](https://intl.cloud.tencent.com/document/product/436/48249) | Submits video moderation job.   |
| [Querying video moderation job result](https://intl.cloud.tencent.com/document/product/436/48250)  | Queries the result of specified video moderation job. |

## Submitting Video Moderation Job

#### Feature description

This API is used to submit a video moderation job.

#### Method prototype

```cpp
cos_status_t *ci_create_video_auditing_job(const cos_request_options_t *options,
                                           const cos_string_t *bucket, 
                                           const ci_video_auditing_job_options_t *job_options,
                                           cos_table_t *headers, 
                                           cos_table_t **resp_headers,
                                           ci_video_auditing_job_result_t **job_result);
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------------------------------------------------------ | ------- |
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID`. The bucket name entered here must be in this format.  | String |
| job_options      | Parameter configuration of the submitted video moderation job                                   | Struct  |
| input_object     | Object name                                                       | String  |
| detect_type      | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. | String  |
| callback         | Callback address, which must start with `http://` or `https://`.                    | String  |
| callback_version | Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`. | String |
| biz_type         | Moderation policy. If this parameter is not specified, the default policy will be used.                         | String  |
| detect_content   | Whether to moderate video sound. Valid values: `0` (moderates the video image only), `1` (moderates both the video image and video sound). Default value: `0`. | Integer |
| snapshot         | Video image moderation is implemented by taking a certain number of screenshots based on the video frame capturing capability and then moderating the screenshots one by one. This parameter is used to specify the configuration of video frame capturing. | Struct |
| mode             | Frame capturing mode. Valid values: `Interval` (interval mode), `Average` (average mode), `Fps` (fixed frame rate mode). <li>`Interval` mode: The `TimeInterval` and `Count` parameters take effect. If `Count` is set but `TimeInterval` is not, all frames will be captured to generate a total of `Count` images. <li>`Average` mode: The `Count` parameter takes effect, indicating to capture a total of `Count` images at an average interval in the entire video. <li>`Fps` mode: `TimeInterval` indicates how many frames to capture per second, and `Count` indicates how many frames to capture in total.</li> | String |
| count        | The number of captured frames. Value range: (0, 10000].                                | Integer |
| time_interval    | Video frame capturing frequency. Value range: (0.000, 60.000] seconds. The value supports the float format, accurate to the millisecond. | Float  |
| headers            | COS request headers                                              | Struct |
| resp_headers       | Returned HTTP response headers                                       | Struct  |
| job_result       | Returned response to job submission                                       | Struct  |
| job_id           | ID of the video moderation job                                        | String  |
| state            | Status of the video moderation job. Valid values: `Submitted`, `Snapshoting`, `Success`, `Failed`, `Auditing`. | String |
| creation_time    | Creation time of the video moderation job. | String |

#### Response description

| Returned Result   | Description        | Type   |
| ---------- | ----------- | ------ |
| code       | Error code      | Int    |
| error_code | Error code  | String |
| error_msg  | Error message  | String |
| req_id     | Request ID | String |

#### Sample

For the complete code, see the `test_ci_video_auditing()` function in `cos_demo.c`.

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <sys/stat.h>

// CI endpoint. For more information, visit https://www.tencentcloud.com/document/product/1045/33423.
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

static void log_video_auditing_result(ci_video_auditing_job_result_t *result)
{
    cos_warn_log("jobid: %s", result->jobs_detail.job_id.data);
    cos_warn_log("state: %s", result->jobs_detail.state.data);
    cos_warn_log("creation_time: %s", result->jobs_detail.creation_time.data);
}

void test_ci_create_video_auditing()
{
    cos_pool_t *p = NULL;
    int is_cname = 0; 
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers;
    ci_video_auditing_job_options_t *job_options;
    ci_video_auditing_job_result_t *job_result;

    // Basic configuration
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    cos_str_set(&options->config->endpoint, TEST_CI_ENDPOINT);     // https://ci.<Region>.myqcloud.com
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Replace with your configuration information. For more information, visit https://intl.cloud.tencent.com/document/product/436/48249.
    job_options = ci_video_auditing_job_options_create(p);
    cos_str_set(&job_options->input_object, "test.mp4");
    cos_str_set(&job_options->job_conf.detect_type, "Porn,Ads");
    cos_str_set(&job_options->job_conf.callback_version, "Detail");
    job_options->job_conf.detect_content = 1;
    cos_str_set(&job_options->job_conf.snapshot.mode, "Interval");
    job_options->job_conf.snapshot.time_interval = 1.5;
    job_options->job_conf.snapshot.count = 10;

    // Submit a video moderation job
    s = ci_create_video_auditing_job(options, &bucket, job_options, NULL, &resp_headers, &job_result);
    log_status(s);
    if (s->code == 200) {
        log_video_auditing_result(job_result);
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

    test_ci_create_video_auditing();

    cos_http_io_deinitialize();

    return 0;
}
```

## Querying Video Moderation Job

#### Feature description

This API is used to query the status and result of a video moderation job.

#### Method prototype

```cpp
cos_status_t *ci_get_auditing_job(const cos_request_options_t *options,
                                  const cos_string_t *bucket, 
                                  const cos_string_t *job_id,
                                  cos_table_t *headers, 
                                  cos_table_t **resp_headers,
                                  ci_auditing_job_result_t **job_result);
```

#### Parameter description

| Parameter | Description | Type |
| ----------------------- | ------------------------------------------------------------ | ------- |
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID`. The bucket name entered here must be in this format.  | String |
| job_id           | ID of the video moderation job                                        | String  |
| headers            | COS request headers                                              | Struct |
| resp_headers       | Returned HTTP response headers                                       | Struct  |
| job_result       | Returned response to job query                                       | Struct  |
| nonexist_job_ids        | List of non-existing job IDs queried. If all jobs exist, this node will not be returned. |  String |
| jobs_detail             | Details of the video moderation job                                       | Struct  |
| code                    | Error code, which will be returned only if `State` is `Failed`.                         | String  |
| message                 | Error message, which will be returned only if `State` is `Failed`.                      | String  |
| job_id           | ID of the video moderation job                                        | String  |
| state            | Status of the video moderation job. Valid values: `Submitted`, `Snapshoting`, `Success`, `Failed`, `Auditing`. | String |
| creation_time    | Creation time of the video moderation job. | String |
| object                  | Name of the video file to be moderated                                       | String  |
| snapshot_count          | Total number of video screenshot                                             | String  |
| result | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), and `2` (suspiciously sensitive, with human review recommended). | Integer |
| porn_info        | The moderation result of the pornographic information moderation scene.                           | Struct  |
| ads_info         | The moderation result of the advertising information moderation scene.                       | Struct  |
| hit_flag                | Whether the moderation type is hit. Valid values: `0` (miss), `1` (hit), and `2` (suspected). | Integer |
| count              | The number of screenshots that hit this moderation scene.                              | Integer |
| snapshot_info_list      | This field is used to return the screenshot moderation result of the video. Note: Each URL is valid for two hours. If you need to view the data after two hours, initiate a new query request. | Struct |
| audio_section_info_list | This field is used to return the audio moderation result of the video. Note: Each URL is valid for two hours. If you need to view the data after two hours, initiate a new query request. | Struct |

#### `snapshot_info_list` structure description

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------- |
| url | URL of the current video screenshot, at which you can view the screenshot. It must be a standard URL. | String |
| snapshot_time  | This field is used to return the time where the current screenshot is in the entire video in milliseconds, such as 5000 (i.e., 5000 milliseconds after the video starts). | Integer |
| text | This field is used to return the OCR text recognition result of the current screenshot. It will be returned only if text content detection is enabled in the moderation policy. Up to 5,000 bytes can be recognized. | String |
| porn_info        | The moderation result of the pornographic information moderation scene.                           | Struct  |
| ads_info         | The moderation result of the advertising information moderation scene.                       | Struct  |
| hit_flag                | Whether the moderation type is hit. Valid values: `0` (miss), `1` (hit), and `2` (suspected). | Integer |
| score          | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. For example, `Porn 99` means that the content is very likely to be pornographic. | Integer |
| label          | This field indicates the result tag of the screenshot, which may be `SubLabel`, a person name, etc. It is a reserved field for compatibility with legacy versions. | String  |
| sub_lable      | This field indicates the specific sub-tag hit by the moderation job; for example, `SexBehavior` is a sub-tag under the `Porn` tag. Note: This field may return null, indicating that no specific sub-tags are hit. | String  |

#### `audio_section_info_list` structure description

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------- |
| url | URL of the current audio segment of the video, at which you can get the content of the audio segment. It must be a standard URL. | String |
| text | This field is used to return the ASR text recognition result of the audio of the current video. It will be returned only if text content detection is enabled in the moderation policy. Up to 5 hours of content can be recognized. | String |
| offset_time    | This field is used to return the time where the current audio segment is in the entire video in milliseconds, such as 5000 (i.e., 5000 milliseconds after the video starts). | Integer |
| duration | The duration of the current video sound segment in milliseconds. | Integer |
| porn_info        | The moderation result of the pornographic information moderation scene.                           | Struct  |
| ads_info         | The moderation result of the advertising information moderation scene.                       | Struct  |
| hit_flag                | Whether the moderation type is hit. Valid values: `0` (miss), `1` (hit), and `2` (suspected). | Integer |
| score          | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. For example, `Porn 99` means that the content is very likely to be pornographic. | Integer |
| key_words      | Keywords hit by the current moderation scene.      | String  |

#### Response description

| Returned Result   | Description        | Type   |
| ---------- | ----------- | ------ |
| code       | Error code      | Int    |
| error_code | Error code  | String |
| error_msg  | Error message  | String |
| req_id     | Request ID | String |

#### Sample

For the complete code, see the `test_ci_video_auditing()` function in `cos_demo.c`.

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// CI endpoint. For more information, visit https://www.tencentcloud.com/document/product/1045/33423.
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

static void log_get_auditing_result(ci_auditing_job_result_t *result)
{
    int index = 0;
    ci_auditing_snapshot_result_t *snapshot_info;
    ci_auditing_audio_section_result_t *audio_section_info;

    cos_warn_log("nonexist_job_ids: %s", result->nonexist_job_ids.data);
    cos_warn_log("code: %s", result->jobs_detail.code.data);
    cos_warn_log("message: %s", result->jobs_detail.message.data);
    cos_warn_log("state: %s", result->jobs_detail.state.data);
    cos_warn_log("creation_time: %s", result->jobs_detail.creation_time.data);
    cos_warn_log("object: %s", result->jobs_detail.object.data);
    cos_warn_log("snapshot_count: %s", result->jobs_detail.snapshot_count.data);
    cos_warn_log("result: %d", result->jobs_detail.result);

    cos_warn_log("porn_info.hit_flag: %d", result->jobs_detail.porn_info.hit_flag);
    cos_warn_log("porn_info.count: %d", result->jobs_detail.porn_info.count);
    cos_warn_log("ads_info.hit_flag: %d", result->jobs_detail.ads_info.hit_flag);
    cos_warn_log("ads_info.count: %d", result->jobs_detail.ads_info.count);

    cos_list_for_each_entry(ci_auditing_snapshot_result_t, snapshot_info, &result->jobs_detail.snapshot_info_list, node) {
        cos_warn_log("snapshot index:%d", ++index);
        cos_warn_log("snapshot_info->url: %s", snapshot_info->url.data);
        cos_warn_log("snapshot_info->snapshot_time: %d", snapshot_info->snapshot_time);
        cos_warn_log("snapshot_info->text: %s", snapshot_info->text.data);

        cos_warn_log("snapshot_info->porn_info.hit_flag: %d", snapshot_info->porn_info.hit_flag);
        cos_warn_log("snapshot_info->porn_info.score: %d", snapshot_info->porn_info.score);
        cos_warn_log("snapshot_info->porn_info.label: %s", snapshot_info->porn_info.label.data);
        cos_warn_log("snapshot_info->porn_info.sub_lable: %s", snapshot_info->porn_info.sub_lable.data);
        cos_warn_log("snapshot_info->ads_info.hit_flag: %d", snapshot_info->ads_info.hit_flag);
        cos_warn_log("snapshot_info->ads_info.score: %d", snapshot_info->ads_info.score);
        cos_warn_log("snapshot_info->ads_info.label: %s", snapshot_info->ads_info.label.data);
        cos_warn_log("snapshot_info->ads_info.sub_lable: %s", snapshot_info->ads_info.sub_lable.data);
    }

    index = 0;
    cos_list_for_each_entry(ci_auditing_audio_section_result_t, audio_section_info, &result->jobs_detail.audio_section_info_list, node) {
        cos_warn_log("audio_section index:%d", ++index);
        cos_warn_log("audio_section_info->url: %s", audio_section_info->url.data);
        cos_warn_log("audio_section_info->text: %s", audio_section_info->text.data);
        cos_warn_log("audio_section_info->offset_time: %d", audio_section_info->offset_time);
        cos_warn_log("audio_section_info->duration: %d", audio_section_info->duration);

        cos_warn_log("audio_section_info->porn_info.hit_flag: %d", audio_section_info->porn_info.hit_flag);
        cos_warn_log("audio_section_info->porn_info.score: %d", audio_section_info->porn_info.score);
        cos_warn_log("audio_section_info->porn_info.key_words: %s", audio_section_info->porn_info.key_words.data);
        cos_warn_log("audio_section_info->ads_info.hit_flag: %d", audio_section_info->ads_info.hit_flag);
        cos_warn_log("audio_section_info->ads_info.score: %d", audio_section_info->ads_info.score);
        cos_warn_log("audio_section_info->ads_info.key_words: %s", audio_section_info->ads_info.key_words.data);
    }
}

void test_ci_get_video_auditing()
{
    cos_pool_t *p = NULL;
    int is_cname = 0; 
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers;
    ci_video_auditing_job_options_t *job_options;
    ci_video_auditing_job_result_t *job_result;
    ci_auditing_job_result_t *auditing_result;

    // Basic configuration
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    cos_str_set(&options->config->endpoint, TEST_CI_ENDPOINT);     // https://ci.<Region>.myqcloud.com
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    // Replace with your configuration information. For more information, visit https://intl.cloud.tencent.com/document/product/436/48249.
    job_options = ci_video_auditing_job_options_create(p);
    cos_str_set(&job_options->input_object, "test.mp4");
    cos_str_set(&job_options->job_conf.detect_type, "Porn,Ads");
    cos_str_set(&job_options->job_conf.callback_version, "Detail");
    job_options->job_conf.detect_content = 1;
    cos_str_set(&job_options->job_conf.snapshot.mode, "Interval");
    job_options->job_conf.snapshot.time_interval = 1.5;
    job_options->job_conf.snapshot.count = 10;

    // Submit a video moderation job
    s = ci_create_video_auditing_job(options, &bucket, job_options, NULL, &resp_headers, &job_result);
    log_status(s);

    // Wait for the video moderation job to complete. You can modify the wait time here.
    sleep(300);

    // Get the moderation job result
    s = ci_get_auditing_job(options, &bucket, &job_result->jobs_detail.job_id, NULL, &resp_headers, &auditing_result);
    log_status(s);
    if (s->code == 200) {
        log_get_auditing_result(auditing_result);
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

    test_ci_get_video_auditing();

    cos_http_io_deinitialize();

    return 0;
}
```
