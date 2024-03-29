当您调用触发器接口 [设置函数触发方式（CreateTrigger）](https://intl.cloud.tencent.com/document/product/583/18589)时，对应的 `TriggerDesc` 参数为触发器描述，您可参考本文进行使用。

## 定时触发器
该参数直接填写 Cron 表达式，相关内容请参考 [Cron 表达式](https://intl.cloud.tencent.com/document/product/583/9708)。

###  TriggerDesc 示例
每五分种触发一次
```json
0 */5 * * * * *
```


## API 网关触发器

| 名称    | 类型                          | 必选 | 描述                         |
| ------- | ----------------------------- | ---- | ---------------------------- |
| api     | [ApigwApi](#ApigwApi)         | 否   | 创建 API 网关的 API 配置     |
| service | [ApigwService](#ApigwService) | 否   | 创建 API 网关的 Service 配置 |
| release | [ApigwRelease](#ApigwRelease) | 否   | 创建 API 网关后，发布的环境  |

### ApigwApi[](id:ApigwApi)


| 名称                 | 类型                                              | 必选 | 描述                                                 |
| -------------------- | ------------------------------------------------- | ---- | ---------------------------------------------------- |
| authRequired         | String                                            | 否   | 是否需要鉴权，可选 TRUE 或者 FALSE，默认为 FALSE     |
| requestConfig        | [ApigwApiRequestConfing](#ApigwApiRequestConfing) | 否   | 请求后端 API 的配置                                  |
| isIntegratedResponse | String                                            | 否   | 是否使用集成响应，可选 TRUE 或者 FALSE，默认为 FALSE |
| IsBase64Encoded | String | 否 | 是否打开Base64编码，可选 TRUE 或者 FALSE，默认为 FALSE|

### ApigwApiRequestConfing[](id:ApigwApiRequestConfing)
| 名称   | 类型   | 必选 | 描述                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| method | String | 否   | 请求后端 API 的 method 配置，必须是 `ANY`、`GET`、`HEAD`、`POST`、`PUT`、`DELETE` 中的一种 |

### ApigwService[](id:ApigwService)

| 名称      | 类型   | 必选 | 描述                                         |
| --------- | ------ | ---- | -------------------------------------------- |
| serviceId | String | 否   | Apigw Service ID（不传入则新建一个 Service） |

### ApigwRelease[](id:ApigwRelease)

| 名称            | 类型   | 必选 | 描述                                                         |
| --------------- | ------ | ---- | ------------------------------------------------------------ |
| environmentName | String | 是   | 发布的环境，填写 `release`、`test` 或 `prepub`，不填写默认为`release` |

### TriggerDesc 示例

```json
{
  "api":{
    "authRequired":"FALSE",
    "requestConfig":{
      "method":"ANY"
    },
    "isIntegratedResponse":"FALSE"
  },
  "service":{
    "serviceName":"SCF_API_SERVICE"
  },
  "release":{
    "environmentName":"release"
  }
}
```



## Ckafka 触发器
| 名称      | 类型   | 必选 | 描述                                                       |
| --------- | ------ | ---- | ---------------------------------------------------------- |
| maxMsgNum | String | 是   | 5秒内每汇聚 maxMsgNum 条 Ckafka 消息，则触发一次函数调用   |
| offset    | String | 是   | offset 为开始消费 Ckafka 消息的位置，目前支持 `latest`、`earliest` 和`毫秒级时间戳`三种方式|
| retry     | String | 是   | 当函数报错时最大重试次数|


### TriggerDesc 示例
```json
{"maxMsgNum":100,"offset":"latest","retry":10000}
```
```json
{"maxMsgNum":999,"offset":"1595927203000","retry":10}
```

### API 请求说明
使用 API 请求创建 Ckafka 触发器时，TriggerName 字段需定义为要转储的 Ckafka instanceId，topicName 信息。<br>`[instanceId]-[topicName]`，请求示例如下：

```json
TriggerName: "ckafka-8tfxzia3-test"
```



## COS 触发器

| 名称   | 类型                    | 必选 | 描述                 |
| ------ | ----------------------- | ---- | -------------------- |
| event  | String                  | 是   | [COS 的事件类型 ](https://intl.cloud.tencent.com/document/product/583/9707)      |
| filter | [CosFilter](#CosFilter) | 是   | COS 文件名的过滤规则 |

### CosFilter[](id:CosFilter)

| 名称   | 类型   | 必选 | 描述                              |
| ------ | ------ | ---- | --------------------------------- |
| Prefix | String | 否   | 过滤文件的前缀规则                |
| Suffix | String | 否   | 过滤文件的后缀规则，必须以`.`开头 |


### COS 事件冲突规则
- 核心思想：一个事件最多触发一次函数调用。如果一个事件有其他产品绑定，该事件也不可再绑定至函数。
- 最多设置一个前缀过滤及一个后缀过滤。
- 若已设置 `cos:ObjectCreated:*` 事件，且没有设置前后缀，则后续再绑定任何以 `cos:ObjectCreated` 作为开头的事件都会失败。
- 前缀及后缀均匹配才有效，且当前缀和后缀都冲突的时候，后面的绑定会失败。

### TriggerDesc 示例
```json
{"event":"cos:ObjectCreated:*","filter":{"Prefix":"","Suffix":""}}
```
>!在 `TriggerDesc` 中作为触发器描述时，JSON 字符串须是连续且中间不能有空格的字符串。

### API 请求说明

使用 API 请求创建 COS 触发器，TriggerName 字段需定义为要转储的 COS 存储桶 XML API 访问域名，示例如下：
```json
TriggerName: "xxx.cos.ap-guangzhou.myqcloud.com"
```
>!访问域名请在对象存储控制台**存储桶列表** > **基础配置** > **基本信息**中查看。


## CMQ 触发器

| 名称   | 类型                    | 必选 | 描述                 |
| ------ | ----------------------- | ---- | -------------------- |
| filterType  | String                  | 否  |  消息过滤类型，`1`为标签类型，`2`为路由匹配类型	   |
| filterKey | String  | 否   | 当 `filterType` 为`1`时表示消息过滤标签，当 `filterType` 为`2`时表示 Binding Key |

### TriggerDesc 示例
```json
{"filterType":1,"filterKey":["test"]}
```

```json
{"filterType":2,"filterKey":["#test"]}
```

### API 请求说明

使用 API 请求创建 CMQ 触发器，TriggerName 字段需定义为 CMQ Topic，示例如下：
```json
TriggerName: "Tabortest"
```
