## Overview

This document provides an overview of APIs and SDK code samples for media buckets.

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
| [DescribeMediaBuckets](https://intl.cloud.tencent.com/document/product/436/46909) | Querying media processing activation status | Queries buckets with media processing enabled   |


## Querying Media Processing Activation Status

#### Feature description

This API is used to query buckets with media processing enabled.

#### Method prototype

```cpp
cos_status_t *ci_describe_media_buckets(const cos_request_options_t *options,
                                        const ci_media_buckets_request_t *media_request,
                                        cos_table_t *headers, 
                                        cos_table_t **resp_headers,
                                        ci_media_buckets_result_t **media_result);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------- |
| options | COS request options. | Struct |
| media_request      | Request parameters for media bucket query.                                           | Struct  |
| regions            | Region information, such as `ap-shanghai` and `ap-beijing`. To specify multiple regions, separate them with commas.   | String  |
| bucket_names       | Bucket name. To specify multiple bucket names, separate them with commas. Exact search is supported.                    | String  |
| bucket_name        | Bucket name prefix for prefix search.                                        | String  |
| page_number        | Page number.                                                       | String  |
| page_size          | Number of entries per page.                                                     | String  |
| headers            | COS request headers.                                              | Struct |
| resp_headers       | Returned HTTP response headers.                                       | Struct  |
| media_result       | Returned information of buckets with media processing enabled.                                    | Struct  |
| total_count        | Total number of media buckets.                                              | Int  |
| page_number        | Current page number, which is the same as `pageNumber` in the request.                               | Int  |
| page_size          | Number of entries per page, which is the same as `pageSize` in the request.                                  | Int  |
| media_bucket_list  | Media bucket list.                                             | Struct  |
| bucket_id          | Bucket ID.                                                     | String  |
| name               | Bucket name, which is the same as `BucketId`.                                        | String  |
| region             | Region.                                                     | String  |
| create_time        | Creation time.                                                       | String  |

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code | Error code | Int |
| error_code | Error code | String |
| error_msg | Error message | String |
| req_id | Request message ID | String |

#### Sample
For the complete code, see the `test_ci_media_process_media_bucket()` function in `cos_demo.c`.

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// CI endpoint. For more information, visit https://intl.cloud.tencent.com/document/product/1045/33423
static char TEST_CI_ENDPOINT[] = "https://ci.ap-guangzhou.myqcloud.com";
// A developer-owned secret ID/key used for the project. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char *TEST_ACCESS_KEY_ID;                //your secret_id
static char *TEST_ACCESS_KEY_SECRET;            //your secret_key
// A unique user-level resource identifier for COS access. It can be obtained at https://console.cloud.tencent.com/cam/capi.
static char TEST_APPID[] = "<APPID>";    //your appid

void log_status(cos_status_t *s)
{
    cos_warn_log("status->code: %d", s->code);
    if (s->error_code) cos_warn_log("status->error_code: %s", s->error_code);
    if (s->error_msg) cos_warn_log("status->error_msg: %s", s->error_msg);
    if (s->req_id) cos_warn_log("status->req_id: %s", s->req_id);
}

static void log_media_buckets_result(ci_media_buckets_result_t *result)
{
    int index = 0;
    ci_media_bucket_list_t *media_bucket;

    cos_warn_log("total_count: %d", result->total_count);
    cos_warn_log("page_number: %d", result->page_number);
    cos_warn_log("page_size: %d", result->page_size);

    cos_list_for_each_entry(ci_media_bucket_list_t, media_bucket, &result->media_bucket_list, node) {
        cos_warn_log("media_bucket index:%d", ++index);
        cos_warn_log("media_bucket->bucket_id: %s", media_bucket->bucket_id.data);
        cos_warn_log("media_bucket->name: %s", media_bucket->name.data);
        cos_warn_log("media_bucket->region: %s", media_bucket->region.data);
        cos_warn_log("media_bucket->create_time: %s", media_bucket->create_time.data);
    }
}

void test_ci_media_process_media_bucket()
{
    cos_pool_t *p = NULL;
    int is_cname = 0; 
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_table_t *resp_headers;
    ci_media_buckets_request_t *media_buckets_request;
    ci_media_buckets_result_t *media_buckets_result;

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

    // Use your own configuration. For more information, visit https://intl.cloud.tencent.com/document/product/436/46909.
    media_buckets_request = ci_media_buckets_request_create(p);
    cos_str_set(&media_buckets_request->regions, "");
    cos_str_set(&media_buckets_request->bucket_names, "");
    cos_str_set(&media_buckets_request->bucket_name, "");
    cos_str_set(&media_buckets_request->page_number, "1");
    cos_str_set(&media_buckets_request->page_size, "10");
    s = ci_describe_media_buckets(options, media_buckets_request, NULL, &resp_headers, &media_buckets_result);
    log_status(s);
    if (s->code == 200) {
        log_media_buckets_result(media_buckets_result);
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

    test_ci_media_process_media_bucket();

    cos_http_io_deinitialize();

    return 0;
}
```