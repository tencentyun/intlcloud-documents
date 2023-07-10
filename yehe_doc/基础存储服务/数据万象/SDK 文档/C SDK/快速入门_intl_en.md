## Download and Installation

#### Relevant resources

- Download COS XML C SDK source code: [XML C SDK](https://github.com/tencentyun/cos-c-sdk-v5).
- Download demo: [XML C SDK Demo](https://github.com/tencentyun/cos-c-sdk-v5/blob/master/cos_c_sdk_test/cos_demo.c).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cos-c-sdk-v5/blob/master/CHANGELOG.md).
- For SDK FAQs, see [C SDK FAQs](https://intl.cloud.tencent.com/document/product/436/40772).


>? If you encounter errors such as non-existent functions or methods when using the SDK, you can update the SDK to the latest version and try again.
>

#### Environmental dependencies

Dependent library: libcurl apr apr-util minixml.

#### Installing SDK

1. Download the CMake tool (v2.6.0 and higher recommended) [here](http://www.cmake.org/download/) and install it as shown below:
```bash
./configure
make
make install
```
2. Download libcurl (v7.32.0 or higher recommended) [here](http://curl.haxx.se/download.html?spm=5176.doc32132.2.7.23MmBq) and install it as shown below:
```bash
./configure
make
make install
```
3. Download apr (v1.5.2 or higher recommended) [here](https://apr.apache.org/download.cgi?spm=5176.doc32132.2.9.23MmBq&file=download.cgi) and install it as shown below:
```bash
./configure
make
make install
```
4. Download apr-util (v1.5.4 or higher recommended) [here](https://apr.apache.org/download.cgi?spm=5176.doc32132.2.10.23MmBq&file=download.cgi) and install it as shown below. You need to specify the `--with-apr` option during installation.
```bash
./configure --with-apr=/your/apr/install/path
make
make install
```
5. Download minixml (v2.8 - 2.12 recommended) [here](https://www.msweet.org/mxml/) and install it as shown below:
```bash
./configure
make
make install
```
6. Compile the COS C SDK. Download the [XML C SDK source code](https://github.com/tencentyun/cos-c-sdk-v5) and run the following compiling commands:
```bash
cmake .
make
make install
```

## Getting Started

Below is the general process of using COS XML C SDK.

1. Initialize the SDK.
2. Set the request option parameters. For the definitions of parameters such as APPID, SecretId, SecretKey, and Bucket, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).
 - APPID is one of the account IDs assigned by the system after you register for a Tencent Cloud account.
 - `access_key_id` and `access_key_secret` are account API keys.
 - `endpoint` is the COS access domain name. For more information, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). For example, the endpoint of the Guangzhou region is `cos.ap-guangzhou.myqcloud.com`, and the endpoint of a global acceleration domain name is `cos.accelerate.myqcloud.com`. You can add "http" or "https" to the endpoints. The SDK accesses COS via HTTP by default. For example, the endpoint for accessing the Guangzhou region via HTTPS is `https://cos.ap-guangzhou.myqcloud.com`.
 - `is_cname` specifies whether an endpoint is a custom domain name. If `is_cname` is set to 1, the endpoint is a custom domain name.
3. Set the parameters required for APIs.
4. Call the SDK API to initiate a request and get the response.

### Initialization

>!
> - We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) to call the SDK for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.


```cpp
int main(int argc, char *argv[])
{
    /* Call the cos_http_io_initialize method at the program entry to perform certain global resource initialization tasks internally covering network, memory, etc. */
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
        exit(1);
    }

    /* Call a COS SDK API to upload/download files */
    /* ... User logic code, omitted here */

    /* Call the cos_http_io_deinitialize method to release global resources allocated previously before the program ends */
    cos_http_io_deinitialize();
    return 0;
}
```

### Initializing request options

```cpp
/* Equivalent to `apr_pool_t`, the memory pool for memory management. The implementation code can be found in the apr library */
cos_pool_t *pool;
cos_request_options_t *options;

/* Create a new memory pool. The second parameter is NULL, indicating that it is not inherited from other memory pools */
cos_pool_create(&pool, NULL);

/* Create and initialize `options`. This parameter contains global configuration information such as endpoint, access_key_id, acces_key_secret, is_cname, and curl
 * The memory of `options` is allocated by the pool, and will be released upon pool release, so there is no need to release the memory separately.
 */ 
options = cos_request_options_create(pool);
options->config = cos_config_create(options->pool);

/* cos_str_set is a cos_string_t type initialized with a char* string */
cos_str_set(&options->config->endpoint, "<user's endpoint>");              // Enter the endpoint based on the COS service domain name of your region
cos_str_set(&options->config->access_key_id, "<user's SecretId>");         // This is the SecretId obtained after you register for the COS service
cos_str_set(&options->config->access_key_secret, "<user's SecretKey>");    // This is the SecretKey obtained after you register for the COS service
cos_str_set(&options->config->appid, "<user's AppId>");                    // This is the AppId obtained after you register for the COS service

/* You can use a temporary key by setting `sts_token`. When you use a temporary key, you need to set `access_key_id` and `access_key_secret` to its SecretId and SecretKey */
//cos_str_set(&options->config->sts_token, "MyTokenString");
/* Whether CNAME is used */
options->config->is_cname = 0;
/* Use a custom domain name to access COS */
/*
options->config->is_cname = 1;
cos_str_set(&options->config->endpoint, "<Custom domain name>");
*/

/* Used to set network-related parameters, such as the timeout duration */
options->ctl = cos_http_controller_create(options->pool, 0);

/* Used to set whether to add Content-MD5 header automatically to the upload request. If `enable` is COS_FALSE, the header will not be automatically added; if `enable` is COS_TRUE, the header will be automatically added. If this parameter is not set, the header will be added by default */
cos_set_content_md5_enable(options->ctl, COS_FALSE);

/* Used to set the request routing address and port. Normally, you do not need to set this parameter. The request will be routed according to the result of domain name resolution */
//cos_set_request_route(options->ctl, "192.168.12.34", 80);
```

>? For more information about how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
>


### Creating a bucket

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_acl_e cos_acl = COS_ACL_PRIVATE;
cos_string_t bucket;
cos_table_t *resp_headers = NULL;

/* Create a new memory pool. The second parameter is NULL, indicating that it is not inherited from other memory pools */
cos_pool_create(&p, NULL);

/* Create and initialize `options`. This parameter contains global configuration information such as endpoint, access_key_id, acces_key_secret, is_cname, and curl
 * The memory of `options` is allocated by the pool, and will be released upon pool release, so there is no need to release the memory separately.
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* Set configuration information such as appid, endpoint, access_key_id, acces_key_secret, is_cname, and curl parameters */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* Enter the bucket name in the format of BucketName-APPID. */
cos_str_set(&bucket, TEST_BUCKET_NAME);

/* Call an API to create a bucket */
s = cos_create_bucket(options, &bucket, cos_acl, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("create bucket succeeded\n");
} else {
		printf("create bucket failed\n");
}

//destroy memory pool
cos_pool_destroy(p); 
```

### Querying objects

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_list_object_params_t *list_params = NULL;
cos_string_t bucket;
cos_table_t *resp_headers = NULL;

/* Re-create a new memory pool. The second parameter is NULL, which indicates it is not inherited from other memory pools */
cos_pool_create(&p, NULL);

/* Create and initialize `options`. This parameter contains global configuration information such as endpoint, access_key_id, acces_key_secret, is_cname, and curl
 * The memory of `options` is allocated by the pool, and will be released upon pool release, so there is no need to release the memory separately.
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* Set configuration information such as appid, endpoint, access_key_id, acces_key_secret, is_cname, and curl parameters */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* The bucket name entered here must be in the format of BucketName-APPID. */
cos_str_set(&bucket, TEST_BUCKET_NAME);

/* Call an API to query object list */
list_params = cos_create_list_object_params(p);
cos_str_set(&list_params->encoding_type, "url");
s = cos_list_object(options, &bucket, list_params, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("list object succeeded\n");
} else {
		printf("list object failed\n");
}

//destroy memory pool
cos_pool_destroy(p); 
```

### Uploading an object

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;

/* Re-create a new memory pool. The second parameter is NULL, which indicates it is not inherited from other memory pools */
cos_pool_create(&p, NULL);

/* Create and initialize `options`. This parameter contains global configuration information such as endpoint, access_key_id, acces_key_secret, is_cname, and curl
 * The memory of `options` is allocated by the pool, and will be released upon pool release, so there is no need to release the memory separately.
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* Set configuration information such as appid, endpoint, access_key_id, acces_key_secret, is_cname, and curl parameters */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* The bucket name entered here must be in the format of BucketName-APPID. */
cos_str_set(&bucket, TEST_BUCKET_NAME);

/* Call an API to upload an object */
cos_str_set(&file, TEST_DOWNLOAD_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_put_object_from_file(options, &bucket, &object, &file, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("put object succeeded\n");
} else {
		printf("put object failed\n");
}

//destroy memory pool
cos_pool_destroy(p); 
```

### Downloading an object

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;

/* Re-create a new memory pool. The second parameter is NULL, which indicates it is not inherited from other memory pools */
cos_pool_create(&p, NULL);

/* Create and initialize `options`. This parameter contains global configuration information such as endpoint, access_key_id, acces_key_secret, is_cname, and curl
 * The memory of `options` is allocated by the pool, and will be released upon pool release, so there is no need to release the memory separately.
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* Set configuration information such as appid, endpoint, access_key_id, acces_key_secret, is_cname, and curl parameters */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* The bucket name entered here must be in the format of BucketName-APPID. */
cos_str_set(&bucket, TEST_BUCKET_NAME);

/* Call an API to download an object */
cos_str_set(&file, TEST_DOWNLOAD_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_get_object_to_file(options, &bucket, &object, NULL, NULL, &file, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("get object succeeded\n");
} else {
		printf("get object failed\n");
}

//destroy memory pool
cos_pool_destroy(p); 
```

### Deleting an object

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

/* Create a new memory pool. The second parameter is NULL, indicating that it is not inherited from other memory pools */
cos_pool_create(&p, NULL);

/* Create and initialize `options`. This parameter contains global configuration information such as endpoint, access_key_id, access_key_secret, is_cname, and curl
 * The memory of `options` is allocated by the pool, and will be released upon pool release, so there is no need to release the memory separately.
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* Set configuration information such as appid, endpoint, access_key_id, acces_key_secret, is_cname, and curl parameters */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* The bucket name entered here must be in the format of BucketName-APPID. */
cos_str_set(&bucket, TEST_BUCKET_NAME);

/* Call an API to delete an object */
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_delete_object(options, &bucket, &object, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("delete object succeeded\n");
} else {
		printf("delete object failed\n");
}

//destroy memory pool
cos_pool_destroy(p); 
```
