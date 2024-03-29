

## 简介

本文档提供关于清单的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                 |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | 设置清单任务 | 设置存储桶的清单任务     |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | 查询清单任务 | 查询存储桶的清单任务     |
| [List Bucket Inventory Configurations](https://intl.cloud.tencent.com/document/product/436/30627) | 查询所有清单 | 查询存储桶的所有清单任务 |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | 删除清单任务 | 删除存储桶的清单任务     |

## 设置清单任务

#### 功能说明

PUT Bucket inventory 用于在存储桶中创建清单任务。

#### 方法原型

```c
cos_status_t *cos_put_bucket_inventory(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_inventory_params_t *inventory_params,
                                      cos_table_t **resp_headers
```

#### 请求示例

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// endpoint 是 COS 访问域名信息，详情请参见 https://cloud.tencent.com/document/product/436/6224 文档
static char TEST_COS_ENDPOINT[] = "cos.ap-guangzhou.myqcloud.com";
// 开发者拥有的项目身份ID/密钥，可在 https://console.cloud.tencent.com/cam/capi 页面获取
static char *TEST_ACCESS_KEY_ID;                //your secret_id
static char *TEST_ACCESS_KEY_SECRET;            //your secret_key
// 开发者访问 COS 服务时拥有的用户维度唯一资源标识，用以标识资源，可在 https://console.cloud.tencent.com/cam/capi 页面获取
static char TEST_APPID[] = "<APPID>";    //your appid
// 地域信息，枚举值可参见 https://cloud.tencent.com/document/product/436/6224 文档，例如：ap-beijing、ap-hongkong、eu-frankfurt 等
static char TEST_REGION[] = "ap-guangzhou";    //region in endpoint
// 对象拥有者，例如用户UIN：100000000001
static char TEST_UIN[] = "<Uin>";    //your uin
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

void test_put_bucket_inventory()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    int inum = 3, i, len;
    char buf[inum][32];
    char dest_bucket[128];
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;
    
    //创建内存池
    cos_pool_create(&pool, NULL);
    
    //初始化请求选项
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    
    // put bucket inventory 
    len = snprintf(dest_bucket, 128, "qcs::cos:%s::%s", TEST_REGION, TEST_BUCKET_NAME);
    dest_bucket[len] = 0;
    // 设置多个清单
    for (i = 0; i < inum; i++) {
        cos_inventory_params_t *params = cos_create_inventory_params(pool);
        cos_inventory_optional_t *optional;
        len = snprintf(buf[i], 32, "id%d", i);
        buf[i][len] = 0;
        cos_str_set(&params->id, buf[i]);
        cos_str_set(&params->is_enabled, "true");
        cos_str_set(&params->frequency, "Daily");
        cos_str_set(&params->filter_prefix, "myPrefix");
        cos_str_set(&params->included_object_versions, "All");
        cos_str_set(&params->destination.format, "CSV");
        cos_str_set(&params->destination.account_id, TEST_UIN);
        cos_str_set(&params->destination.bucket, dest_bucket);
        cos_str_set(&params->destination.prefix, "invent");
        params->destination.encryption = 1;
        optional = cos_create_inventory_optional(pool);
        cos_str_set(&optional->field, "Size");
        cos_list_add_tail(&optional->node, &params->fields);
        optional = cos_create_inventory_optional(pool);
        cos_str_set(&optional->field, "LastModifiedDate");
        cos_list_add_tail(&optional->node, &params->fields);
        optional = cos_create_inventory_optional(pool);
        cos_str_set(&optional->field, "ETag");
        cos_list_add_tail(&optional->node, &params->fields);
        optional = cos_create_inventory_optional(pool);
        cos_str_set(&optional->field, "StorageClass");
        cos_list_add_tail(&optional->node, &params->fields);
        optional = cos_create_inventory_optional(pool);
        cos_str_set(&optional->field, "ReplicationStatus");
        cos_list_add_tail(&optional->node, &params->fields);
    
        // 设置存储桶清单
        status = cos_put_bucket_inventory(options, &bucket, params, &resp_headers);
        log_status(status);
    }

    // 销毁内存池
    cos_pool_destroy(pool);
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

    test_put_bucket_inventory();

    cos_http_io_deinitialize();

    return 0;
}
```

#### 参数说明

| 参数名称                 | 描述                                                         | 类型   |
| ------------------------ | ------------------------------------------------------------ | ------ |
| options                  | COS 请求选项                                                 | Struct |
| bucket                   | 设置清单任务的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| inventory_params         | 存储桶清单配置信息                                           | Struct |
| node                     | 用于list inventory接口链接清单配置                           | List   |
| id                       | 清单的名称，与请求参数中的 id 对应                           | String |
| is_enabled               | 清单是否启用的标识： <br><li>如果设置为 true，清单功能将生效 <br><li>如果设置为 false，将不生成任何清单 | Struct |
| frequency                | 清单任务周期，可选项为按日或者按周，枚举值：Daily、Weekly    | String |
| filter_prefix            | 需要分析的对象的前缀                                         | String |
| included_object_versions | 是否在清单中包含对象版本：<br><li>  如果设置为 All，清单中将会包含所有对象版本，并在清单中增加 VersionId，IsLatest，DeleteMarker 这几个字段<br><li>  如果设置为 Current，则清单中不包含对象版本信息 | String |
| destination              | 描述存放清单结果的信息                                       | Struct |
| format                   | 清单分析结果的文件形式，可选项为 CSV 格式                    | String |
| account_id               | 存储桶的所有者 ID，例如100000000001                          | String |
| bucket                   | 清单分析结果的存储桶名                                       | String |
| prefix                   | 清单分析结果的前缀                                           | String |
| encryption               | 为清单结果提供服务端加密的选项                               | Int    |
| fields                   | 设置清单结果中应包含的分析项目                               | Struct |
| field                    | 清单结果中可选包含的分析项目名称，可选字段包括：Size，LastModifiedDate，StorageClass，ETag，IsMultipartUploaded，ReplicationStatus | String |
| resp_headers             | 返回 HTTP 响应消息的头域                                     | Struct |

#### 返回结果说明

| 返回结果   | 描述        | 类型   |
| :--------- | :---------- | :----- |
| code       | 错误码      | Int    |
| error_code | 错误码内容  | String |
| error_msg  | 错误码描述  | String |
| req_id     | 请求消息 ID | String |

#### 错误码说明

该请求可能会发生的一些常见的特殊错误如下：

| 错误码                | 描述                                         | 状态码               |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument       | 不合法的参数值                               | HTTP 400 Bad Request |
| TooManyConfigurations | 清单数量已经达到1000条的上限                 | HTTP 400 Bad Request |
| AccessDenied          | 未授权的访问。您可能不具备访问该存储桶的权限 | HTTP 403 Forbidden   |

## 查询清单任务

#### 功能说明

GET Bucket inventory 用于查询存储桶中用户的清单任务信息。

#### 方法原型

```c
cos_status_t *cos_get_bucket_inventory(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_inventory_params_t *inventory_params,
                                      cos_table_t **resp_headers);
```

#### 请求示例

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// endpoint 是 COS 访问域名信息，详情请参见 https://cloud.tencent.com/document/product/436/6224 文档
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

void test_get_bucket_inventory()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    int inum = 3;
    char buf[inum][32];
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;
    cos_inventory_params_t *get_params = NULL;
    cos_inventory_optional_t *optional = NULL;
    
    //创建内存池
    cos_pool_create(&pool, NULL);
    
    //初始化请求选项
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    
    // get inventory 
    get_params = cos_create_inventory_params(pool);
    cos_str_set(&get_params->id, buf[inum/2]);
    status = cos_get_bucket_inventory(options, &bucket, get_params, &resp_headers);
    log_status(status); 

    printf("id: %s\nis_enabled: %s\nfrequency: %s\nfilter_prefix: %s\nincluded_object_versions: %s\n", 
            get_params->id.data, get_params->is_enabled.data, get_params->frequency.data, get_params->filter_prefix.data, get_params->included_object_versions.data);
    printf("destination:\n");
    printf("\tencryption: %d\n", get_params->destination.encryption);
    printf("\tformat: %s\n", get_params->destination.format.data);
    printf("\taccount_id: %s\n", get_params->destination.account_id.data);
    printf("\tbucket: %s\n", get_params->destination.bucket.data);
    printf("\tprefix: %s\n", get_params->destination.prefix.data);
    cos_list_for_each_entry(cos_inventory_optional_t, optional, &get_params->fields, node) {
        printf("field: %s\n", optional->field.data);
    }

    // 销毁内存池
    cos_pool_destroy(pool);
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

    test_get_bucket_inventory();

    cos_http_io_deinitialize();

    return 0;
}
```

#### 参数说明

| 参数名称                 | 描述                                                         | 类型   |
| ------------------------ | ------------------------------------------------------------ | ------ |
| options                  | COS 请求选项                                                 | Struct |
| bucket                   | 查询清单任务的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| inventory_params         | 用于 list inventory 接口链接清单配置                         | Struct |
| node                     | 链接清单配置                                                 | List   |
| id                       | 清单的名称，与请求参数中的 id 对应                           | String |
| is_enabled               | 清单是否启用的标识： <br><li>如果设置为 true，清单功能将生效 <br><li>如果设置为 false，将不生成任何清单 | Struct |
| frequency                | 清单任务周期，可选项为按日或者按周，枚举值：Daily、Weekly    | String |
| filter_prefix            | 需要分析的对象的前缀                                         | String |
| included_object_versions | 是否在清单中包含对象版本：<br><li> 如果设置为 All，清单中将会包含所有对象版本，并在清单中增加 VersionId，IsLatest，DeleteMarker 这几个字段<br><li>  如果设置为 Current，则清单中不包含对象版本信息 | String |
| destination              | 描述存放清单结果的信息                                       | Struct |
| format                   | 清单分析结果的文件形式，可选项为 CSV 格式                    | String |
| account_id               | 存储桶的所有者 ID，例如100000000001                          | String |
| bucket                   | 清单分析结果的存储桶名                                       | String |
| prefix                   | 清单分析结果的前缀                                           | String |
| encryption               | 为清单结果提供服务端加密的选项                               | Int    |
| fields                   | 设置清单结果中应包含的分析项目                               | Struct |
| field                    | 清单结果中可选包含的分析项目名称，可选字段包括：Size，LastModifiedDate，StorageClass，ETag，IsMultipartUploaded，ReplicationStatus | String |
| resp_headers             | 返回 HTTP 响应消息的头域                                     | Struct |

#### 返回结果说明

| 返回结果   | 描述        | 类型   |
| :--------- | :---------- | :----- |
| code       | 错误码      | Int    |
| error_code | 错误码内容  | String |
| error_msg  | 错误码描述  | String |
| req_id     | 请求消息 ID | String |

## 查询所有清单

#### 功能说明

List Bucket Inventory Configurations 用于请求返回一个存储桶中的所有清单任务。每一个存储桶中最多配置1000条清单任务。

#### 方法原型

```c
cos_status_t *cos_list_bucket_inventory(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      cos_list_inventory_params_t *inventory_params,
                                      cos_table_t **resp_headers);
```

#### 请求示例

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// endpoint 是 COS 访问域名信息，详情请参见 https://cloud.tencent.com/document/product/436/6224 文档
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

void test_list_bucket_inventory()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;
    cos_inventory_params_t *get_params = NULL;
    cos_inventory_optional_t *optional = NULL;
    cos_list_inventory_params_t *list_params = NULL;
    
    //创建内存池
    cos_pool_create(&pool, NULL);
    
    //初始化请求选项
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    
    // list inventory
    list_params = cos_create_list_inventory_params(pool); 
    status = cos_list_bucket_inventory(options, &bucket, list_params, &resp_headers);
    log_status(status);

    // 查看结果
    get_params = NULL;
    cos_list_for_each_entry(cos_inventory_params_t, get_params, &list_params->inventorys, node) {
        printf("id: %s\nis_enabled: %s\nfrequency: %s\nfilter_prefix: %s\nincluded_object_versions: %s\n",  get_params->id.data, get_params->is_enabled.data, get_params->frequency.data, get_params->filter_prefix.data, get_params->included_object_versions.data);
        printf("destination:\n");
        printf("\tencryption: %d\n", get_params->destination.encryption);
        printf("\tformat: %s\n", get_params->destination.format.data);
        printf("\taccount_id: %s\n", get_params->destination.account_id.data);
        printf("\tbucket: %s\n", get_params->destination.bucket.data);
        printf("\tprefix: %s\n", get_params->destination.prefix.data);
        cos_list_for_each_entry(cos_inventory_optional_t, optional, &get_params->fields, node) {
            printf("field: %s\n", optional->field.data);
        }
    }

    // 销毁内存池
    cos_pool_destroy(pool);
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

    test_list_bucket_inventory();

    cos_http_io_deinitialize();

    return 0;
}
```

#### 参数说明

| 参数名称                | 描述                                                         | 类型   |
| ----------------------- | ------------------------------------------------------------ | ------ |
| options                 | COS 请求选项                                                 | Struct |
| bucket                  | 存放清单的目标存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| inventory_params        | 存储桶所有清单配置信息                                       | Struct |
| inventorys              | 链接 cos_inventory_params_t 的 node 成员                     | List   |
| is_truncated            | 是否已列出所有清单任务信息的标识。如果已经展示完则为 false，否则为 true | Struct |
| continuation_token      | 当页清单列表的标识，可理解为页数。该标识与请求中的 continuation-token 参数对应 | String |
| next_continuation_token | 下一页清单列表的标识。如果该参数中有值，则可将该值作为 continuation-token 参数并发起 GET 请求以获取下一页清单任务信息 | String |
| resp_headers            | 返回 HTTP 响应消息的头域                                     | Struct |

#### 返回结果说明

| 返回结果   | 描述        | 类型   |
| :--------- | :---------- | :----- |
| code       | 错误码      | Int    |
| error_code | 错误码内容  | String |
| error_msg  | 错误码描述  | String |
| req_id     | 请求消息 ID | String |

## 删除清单任务

#### 功能说明

DELETE Bucket inventory 用于删除存储桶中指定的清单任务。

#### 方法原型

```c
cos_status_t *cos_delete_bucket_inventory(const cos_request_options_t *options,
                                      const cos_string_t *bucket,
                                      const cos_string_t *id,
                                      cos_table_t **resp_headers);
```

#### 请求示例

```cpp
#include "cos_http_io.h"
#include "cos_api.h"
#include "cos_log.h"

// endpoint 是 COS 访问域名信息，详情请参见 https://cloud.tencent.com/document/product/436/6224 文档
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

void test_delete_bucket_inventory()
{
    cos_pool_t *pool = NULL;
    int is_cname = 0;
    cos_status_t *status = NULL;
    cos_request_options_t *options = NULL;
    cos_table_t *resp_headers = NULL;
    cos_string_t bucket;
    int inum = 3, i;
    char buf[inum][32];
    
    //创建内存池
    cos_pool_create(&pool, NULL);
    
    //初始化请求选项
    options = cos_request_options_create(pool);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    
    // delete inventory
    for (i = 0; i < inum; i++) {
        cos_string_t id;
        cos_str_set(&id, buf[i]);
        status = cos_delete_bucket_inventory(options, &bucket, &id, &resp_headers);
        log_status(status);
    }

    // 销毁内存池
    cos_pool_destroy(pool);
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

    test_delete_bucket_inventory();

    cos_http_io_deinitialize();

    return 0;
}
```

#### 参数说明

| 参数名称     | 描述                                                         | 类型   |
| ------------ | ------------------------------------------------------------ | ------ |
| options      | COS 请求选项                                                 | Struct |
| bucket       | 被删除清单任务的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| id           | 清单的名称                                                   | String |
| resp_headers | 返回 HTTP 响应消息的头域                                     | Struct |

#### 返回结果说明

| 返回结果   | 描述        | 类型   |
| :--------- | :---------- | :----- |
| code       | 错误码      | Int    |
| error_code | 错误码内容  | String |
| error_msg  | 错误码描述  | String |
| req_id     | 请求消息 ID | String |
