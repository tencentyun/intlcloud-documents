## Overview

You can encrypt uploaded objects in the following ways.

## Using SSE-COS Encryption

#### Description

With this method, your master key and data are managed by COS. COS can automatically encrypt your data when written into the IDC and automatically decrypt it when accessed. Currently, COS supports AES-256 encryption using a COS master key pair.

In the C SDK, you need to configure the encryption by specifying the `x-cos-server-side-encryption` header.

#### Sample

```cpp
int main(int argc, char *argv[])
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers = NULL;
    cos_table_t *headers = NULL;
    cos_string_t file;
    cos_string_t download_file;
	// Initialize
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }
    cos_pool_create(&p, NULL);
    // Initialize the request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    cos_str_set(&options->config->endpoint, "cos.ap-guangzhou.myqcloud.com"); // Your endpoint
    cos_str_set(&options->config->access_key_id, "SECRETID");// Your SecretId 
    cos_str_set(&options->config->access_key_secret, "SECRETKEY"); // Your SecretKey
    cos_str_set(&options->config->appid, "APPID");// Your APPID
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, "<BucketName-APPID>");// Your bucket name in the format: BucketName-APPID

    // Set headers for server-side SSE-COS encryption
    headers = cos_table_make(p, 1);
    apr_table_add(headers, "x-cos-server-side-encryption", "AES256");

    cos_str_set(&file, "example1.txt");// Your filename
    cos_str_set(&object, "example_object");// Your object name

    // Upload an object
    s = cos_put_object_from_file(options, &bucket, &object, &file, headers, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put object succeeded\n");
    } else {
        printf("put object failed\n");
    }
    
    // Download an object
    cos_str_set(&download_file, "example2.txt");
    s = cos_get_object_to_file(options, &bucket, &object, NULL, NULL, &download_file, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("get object succeeded\n");
    } else {
        printf("get object failed\n");
    }
    
    cos_pool_destroy(p);

    cos_http_io_deinitialize();
    return 0;
}
```

## Using SSE-C Encryption

The encryption key is provided by the customer. When you upload an object, COS will apply AES-256 encryption to your data using the customer-provided encryption key pair. In the C SDK, you need to configure the encryption by specifying the `x-cos-server-side-encryption-customer-*` header.

#### Description

> !
>- This type of encryption requires using HTTPS requests.
>- customerKey: the key provided by the user; this key should be a 32-byte string consisting of numbers, letters, and symbols. Chinese characters are not supported.
>- If this encryption method was used when you uploaded the source file, you should also use it when you GET (download) or HEAD (query) this file.


#### Sample
```cpp
int main(int argc, char *argv[])
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers = NULL;
    cos_table_t *headers = NULL;
    cos_string_t file;
    cos_string_t download_file;
	// Initialize
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }
    cos_pool_create(&p, NULL);
    // Initialize the request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    cos_str_set(&options->config->endpoint, "https://cos.ap-guangzhou.myqcloud.com"); // Your endpoint, which requires requests to be sent over HTTPS
    cos_str_set(&options->config->access_key_id, "SECRETID");// Your SecretId 
    cos_str_set(&options->config->access_key_secret, "SECRETKEY"); // Your SecretKey
    cos_str_set(&options->config->appid, "APPID");// Your APPID
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, "<BucketName-APPID>");// Your bucket name in the format: BucketName-APPID

    // Set headers for SSE-C encryption
    headers = cos_table_make(p, 3);
    apr_table_add(headers, "x-cos-server-side-encryption-customer-algorithm", "AES256");
    apr_table_add(headers, "x-cos-server-side-encryption-customer-key", "MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=");// Replace with your own Base64-encoded server-side encryption key
    apr_table_add(headers, "x-cos-server-side-encryption-customer-key-MD5", "U5L61r7jcwdNvT7frmUG8g==");// Replace with the Base64-encoded MD5 hash of your own server-side encryption key

    cos_str_set(&file, "example1.txt");// Your file name
    cos_str_set(&object, "example_object");// Your object name

    // Upload an object
    s = cos_put_object_from_file(options, &bucket, &object, &file, headers, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put object succeeded\n");
    } else {
        printf("put object failed\n");
    }
    
    // Download an object, which also requires the headers for server-side encryption
    cos_str_set(&download_file, "example2.txt");
    s = cos_get_object_to_file(options, &bucket, &object, headers, NULL, &download_file, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("get object succeeded\n");
    } else {
        printf("get object failed\n");
    }

    cos_pool_destroy(p);

    cos_http_io_deinitialize();
    return 0;
}
```
