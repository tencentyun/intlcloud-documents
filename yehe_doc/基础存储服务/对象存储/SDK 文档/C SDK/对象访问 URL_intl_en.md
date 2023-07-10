## Overview
This document provides code samples related to obtaining an object URL.

## Obtaining Object URLs

#### Feature description
The SDK allows you to obtain object access URLs for anonymous download or distribution.

#### Method prototype

```
const char *cos_gen_object_url(const cos_request_options_t *options, const cos_string_t *bucket, const cos_string_t *object)
```

#### Sample request

[//]: # ".cssg-snippet-get-object-url-alias"
```go
cos_pool_t *p = NULL;
int is_cname = 0; 
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t filepath;
cos_resumable_clt_params_t *clt_params;
      
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
init_test_request_options(options, is_cname);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, "exampleobject");

printf("url:%s\n", cos_gen_object_url(options, &bucket, &object));

cos_pool_destroy(p);
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| options | COS request options | Struct | Yes |
| Bucket | Bucket name in the format of `BucketName-APPID` | Struct | Yes |
| object | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |

#### Response description

An object access URL is returned upon success.	
