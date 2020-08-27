直播推流默认关闭回调功能，本文将向您介绍如何对指定推流域名关联回调模板开启回调功能，以及关联成功后如何解绑模板关闭域名回调功能。

## 注意事项
- 模板配置完后约5分钟 - 10分钟生效。
- 回调配置成功后，直播过程中事件触发时，可以通过事件消息通知被动获取到具体直播事件信息，具体请参见 [事件消息通知](https://intl.cloud.tencent.com/document/product/267/31566)。

## 前提条件
- 已登录 [云直播控制台](https://console.cloud.tencent.com/live)，并成功添加 [推流域名](https://intl.cloud.tencent.com/document/product/267/35970)。
- 已创建 [回调模板](https://intl.cloud.tencent.com/document/product/267/31074)。

## 关联回调模板
1.	进入[【域名管理】](https://console.cloud.tencent.com/live/domainmanage)，单击需配置的推流域名对应的【管理】进入域名详情页。
2.	选择【模板配置】页签，单击【回调配置】标签右上角的【编辑】。
![](https://main.qcloudimg.com/raw/d3e31f428ab1463335e234007c663311.png)
3.	选择指定对应的回调模板，单击【保存】即可。
![](https://main.qcloudimg.com/raw/27f9da682e20283e25cc2478e1a53a0b.png)

## 取消模板关联

1. 进入[【域名管理】](https://console.cloud.tencent.com/live/domainmanage)，单击需配置的推流域名或右侧的【管理】，进入域名详情页。
2. 选择【模板配置】页签，单击【回调配置】标签右上角的【编辑】。
3. 取消关联模板的勾选，单击【保存】即可。
![](https://main.qcloudimg.com/raw/0f8ec4ae49d2f1c5329bdb509f056366.png)

