## 云审计事件简介
使用腾讯云云审计（CloudAudit），可以获取您腾讯云账号下 API 调用历史记录，包括通过腾讯云管理控制台，腾讯云 SDK，命令行工具和其他腾讯云服务进行的 API 调用，监控腾讯云中的任何部署行为。可以确定某些子用户、协作者使用腾讯云 API 时，从某个源 IP 地址进行调用，以及何时发生调用。

目前 EventBridge 已完成云审计日志接入，通过云服务默认事件集接收云上**写入**操作事件，从而进行云上操作的管理和运维。支持审计的服务及接口列表详情见 [云审计支持事件列表](https://intl.cloud.tencent.com/document/product/1021/37598)。

## 事件格式

```json
{
    "specversion":"1.0",
    "id":"13a3f42d-7258-4ada-da6d-023a33******",
    "source":"${ProductName}.cloud.tencent",
    "type":"cvm:CloudEvent:ApiCall",
    "subject":"${资源 ID}",
    "time": 1615430559146,
    "region":"ap-guangzhou",
    "resource":[
        "qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"
    ],
    "datacontenttype":"application/json;charset=utf-8",
    "tags":{
        "key1":"value1",
        "key2":"value2"
     },
    "data":{
        ${原始 API 操作日志}
    }
}
```
事件涉及的参数如下说明：

| 字段            | 描述                                                         | 字符串类型 |
| --------------- | ------------------------------------------------------------ | ---------- |
| specversion     | 事件结构体版本（cloudevents 遵循版本，目前仅支持 1.0）。        | String     |
| id              | PUT Event 返回的 ID 信息。                                   | String     |
| type            | PUT Event 输入的事件类型，对于云审计类型事件，根据来源不同，分为`${产品缩写}:CloudEvent:ApiCall`、 `${产品缩写}:CloudEvent:ConsoleCall`、`${产品缩写}:CloudEvent:MiniProgramCall` 三类| String     |
| source          | 事件来源（云服务事件必传此参数，为 subject 的缩写 ）。云服务默认为 `xxx.cloud.tencent`。 | String     |
| subject        | 事件来源详情可自定义，云服务默认使用 QCS 描述，例如 `qcs::dts:ap-guangzhou:appid/uin:xxx`。 | String     |
| time          | 发生事件的时间，0 时区毫秒时间戳，例如 1615430559146。         | Timestamp  |
| datacontenttype | 数据类型申明。                                               | String     |
| region          | 地域信息。                                                   | String     |
| data            | PUT Event 输入的事件详情，对与审计事件，此处传入完整云审计日志                                   |  Json     |

## 调用方式
接收云审计事件前，请保证您已经**开启云审计服务并创建相关服务角色**。

1. 登录 [事件总线控制台](https://console.cloud.tencent.com/eb)，在**广州地域**打开**云服务事件集**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/a0c6a84612400e9194b6d67e8b3fc265.png)
2. 在事件集详情页，选择开启云审计。
3. 在**事件规则**页，选择对应的事件集后，在事件集下创建事件规则，完成需要处理的事件类型筛选，并绑定投递目标。操作详情见 [创建事件规则](https://intl.cloud.tencent.com/document/product/1108/42289)。
