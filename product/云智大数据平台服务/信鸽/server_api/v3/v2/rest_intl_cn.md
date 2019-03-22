# Rest API 概述（V2）

信鸽推送提供遵从 REST 规范的 HTTP API，以供开发者远程调用信鸽提供的服务。接口主要分为四大类：

- Push API，包含多种消息推送的接口
- 标签 API， 主要完成标签的新增、删除、查询
- 账号 API，主要完成账号的查询、删除
- 工具类 API，用来定位问题和其他数据查询


 <font color=#FF0000>V2版本支持HTTP和HTTPs协议</font>


## 请求方式

支持GET;

支持POST，但要求HTTP HEADER中"Content-type"字段要设置为"application/x-www-form-urlencoded"



## 协议描述

**请求URL**：
`http://openapi.xg.qq.com/v2/class_path/method?params`

| 字段名            | 用途                 | 备注                                                         |
| :---------------- | -------------------- | :----------------------------------------------------------- |
| openapi.xg.qq.com | 接口域名             | 无                                                           |
| v2                | 版本号               | 无                                                           |
| class_path        | 提供的接口类别       | 不同的接口有不同的路径名                                     |
| method            | 功能接口名称         | 不同的功能接口有不同的名称                                   |
| params            | 调用接口时传递的参数 | 1.包括两部分：通用基础参数、接口特定参数；<br>2.所有的参数都必须为utf8编码；<br>3.params中所有K-V对的V必须进行url encode |

## 通用基础参数

通用基础参数是指，在各个接口请求URL结构中的params字段都需要包含(基础)的参数

具体如下表：

| 参数名     | 类型   | 必需 | 参数描述                                                     |
| ---------- | :----- | ---- | ------------------------------------------------------------ |
| access_id  | uint   | 是   | 应用唯一标识，可在xg.qq.com管理台查看                        |
| timestamp  | uint   | 是   | 1.unix时间戳，用于确认请求的有效期<br>2.与服务器时间（北京时间）偏差大于valid_time,请求会被拒绝 |
| valid_time | uint   | 否   | 1.配合timestamp确定请求的有效期<br>2.单位为秒<br>3.最大值为600<br>4.不传或者小于0 或者大于600 都会被设置600 |
| sign       | string | 是   | 接口鉴权，具体生成规则见<a href="#鉴权方式">鉴权方式</a>              |

## 鉴权方式

计算公式：Sign=MD5(http_methodURIK1=V1…Kn=Vnsecret_key);（注意：参数必须按照此顺序放置）

| 参数名      | 参数描述                                                     |
| :---------- | :----------------------------------------------------------- |
| http_method | 请求方法，GET或是POST                                        |
| URI         | 请求URL信息，包括IP或域名、URI的path部分<br>举例说明：<br>域名：openapi.xg.qq.com/v2/push/single_device<br>IP：10.198.18.239/v2/push/single_device<br>（注意不包括端口和请求串） |
| K1=V1…Kn=Vn | 1.将全部请求参数格式化成K=V<br>2.将格式化后的参数以K的字典序升序排列，拼接在一起<br>（注意：1.不包括sign参数， 2.V不应进行url encode） |
| secret_key  | 接口秘钥，可在【信鸽管理台】【应用配置】【应用信息】中查询   |

例如： 

单推接口调用：

POST请求 `http://openapi.xg.qq.com/v2/push/single_device`

参数列表：

access_id=123，timestamp=1386691200，Param1=Value1，Param2=Value2，secret_key=abcde，

根据上述公式得出：

sign=MD5(POSTopenapi.xg.qq.com/v2/push/single_deviceaccess_id=123Param1=Value1Param2=Value2timestamp=1386691200abcde)

得出，

sign=6b90c7f4a137c7d0b756d48f748c93b2



## 通用基础返回值

通用基础返回值，是所有请求的响应中都会包含的字段，JSON格式
```json
{ 
    "ret_code":0, 
    "err_msg":"",
    "result":{"":""} 
}
```

具体描述见下表：

| 参数名   | 类型   | 必需 | 参数描述                                     |
| -------- | :----- | ---- | -------------------------------------------- |
| ret_code | int    | 是   | <a href="#返回码一览">返回码</a>                      |
| err_msg  | string | 否   | 结果描述                                     |
| result   | JSON   | 否   | 请求正确时且有额外数据，则结果封装在该字段中 |

## API限制

1. 除去<a href="#全量推送">全量推送</a>接口有调用频率的限制外，其他均无此限制
2. 推送的消息体大小限制为4K，此限制适用于Push API中的message字段
3. <a href="#标签群推">标签群推</a>限制标签数量最多是<font color=FF0000>50</font>个




## Push API

### Push API基础参数

推送接口的基础参数是指，所有推送消息的接口的通用参数，切记接口调用参数中必须还要包含<a href="#通用基础参数">通用基础参数</a>

具体通用参数见下表：

| 参数名        | 类型   | 必需          | 默认值   | 描述                                                         |
| ------------- | :----- | ------------- | :------- | ------------------------------------------------------------ |
| message       | string | 是            | 无       | 消息体，参见<a href="#消息体格式">消息体格式</a>             |
| message_type  | uint   | 是            | 无       | iOS平台用，必须为0，不区分通知栏消息和静默消息<br>1，表示Android通知栏消息<br> 2，表示Android透传消息 |
| expire_time   | uint   | 否            | 259200（72小时）      | 消息离线存储时间（单位为秒），最长存储时间72小时<br>1.若expire_time=0，则取默认值（72小时）<br>2.若expire_time大于0且小于800，则系统会重置为800s<br>3.若expire_time>=800s，按实际设置时间存储，最长72小时<br>4.设置的最大值不得超过2147483647，否则会导致推送失败 |
| send_time     | string | 否            | 当前时间 | 1.指定推送时间,格式为yyyy-MM-DD HH:MM:SS<br>2.若小于服务器当前时间，则会立即推送<br>3.仅<a href="#全量推送">全量推送</a>和<a href="#标签群推">标签群推</a>支持此字段 |
| multi_pkg     | uint   | 否            | 0        | 多包名推送<br>0，按注册时提供的包名分发消息；<br>1，忽略包名，按access id分发消息<br>(仅Android用) |
| environment   | uint   | 是<br>(仅iOS) | 1        | 此字段描述的是App的环境<br>1，表示发布环境，对应App已经发布到AppStore<br>2，表示开发环境，对应App仍处于调试环境<br>(对于iOS，消息推送有两种情况：开发环境、发布环境) |
| loop_times    | uint   | 否            | 无       | 循环执行消息下发的次数，<br>建议取值[1, 15]                  |
| loop_interval | uint   | 否            | 无       | 循环执行消息下发的间隔，以天为单位，取值[1, 14]。loop_times和loop_interval一起表示消息下发任务的循环规则，不可超过14天 |

### 全量推送

此接口用于对全部设备推送消息，后台对本接口的调用频率有限制:

- 1小时内不能推相同内容的消息；

- 1小时内最多调用此接口30次

  

**请求URL**:

`http://openapi.xg.qq.com/v2/push/all_device?params`

**请求参数**：

<a href="#通用基础参数">通用基础参数</a>和<a href="#push-api基础参数">Push API 基础参数</a>

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>，result字段会包含给app下发的任务id:

```json
{
    "push_id":10000
}
```

如果是循环任务，返回全部任务的id

具体示例如下：

```json
{
    "push_id":10000,//父任务id
    "sub_push_ids":[234,235,236] //子任务id
}
```



### 群推送

群推送是指，根据标签、账号、设备(Token)进行群组推送

#### 标签群推

可以针对设置过标签的设备进行推送。如：性别、身份等

**请求URL**:

`http://openapi.xg.qq.com/v2/push/tags_device?params`

**请求参数**：

除了<a href="#通用基础参数">通用基础参数</a>和<a href="#push-api基础参数">Push API 基础参数</a>，还包括如下特定参数：

| 参数名    | 类型   | 必需 | 默认值 | 描述                   |
| --------- | :----- | ---- | :----- | ---------------------- |
| tags_list | JSON   | 是   | 无     | [“tag1”,”tag2”,”tag3”] <br>限制不能超过50个，否则消息将下发失败<br>若超过50个，推荐使用全量接口推送消息|
| tags_op   | string | 是   | 无     | 运算符，取值为AND或OR  |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>，result字段会包含给app下发的任务id

```json
{
    "push_id":10000
}
```

如果是循环任务，返回全部任务的id

具体示例如下：

```json
{
    "push_id":10000,//父任务id
    "sub_push_ids":[234,235,236] //子任务id
}
```



#### 帐号群推

账号群推是指，对通过客户端SDK绑定接口绑定的账号的群组推送，iOS和Android的SDK都提供相应的接口。

**请求URL**：

`http://openapi.xg.qq.com/v2/push/account_list?params `

**请求参数**：

除了<a href="#通用基础参数">通用基础参数</a> 和 <a href="#push-api基础参数">Push API 基础参数</a>，还包括如下特定参数：

| 参数名       | 类型  | 必需 | 默认值 | 描述                                                         |
| ------------ | :---- | ---- | :----- | ------------------------------------------------------------ |
| account_list | array | 是   | 无     | JSON数组格式<br>每个元素是一个account<br>单次发送account不超过100个<br>例：[“account1”,”account2”,”account3”] |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>，result字段的JSON为每个account发送返回码



#### 超大批量账号群推

如果推送目标帐号数量很大（比如>100），推荐使用此方法，分为以下两步：

(1)第一步，创建推送消息：

**请求URL**:

`http://openapi.xg.qq.com/v2/push/create_multipush?params`

**请求参数**：

<a href="#通用基础参数">通用基础参数</a> 和 <a href="#push-api基础参数">Push API 基础参数</a>

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>，其中result字段的JSON包含消息标识，举例如下：

```json
{
"push_id":100000
}
```



(2)第二步，使用超大批量推送接口进行消息推送

**请求URL**:

`http://openapi.xg.qq.com/v2/push/account_list_multiple?params`

**请求参数**：

除<a href="#通用基础参数">通用基础参数</a>外，还包括如下参数：

| 参数名       | 类型  | 必需 | 默认值 | 描述                                                         |
| ------------ | :---- | ---- | :----- | ------------------------------------------------------------ |
| account_list | array | 是   | 无     | JSON数组格式<br>每个元素是一个account<br><font color=#E53333>单次发送account不超过1000个</font> |
| push_id      | uint  | 是   | 无     | 创建推送消息接口返回的消息标识                               |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>



#### 设备群推

设备群推是指，使用设备标识(Device Token)进行消息的推送

使用此接口需要2步：

（1）第一步，创建消息

**请求URL**:

`http://openapi.xg.qq.com/v2/push/create_multipush?params`

**请求参数**：

<a href="#通用基础参数">通用基础参数</a> 和 <a href="#push-api基础参数">Push API 基础参数</a>

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>，其中result字段的JSON包含消息标识，举例如下：

```json
{
"push_id":100000
}
```



（2）第二步，调用推送接口

**请求URL**:

`http://openapi.xg.qq.com/v2/push/device_list_multiple?params`

**请求参数**：

除了<a href="#通用基础参数">通用基础参数</a> ，还包括如下特定参数：

| 参数名      | 类型  | 必需 | 默认值 | 描述                                                         |
| ----------- | :---- | ---- | :----- | ------------------------------------------------------------ |
| device_list | array | 是   | 无     | JSON数组格式<br>每个元素是一个token<br>单次发送token不超过1000个<br>例：[“token1”,”token2”,”token3”] |
| push_id     | uint  | 是   | 无     | 创建推送消息接口的返回的消息标识                             |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>



### 单推

单推，指定账号，设备标识（Device Token）进行推送



#### 账号单推

账号单推是指，对通过客户端SDK绑定接口绑定的指定单个账号的推送，iOS和Android的SDK都提供相应的接口。

**请求URL**:

`http://openapi.xg.qq.com/v2/push/single_account?params`

**请求参数**：

除了<a href="#通用基础参数">通用基础参数</a> 和 <a href="#push-api基础参数">Push API 基础参数</a>，还包括如下特定参数：

| 参数名  | 类型   | 必需 | 默认值 | 描述 |
| ------- | :----- | ---- | :----- | ---- |
| account | string | 是   | 无     | 无   |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>



#### 设备单推

设备单推是指，使用指定的一个设备标识(Device Token)进行消息的推送，关于设备标识的获取，客户端SDK有相应的接口

**请求URL**：

`http://openapi.xg.qq.com/v2/push/single_device?params`

**请求参数**：

除了<a href="#通用基础参数">通用基础参数</a> 和 <a href="#push-api基础参数">Push API 基础参数</a>，还包括如下特定参数：

|参数名 |类型 |必需 |默认值 |描述 |
| ------------- |:-------------|: -----------|:-------------|: -----------|
|device_token |string |是 |无 |设备标识 |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>

### 消息体格式

消息体，即下发到客户端的消息。

Push API对iOS和Android两个平台的消息有不同处理，需要分开来实现对应平台的推送消息，推送的消息体是JSON格式，对应PushAPI接口中的message参数。

针对不同平台，消息类型稍有不同，具体参照下表：

|  消息类型  |   支持平台   |     特性说明     |
| :--------: | :----------: | :--------------: |
| 通知栏消息 | Android，iOS |  通知栏展示消息  |
|  透传消息  |   Android    | 通知栏不展示消息 |
|  静默消息  |     iOS      | 通知栏不展示消息 |

#### Android普通消息

Android平台具体字段如下表：

| 字段名         |  类型  | 默认值 | 必需 | 参数描述                                                     |
| :------------- | :----: | :----: | :--: | ------------------------------------------------------------ |
| title          | string |   无   |  是  | 消息标题                                                     |
| content        | string |   无   |  是  | 消息内容                                                     |
| xg_media_resources          | array |   无   |  否  | 富媒体元素地址，建议小于5个  （仅限SDK4.2.0以上版本使用）                                                  |
| builder_id     |  int   |   无   |  否  | 本地通知样式标识                                             |
| n_id           |  int   |   0    |  否  | 通知消息对象的唯一标识<br><font size=0.5 color=#ff6a6a>1.大于0，会覆盖先前相同id的消息；<br>2.等于0，展示本条通知且不影响其他消息；<br>3.等于-1，将清除先前所有消息，仅展示本条消息</font> |
| ring           |  int   |   1    |  否  | 是否有铃声<br>0, 没有铃声<br>1, 有铃声                       |
| ring_raw       | string |   无   |  否  | 指定Android工程里raw目录中的铃声文件名，不需要后缀名         |
| vibrate        |  int   |   1    |  否  | 是否使用震动<br>0, 没有震动<br>1, 有震动                     |
| lights         |  int   |   1    |  否  | 是否使用呼吸灯<br>0, 使用呼吸灯<br>1, 不使用呼吸灯           |
| clearable      |  int   |   1    |  否  | 通知栏是否可清除                                             |
| icon_type      |  int   |   0    |  否  | 通知栏图标是应用内图标还是上传图标<br>0，应用内图标<br>1，上传图标 |
| icon_res       | string |   无   |  否  | 应用内图标文件名或者下载图标的url地址                        |
| style_id       |  int   |   1    |  否  | 设置是否覆盖指定编号的通知样式                               |
| small_icon     | string |   无   |  否  | 消息在状态栏显示的图标，若不设置，则显示应用图标             |
| action         |  JSON  |   有   |  否  | 设置点击通知栏之后的行为，默认为打开app                      |
| custom_content |  JSON  |   无   |  否  | 用户自定义的键值对                                           |
| accept_time    | array  |   无   |  否  | 消息将在哪些时间段允许推送给用户，建议小于10个               |

完整的消息示例如下：

```json
{
    "title ":"xxx",
    "content ":"xxxxxxxxx",
    "xg_media_resources"：“xxx”,//富媒体元素地址，例如https://www.xx.com/img/bd_logo1.png?qua=high
    "n_id":0,
    "builder_id":0,
    "ring":1,
    "ring_raw":"ring",
    "vibrate":1,
    "lights":1,
    "clearable":1,
    "icon_type":0,
    "icon_res":"xg",
    "style_id":1,
    "small_icon":"xg",
    "custom_content":{
        "key1":"value1",
        "key2":"value2"
    },
    "action":{
        "action_type":1,// 动作类型，1，打开activity或app本身；2，打开浏览器；3，打开Intent
        "activity":"MyActivityClassName"
        "aty_attr":{ // activity属性，只针对action_type=1的情况
            "if":0,  // Intent的Flag属性
            "pf":0   // PendingIntent的Flag属性
        },
        "browser":{
            "url":"http://xg.qq.com", // 仅支持http、https
            "confirm":1   // 是否需要用户确认
        },
        "intent":"xgscheme://com.xg.push/notify_detail"// 客户端 Android SDK版本需要大于等于3.2.3，然后在客户端的intent配置data标签，并设置scheme属性
    },
    "accept_time":[//在下午1点到下午2点或者是凌晨0点到上午9点之间，消息可以展示，其他时间段，消息不会展示
        {
            "start":{
                "hour":"13",
                "min":"00"
            },
            "end":{
                "hour":"14",
                "min":"00"
            }
        },
        {
            "start":{
                "hour":"00",
                "min":"00"
            },
            "end":{
                "hour":"09",
                "min":"00"
            }
        }
    ]
}

```

#### iOS 普通消息

iOS平台具体字段如下表：

| 字段名 |    类型     | 默认值 | 必需 | 参数描述                                                     |
| :----- | :---------: | :----: | :--: | ------------------------------------------------------------ |
| aps    |    JSON     |   无   |  是  | 苹果推送服务(APNs)特有的消息体字段<br>其中比较重要的键值对:<br>alert：包含标题和消息内容(必选)<br>badge_type：App显示的角标数(可选),参数设置有三种情况： <br>1) -1：角标数字不变 <br>2）-2: 角标数字自动加1 <br>3) >=0:设置显示「自定义」角标数字<br>category：下拉消息时显示的操作标识(可选)<br>详细介绍可以参照：[Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1) |
| custom | string/JSON |   无   |  否  | 自定义下发的参数                                             |
| xg     |   string    |   无   |  否  | 系统保留key，应避免使用                                      |

完整的消息示例如下：

```json
{
    "aps":{
        "alert":{
            "title":"this is a title",
            "body":"this is content"
        },
        "badge_type":1,
        "category":"CategoryID"
    },
    "custom":{
        "key":"value"
    }
}
```



#### Android透传消息

透传消息，Android平台特有，即不显示在手机通知栏中的消息，可以用来实现让用户无感知的向App下发带有控制性质的消息

Android平台具体字段如下表：

| 字段名         |  类型  | 默认值 | 是否必需 | 参数描述                                       |
| -------------- | :----: | :----: | :------: | ---------------------------------------------- |
| title          | string |   无   |    是    | 消息标题                                       |
| content        | string |   无   |    是    | 消息内容                                       |
| custom_content |  JSON  |   无   |    否    | 自定义内容                                     |
| accept_time    | array  |   无   |    否    | 消息将在哪些时间段允许推送给用户，建议小于10个 |

具体完整示例：

```json
{
    "title":"this is title",
    "content":"this is content",
    "custom_content":{
        "key1":"value1",
        "key2":"value2"
    },
    "accept_time":[//在下午1点到下午2点或者是凌晨0点到上午9点之间，消息可以展示，其他时间段，消息不会展示
        {
            "start":{
                "hour":"13",
                "min":"00"
            },
            "end":{
                "hour":"14",
                "min":"00"
            }
        },
        {
            "start":{
                "hour":"00",
                "min":"00"
            },
            "end":{
                "hour":"09",
                "min":"00"
            }
        }
    ]
}

```

#### iOS静默消息

静默消息，iOS平台特有，类似Android中的透传消息，消息不展示，当静默消息到达终端时，iOS会在后台唤醒App一段时间(小于30s)，让App来处理消息逻辑

具体字段如下表：

| 字段名 | 类型        | 默认值 | 是否必要 | 参数描述                                                     |
| ------ | ----------- | ------ | -------- | ------------------------------------------------------------ |
| aps    | JSON        | 无     | 是       | 苹果推送服务(APNs)特有的，<br>其中最重要的键值对:<br> content-available：标识消息类型(必须为1)<br>且不能包含alert、sound、badge_type字段<br>详细介绍可以参照：[Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1) |
| custom | string/JSON | 无     | 否       | 自定义下发的参数                                             |
| xg     | string      | 无     | 否       | 系统保留key，应避免使用                                      |

具体完整示例：

```json
{
    "aps":{
        "content-available":1
    },
    "custom":{
        "key1":"value1",
        "key2":"value2"
    }
}
```



### 查询消息状态（V2不可用，V3后续上线）

此接口目前仅支持全量推送和标签群推消息的发送状态的查询，不支持其他推送方式的查询

**请求URL**：

`http://openapi.xg.qq.com/v2/push/get_msg_status?params`

除了<a href="#通用基础参数">通用基础参数</a> ，还包括如下特定参数：

| 参数名     | 类型   | 必需 | 默认值 | 描述                                                         |
| ---------- | :----- | :--: | :----: | :----------------------------------------------------------- |
| push_ids   | array  |  是  |   无   | 消息唯一标识，可在管理台查看<br>JSON格式<br>举例：<br> [{"push_id": "10000"}] |
| start      | int    |  是  |   无   | 起始记录id，分页查询使用                                     |
| length     | int    |  是  |   无   | 查询记录条数                                                 |
| type       | int    |  是  |   无   | 推送消息类型：<br>1-通知栏消息<br>2-透传消息（应用内消息）   |
| push_type  | int    |  否  |   无   | 方式： 1 -WEB，2-restAPI， 3-all                             |
| task_type  | string |  否  |   无   | 推送取值范围：<br>0-所有范围（设备、账号、标签）<br>1-设备<br>2-帐号<br>3-标签 |
| platform   | int    |  否  |   无   | 平台：1-Android， 2-iOS                                      |
| start_date | string |  否  |   无   | 格式： yyyy-mm-dd                                            |
| end_date   | string |  否  |   无   | 格式： yyyy-mm-dd                                            |
| status     | int    |  否  |   无   | 0-(所有状态)<br>1-待推送<br>2-推送中<br>3-推送完成<br>4-推送失败<br>5-非法任务<br>6-其他状态 |
| message    | string |  否  |   无   | 根据消息内容进行模糊查找                                     |
| operation  | int    |  是  |   无   | 建议取值1                                                    |



**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>，其中result字段的JSON形式为：

```json
{
    "Total": "1", 
    "list": {
        "0": {
            "Content": "test", //推送消息体
            "OfflineSave": "86400", //Android 离线保存时间
            "ScheduleSendTime": "2017-04-12 17:50:00", 
            "SendTime": "2017-04-12 17:50:01", //根据算法从tobe_sent_tome、creat_time\start_time中选择
            "TagsList": "", //标签时的标签列表
            "Title": "this is title", //推送标题
            "Type": "3", //任务类型：3-全推、4-标签推送
            "cleanup": "0", //清除
            "click": "0", //点击
            "create_time": "2017-04-12 17:49:01", //任务创建时间
            "push_active": "0", //Android最近30天活跃设备
            "push_id": "2511161036", 
            "push_online": "0", //实发
            "start_time": "2017-04-12 17:50:01", //任务开始推送时间
            "status": "2", //0-待推送，1-推送中，2-推送完成，3-推送失败，4-推送任务过期，6-推送中，7-已停止，9-推送失败(频次过高)，10-推送失败(内容重复)，11-已停止，12-已停止
            "verify": "123", //展示
            "verify_svc":"0"//到达设备数量
            "cal_type": "0"
        }
    }
}

```



### 取消推送

目前V2版本支持根据消息ID来取消尚未触发的、定时的<a href="#全量推送">全量推送</a>或<a href="#标签群推">标签群推</a>的推送消息

**请求URL**：

`http://openapi.xg.qq.com/v2/push/cancel_timing_task?params`

**请求参数**：

除了<a href="#通用基础参数">通用基础参数</a> ，还包括如下特定参数：

| 参数名  | 类型   | 必需 | 默认值 | 描述                                                         |
| ------- | :----- | ---- | :----- | ------------------------------------------------------------ |
| push_id | string | 是   | 无     | 已创建的全量推送或标签群推消息的唯一标识，信鸽管理台可以查看 |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>，其中result字段的JSON形式为：

```json
{
"status": 0 //0为成功，其余为失败
}
```



##标签(Tag)接口

标签接口主要是用来对标签进行查询、设置、删除操作

V2版本支持的具体接口如下：

1. 批量新增标签
2. 批量删除标签
3. 查询全部标签
4. 查询单个设备(根据Device Token)的标签
5. 查询单个标签的设备(Device Token)总数



#### 批量新增标签
批量新增标签，可以给多定的设备(Device Token)设置标签，但是一个 App 下面最多只能有1万个标签，若超出，此接口将返回失败

**请求URL**:

`http://openapi.xg.qq.com/v2/tags/batch_set`

**请求参数**：

除了<a href="#通用基础参数">通用基础参数</a>，还包括如下特定参数：

|参数名 |类型 |必需 |默认值 |描述 |
| ------------- |:-------------|: -----------|:-------------|: -----------|
|tag_token_list |array |是 |无 |JSON字符串<br>每一个数组元素是一个tag-token对的数组<br>每次调用最多允许设置20对<br>每个tag-token对里面tag在前，token在后<br></font>示例：<br> [[”tag1”,”token1”],[”tag2”,”token2”]]<br>注意:<br>1，标签字符串长度限制在50字节以内，不可包含空格<br>2，要求token必须是符合消息接收的设备端标识 |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>



#### 批量删除标签

**请求URL**:

`http://openapi.xg.qq.com/v2/tags/batch_del`

**请求参数**：

除了<a href="#通用基础参数">通用基础参数</a>，还包括如下特定参数：

| 参数名         | 类型  | 必需 | 默认值 | 描述                                                         |
| -------------- | :---- | ---- | :----- | ------------------------------------------------------------ |
| tag_token_list | array | 是   | 无     | JSON字符串<br>每一个数组元素是一个tag-token对的数组<br>每次调用最多允许设置20对<br>每个tag-token对里面tag在前，token在后<br></font>示例：<br> [[”tag1”,”token1”],[”tag2”,”token2”]]<br>注意:<br>1，标签字符串长度限制在50字节以内，不可包含空格<br>2，要求token必须是符合消息接收的设备端标识 |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>



#### 查询全部标签

此接口用来查询当前指定应用下被设置的全部标签数量和对应的标签名

**请求URL**:

`http://openapi.xg.qq.com/v2/tags/query_app_tags?params`

**请求参数**：

除了<a href="#通用基础参数">通用基础参数</a>，还可以包括如下特定参数：

| 参数名 | 类型 | 必需 | 默认值 | 描述                          |
| ------ | :--- | ---- | :----- | ----------------------------- |
| start  | uint | 否   | 0      | 开始索引值                    |
| limit  | uint | 否   | 100    | 限制单次查询数量，建议小于200 |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>中，result字段的JSON格式如下：

```json
{
"total": 2, //指定应用的总tag数
"tags":["tag1","tag2"] //依据limit参数查询出的标签数组
}
```



#### 查询单个指定设备的标签

此接口根据设备标识(Device Token)来查询相应设备被设置的全部标签，请务必保证设备标识（Device Token）的合法性

**请求URL**:

`http://openapi.xg.qq.com/v2/tags/query_token_tags?params`

**请求参数**：

除了<a href="#通用基础参数">通用基础参数</a>，还包括如下特定参数：

| 参数名       | 类型   | 必需 | 默认值 | 描述               |
| ------------ | :----- | ---- | :----- | ------------------ |
| device_token | string | 是   | 无     | 设备接收消息的标识 |

**响应结果**：

在<a href="#通用基础返回值">用基础返回值</a>参数中，result字段的JSON格式如下：

```json
{
"tags":["tag1","tag2"]
}
```



#### 查询单个指定标签的Token总数

**请求URL**:

`http://openapi.xg.qq.com/v2/tags/query_tag_token_num?params`

**请求参数**：

除了<a href="#通用基础参数">通用基础参数</a>，还包括如下特定参数：

| 参数名 | 类型   | 必需 | 默认值 | 描述                 |
| ------ | :----- | ---- | :----- | -------------------- |
| tag    | string | 是   | 无     | 需要查询的标签字符串 |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>中，result字段的JSON格式如下：

```json
{
"device_num":100000
}
```



## 账号(Account)接口（V2不可用，请使用V3）


账号接口主要是用来查询、删除终端设备Token关联的账号

V2版本支持的具体接口如下：

1. 查询单个账号关联的设备(Device Token)
2. 删除单个账号关联的设备(Device Token)
3. 删除账号关联的全部设备(Device Token)





#### 查询单个账号关联的设备（暂不可用）

**请求URL**:

`http://openapi.xg.qq.com/v2/application/get_app_account_tokens?params`

**请求参数**：

除了<a href="#通用基础参数">通用基础参数</a>，还包括如下特定参数：

| 参数名  | 类型   | 必需 | 默认值 | 描述     |
| ------- | :----- | ---- | :----- | -------- |
| account | string | 是   | 无     | 帐号标识 |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>中，result字段的JSON格式如下：

```json
{
"tokens":["token1","token2"]
}
```



#### 删除单个账号关联的单个设备Token

**请求URL**:

`http://openapi.xg.qq.com/v2/application/del_app_account_tokens?params`

**请求参数**：

除了<a href="#通用基础参数">通用基础参数</a>，还包括如下特定参数：

|参数名 |类型 |必需 |默认值 |描述 |
| ------------- |:-------------|: -----------|:-------------|: -----------|
|account |string |是 |无 |与设备标识关联的账号 |
|device_token |string |是 |无 |设备接收消息的标识 |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>中，result字段的JSON格式如下：

```json
{
"tokens":["token1"]
}
```

注意：tokens字段对应的值表示当前账号目前仍关联的设备标识



#### 删除单个账号关联的全部设备Token

**请求URL**:

`http://openapi.xg.qq.com/v2/application/del_app_account_all_tokens?params`

除了<a href="#通用基础参数">通用基础参数</a>，还包括如下特定参数：

|参数名 |类型 |必需 |默认值 |描述 |
| ------------- |:-------------|: -----------|:-------------|: -----------|
|account |string |是 |无 |账号标识 |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>



## 工具类接口（V2不可用，V3后续上线）

### 查询应用覆盖的设备Token总数

此接口用来查询指定应用的全部已注册的设备标识(Device Token)的总数

**请求URL**:

`http://openapi.xg.qq.com/v2/application/get_app_device_num?params`

**请求参数**：

<a href="#通用基础参数">通用基础参数</a>

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>，其中result字段的JSON形式为：

```json
{
"device_num": 34567
}
```


### 查询指定设备Token的注册状态

此接口是为了查询指定设备(Device Token)在信鸽服务器上注册的状态，设备能收到信鸽推送的消息的首要条件是设备(Device Token)已经被注册到信鸽的后台，否则信鸽无法给指定设备下发消息的

**注意：**此接口仅支持Android端的token查询

**请求URL**:

`http://openapi.xg.qq.com/v2/application/get_app_token_info?params`

**请求参数**：

除了<a href="#通用基础参数">通用基础参数</a>，还包括如下特定参数：

|参数名 |类型 |必需 |默认值 |描述 |
| ------------- |:-------------|: -----------|:-------------|: -----------|
|device_token |string |是 | 无 |设备接收消息的标识 |

**响应结果**：

<a href="#通用基础返回值">用基础返回值</a>，其中result字段的JSON形式为：

```json
{
"isReg":1,//（1为token已注册，0为未注册）
"connTimestamp":1426493097, //（最新活跃时间戳）
"msgsNum":2 //（该应用的离线消息数）
}
```



## 返回码一览

信鸽REST API接口较多，开发者使用过程中不可避难会遇到各种问题，这里提供了常见的错误码释义，对应着是<a href="#通用基础返回值">用基础返回值</a>中的ret_code字段的可能值

| 值            | 含义                                   | 可采取措施                                                   |
| ------------- | -------------------------------------- | ------------------------------------------------------------ |
| 0             | 调用成功                               |                                                              |
| -1            | 参数错误                               | 检查参数配置                                                 |
| -2            | 请求时间戳不在有效期内                 | 检查timestamp和valid_time参数                                |
| -3<br>-5<br>5 | 信鸽服务器处理错误                     | 稍后重试                                                     |
| 2             | 标签绑定错误                           | 绑定标签时，Token或者是标签为空                              |
| 6             | 设备token未成功注册                    | 请检查终端设备注册是否成功                                   |
| 7             | 通用错误，账号超限                     | 删除其他未使用的账号(调用账号解绑）                          |
| 48            | 推送的账号没有绑定token                | 检查account和token是否有绑定关系                             |
| 73            | 消息体超限                             | 目前是4K字节                                                 |
| 75            | 消息体格式不符合json格式               | 检查消息体即message字段内容                                  |
| 78            | 循环任务参数错误                       | 检查loop_time
| 83            | 推送内容不合法                       | 检测文本是否含有有害信息                                       |
| 91            | 设备Token关联的tag过多                 | 清理不使用的tag                                              |
| 92            | App的关联的tag过多                     | 清理不使用的tag，限制10000                                   |
| 100           | APNs证书错误                           | 信鸽使用的推送证书格式是pem，另外，注意区分生产证书、开发证书的区别 |
| -101          | 参数错误                               | 请检查<a href="#通用基础参数">通用基础参数</a>                         |
| -102          | 请求时间戳不在有效期内                 | 检查timestamp和valid_time参数                                |
| -103          | sign 不合法                            | 检查签名生成流程，生成sign是METHOD 必须与请求时所使用的一致  |
| -104          | 内部错误                            | 稍后重试  |
| -106          | 证书过期                               | 证书过期，需重新上传证书                                                     |
