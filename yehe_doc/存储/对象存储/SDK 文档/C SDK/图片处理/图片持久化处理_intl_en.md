

## Overview

This document provides an overview of APIs and SDK code samples related to persistent image processing.

| API | Description |
| :----------------------------------------------------------- | :----------------------------------- |
| [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/436/40482) | COS supports processing images upon upload. You can also process images that are already stored in COS and save the processed images to COS. |


## Processing upon Upload

#### Feature description 

COS allows you to process images upon upload. To do so, you can add the `Pic-Operations` option to the request header and set the relevant parameters. You can also save the input images and processing results to COS. Currently, images smaller than 20 MB can be processed.

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


#### Sample request 

```c
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *headers = NULL;
cos_table_t *resp_headers = NULL;
ci_operation_result_t *results = NULL;

// Create a memory pool.
cos_pool_create(&p, NULL);

// Initialize the request options.
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

// Process images upon upload.
headers = cos_table_make(p, 1);
apr_table_addn(headers, "pic-operations", "{\"is_pic_info\":1,\"rules\":[{\"fileid\":\"test.png\",\"rule\":\"imageView2/format/png\"}]}");
cos_str_set(&file, "test.jpg");
cos_str_set(&object, "test.jpg");
s = ci_put_object_from_file(options, &bucket, &object, &file, headers, &resp_headers, &results);
if (!cos_status_is_ok(s)) {
    printf("put object failed: %s\n", s->req_id);
}
printf("origin key: %s\n", results.origin.key.data);
printf("process key: %s\n", results.object.key.data);

// Destroy the memory pool.
cos_pool_destroy(p); 
```

#### Parameter description

| Parameter | Description | Type |
| :----------- | :----------------------------------------------------------- | :----- |
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | String |
| object | Object name | String |
| filename | Filename of the local object before it is uploaded to COS | String |
| headers      | Additional headers of a COS request | Struct |
| resp_headers | Returns the HTTP response headers | Struct |
| results      | Processing results of in-cloud data  | Struct |



## Processing In-Cloud Images
#### Feature description 

This API is used to process an in-cloud image and save the processing result to COS.

#### Method prototype
```c
cos_status_t *ci_image_process(const cos_request_options_t *options,
								const cos_string_t *bucket,
								const cos_string_t *object,
								cos_table_t *headers,
								cos_table_t **resp_headers,
								ci_operation_result_t *results);
```

#### Sample request 

```c
cos_pool_t *p = NULL;
int is_cname = 0; 
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers;
cos_table_t *headers = NULL;
ci_operation_result_t results;
  
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

cos_str_set(&object, "test.jpg");
headers = cos_table_make(p, 1);
apr_table_addn(headers, "pic-operations", "{\"is_pic_info\":1,\"rules\":[{\"fileid\":\"test.png\",\"rule\":\"imageView2/format/png\"}]}");
      
s = ci_image_process(options, &bucket, &object, headers, &resp_headers, &results);
if (!cos_status_is_ok(s)) {
    printf("ci image process fail, req_id:%s\n", s->req_id);
}
printf("origin key: %s\n", results.origin.key.data);
printf("process key: %s\n", results.object.key.data);
cos_pool_destroy(p);
```



#### Parameter description

| Parameter | Description | Type |
| --------- | ------------------------------------------------------------ | ------ |
| options | COS request options | Struct |
| bucket | Bucket name in the format of `BucketName-APPID` | string |
| object | Object name | string |
| headers | Additional headers of a COS request. You need to add the `Pic-Operations` header for CI to process images. | Struct |
| resp_headers | Returns the HTTP response headers | Struct |
| results | Processing results of in-cloud data | Struct |

