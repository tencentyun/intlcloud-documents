媒体生产业务存在内容不可控性，如有存在不合规的内容，可能带来相关法律风险和品牌伤害。为确保业务健康，保障服务稳定，云点播提供了 [音视频审核](https://intl.cloud.tencent.com/document/product/266/33944) 以及 [图片内容审核](https://cloud.tencent.com/document/product/266/73655) 能力。

## 音视频内容审核
云点播提供的 [音视频内容审核](https://intl.cloud.tencent.com/document/product/266/33944) 功能，可对音视频内容发起审核，并在识别结果中给出审核建议（建议复核和建议通过）。开发者可根据结果对音视频内容进行处理。

有两种方式发起音视频内容审核：
1. 通过云点播 [控制台](https://intl.cloud.tencent.com/document/product/266/33897) 操作。
2. 通过服务端 API [音视频内容审核](https://intl.cloud.tencent.com/document/product/266/33944) 调用。

### 服务端 API 音视频内容审核 调用
示例，某视频 App 接入云点播音视频审核服务，服务端 API 调用流程如下：
![](https://main.qcloudimg.com/raw/99544692ba8d62874a0f718e805f2d57.png)

1. App 后台对内容提供方进行鉴权，鉴权通过后派发视频 [客户端上传签名](https://intl.cloud.tencent.com/document/product/266/33922)。
2. 内容提供方执行上传，把分享的内容上传到云点播。
3. 云点播将成功上传的视频 FileId 以及播放 URL 等 [相关信息](https://intl.cloud.tencent.com/document/product/266/33950) 通知到 App 后台。
4. 云点播执行上传签名时对`procedure`参数进行配置的视频内容进行审核任务。
5. 云点播通过 [任务流状态变更](https://intl.cloud.tencent.com/document/product/266/33953) 通知 App 后台审核结果。
 - 审核结果为“block”时，嫌疑度很高，建议直接屏蔽。
 -  审核结果为“pass”时，嫌疑度不高，建议直接通过。
 -  审核结果为“review”时，嫌疑度较高，建议人工复核。
6. App 后台发布“建议通过”的视频，以及“建议复核”且经人工复核通过的视频。
7. 内容消费方向 App 后台请求已发布视频的播放 URL。
8. 内容消费方通过播放 URL，从云点播加速播放视频。

第4 - 6步的流程可以保证内容消费方在第7步获取到的视频是经审核验证的合规视频。

>! 此处介绍的流程属于“先审后发”模式（仅发布审核通过的视频）。如有需要，也可采用“先发后审”模式（视频上传完成后即发布，审核发现不适宜内容后再撤下视频）。



