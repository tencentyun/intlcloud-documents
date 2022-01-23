## Overview

Errors may occur when data is transferred between the client and the server. COS can not only verify data integrity through [MD5 and custom attributes](https://intl.cloud.tencent.com/document/product/436/32467), but also the CRC64 check code.

COS will calculate the CRC64 of the newly uploaded object and store the result as object attributes. It will carry x-cos-hash-crc64ecma in the returned response header, which indicates the CRC64 value of the uploaded object calculated according to [ECMA-182 standard](https://www.ecma-international.org/publications/standards/Ecma-182.htm). If an object already has a CRC64 value stored before this feature is activated, COS will not calculate its CRC64 value, nor will it be returned when the object is obtained.

## Description

APIs that currently support CRC64 include:

- APIs for simple upload
	- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) and [POST Object](https://intl.cloud.tencent.com/document/product/436/14690): you can get the CRC64 check value for your file from the response headers.
- Multipart upload APIs
	- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750): you can compare and verify the CRC64 value returned by COS against the value calculated locally.
	- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742): returns a CRC64 value for the entire object only if each part has a CRC64 attribute. Otherwise, no value is returned.
- The [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) operation returns a corresponding CRC64 value.
- When you call the [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881), the CRC64 value is returned only if the source object has one.
- The [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) and [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) operations return the CRC64 value provided the object has one. You can compare and verify the CRC64 value returned by COS against that calculated locally.

## API Samples

#### Upload Part response

The following example shows the response to an Upload Part request. The `x-cos-hash-crc64ecma` header represents the CRC64 value of a part, which you can compare against the locally calculated CRC64 value to verify the part integrity.

```shell
HTTP/1.1 200 OK
content-length: 0
connection: close
date: Thu, 05 Dec 2019 01:58:03 GMT
etag: "358e8c8b1bfa35ee3bd44cb3d2cc416b"
server: tencent-cos
x-cos-hash-crc64ecma: 15060521397700495958
x-cos-request-id: NWRlODY0MmJfMjBiNDU4NjRfNjkyZl80ZjZi****
```

#### Complete Multipart Upload response

The following example shows the response to a Complete Multipart Upload request. The `x-cos-hash-crc64ecma` header represents the CRC64 value of an entire object, which you can compare against the locally calculated CRC64 value to verify the object integrity.

```shell
HTTP/1.1 200 OK
content-type: application/xml
transfer-encoding: chunked
connection: close
date: Thu, 05 Dec 2019 02:01:17 GMT
server: tencent-cos
x-cos-hash-crc64ecma: 15060521397700495958
x-cos-request-id: NWRlODY0ZWRfMjNiMjU4NjRfOGQ4Ml81MDEw****

[Object Content]
```

## SDK Samples

#### Description

This API is used to verify the CRC64 value consistency of the object data when the object is uploaded or downloaded.

#### Method prototype

```cpp
cos_status_t *cos_upload_part_from_buffer(const cos_request_options_t *options,
                                          const cos_string_t *bucket, 
                                          const cos_string_t *object, 
                                          const cos_string_t *upload_id, 
                                          int part_num, 
                                          cos_list_t *buffer, 
                                          cos_table_t **resp_headers);

cos_status_t *cos_upload_part_from_file(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        const cos_string_t *object,
                                        const cos_string_t *upload_id, 
                                        int part_num, 
                                        cos_upload_file_t *upload_file,
                                        cos_table_t **resp_headers);

cos_status_t *cos_download_part_to_file(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        const cos_string_t *object,
                                        cos_upload_file_t *download_file,
                                        cos_table_t **resp_headers);

cos_status_t *cos_put_object_from_buffer(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         const cos_string_t *object, 
                                         cos_list_t *buffer,
                                         cos_table_t *headers, 
                                         cos_table_t **resp_headers);

cos_status_t *cos_put_object_from_file(const cos_request_options_t *options,
                                       const cos_string_t *bucket, 
                                       const cos_string_t *object, 
                                       const cos_string_t *filename,
                                       cos_table_t *headers, 
                                       cos_table_t **resp_headers);

cos_status_t *cos_get_object_to_buffer(const cos_request_options_t *options, 
                                       const cos_string_t *bucket, 
                                       const cos_string_t *object,
                                       cos_table_t *headers, 
                                       cos_table_t *params,
                                       cos_list_t *buffer, 
                                       cos_table_t **resp_headers);

cos_status_t *cos_get_object_to_file(const cos_request_options_t *options,
                                     const cos_string_t *bucket, 
                                     const cos_string_t *object,
                                     cos_table_t *headers, 
                                     cos_table_t *params,
                                     cos_string_t *filename, 
                                     cos_table_t **resp_headers);

cos_status_t *cos_append_object_from_buffer(const cos_request_options_t *options,
                                            const cos_string_t *bucket, 
                                            const cos_string_t *object, 
                                            int64_t position,
                                            cos_list_t *buffer, 
                                            cos_table_t *headers, 
                                            cos_table_t **resp_headers);

cos_status_t *cos_append_object_from_file(const cos_request_options_t *options,
                                          const cos_string_t *bucket, 
                                          const cos_string_t *object, 
                                          int64_t position,
                                          const cos_string_t *append_file, 
                                          cos_table_t *headers, 
                                          cos_table_t **resp_headers);

cos_status_t *cos_resumable_download_file(cos_request_options_t *options,
                                            cos_string_t *bucket,
                                            cos_string_t *object,
                                            cos_string_t *filepath,
                                            cos_table_t *headers,
                                            cos_table_t *params,
                                            cos_resumable_clt_params_t *clt_params,
                                            cos_progress_callback progress_callback);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ------------------------------------------------------------ | ------- |
| options | COS request options | Struct |
| options.ctl.options.enable_crc  | Whether to enable CRC check. CRC check is enabled by default.                      | Int  |

>?For other parameters, please see [Object Operations](https://intl.cloud.tencent.com/document/product/436/31518).

#### Response description

| Response Parameter  | Description        | Type   |
| ---------- | ----------- | ------ |
| code       | Error code (If CRC fails, `COSE_CRC_INCONSISTENT_ERROR` is returned.)      | Int    |
| error_code | Error code content | String |
| error_msg | Error code description | String |
| req_id | Request message ID | String |


#### Sample
The APIs for simple upload and simple download are used as examples. It is the same with other APIs. You only need to set **options** > **ctl** > **options** > **enable_crc** to `COS_TRUE`, which is the default value.

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

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

void test_data_crc64()
{
    cos_pool_t *p = NULL;
    int is_cname = 0; 
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers;
    cos_table_t *headers = NULL;
    cos_list_t buffer;
    cos_list_t download_buffer;
    cos_string_t object;
    cos_buf_t *content = NULL;
    char *str = "This is my test data.";

    // Basic configuration
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    options->ctl->options->enable_crc = COS_TRUE;   // Enable CRC check (enabled by default)
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, TEST_OBJECT_NAME1);

    // Upload an object and enable CRC check
    cos_list_init(&buffer);
    content = cos_buf_pack(options->pool, str, strlen(str));
    cos_list_add_tail(&content->node, &buffer);
    s = cos_put_object_from_buffer(options, &bucket, &object, 
                    &buffer, headers, &resp_headers);
    log_status(s);

    // Download an object and enable CRC check
    cos_list_init(&download_buffer);
    s = cos_get_object_to_buffer(options, &bucket, &object, 
                        headers, NULL, &download_buffer, &resp_headers);
    log_status(s);

    // Destroy the memory pool
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

    test_data_crc64();

    cos_http_io_deinitialize();

    return 0;
}
```
