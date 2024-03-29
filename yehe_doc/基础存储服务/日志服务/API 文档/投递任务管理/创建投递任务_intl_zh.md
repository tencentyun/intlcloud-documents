## 功能描述

本接口用于创建新的投递任务，如果使用此接口，需要自行处理 CLS 对指定 Bucket 的写权限。

## 请求

#### 请求示例

```plaintext
POST /shipper HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
  "topic_id": "xxxx-xx-xx-xx-xxxxxxxx",
  "bucket": "test-1250000001",
  "prefix": "test",
  "shipper_name": "myname",
  "interval": 300,
  "max_size": 100,
  "partition": "%Y%m%d",
  "compress": {
    "format": "none"
  },
  "content": {
    "format": "csv",
    "csv_info": {
      "print_key": true,
      "keys": ["key1", "key2"],
      "delimiter": "|",
      "escape_char": "'",
      "non_existing_field": "null"
    }
  }
}
```

#### 请求行

```
POST /shipper
```

#### 请求头

除公共头部外，无特殊请求头部。

#### 请求参数

| 字段名       | 类型   | 位置 | 是否必须 | 含义                                                         |
| ------------ | ------ | ---- | -------- | ------------------------------------------------------------ |
| topic_id     | string | body | 是       | 创建的 Shipper 属于的 topic ID                               |
| bucket       | string | body | 是       | 创建的 Shipper 投递的 bucket，格式：{bucketName}-{appid}     |
| prefix       | string | body | 是       | 创建的 Shipper 投递目录的前缀                                |
| shipper_name | string | body | 是       | 投递规则的名字                                               |
| interval     | int    | body | 否       | 投递的时间间隔，单位：秒，默认300，取值范围为：[300，360，420，480，540，600，660，720，780，840，900]（即整数分钟级别数值） |
| max_size     | int    | body | 否       | 投递的文件的最大值，单位：MB，默认100，范围100 - 256         |
| partition    | string | body | 否       | 投递日志的分区规则，支持`strftime`的时间格式表示             |
| compress     | object | body | 否       | 投递日志的压缩配置                                           |
| content      | object | body | 否       | 投递日志的内容格式配置                                       |

compress 格式如下：

| 字段名 | 类型   | 是否必须 | 含义                                       |
| ------ | ------ | -------- | ------------------------------------------ |
| format | string | 是       | 压缩格式，支持`gzip`、`lzop`和`none`不压缩 |

content 格式如下：

| 字段名   | 类型   | 是否必须 | 含义                        |
| -------- | ------ | -------- | --------------------------- |
| format   | string | 是       | 内容格式，支持`json`、`csv` |
| csv_info | object | 否       | 内容格式为`csv`时设置       |

csv_info 格式如下：

| 字段名             | 类型          | 是否必须 | 含义                                             |
| ------------------ | ------------- | -------- | ------------------------------------------------ |
| print_key          | bool          | 是       | csv 首行是否打印 key                             |
| keys               | array(string) | 是       | 每列 key 的名字                                  |
| delimiter          | string        | 是       | 各字段间的分隔符                                 |
| escape_char        | string        | 是       | 若字段内容中包含分隔符，则使用该转义符包裹改字段 |
| non_existing_field | string        | 是       | 对于上面指定的不存在字段使用该内容填充           |

## 响应

#### 响应示例

```plaintext
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
{
 "shipper_id": "xxxx-xx-xx-xx-xxxxxxxx",
}
```

#### 响应头

除公共响应头部外，无特殊响应头部。

#### 响应参数

| 字段名     | 类型   | 是否必须 | 含义              |
| ---------- | ------ | -------- | ----------------- |
| shipper_id | string | 是       | 新创建的投递的 ID |

## 错误码

参见 [错误码](https://intl.cloud.tencent.com/document/product/614/12402)。
