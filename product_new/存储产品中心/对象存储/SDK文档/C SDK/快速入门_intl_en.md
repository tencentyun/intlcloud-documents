## Download and Installation

### Relevant Resources

- The COS XML SDK for C source code can be downloaded [here](https://github.com/tencentyun/cos-c-sdk-v5).
- The demo can be downloaded [here](https://github.com/tencentyun/cos-c-sdk-v5/blob/master/cos_c_sdk_test/cos_demo.c).

### Environmental Dependency

Dependency library: libcurl apr apr-util minixml.

### Installing the SDK

1. Download the CMake tool (v2.6.0 and higher recommended) [here](http://www.cmake.org/download/) and install it as shown below:
```bash
./configure
make
make install
```
2. Download libcurl (v7.32.0 and higher recommended) [here](http://curl.haxx.se/download.html?spm=5176.doc32132.2.7.23MmBq) and install it as shown below:
```bash
./configure
make
make install
```
3. Download apr (v1.5.2 and higher recommended) [here](https://apr.apache.org/download.cgi?spm=5176.doc32132.2.9.23MmBq&file=download.cgi) and install it as shown below:
```bash
./configure
make
make install
```
4. Download apr-util (v1.5.4 and higher recommended) [here](https://apr.apache.org/download.cgi?spm=5176.doc32132.2.10.23MmBq&file=download.cgi) and install it as shown below. You need to specify the `--with-apr` option during installation:
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
6. Compile the COS SDK for C. Download the [XML SDK for C source code](https://github.com/tencentyun/cos-c-sdk-v5) and run the following compiling commands:
```bash
cmake .
make
make install
```

## Getting Started

Below is the general flow of using COS XML SDK for C.

1. Initialize the SDK.
2. Set the request option parameters. For more information on the meanings of parameters such as APPID, SecretId, SecretKey, and Bucket contained herein and how to get them, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/18507).
	- APPID is one of the account IDs assigned by the system after you register a Tencent Cloud account.
	- access_key_id and access_key_secret are account API keys.
	- endpoint is the COS access domain name. For more information, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224). For example, the endpoint of Guangzhou region is `cos.ap-guangzhou.myqcloud.com`.
3. Set the parameters required by APIs.
4. Call an SDK API to initiate a request and get the response result of the request.

### Initialization

```cpp
int main(int argc, char *argv[])
{
    /* Call the cos_http_io_initialize method at the program entry. This method internally performs certain global resource initialization tasks related to network and memory */
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
        exit(1);
    }

    /* Call the COS SDK API to upload or download a file */
    /* ... user logic code which is omitted here */

    /* Before the program ends, call the cos_http_io_deinitialize method to release the previously allocated global resources */
    cos_http_io_deinitialize();
    return 0;
}
```

### Initializing Request Options

```cpp
/* This is equivalent to apr_pool_t, which is the memory pool for memory management. Its implementation code is in the apr library */
cos_pool_t *pool;
cos_request_options_t *options;

/* Create a new memory pool. The second parameter is NULL, indicating that it does not inherit from other memory pools */
cos_pool_create(&pool, NULL);

/* Create and initialize options. This parameter mainly contains global configuration information such as endpoint, access_key_id, acces_key_secret, is_cname, and curl
 * The memory of options is allocated by the pool. After the pool is released, the memory of options will be released too, so there is no need to release the memory separately
 */ 
options = cos_request_options_create(pool);
options->config = cos_config_create(options->pool);

/* cos_str_set is a cos_string_t type initialized with a char* string */
cos_str_set(&options->config->endpoint, "<user endpoint>");              // Enter the endpoint based on the COS service domain name in your region
cos_str_set(&options->config->access_key_id, "<user SecretId>");         // This is the SecretId obtained after you register the COS service
cos_str_set(&options->config->access_key_secret, "<user SecretKey>");    // This is the SecretKey obtained after you register the COS service
cos_str_set(&options->config->appid, "<user AppId>");                    // This is the AppId obtained after you register the COS service

/* You can use a temporary key by setting sts_token. When the temporary key is used, access_key_id and access_key_secret need to be set to its SecretId and SecretKey */
//cos_str_set(&options->config->sts_token, "MyTokenString");
/* Whether CNAME is used */
options->config->is_cname = 0;

/* Used to set network-related parameters, such as timeout period */
options->ctl = cos_http_controller_create(options->pool, 0);

/* Used to set whether the Content-MD5 header is automatically added to the upload request. If enable is COS_FALSE, the header will not be automatically added; if enable is COS_TRUE, the header will be automatically added. If this parameter is not set, the header will be added by default */
cos_set_content_md5_enable(options->ctl, COS_FALSE);

/* Used to set the request routing address and port. Generally, this parameter does not need to be set, and the request will be routed according to the domain name resolution result */
//cos_set_request_route(options->ctl, "192.168.12.34", 80);
```

### Creating a Bucket

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_acl_e cos_acl = COS_ACL_PRIVATE;
cos_string_t bucket;
cos_table_t *resp_headers = NULL;

/* Create a new memory pool. The second parameter is NULL, indicating that it does not inherit from other memory pools */
cos_pool_create(&p, NULL);

/* Create and initialize options. This parameter mainly contains global configuration information such as endpoint, access_key_id, acces_key_secret, is_cname, and curl
 * The memory of options is allocated by the pool. After the pool is released, the memory of options will be released too, so there is no need to release the memory separately
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* Set configuration information of parameters such as appid, endpoint, access_key_id, acces_key_secret, is_cname, and curl */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format */
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

### Querying Object List

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_list_object_params_t *list_params = NULL;
cos_string_t bucket;
cos_table_t *resp_headers = NULL;

/* Create a new memory pool. The second parameter is NULL, indicating that it does not inherit from other memory pools */
cos_pool_create(&p, NULL);

/* Create and initialize options. This parameter mainly contains global configuration information such as endpoint, access_key_id, acces_key_secret, is_cname, and curl
 * The memory of options is allocated by the pool. After the pool is released, the memory of options will be released too, so there is no need to release the memory separately
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* Set configuration information of parameters such as appid, endpoint, access_key_id, acces_key_secret, is_cname, and curl */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format */
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

### Uploading an Object

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;

/* Create a new memory pool. The second parameter is NULL, indicating that it does not inherit from other memory pools */
cos_pool_create(&p, NULL);

/* Create and initialize options. This parameter mainly contains global configuration information such as endpoint, access_key_id, acces_key_secret, is_cname, and curl
 * The memory of options is allocated by the pool. After the pool is released, the memory of options will be released too, so there is no need to release the memory separately
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* Set configuration information of parameters such as appid, endpoint, access_key_id, acces_key_secret, is_cname, and curl */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format */
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

### Downloading an Object

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;

/* Create a new memory pool. The second parameter is NULL, indicating that it does not inherit from other memory pools */
cos_pool_create(&p, NULL);

/* Create and initialize options. This parameter mainly contains global configuration information such as endpoint, access_key_id, acces_key_secret, is_cname, and curl
 * The memory of options is allocated by the pool. After the pool is released, the memory of options will be released too, so there is no need to release the memory separately
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* Set configuration information of parameters such as appid, endpoint, access_key_id, acces_key_secret, is_cname, and curl */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format */
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

### Deleting an Object

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

/* Create a new memory pool. The second parameter is NULL, indicating that it does not inherit from other memory pools */
cos_pool_create(&p, NULL);

/* Create and initialize options. This parameter mainly contains global configuration information such as endpoint, access_key_id, acces_key_secret, is_cname, and curl
 * The memory of options is allocated by the pool. After the pool is released, the memory of options will be released too, so there is no need to release the memory separately
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* Set configuration information of parameters such as appid, endpoint, access_key_id, acces_key_secret, is_cname, and curl */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format */
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
