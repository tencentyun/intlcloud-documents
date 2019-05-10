# Push API v3

## Push API 概述

- Push API 是所有推送接口的统称

- Push API 有多种推送目标，推送目标如下：
  - 全量推送
  - 标签推送
  - 单设备推送
  - 设备列表推送
  - 单账号推送
  - 账号列表推送

- 所有推送目标都采用相同的 URL 发起请求，URL：`https://openapi.xg.qq.com/v3/push/app`

- 所有请求参数通过 JSON 封装上传给后台，后台通过请求参数区分不同的推送目标

  ​

## 调用地址

```text
https://openapi.xg.qq.com/v3/push/app
```



## Push API 必要参数

推送必要参数指一条推送消息必需携带的参数

| 参数名           | 类型     | 是否必需 | 描述                                       |
| ------------- | ------ | ---- | ---------------------------------------- |
| audience_type | string | 是    | 推送目标<br>1）all：全量推送<br>2）tag：标签推送<br>3）token：单设备推送<br>4）token_list：设备列表推送<br>5）account：单账号推送<br>6）account_list：账号列表推送 |
| platform      | string | 是    | 客户端平台类型<br>1）android：安卓<br>2）ios：苹果<br>3）all：安卓&&苹果，仅支持全量推送和标签推送（预留参数，暂不可用） |
| message       | object | 是    | 消息体，参见<a href="#message：消息体">消息体</a> |
| message_type  | string | 是    | 消息类型<br>1）notify：通知<br>2）message：透传消息/静默消息 |



### audience_type：推送目标

推送目标，表示一条推送可以被推送到哪些设备

Push API 提供了多种推送目标的，比如：全量、标签、单设备、设备列表、单账号、账号列表

| 推送目标         | 描述     | 必需参数及使用说明                                |
| ------------ | ------ | ---------------------------------------- |
| all          | 全量推送   | 无                                        |
| tag          | 标签推送   | `tag_list`<br>1）推送 tag1 和 tag2 的设备<br>{“tags”:[“tag1”,”tag2”],”op”:”AND”}<br>2）推送 tag1 或 tag 的设备<br>{“tags”:[“tag1”,“tag2”],”op”:“OR”}<br>3) 标签列表不能超过512个字符|
| token        | 单设备推送  | `token_list`<br>1）如果该参数包含多个token 只会推送第一个token<br>2）格式eg：[“token1”]<br>3）token字符串长度不能超过64 |
| token_list   | 设备列表群推 | `token_list`<br>1）最多1000 个token<br>2）格式eg：[“token1”,”token2”]<br>3）token字符串长度不能超过64<br>`push_id`<br>1）第一次推送该值填0，系统会创建对应的推送任务，并且返回pushid：123<br>2）后续推送push_id 填123(同一个文案）表示使用与123 id 对应的文案进行推送 |
| account      | 单账号推送  | `account_list`<br>1）该参数有多个账号时，仅推送第一个账号<br>2）格式eg：[“account1”] |
| account_list | 账号列表群推 | `account_list`<br>1）最多1000 个account2. 格式eg：[“account1”,”account2”]<br>`push_id`<br>1）第一次推送该值填0，系统会创建对应的推送任务，并且返回pushid：123<br>2）后续推送push_id 填123(同一个文案）表示使用与123 id 对应的文案进行推送 |

- 全量推送：推送给全部设备

  ```json
  {
    "audience_type": "all"
  }
  ```

- 标签推送：推送给同时设置了"tag1"和”tag2“标签的设备

  ```json
  {
    "audience_type": "tag",
    "tag_list": {
        "tags": [
            "tag1",
            "tag2"
        ],
        "op": "AND"
    }
  }
  ```

- 单设备推送：推送给token为"token1"的设备

  ```json
  {
    "audience_type": "token",
    "token_list": [
        "token1"
    ]
  }
  ```

- 设备列表推送，推送给token为"token1"和"token2"的设备

  ```json
  {
    "audience_type": "token_list",
    "token_list": [
        "token1",
        "token2"
    ],
    "push_id": "0"
  }
  ```

- 单账号推送：推送给账号为"account1"的设备

  ```json
  {
    "audience_type": "account",
    "account_list": [
        "account1"
    ]
  }
  ```

- 账号列表推送：推送账号为"account1"和"account2"的设备

  ```json
  {
    "audience_type": "account_list",
    "account_list": [
        "account1",
        "account2"
    ],
    "push_id": "0"
  }
  ```



### platform：推送平台

当前支持 Android、iOS 两个平台的推送

其关键字分别为："android", "ios"，如果要同时推送两个平台，则关键字为："all"

- 推送到所有平台：

  ```json
  {
    "platform": "all"
  }
  ```

- 推送到安卓平台：

  ```json
  {
    "platform": "android"
  }
  ```

- 推送到iOS平台：

  ```json
  {
    "platform": "ios"
  }
  ```



### message_type：消息体类型

针对不同平台，消息类型稍有不同，具体参照下表：

| 消息类型    | 描述        | 支持平台                       | 特性说明     |
| ------- | --------- | -------------------------- | -------- |
| notify  | 通知栏消息     | AndroidiOS                 | 通知栏展示消息  |
| message | 透传消息/静默消息 | Android(透传消息)<br>iOS(静默消息) | 通知栏不展示消息 |



### message：消息体

消息体，即下发到客户端的消息

Push API 对 iOS 和 Android 两个平台的消息有不同处理，需要分开来实现对应平台的推送消息，推送的消息体是 JSON格式

#### Android普通消息

Android平台具体字段如下表：

| 字段名            | 类型     | 默认值  | 必需   | 参数描述                                     |
| -------------- | ------ | ---- | ---- | ---------------------------------------- |
| title          | string | 无    | 是    | 消息标题                                     |
| content        | string | 无    | 是    | 消息内容                                     |
| accept_time    | array  | 无    | 否    | 消息将在哪些时间段允许推送给用户，建议小于10个，不能为空                 |
| xg_media_resources    | string  | 无    | 否    | 富媒体元素地址，建议小于5个   （仅限SDK4.2.0及以上版本使用）              |
| n_id           | int    | 0    | 否    | 通知消息对象的唯一标识（只对信鸽通道生效）<br>1）大于0：会覆盖先前相同id的消息<br>2）等于0：展示本条通知且不影响其他消息<br>3）等于-1：将清除先前所有消息，仅展示本条消息 |
| builder_id     | int    | 0    | 否    | 本地通知样式标识                                 |
| ring           | int    | 1    | 否    | 是否有铃声<br>1）0：没有铃声<br>1）1：有铃声             |
| ring_raw       | string | 无    | 否    | 指定Android工程里raw目录中的铃声文件名，不需要后缀名          |
| vibrate        | int    | 1    | 否    | 是否使用震动<br>1）0：没有震动<br>2）1：有震动            |
| lights         | int    | 1    | 否    | 是否使用呼吸灯<br>1）0：不使用呼吸灯<br>2）1：使用呼吸灯       |
| clearable      | int    | 1    | 否    | 通知栏是否可清除                                 |
| icon_type      | int    | 0    | 否    | 通知栏图标是应用内图标还是上传图标<br>1）0：应用内图标<br>2）1：上传图标 |
| icon_res       | string | 无    | 否    | 应用内图标文件名或者下载图标的url地址                     |
| style_id       | int    | 1    | 否    | 设置是否覆盖指定编号的通知样式                          |
| small_icon     | string | 无    | 否    | 消息在状态栏显示的图标，若不设置，则显示应用图标                 |
| action         | JSON   | 有    | 否    | 设置点击通知栏之后的行为，默认为打开app                    |
| custom_content | JSON   | 无    | 否    | 用户自定义的键值对                                |

完整的消息示例如下：

```json
{
    "title": "xxx",
    "content": "xxxxxxxxx",
    "xg_media_resources": "xxx1" , //此处填富媒体元素地址，例如https://www.xx.com/img/bd_logo1.png?qua=high

    "accept_time": [
        {
            "start": {
                "hour": "13",
                "min": "00"
            },
            "end": {
                "hour": "14",
                "min": "00"
            }
        },
        {
            "start": {
                "hour": "00",
                "min": "00"
            },
            "end": {
                "hour": "09",
                "min": "00"
            }
        }
    ],
    "android": {
        "n_id": 0,
        "builder_id": 0,
        "ring": 1,
        "ring_raw": "ring",
        "vibrate": 1,
        "lights": 1,
        "clearable": 1,
        "icon_type": 0,
        "icon_res": "xg",
        "style_id": 1,
        "small_icon": "xg",
        "action": {
            "action_type": 1,// 动作类型，1，打开activity或app本身；2，打开浏览器；3，打开Intent
            "activity": "xxx",
            "aty_attr": {// activity属性，只针对action_type=1的情况
                "if": 0, // Intent的Flag属性
                "pf": 0  // PendingIntent的Flag属性
            },
            "browser": {
                "url": "xxxx ", // 仅支持http、https
                "confirm": 1 // 是否需要用户确认
            },
            "intent": "xxx" //SDK版本需要大于等于3.2.3，然后在客户端的intent配置data标签，并设置scheme属性
        },
        "custom_content": {
            "key1": "value1",
            "key2": "value2"
        }
    }
}
```

#### iOS普通消息

iOS平台具体字段如下表：

| 字段名    | 类型          | 默认值  | 必需   | 参数描述                                     |
| ------ | ----------- | ---- | ---- | ---------------------------------------- |
| aps    | JSON        | 无    | 是    | 苹果推送服务(APNs)特有的消息体字段，其中比较重要的键值对如下<br>alert：包含标题和消息内容(必选)<br>badge_type：App显示的角标数(可选)<br>category：下拉消息时显示的操作标识(可选)<br>详细介绍可以参照：[Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1) |
| custom | string/JSON | 无    | 否    | 自定义下发的参数                                 |
| xg     | string      | 无    | 否    | 系统保留key，应避免使用                            |


完整的消息示例如下：

```json
{
    "title": "xxx",
    "content": "xxxxxxxxx",
    "ios":{
        "aps": {
            "alert": {
                "subtitle": "my subtitle"
            },
            "badge_type": 5,
            "category": "INVITE_CATEGORY"
        },
        "custom1": "bar",
        "custom2": [
            "bang",
            "whiz"
        ],
        "xg": "oops"
    }
}
```

#### Android透传消息

透传消息，Android平台特有，即不显示在手机通知栏中的消息，可以用来实现让用户无感知的向App下发带有控制性质的消息

Android平台具体字段如下表：

| 字段名            | 类型     | 默认值  | 是否必需 | 参数描述                     |
| -------------- | ------ | ---- | ---- | ------------------------ |
| title          | string | 无    | 是    | 消息标题                     |
| content        | string | 无    | 是    | 消息内容                     |
| custom_content | JSON   | 无    | 否    | 自定义内容                    |
| accept_time    | array  | 无    | 否    | 消息将在哪些时间段允许推送给用户，建议小于10个 |

具体完整示例：

```json
{
    "title": "this is title",
    "content": "this is content",
    "android": {
       "custom_content": {
          "key1": "value1",
          "key2": "value2"
             }
    },
    "accept_time": [
        {
            "start": {
                "hour": "13",
                "min": "00"
            },
            "end": {
                "hour": "14",
                "min": "00"
            }
        },
        {
            "start": {
                "hour": "00",
                "min": "00"
            },
            "end": {
                "hour": "09",
                "min": "00"
            }
        }
    ]
}
```

#### iOS静默消息

静默消息，iOS平台特有，类似Android中的透传消息，消息不展示，当静默消息到达终端时，iOS会在后台唤醒App一段时间(小于30s)，让App来处理消息逻辑

具体字段如下表：

| 字段名    | 类型          | 默认值  | 是否必要 | 参数描述                                     |
| ------ | ----------- | ---- | ---- | ---------------------------------------- |
| aps    | JSON        | 无    | 是    | 苹果推送服务(APNs)特有的，其中最重要的键值对如下<br>content-available：标识消息类型(必须为1)，且不能包含alert、sound、badge_type字段<br>详细介绍可以参照：[Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html#//apple_ref/doc/uid/TP40008194-CH17-SW1) |
| custom | string/JSON | 无    | 否    | 自定义下发的参数                                 |
| xg     | string      | 无    | 否    | 系统保留key，应避免使用                            |



具体完整示例：

```json
{
    "ios":{
        "aps": {
            "content-available": 1
        },
        "custom": {
            "key1": "value1",
            "key2": "value2"
        },
        "xg": "oops"
    }
}
```

### Push API 可选参数

Push API 可选参数是除了 `audience_type`、`platform`、`message_type`、`message` 以外，可选的高级参数

| 参数名           | 类型      | 必需               | 默认值     | 描述                                       |
| ------------- | ------- | ---------------- | ------- | ---------------------------------------- |
| expire_time   | int     | 否                | 259200(72小时)  | 消息离线存储时间（单位为秒）,最长72小时<br>1）若expire_time=0，则表示实时消息<br>2）若expire_time大于0且小于800s，则系统会重置为800s<br>3）若expire_time>=800s，按实际设置时间存储，最长72小时 <br>4)设置的最大值不得超过2147483647，否则会导致推送失败|
| send_time     | string  | 否                | 当前系统时间  | 指定推送时间<br>1）格式为yyyy-MM-DD HH:MM:SS<br>2）若小于服务器当前时间，则会立即推送<br>3）仅全量推送和标签推送支持此字段 |
| multi_pkg     | bool    | 否                | false   | 多包名推送<br>1）当app存在多个不同渠道包（例如应用宝、豌豆荚等），推送时如果是希望手机上安装任何一个渠道的app都能收到消息那么该值需要设置为true |
| loop_times    | int     | 否                | 0       | 循环任务重复次数<br>1）仅支持全推、标签推<br>2）建议取值[1, 15] |
| loop_interval | int     | 否                | 0       | 循环执行消息下发的间隔<br>1）必须配合loop_times使用<br>2）以天为单位，取值[1, 14]<br>3）loop_times和loop_interval一起表示消息下发任务的循环规则 |
| environment   | string  | 是（仅iOS平台使用）                | product | 用户指定推送环境，仅限iOS平台推送使用<br>1）product： 推送生产环境<br>2）dev： 推送开发环境 |
|badge_type     |int      |否                 |-1        | 用户设置角标数字，仅限iOS 平台使用,放在aps字段内<br> 1)  -1:角标数字不变 <br>  2) -2:角标数字自动加1 <br>3) >=0:设置「自定义」角标数字|
| stat_tag      | string  | 否                | 无       | 统计标签，用于聚合统计<br>使用场景(示例)：现在有一个活动id：active_picture_123，需要给10000个设备通过单推接口（或者列表推送等推送形式）下发消息，同时设置该字段为active_picture_123，推送完成之后可以使用v3统计查询接口，根据该标签active_picture_123 查询这10000个设备的实发、抵达、展示、点击数据 |
| seq           | int64_t | 否                | 0       | 接口调用时，在应答包中信鸽会回射该字段，可用于异步请求<br>使用场景：异步服务中可以通过该字段找到server端返回的对应应答包 |
| tag_list      | object  | 仅标签推送必需          | 无       | 1）推送 tag1 和 tag2 的设备：{“tags”:[“tag1”,”tag2”],”op”:”AND”}<br>2）推送 tag1 或 tag2 的设备： {“tags”:[“tag1”,“tag2”],”op”:“OR”} |
| account_list  | array   | 单账号推送、账号列表推送时必需  | 无       | 若单账号推送<br>1）要求 audience_type=account<br>2）参数格式：[“account1”]<br>若账号列表推送<br>1）参数格式：[“account1”,”account2”]<br>2）最多1000 个account |
| account_push_type  | int     | 单账号推送时可选         | 0       |1) 0: 往单个账号的最新的device上推送信息<br>2) 1: 往单个账号关联的所有device设备上推送信息|
| account_type  | int     | 单账号推送时可选         | 0       | 1）账号类型，参考后面账号说明<br>2）必须与账号绑定时设定的账号类型一致   |
| token_list    | array   | 单设备推送、设备列表推送时必需  | 无       | 若单设备推送<br>1）要求 audience_type=token<br>2）参数格式：[“token1”]<br>若设备列表推送<br>1）参数格式：[“token1”,”token2”]<br>2）最多 1000 个 token |
| push_id       | string  | 账号列表推送、设备列表推送时必需 | 无       | 账号列表推送和设备列表推送时，第一次推送该值填0，系统会创建对应的推送任务，并且返回对应的pushid：123，后续推送push_id填123(同一个文案）表示使用与123 id 对应的文案进行推送。(注：文案的有效时间由前面的expire_time 字段决定） |



### Push API应答参数

| 字段名      | 类型      | 是否必填 | 注释                                       |
| -------- | ------- | ---- | ----------------------------------------          |
| seq      | int64_t | 是    | 与请求包一致（如果请求包是非法json该字段为0）        |
| push_id | string   | 是    | 推送id |
| ret_code | int32_t | 是    | 错误码，详细参照错误码对照表                        |
| environment | string | 是 | 用户指定推送环境，仅支持iOS<br>product： 生产环境<br>dev： 开发环境 |
| err_msg  | string  | 否    | 请求出错时的错误信息                               |
| result   | string  | 否    | 请求正确时，若有额外数据要返回，则结果封装在该字段的json中，若无额外数据，则可能无此字段 |



### Push API 请求完整示例

#### Android标签推送请求消息

```json
POST /v3/push/app HTTP/1.1
Host: openapi.xg.qq.com
Content-Type: application/json
Authorization: Basic YTViNWYwNzFmZjc3YTplYTUxMmViNzcwNGQ1ZmI1YTZhOTM3Y2FmYTcwZTc3MQ==
Cache-Control: no-cache
Postman-Token: 4b82a159-afdd-4f5c-b459-de978d845d2f
{
    "platform": "android",
    "audience_type": "tag",
    "tag_list": {
        "tags": [
            "tag1",
            "tag2"
        ],
        "op": "AND"
    },
    "message_type": "notify",
    "message": {
        "title": "this is title",
        "content": "this is content",
        "custom_content": {
            "key1": "value1",
            "key2": "value2"
        },
        "accept_time": [
            {
                "start": {
                    "hour": "13",
                    "min": "00"
                },
                "end": {
                    "hour": "14",
                    "min": "00"
                }
            }
        ]
    }
}
```

#### 标签推送应答消息

```json
{
    "seq": 0,
    "environment": "product",
    "ret_code": 0,
    "push_id": "3895624686"
}
```
### iOS单设备推送请求消息

```json

POST /v3/push/app HTTP/1.1
Host: openapi.xg.qq.com
Content-Type: application/json
Authorization: Basic ODhjNzE1Mzc1MDQ0ZDowNGM4NmNhZmI0ZTMxZDU4M2UzYjg0M2VhMDc4YTU5ZQ==
Cache-Control: no-cache
Postman-Token: 71670b5b-3149-4883-a427-d75cf9f42188

{
 
    "platform": "ios",
    "audience_type": "token",
    "environment":"dev",
    "token_list": [ "55c2ddba664e9abcacea7daab0887939893b18e1a2cf4475c5382f5bcb2ab25b"],
    "message_type":"notify",
    "message":{
     "title": "xxx",
    "content": "https://xg.qq.com/docs/ios_access/ios_faq.html",
    "ios":{
        "aps": {
            "alert": {
                "subtitle": "my subtitle"
            },
            "badge_type": -2,
            "sound":"Tassel.wav",
            "category": "INVITE_CATEGORY"
            
        },
        "custom1": "bar",
        "custom2": [
            "bang",
            "whiz"
        ],
        "xg": "oops"
    }
 }
}
```
#### 单设备推送应答消息

```json
{
    "seq": 0,
    "push_id": "427184209",
    "ret_code": 0,
    "environment": "dev",
    "err_msg": "",
    "result": "[0]"
}
```


## 账号类型

账号类型是客户端调用SDK接口绑定，类型如下表所示：

| 账号类型   | 含义        |
| ------ | --------- |
| 0      | 未知        |
| 1      | 手机号       |
| 2      | 邮箱        |
| 1000   | 微信openid  |
| 1001   | qq openid |
| 1002   | 新浪微博      |
| 1003   | 支付宝       |
| 1004   | 淘宝        |
| 1005   | 豆瓣        |
| 1006   | facebook  |
| 1007   | twitter   |
| 1008   | google    |
| 1009   | 百度        |
| 1010   | 京东        |
| 1011   | linkin    |
| 1999   | 其他        |
| 2000   | 游客登录      |
| 2001以上 | 用户自定义     |



## 错误码

信鸽REST API接口较多，开发者使用过程中不可避难会遇到各种问题，这里提供了常见的错误码释义，对应着是<a href="#通用基础返回值">通用基础返回值</a>中的ret_code字段的可能值

| 错误码   | 含义                    |
| ----- | --------------------- |
| 10100 | 系统繁忙请稍后重试!            |
| 10101 | 系统繁忙请稍后重试!            |
| 10102 | 缺少参数请检查后重试            |
| 10103 | 参数值非法，请检查后重试          |
| 10104 | 鉴权未通过，请检查secret key!  |
| 10105 | 证书无效!                 |
| 10106 | 当前推送类型不支持多平台推送!       |
| 10107 | 消息体是非法json 格式         |
| 10108 | 内部错误,请稍候重试!           |
| 10109 | 内部错误,请稍候重试!           |
| 10110 | 设备未注册!                |
| 10111 | 内部错误,请稍候重试!           |
| 10112 | 内部错误,请稍候重试!           |
| 10113 | 内部错误,请稍候重试!           |
| 10114 | 内部错误,请稍候重试!           |
| 10115 | 帐号不能为空,帐号为空!          |
| 10116 | 帐号不存在                 |
| 10117 | 推送内容太大                |
| 10201 | 创建推送任务失败,请稍后重试!       |
| 10202 | 推送消息内容转换APNs 失败!      |
| 10203 | 创建推送任务失败，请稍后重试!       |
| 10204 | 推送失败，请稍后重试!           |
| 10205 | 推送任务过期，请检查！           |
| 10206 | 获取消息副本失败，请稍后重试！       |
| 10207 | 获取消息副本失败，请稍后重试！       |
| 10301 | 帐号列表推送失败，请稍后重试!       |
| 10302 | 帐号列表推送部分失败,请检查部分账号是否有绑定设备！           |
| 10303 | 帐号列表推送全部失败,请检查账号是否有绑定设备!     |
| 10304 | token 列表推送部分失败，检查部分设备是否有正常注册！       |
| 10305 | token 列表推送全部失败,请检查设备是否有正常注册! |
| 10401 | 内部错误，请稍候重试!           |
| 10402 | 内部错误，请稍候重试!           |
| 10403 | 内部错误，请稍候重试!           |
| 10404 | 内部错误，请稍候重试!           |
| 10405 | 内部错误，请稍候重试!           |
| 10406 | 内部错误，请稍候重试!           |
| 10407 | 内部错误，请稍候重试!           |
| 10501 | 内部错误，请稍候重试!           |
| 10502 | 内部错误，请稍候重试!           |
| 10503 | 内部错误，请稍候重试!           |
| 10504 | 内部错误，请稍候重试!           |
| 10505 | 内部错误，请稍候重试!           |
| 10506 | 内部错误，请稍候重试!           |
| 10507 | 内部错误，请稍候重试!           |
| 10601 | 内部错误，请稍候重试!           |
| 10602 | 内部错误，请稍候重试!           |
| 10603 | 内部错误，请稍候重试!           |
| 10604 | 内部错误，请稍候重试!           |
| 10605 | 内部错误，请稍候重试!           |
| 10606 | app 未注册，请注册后重试!       |
| 10701 | 内部错误,请稍候重试!           |
| 10702 | 内部错误，请稍候重试!           |
| 10707 | 内部错误，请稍候重试!           |
| 10708 | 内部错误，请稍候重试!           |
| 10709 | 内部错误，请稍候重试!           |
| 10710 | 内部错误，请稍候重试!           |
| 10711 | 内部错误，请稍候重试!           |
| 10712 | 内部错误，请稍候重试!           |
| 10713 | 内部错误，请稍候重试!           |
| 其他    | 未知错误，请稍后重试!           |