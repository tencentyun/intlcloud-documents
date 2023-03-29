## 应用场景
在 App 退后台或者进程被 kill 的情况下，有新消息需要提醒用户时，可使用离线推送功能，在 iOS 端会有 APNs 推送，Android 端则需要用户注册离线消息回调。

## iOS APNs 推送
### 推送格式说明

![](https://main.qcloudimg.com/raw/8bb11ef0a0ff210c1b0a1ab65da63c2f.png)


上图为一条单聊消息和一条群聊消息的示例。
iOS APNs 推送格式详细说明可参考 [推送格式说明](https://intl.cloud.tencent.com/document/product/1047/34347)。

### 基本接口说明
支持 APNs 必须调用以下接口，具体请参考 [iOS APNs 事件上报](https://intl.cloud.tencent.com/document/product/1047/34347)：
- 设置 Token。
- 切后台上报未读。
- 切前台通知。

### Ext 扩展设置
有时应用需要根据情况设置推送的 Ext 扩展字段，方便用户点击跳转等操作，可以填写到 TIMCustomElem 中的 Ext 字段，推送时即时通信 IM 后台会把该字段填入 Ext，请参考 [自定义离线消息属性](https://intl.cloud.tencent.com/document/product/1047/34347) 定制扩展字段。

### 设置推送声音
有时应用需要根据情况设置单条消息的推送声音，方便特别提醒某类消息，可以把声音填写到 TIMCustomElem 中的 sound 字段，推送时即时通信 IM 后台会把该字段填入 Ext，请参考 [设置自定义推送提示音](https://intl.cloud.tencent.com/document/product/1047/34347) 。

## Android 离线推送
Android 在1.8.0以后版本支持服务和进程分离，如果 App 进程被 kill，服务仍然存活，可以收到离线推送功能。具体配置以及设置过程，可参考 [Android 离线推送](https://intl.cloud.tencent.com/document/product/1047/34336) 文档。

## 后台发送消息
后台发送消息时，对于 iOS 端您可以参考 [推送格式](https://intl.cloud.tencent.com/document/product/1047/34347) 设置 APNs 推送的展示形式，对于 Android 端您可以参考 [离线推送 OfflinePushInfo](https://intl.cloud.tencent.com/document/product/1047/33527) 进行设置。

## 相关文档
- [管理离线推送证书](https://intl.cloud.tencent.com/document/product/1047/34540)
- [Apple 推送证书申请](https://intl.cloud.tencent.com/document/product/1047/34346)
- [iOS 离线推送配置](https://intl.cloud.tencent.com/document/product/1047/34347)
- [Android 离线推送基本配置](https://intl.cloud.tencent.com/document/product/1047/34336)
