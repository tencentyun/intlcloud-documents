# 配置基础信息
在应用详情页，您可以查看并修改应用信息。在应用的【基础配置】页，您可以根据实际需求设置发送总量阈值、设置国际港澳台短信发送限制、配置事件回调、设置发送频率限制、以及管理告警联系人。

## 发送总量阈值设置
1.登录 [短信控制台](https://intl.cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fsmsv2)。
2.您可以通过以下方式进入【基础配置】页签：
- 在左侧导航栏选择【应用管理】>【应用列表】，单击目标应用卡片进入应用详情页，单击【基础配置】。
- 在左侧导航栏选择【应用管理】>【基础配置】。
3.选择【当前应用】为待操作的目标应用。
4.单击【发送总量阈值设置】区域的【设置】，您可以根据实际需求设置发送超量提醒值，发送量超过提醒值，告警联系人会收到告警通知；设置发送限额值，发送量超过限额值当日暂停发送短信。
![](https://qcloudimg.tencent-cloud.cn/raw/dde38d44364076d2ce64eeb48ed90fc2.png)
5.单击【设置】即可保存。
设置成功后，请在【通知与告警】中配置告警联系人，当发送超量后，告警联系人可以收到提醒短信。
![](https://qcloudimg.tencent-cloud.cn/raw/bab6b1bc059170bad7612e7fe998911c.png)

## 国际港澳台短信发送限制设置
<dx-alert infotype="notice" title="">
该能仅支持企业认证用户，个人认证用户暂不支持。
</dx-alert>
1.单击【国际港澳台短信发送限制设置】区域的【设置】，您可以根据实际需求选择能发送短信的目标国家及单自然日发送限额值。

![](https://qcloudimg.tencent-cloud.cn/raw/004b0e6423c3214962c0d7cdad7ee984.png)

2.支持下拉选择单个国家和批量导入多个国家。如需批量导入，可下载模板参考。
![](https://qcloudimg.tencent-cloud.cn/raw/fd0ebeef9e68b6bd55e0b84e56010a7e.png)

<dx-alert infotype="notice" title="">
- 单国家自然日的发送限额值设置不能大于该应用的国际港澳台短信发送限额值。
- 单国家自然日的发送限额值可以不填写，如不填，将默认与当前应用的限额值保持一致。
- 设置成功后，当前应用将仅支持设置好的国家/地区发送短信，其他国家/地区将禁发。
</dx-alert>

3.单击【设置】即可保存。
设置成功后，如需修改某个国家的单自然日发送总量，可点击编辑。同时支持删除和导出已设置好的国家/地区。

## 事件回调配置
1.单击【事件回调配置】区域的【设置】，您可以根据实际需求勾选短信状态回调，并输入对应的回调 URL（回调信息接收接口）。
![](https://qcloudimg.tencent-cloud.cn/raw/8df55c41c5d708b2199e21849f4bb879.png)

<dx-alert infotype="explain" title="">
回调信息所携带的 body 体格式是 JSON 格式。
</dx-alert>

2.单击【设置】即可保存。
设置成功后，您可以更精细化了解短信发送相关信息。如果您配置了短信接收状态回调地址，腾讯云收到运营商回调信息后会及时将回调信息推送到您指定的回调地址，然后您可以自行开发相关代码，接收、解析腾讯云短信推送的回调信息并加以运用。

![](https://qcloudimg.tencent-cloud.cn/raw/c2a11dac4c5cf3a3ab6ec18b42db488b.png)

## 设置发送频率限制
为了保障业务和通道安全，减少业务被刷后的经济损失，短信默认的频率限制策略为：
- 同一号码同一内容30秒内最多发送1条。
- 同一手机号一个自然日最多发送10条。

<dx-alert infotype="notice" title="">
个人认证用户不提供修改频率限制的权限。如需使用该功能，请将 “个人认证” 修改为 “企业认证”。
</dx-alert>

1.单击【发送频率限制】区域的【设置】，您可以根据实际需求勾选限制条件，并设置对应的阈值。
![](https://qcloudimg.tencent-cloud.cn/raw/6911eb24624726fc856d9b3af3457233.png)

2.单击【设置】即可保存。
![](https://qcloudimg.tencent-cloud.cn/raw/b6f36a9aa17e0aa82cbaa8ed81c21acb.png)

## 设置频率限制白名单

<dx-alert infotype="explain" title="">
在白名单的手机号码发送短信不受频率限制策略的影响，最多可以添加300个白名单号码。
</dx-alert>

### 添加白名单号码
1.单击【频率限制白名单】区域的【设置】，输入手机号码，回车换行，每一行表示一个号码，最多可以添加300个白名单号码。
![](https://qcloudimg.tencent-cloud.cn/raw/4d18af62c4e49d89db4de78e8d05cf20.png)

2.单击【设置】即可保存设置。
![](https://qcloudimg.tencent-cloud.cn/raw/72c2f32c724fc4335db26b5e1592523a.png)

### 删除白名单号码
1.在【频率限制白名单】区域，单击目标号码所在行的【删除】。
![](https://qcloudimg.tencent-cloud.cn/raw/83ce9b62a99559d4d8a805e1acd5907c.png)
2.单击【确认删除】即可。




