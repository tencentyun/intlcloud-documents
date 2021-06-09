## Overview

This document provides an overview of APIs and SDK code samples related to Image Advanced Compression.


| API | Description |
| :--------------- |  :--------------------- |
| [Image Advanced Compression](https://intl.cloud.tencent.com/document/product/436/40119) | Image Advanced Compression allows you to easily convert images into formats that provide a high compression ratio, such as TPG and HEIF. This effectively reduces the transmission time, loading time, and the use of bandwidth and traffic. |

#### Method prototype

Image compression is implemented via [object download](https://intl.cloud.tencent.com/document/product/436/31518). All you need to do is adding the request parameters in the following syntax:

```c
imageMogr2/format/<Format>
```
| Parameter | Description |
| :--------- | :--------------------------------------------- |
| format | Target compression format, which can be TPG or HEIF |



#### Sample request 

```c
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
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
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
```
