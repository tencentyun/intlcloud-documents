## 简介

本文档提供关于图片二维码相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作描述                         |
| ------------------------------------------ | -------------------------- |
| [二维码识别](https://intl.cloud.tencent.com/document/product/1045/47945) | 二维码识别功能可识别图片中有效二维码的位置及内容，输出图像中二维码包含的文本信息（每个二维码对应的 URL 或文本），并可对识别出的二维码添加马赛克              |

## 二维码识别

二维码识别功能可识别图片中有效二维码的位置及内容，输出图像中二维码包含的文本信息（每个二维码对应的 URL 或文本），并可对识别出的二维码添加马赛克。

### 上传时识别


#### 方法原型

```c
cos_status_t *ci_put_object_from_file(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         const cos_string_t *object, 
                                         const cos_string_t *filename,
                                         cos_table_t *headers, 
                                         cos_table_t **resp_headers,
                                         ci_operation_result_t **results)
```

#### 功能说明

图片上传时识别二维码的请求包与 COS 简单上传文件接口一致，只需在请求包头部增加图片处理参数 Pic-Operations。


#### 请求示例

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// endpoint 是 COS 访问域名信息，详情请参见 https://cloud.tencent.com/document/product/436/6224 文档
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// 数据万象的访问域名，详情请参见 https://cloud.tencent.com/document/product/460/31066 文档
static char TEST_CI_ENDPOINT[] = "https://ci.ap-guangzhou.myqcloud.com";
// 开发者拥有的项目身份ID/密钥，可在 https://console.cloud.tencent.com/cam/capi 页面获取
static char *TEST_ACCESS_KEY_ID;                //your secret_id
static char *TEST_ACCESS_KEY_SECRET;            //your secret_key
// 开发者访问 COS 服务时拥有的用户维度唯一资源标识，用以标识资源，可在 https://console.cloud.tencent.com/cam/capi 页面获取
static char TEST_APPID[] = "<APPID>";    //your appid
//the cos bucket name, syntax: [bucket]-[appid], for example: mybucket-1253666666，可在 https://console.cloud.tencent.com/cos5/bucket 查看
static char TEST_BUCKET_NAME[] = "<bucketname-appid>"; 

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

void test_ci_image_qrcode()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t file;
    cos_table_t *resp_headers;
    cos_table_t *headers = NULL;
    ci_operation_result_t *results = NULL;
    ci_qrcode_info_t *content = NULL;

    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, "test.jpg");
    
    headers = cos_table_make(p, 1);
    apr_table_addn(headers, "pic-operations", "{\"is_pic_info\":1,\"rules\":[{\"fileid\":\"test.png\",\"rule\":\"QRcode/cover/1\"}]}");
    // 上传时识别
    cos_str_set(&file, "test.jpg");
    cos_str_set(&object, "test.jpg");
    s = ci_put_object_from_file(options, &bucket, &object, &file, headers, &resp_headers, &results);
    log_status(s);
    if (!cos_status_is_ok(s)) {
        printf("put object failed\n");
    }
    printf("CodeStatus: %d\n", results->object.code_status);
    cos_list_for_each_entry(ci_qrcode_info_t, content, &results->object.qrcode_info, node) {
        printf("CodeUrl: %s\n", content->code_url.data);
        printf("Point: %s\n", content->point[0].data);
        printf("Point: %s\n", content->point[1].data);
        printf("Point: %s\n", content->point[2].data);
        printf("Point: %s\n", content->point[3].data);
    }

    //销毁内存池
    cos_pool_destroy(p); 
}

int main(int argc, char *argv[])
{
    // 通过环境变量获取 SECRETID 和 SECRETKEY
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    //set log level, default COS_LOG_WARN
    cos_log_set_level(COS_LOG_WARN);

    //set log output, default stderr
    cos_log_set_output(NULL);

    test_ci_image_qrcode();

    cos_http_io_deinitialize();

    return 0;
}
```

#### 参数说明

| 参数名称     | 参数描述                                                     | 类型   |
| :----------- | :----------------------------------------------------------- | :----- |
| options      | COS 请求选项                                                 | Struct |
| bucket       | 存储桶名称，存储桶的命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String |
| object       | Object 名称                                                  | String |
| filename     | Object 本地保存文件名称                                      | String |
| headers      | COS 请求附加头域                                             | Struct |
| resp_headers | 返回 HTTP 响应消息的头域                                     | Struct |
| results      | 云上数据处理返回信息                                         | Struct |



### 下载时识别

#### 功能说明

下载文件时进行二维码识别。

#### 方法原型
```c
cos_status_t *ci_get_qrcode(const cos_request_options_t *options,
                             const cos_string_t *bucket,
                             const cos_string_t *object,
                             int cover,
                             cos_table_t *headers,
                             cos_table_t *query_params, 
                             cos_table_t **resp_headers,
                             ci_qrcode_result_t **results)
```

#### 请求示例

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <unistd.h>

// endpoint 是 COS 访问域名信息，详情请参见 https://cloud.tencent.com/document/product/436/6224 文档
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// 数据万象的访问域名，详情请参见 https://cloud.tencent.com/document/product/460/31066 文档
static char TEST_CI_ENDPOINT[] = "https://ci.ap-guangzhou.myqcloud.com";
// 开发者拥有的项目身份ID/密钥，可在 https://console.cloud.tencent.com/cam/capi 页面获取
static char *TEST_ACCESS_KEY_ID;                //your secret_id
static char *TEST_ACCESS_KEY_SECRET;            //your secret_key
// 开发者访问 COS 服务时拥有的用户维度唯一资源标识，用以标识资源，可在 https://console.cloud.tencent.com/cam/capi 页面获取
static char TEST_APPID[] = "<APPID>";    //your appid
//the cos bucket name, syntax: [bucket]-[appid], for example: mybucket-1253666666，可在 https://console.cloud.tencent.com/cos5/bucket 查看
static char TEST_BUCKET_NAME[] = "<bucketname-appid>"; 

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

void test_ci_get_image_qrcode()
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers;
    ci_qrcode_info_t *content = NULL;
    ci_qrcode_result_t *result2 = NULL;

    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, "test.jpg");

    // 下载时识别
    s = ci_get_qrcode(options, &bucket, &object, 1, NULL, NULL, &resp_headers, &result2);
    log_status(s);
    if (!cos_status_is_ok(s)) {
        printf("get object failed\n");
    }
    printf("CodeStatus: %d\n", result2->code_status);
    cos_list_for_each_entry(ci_qrcode_info_t, content, &result2->qrcode_info, node) {
        printf("CodeUrl: %s\n", content->code_url.data);
        printf("Point: %s\n", content->point[0].data);
        printf("Point: %s\n", content->point[1].data);
        printf("Point: %s\n", content->point[2].data);
        printf("Point: %s\n", content->point[3].data);
    }
    printf("ImageResult: %s\n", result2->result_image.data);

    //销毁内存池
    cos_pool_destroy(p); 
}

int main(int argc, char *argv[])
{
    // 通过环境变量获取 SECRETID 和 SECRETKEY
    TEST_ACCESS_KEY_ID     = getenv("COS_SECRETID");
    TEST_ACCESS_KEY_SECRET = getenv("COS_SECRETKEY");
 
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }

    //set log level, default COS_LOG_WARN
    cos_log_set_level(COS_LOG_WARN);

    //set log output, default stderr
    cos_log_set_output(NULL);

    test_ci_get_image_qrcode();

    cos_http_io_deinitialize();

    return 0;
}
```


#### 参数说明


| 参数名称  | 参数描述                                                     | 类型   |
| --------- | ------------------------------------------------------------ | ------ |
| options | COS 请求选项 | Struct |
| bucket | 存储桶名称，Bucket 的命名规则为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | string |
| object | Object 名称 | string |
| cover | 二维码覆盖功能，对识别出的二维码覆盖上马赛克。取值为0或1。0表示不开启二维码覆盖，1表示开启二维码覆盖 | int |
| headers | COS 请求附加头域 | Struct |
| query_params | COS 请求操作参数 | Struct |
| resp_headers | 返回 HTTP 响应消息的头域 | Struct |
| results | 二维码识别结果                                               | Struct |


