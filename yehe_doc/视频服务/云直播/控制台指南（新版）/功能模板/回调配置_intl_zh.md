本文档将向您介绍如何通过云直播控制台创建回调配置模板，并在推流域名下进行回调配置。


## 注意事项
- 创建成功后，还需到对应的推流域名下关联 [回调配置](https://intl.cloud.tencent.com/document/product/267/31065)，关联成功后约5分钟 - 10分钟生效。
- 用户也可以通过 API 对直播频道创建回调模板。
- 直播回调相关协议，请参见 [事件消息通知协议](https://intl.cloud.tencent.com/document/product/267/31566)。
- 直播回调参数及示例，请参见 [事件消息通知参数说明](https://intl.cloud.tencent.com/document/product/267/31566)。

## 创建回调模板
1. 登录 [云直播控制台](https://console.cloud.tencent.com/live)。
2. 在左侧菜单栏选择【功能模板】>[【回调配置】](https://console.cloud.tencent.com/live/config/callback)。
3. 单击 【+】创建回调模板，在回调设置弹框中填写完成回调信息，单击【保存】即可。
>**回调密钥**即为客户自定义的一串字符，由大小写字母及数字组成的，最多32个字符。相关使用请参见 [事件消息通知](https://intl.cloud.tencent.com/document/product/267/31566)。

![](https://main.qcloudimg.com/raw/870c6dd664a4eb618bdc1a7fcdf922dc.png)
## 域名关联模板
创建好回调模板后，您需要根据以下步骤进行模板关联。
1. 进入[【域名管理】](https://console.cloud.tencent.com/live/domainmanage)，选择需要配置的推流域名，单击右侧的【管理】。
2. 进入域名详情页，选择【模板配置】。
3. 单击【回调配置】标签右侧的【编辑】，选择已创建好的回调模板，单击【保存】即可。
![](![img](https://main.qcloudimg.com/raw/e18e4c7f58950bd2dbe74f038c455cd9.png)


## 解除关联模板
如果您需要解绑回调配置，在【模板配置】>【回调配置】中，单击右侧的【编辑】，取消相应模板的勾选，然后单击【保存】，即可将该模板与域名取消关联。
> 控制台的回调模板管理为域名维度，暂时无法取消关联接口创建的规则，如果是通过直播回调相关接口关联指定流的，则需要通过调用 [删除回调模板](https://intl.cloud.tencent.com/document/product/267/30813) 解除关联。
>
