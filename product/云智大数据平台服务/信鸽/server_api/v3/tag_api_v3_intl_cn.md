## Tag API v3

### Tag API 概述

- Tag API 是所有tag接口的统称
- Tag API 有多种设置、更新、删除接口，具体的接口如下：
  - 增加单个tag
  - 删除单个tag
  - 增加多个tag
  - 删除多个tag
  - 删除所有tag
  - 更新tag
  - 多个token设置tag
  - 多个token删除tag
  - 批量设置标签
  - 批量删除标签
- 所有推送目标都采用相同的 URL 发起请求，URL：`https://openapi.xg.qq.com/v3/device/tag`
- 所有请求参数通过 JSON 封装上传给后台，后台通过请求参数区分不同的推送目标
  ​

### Tag API 调用地址

```text
https://openapi.xg.qq.com/v3/device/tag
```



### Tag API 请求参数

| 参数名            | 类型      | 是否必需 | 参数说明                                     |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type  | int     | 是    | 操作类型<br>1）1：增加单个tag，对单个token而言 <br>2）2：删除单个tag，对单个token而言 <br>3）3：增加多个tag，对单个token而言 <br>4）4：删除多个tag，对单个token而言 <br> 5）5：删除所有标签，对单个token而言 <br>6）6：标签覆盖接口（支持多个标签），对单个token而言 <br>7）7：添加单个tag，对多个token而言 <br>8）8：删除单个tag，对多个token而言 <br>9）9：批量添加标签（每次调用最多允许设置20对，每个对里面标签在前，token在后）<br>10）10：批量删除标签（每次调用最多允许设置20对，每个对里面标签在前，token在后） |
| platform       | string  | 是    | 客户端平台类型<br>1）android：安卓 <br>2）ios：苹果               |
| token_list     | array   | 否    | 设备列表<br>1）operator_type =1,2,3,4,5,6,7,8时必填 <br>2）operator_type =1,2,3,4,5,6时如果该参数包含多个token只会设置第一个token <br>3）格式eg：["token1","token2"]  <br>4）列表最大不能超过20个值  <br>5）token字符串长度不能超过64 |
| tag_list       | array   | 否    | 标签列表<br>1）operator_type =1,2,3,4,6,7,8时必填，=5时忽略<br>2）operator_type =1,2,3,4,6,7,8时如果该参数包含多个tag时，如果只是对单个tag操作，则只会设置第一个tag<br>3）格式eg：["tag1","tag2"]<br>4）列表最大不能超过20个值<br>5）tag字符串长度不能超过50 |
| tag_token_list | array   | 否    | 标签、设备对应列表<br>1）operator_type =9,10时必填 <br>2）格式eg： [["tag1","token1"],["tag2","token2"]]<br>3）每个对里面标签在前，token在后 <br>4）列表最大不能超过20个值 <br>5）tag字符串长度不能超过50<br>6）token字符串长度不能超过64 |
| seq            | int64_t | 否    | 接口调用时，在应答包中信鸽会回射该字段,可用于异步请求<br>使用场景：异步服务中可以通过该字段找到server端返回的对应应答包           |
| op_type        | string  | 否    | 接口操作人员类型：qq、rtx、email、other              |
| op_id          | string  | 否    | 接口操作人员类型：接口操作人员id（ qq\rtx\email）         |

Tag API 实际例子 

- 增加单个tag1，对单个token1

  ```json
  {   
    "operator_type": 1,
    "platform": "android",
    "tag_list": ["tag1"],
    "token_list": ["token1"]
   }
  ```

- 删除单个tag1，对单个token1

  ```json
  {   
    "operator_type": 2,
    "platform": "android",
    "tag_list": ["tag1"],
    "token_list": ["token1"]
   }
  ```

- 增加多个tag1,tag2，对单个token1

  ```json
  {   
    "operator_type": 3,
    "platform": "android",
    "tag_list": ["tag1","tag2"],
    "token_list": ["token1"]
   }
  ```

- 删除多个tag1,tag2，对单个token1

  ```json
  {   
    "operator_type": 4,
    "platform": "android",
    "tag_list": ["tag1","tag2"],
    "token_list": ["token1"]
   }
  ```

- 删除所有标签，对单个token1

  ```json
  {   
    "operator_type": 5,
    "platform": "android",
    "tag_list": ["tag1","tag2"],
    "token_list": ["token1"]
   }
  ```

- 标签覆盖tag1,tag2，对单个token1

  ```json
  {   
    "operator_type": 6,
    "platform": "android",
    "tag_list": ["tag1","tag2"],
    "token_list": ["token1"]
   }
  ```


- 为多个token1,token2添加单个tag1

  ```json
  {   
    "operator_type": 7,
    "platform": "android",
    "tag_list": ["tag1"],
    "token_list": ["token1","token2"]
  }
  ```

- 多个token1,token2删除单个tag1

  ```json
  {   
    "operator_type": 8,
    "platform": "android",
    "tag_list": ["tag1"],
    "token_list": ["token1","token2"]
  }
  ```

- 批量设置标签,为[tag1,token1],[tag2,token2]设置标签

  ```json
  {   
    "operator_type": 9,
    "platform": "android",
    "tag_token_list":  [["tag1","token1"],["tag2","token2"]]
 
  }
  ```

- 批量删除标签,为[tag1,token1],[tag2,token2]删除标签

  ```json
  {   
    "operator_type": 10,
    "platform": "android",
    "tag_token_list":  [["tag1","token1"],["tag2","token2"]]
  }
  ```

### Tag API应答参数 

| 字段名      | 类型      | 是否必填 | 注释                                       |
| -------- | ------- | ---- | ---------------------------------------- |
| seq      | int64_t | 是    | 与请求包一致（如果请求包是非法json该字段为0）                |
| ret_code | int32_t | 是    | 错误码，详细参照错误码对照表                           |
| err_msg  | string  | 否    | 请求出错时的错误信息                               |
| result   | string  | 否    | 请求正确时，若有额外数据要返回，则结果封装在该字段的json中，若无额外数据，则可能无此字段 |



### Tag API请求完整示例

#### 标签设置请求消息

```json
POST /v3/device/tag HTTP/1.1
Host: openapi.xg.qq.com
Content-Type: application/json
Authorization: Basic YTViNWYwNzFmZjc3YTplYTUxMmViNzcwNGQ1ZmI1YTZhOTM3Y2FmYTcwZTc3MQ==
Cache-Control: no-cache
Postman-Token: 4b82a159-afdd-4f5c-b459-de978d845d2f
{
  "operator_type": 1,
  "platform": "android",
  "tag_list": ["tag1"],
  "token_list": ["token1"]
}
```

#### 标签设置应答消息

```
{
    "seq": 0,
    "ret_code": 0,
}
```



## 错误码

开发者使用过程中不可避难会遇到各种问题，这里提供了常见的错误码释义

| 错误码   | 含义                   |
| ----- | -------------------- |
| 0     | 正常                   |
| 10000 | 未知异常                 |
| 10001 | 超时失败,请重试！            |
| 10102 | 缺少参数，请检查后重试！         |
| 10103 | 参数值非法，请检查后重试！        |
| 10104 | 鉴权未通过，请检查secret key！ |
| 11001 | 内部错误，请稍候重试！          |
| 11002 | 内部错误，请稍候重试！          |
| 11003 | 内部错误，请稍候重试！          |
| 11004 | 内部错误，请稍候重试！          |
| 11005 | 内部错误，请稍候重试！          |
| 11006 | 内部错误，请稍候重试！          |
| 11007 | 内部错误，请稍候重试！          |
| 10113 | 内部错误，请稍候重试！          |