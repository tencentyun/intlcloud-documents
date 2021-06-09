## Overview

This document provides an overview of APIs and SDK code samples related to basic image processing.

| API | Operation    |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Scaling](https://intl.cloud.tencent.com/document/product/436/36366) | Scales up/down an image |
| [Cropping](https://intl.cloud.tencent.com/document/product/436/36367) | Crops an image, including regular cropping, scaling and cropping, inscribed circle cropping, rounded corner cropping, and smart cropping |
| [Rotation](https://intl.cloud.tencent.com/document/product/436/36368) | Rotates an image, including common rotation and adaptive rotation |
| [Format conversion](https://intl.cloud.tencent.com/document/product/436/36369) | Converts the format of an image, optimizes GIF format, and performs progressive display |
| [Quality conversion](https://intl.cloud.tencent.com/document/product/436/36370) | Adjusts the quality of an image |
| [Gaussian blurring](https://intl.cloud.tencent.com/document/product/436/36371) | Blurs an image by a Gaussian function |
| [Sharpening](https://intl.cloud.tencent.com/document/product/436/36372) | Sharpens an image |
| [Image watermarks](https://intl.cloud.tencent.com/document/product/436/36373) | Adds a watermark to an image |
| [Text watermarks](https://intl.cloud.tencent.com/document/product/436/36374) | Adds a real-time text watermark to an image |
| [Obtaining basic image information](https://intl.cloud.tencent.com/document/product/436/36375) | Obtains the basic information (such as format, length, and height) about an image |
| [Obtaining image EXIF data](https://intl.cloud.tencent.com/document/product/436/36376) | Obtains the EXIF data of an image |
| [Obtaining the image average hue](https://intl.cloud.tencent.com/document/product/436/36377) | Obtains the average hue of an image |
| [Removing metadata](https://intl.cloud.tencent.com/document/product/436/36378) | Removes the image metadata, including the EXIF data |
| [Quick thumbnail template](https://intl.cloud.tencent.com/document/product/436/36379) | Provides an image processing template to generate thumbnails |
| [Pipeline operator](https://intl.cloud.tencent.com/document/product/436/36380) | Performs multiple operations on images in sequence |

## Scaling

#### Feature description 

Tencent Cloud’s CI uses the `imageMogr2` API to scale images.

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
apr_table_addn(params, "imageMogr2/thumbnail/!50p", "");
cos_str_set(&file, "test.jpg");
cos_str_set(&object, "test.jpg");
s = cos_get_object_to_file(options, &bucket, &object, NULL, params, &file, &resp_headers);
log_status(s);
if (!cos_status_is_ok(s)) {
    printf("cos_get_object_to_file fail, req_id:%s\n", s->req_id);
}
cos_pool_destroy(p);
```

## Cropping

#### Feature description 

CI uses the `imageMogr2` API to crop images, such as regular cropping, scaling and cropping, inscribed circle cropping, rounded corner cropping, and smart cropping.

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
apr_table_addn(params, "imageMogr2/cut/600x600x100x10", "");
cos_str_set(&file, "test.jpg");
cos_str_set(&object, "test.jpg");
s = cos_get_object_to_file(options, &bucket, &object, NULL, params, &file, &resp_headers);
log_status(s);
if (!cos_status_is_ok(s)) {
    printf("cos_get_object_to_file fail, req_id:%s\n", s->req_id);
}
cos_pool_destroy(p);
```

### Other basic image processing operations

#### Feature description 

You can perform other basic processing operations on images by changing the value of the `operation` parameter. For example, you can rotate the image clockwise by 90 degrees as follows:

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
apr_table_addn(params, "imageMogr2/rotate/90", "");
cos_str_set(&file, "test.jpg");
cos_str_set(&object, "test.jpg");
s = cos_get_object_to_file(options, &bucket, &object, NULL, params, &file, &resp_headers);
log_status(s);
if (!cos_status_is_ok(s)) {
    printf("cos_get_object_to_file fail, req_id:%s\n", s->req_id);
}
cos_pool_destroy(p);
```

