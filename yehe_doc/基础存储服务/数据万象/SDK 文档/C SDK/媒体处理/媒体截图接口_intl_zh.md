## 简介

本文档提供关于媒体截图接口的 API 概览和 SDK 示例代码。

| API                        |             操作名                     | 操作描述                                               |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
|   [GetSnapshot](https://intl.cloud.tencent.com/document/product/436/46912)     |  查询截图 |   用于查询媒体文件在某个时间的截图     |

>! 使用此接口前，请确保已打开官网控制台中数据处理下的媒体处理开关，否则会报错`media bucket unbinded, bucket's host is unavailable`。详情请参见 [开通媒体处理](https://intl.cloud.tencent.com/document/product/436/46275)。


## 查询截图(内存)

#### 功能说明

用于获取媒体文件某个时间的截图，截图信息放到内存buffer。

#### 方法原型

```cpp
cos_status_t *ci_get_snapshot_to_buffer(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        const cos_string_t *object,
                                        const ci_get_snapshot_request_t *snapshot_request,
                                        cos_table_t *headers, 
                                        cos_list_t *buffer, 
                                        cos_table_t **resp_headers);
```

#### 参数说明

| 参数名称           | 参数描述                                                     | 类型    |
| ------------------ | ------------------------------------------------------------ | ------- |
| options            | COS 请求选项                                                 | Struct  |
| bucket             | 存储桶名称，存储桶的命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String  |
| object             | Object 名称                                                  | String  |
| snapshot_request   | 获取媒体截图的请求参数                                           | Struct  |
| time               | 截图的时间点，单位为秒                                          | Float  |
| width              | 截图的宽。默认为0                                              | Int  |
| height             | 截图的高。默认为0<br/>width 和 height 都为0时表示使用视频的宽高，如果单个为0，则以另外一个值按视频宽高比例自动适应   | Int  |
| format             | 截图的格式，支持 jpg 和 png，默认 jpg                           | String  |
| rotate             | 图片旋转方式<br/><li>auto：按视频旋转信息进行自动旋转<br/><li>off：不旋转<br/>默认值为 auto   | String  |
| mode               | 截帧方式<br/><li>keyframe：截取指定时间点之前的最近的一个关键帧<br><li>exactframe：截取指定时间点的帧<br/>默认值为 exactframe   | String  |
| headers            | COS 请求附加头域                                              | Struct |
| buffer             | 返回 截图图片的内容                                            | Struct |
| resp_headers       | 返回 HTTP 响应消息的头域                                       | Struct |

#### 返回结果说明

| 返回结果   | 描述        | 类型   |
| ---------- | ----------- | ------ |
| code       | 错误码      | Int    |
| error_code | 错误码内容  | String |
| error_msg  | 错误码描述  | String |
| req_id     | 请求消息 ID | String |

#### 示例
完整代码请参见cos_demo.c中test_ci_media_process_snapshot()函数。

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// endpoint 是 COS 访问域名信息，详情请参见 https://intl.cloud.tencent.com/document/product/436/6224 文档
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
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

void test_ci_media_process_snapshot()
{
    cos_pool_t *p = NULL;
    int is_cname = 0; 
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers;
    cos_list_t download_buffer;
    cos_string_t object;
    ci_get_snapshot_request_t *snapshot_request;

    // 基本配置
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
    cos_str_set(&object, "test.mp4");

    // 替换为您的配置信息，可参见文档 https://intl.cloud.tencent.com/document/product/436/46912
    snapshot_request = ci_snapshot_request_create(p);
    snapshot_request->time = 7.5;
    snapshot_request->width = 0;
    snapshot_request->height = 0;
    cos_str_set(&snapshot_request->format, "jpg");
    cos_str_set(&snapshot_request->rotate, "auto");
    cos_str_set(&snapshot_request->mode, "exactframe");
    cos_list_init(&download_buffer);

    s = ci_get_snapshot_to_buffer(options, &bucket, &object, snapshot_request, NULL, &download_buffer, &resp_headers);
    log_status(s);

    // 销毁内存池
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

    test_ci_media_process_snapshot();

    cos_http_io_deinitialize();

    return 0;
}
```


## 查询截图(文件)

#### 功能说明

用于获取媒体文件某个时间的截图，截图信息放到本地文件中。

#### 方法原型

```cpp
cos_status_t *ci_get_snapshot_to_file(const cos_request_options_t *options,
                                      const cos_string_t *bucket, 
                                      const cos_string_t *object,
                                      const ci_get_snapshot_request_t *snapshot_request,
                                      cos_table_t *headers, 
                                      cos_string_t *filename, 
                                      cos_table_t **resp_headers);
```

#### 参数说明

| 参数名称           | 参数描述                                                     | 类型    |
| ------------------ | ------------------------------------------------------------ | ------- |
| options            | COS 请求选项                                                 | Struct  |
| bucket             | 存储桶名称，存储桶的命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String  |
| object             | Object 名称                                                  | String  |
| snapshot_request   | 获取媒体截图的请求参数                                           | Struct  |
| time               | 截图的时间点，单位为秒                                          | Float  |
| width              | 截图的宽。默认为0                                              | Int  |
| height             | 截图的高。默认为0<br/>width 和 height 都为0时表示使用视频的宽高，如果单个为0，则以另外一个值按视频宽高比例自动适应   | Int  |
| format             | 截图的格式，支持 jpg 和 png，默认 jpg                           | String  |
| rotate             | 图片旋转方式<br/><li>auto：按视频旋转信息进行自动旋转<br/><li>off：不旋转<br/>默认值为 auto   | String  |
| mode               | 截帧方式<br/><li>keyframe：截取指定时间点之前的最近的一个关键帧<br><li>exactframe：截取指定时间点的帧<br/>默认值为 exactframe   | String  |
| headers            | COS 请求附加头域                                              | Struct |
| filename           | 存放截图信息的文件名                                           | String |
| resp_headers       | 返回 HTTP 响应消息的头域                                       | Struct |

#### 返回结果说明

| 返回结果   | 描述        | 类型   |
| ---------- | ----------- | ------ |
| code       | 错误码      | Int    |
| error_code | 错误码内容  | String |
| error_msg  | 错误码描述  | String |
| req_id     | 请求消息 ID | String |

#### 示例
完整代码请参见cos_demo.c中test_ci_media_process_snapshot()函数。

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"
#include <sys/stat.h>

// endpoint 是 COS 访问域名信息，详情请参见 https://intl.cloud.tencent.com/document/product/436/6224 文档
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
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

void test_ci_media_process_snapshot()
{
    cos_pool_t *p = NULL;
    int is_cname = 0; 
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers;
    cos_string_t object;
    ci_get_snapshot_request_t *snapshot_request;
    cos_string_t pic_file = cos_string("snapshot.jpg");

    // 基本配置
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
    cos_str_set(&object, "test.mp4");

    // 替换为您的配置信息，可参见文档 https://intl.cloud.tencent.com/document/product/436/46912
    snapshot_request = ci_snapshot_request_create(p);
    snapshot_request->time = 7.5;
    snapshot_request->width = 0;
    snapshot_request->height = 0;
    cos_str_set(&snapshot_request->format, "jpg");
    cos_str_set(&snapshot_request->rotate, "auto");
    cos_str_set(&snapshot_request->mode, "exactframe");

    s = ci_get_snapshot_to_file(options, &bucket, &object, snapshot_request, NULL, &pic_file, &resp_headers);
    log_status(s);

    // 销毁内存池
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

    test_ci_media_process_snapshot();

    cos_http_io_deinitialize();

    return 0;
}
```