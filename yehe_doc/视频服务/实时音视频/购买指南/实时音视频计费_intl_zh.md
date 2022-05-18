本文介绍 TRTC 如何按月统计使用[语音通话](https://intl.cloud.tencent.com/document/product/647/36066)、[视频通话](https://intl.cloud.tencent.com/document/product/647/36066)、[音视频互动直播](https://intl.cloud.tencent.com/document/product/647/37286)的费用。

如需预估业务费用，请使用[TRTC价格计算器](https://intl.cloud.tencent.com/pricing/trtc/calculator)。

如果你已与我们的销售签约，则实际计费信息以合同为准。

>? 2021年10月27日起首次在 TRTC 控制台创建[应用](https://intl.cloud.tencent.com/document/product/647/37714)的账号，开始按照本文档中的“订阅视频的总分辨率”方式计量计费。



## 费用计算 

每月结束时，TRTC 会统计你 [腾讯云账号](https://console.intl.cloud.tencent.com/trtc)下所有项目当月产生的音频和视频时长用量（单位为分钟）。需注意，视频时长用量按照“订阅视频的总分辨率”分为四个档位，分档定价。扣除 TRTC 为每个开发者账号提供的[每月一万分钟免费分钟数](https://intl.cloud.tencent.com/document/product/647/42735)后，TRTC 将剩余的音频时长用量和视频时长用量乘以对应的单价，最后相加得出本月总费用。

### 第一步，了解基础的计费公式：

**月度费用** = **音频时长用量** × **音频单价** + **各档位视频时长用量** × **对应视频单价**

### 第二步，计算音频和视频时长用量：

其中，每个会话的时长用量，是这个会话中**所有用户产生的时长用量之和**。

-   **视频时长用量**：如果用户成功订阅了视频流，则产生视频用量。注意，如果同时订阅音频流和视频流，只计算视频用量。
-   **音频时长用量**：如果用户没有订阅视频流，则无论其是否订阅了音频流，都会产生音频用量。也就是说，当用户进入房间后，若其订阅了视频流，则只计算视频用量，但若其未订阅任何视频或者音频流，都会计算其在房的时长，算作音频时长用量。

### 第三步，不同档位对应的单价：

| 用量类型          | 单价（美元/千分钟） | 用户订阅视频的总分辨率                                       |
| :---------------- | :------------------ | ------------------------------------------------------------ |
| 音频              | 0.99                | -                                                            |
| 高清（HD）        | 3.99                | 分辨率 ≤ 921,600（1280x720）                                 |
| 全高清（Full HD） | 8.99                | 921,600（1280 × 720）＜ 分辨率 ≤ 2,073,600（1920 × 1080）    |
| 视频2K            | 15.99               | 2,073,600 (1920 × 1080) ＜ 分辨率 ≤ 3,686,400 （2560 × 1440） |
| 视频4K            | 35.99               | 3,686,400 （2560 × 1440）＜ 分辨率 ≤ 8,847,360 （4096 × 2160） |

例如，用户 A 同时订阅 2 路分辨率为 960 × 720 的视频流，则该用户接收的视频总面积为 960 × 720 + 960 × 720 = 1,382,400，其视频用量按全高清（Full HD）类型的单价计费。



## 计费示例1

本节举例说明 TRTC 如何计算费用。

假设有 6 位用户同时加入一个频道，并且进行了 60 分钟的视频互动直播。

在视频互动直播中，有 3 位主播（主播 A、B 和 C），A 主播的视频分辨率为 960 × 720，B 和 C 主播的视频分辨率为 640 × 480。2 位观众订阅了所有主播的视频流，另1位观众没有订阅视频流，仅订阅音频流。 此外，主播 A 向频道中的所有其他用户共享了自己的屏幕。 发送和接收的屏幕共享流的分辨率均为 1920 × 1080。

### 第一步，计算各用户订阅的视频总分辨率，以及时长用量

下表展示了如何计算每位用户接收视频流的总分辨率，从而得出各用户视频用量的档位和对应的单价：

| 用户              | 订阅的视频流                            | 视频的分辨率                                  | 总分辨率  | 总分辨率档位 | 时长（分钟） |
| :---------------- | :-------------------------------------- | :-------------------------------------------- | :-------- | :----------- | ------------ |
| 主播 A + 屏幕共享 | 主播B+主播C的视频流                     | 640 × 480 × 2                                 | 614,400   | 高清 (HD)    | 60           |
| 主播 B            | 主播A + 主播C + 主播 A 共享的屏幕视频流 | (960 × 720) + (640 × 480) + (1920 x 1080)     | 3,072,000 | 视频2K       | 60           |
| 主播 C            | 主播A +主播B + 主播 A 共享的屏幕视频流  | (960 × 720) + (640 × 480) + (1920 x 1080)     | 3,072,000 | 视频2K       | 60           |
| 观众 1            | 3 位主播 + 主播 A 共享的屏幕            | (960 × 720) + (640 × 480 × 2) + (1920 x 1080) | 3,379,200 | 视频2K       | 60           |
| 观众 2            | 3 位主播 + 主播 A 共享的屏幕            | (960 × 720) + (640 × 480 × 2) + (1920 x 1080) | 3,379,200 | 视频2K       | 60           |
| 观众 3            | 未订阅视频流，只订阅音频流              | -                                             | -         | 音频         | 60           |

示例图片：

![计费说明图例 -2@2x](https://qcloudimg.tencent-cloud.cn/raw/b9284fc7114058229815f4ce13168aa3.png)

### 第二步，查询对应档位单价，根据公式计算最终费用

按**月度费用** = **音频时长用量** × **音频单价** + **各档位视频时长用量** × **对应视频单价**计算上述场景的费用：

<table>
     <tr>
         <th style="text-align:center">收费服务（视频面积档位）</th>
         <th style="text-align:center">总时长用量（分钟） = 各用户时长用量总和</th>
         <th style="text-align:center">单价（美元/千分钟）</th>
         <th style="text-align:center">各服务费用（美元）</th>
         <th style="text-align:center">总费用（美元） （四舍五入至小数点后两位）</th>
     </tr>
     <tr>
         <td style="text-align:center">高清 (HD)</td>
         <td style="text-align:center">60 × 1 = 60</td>
         <td style="text-align:center">3.99</td>
         <td style="text-align:center">(60/1000) × 3.99 = 0.2394</td>
         <td style="text-align:center" rowspan="3">4.14</td>
     </tr>
     <tr>
         <td style="text-align:center">视频2K</td>
         <td style="text-align:center">60 × 4 = 240</td>
         <td style="text-align:center">15.99</td>
         <td style="text-align:center">(240/1000) × 15.99 = 3.8376</td>
     </tr>
 		 <tr>
         <td style="text-align:center">音频</td>
         <td style="text-align:center">60 × 1 = 60</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">(60/1000) × 0.99 = 0.0594</td>
     </tr>
</table>


## 计费示例2

本节举例说明 TRTC 如何计算费用。
假设有 6 位用户同时加入一个频道，并且进行了 60 分钟的视频互动直播。
在视频互动直播中，有 4 位主播（主播 A、B 、 C、D），A 、B、C主播直播设置的视频分辨率为 480 × 480，D主播仅推送音频流。1 位观众订阅了所有主播的视频流，另1位观众没有订阅视频流，仅订阅音频流。

### 第一步，计算各用户订阅的视频总分辨率，以及时长用量

下表展示了如何计算每位用户接收视频流的总分辨率，从而得出各用户视频用量的档位和对应的单价：

| 用户   | 订阅的视频流                                  | 视频的分辨率  | 分辨率之和 | 视频总分辨率档位 | 时长（分钟） |
| ------ | --------------------------------------------- | ------------- | ---------- | ---------------- | ------------ |
| 主播 A | 主播B + 主播C的视频流 + 主播D的音频流         | 480× 480 × 2  | 460,800    | 高清 (HD)        | 60           |
| 主播 B | 主播A + 主播C的视频流 + 主播D的音频流         | 480× 480 × 2  | 460,800    | 高清 (HD)        | 60           |
| 主播 C | 主播A + 主播B的视频流 + 主播D的音频流         | 480× 480 × 2  | 460,800    | 高清 (HD)        | 60           |
| 主播 D | 主播A + 主播B + 主播C的视频流                 | 480 × 480 × 3 | 691,200    | 高清 (HD)        | 60           |
| 观众 1 | 主播A + 主播B + 主播C的视频流 + 主播D的音频流 | 480 × 480 × 3 | 691,200    | 高清 (HD)        | 60           |
| 观众 2 | 未订阅视频流，只订阅音频流                    | -             | -          | 音频             | 60           |

### 第二步，查询对应档位单价，根据公式计算最终费用

按**月度费用** = **音频时长用量** × **音频单价** + **各档位视频时长用量** × **对应视频单价**计算上述场景的费用：

<table>
     <tr>
         <th style="text-align:center">收费服务（视频面积档位）</th>
         <th style="text-align:center">总时长用量（分钟） = 各用户时长用量总和</th>
         <th style="text-align:center">单价（美元/千分钟）</th>
         <th style="text-align:center">各服务费用（美元）</th>
         <th style="text-align:center">总费用（美元） （四舍五入至小数点后两位）</th>
     </tr>
     <tr>
         <td style="text-align:center">高清 (HD)</td>
         <td style="text-align:center">60 × 5 = 300</td>
         <td style="text-align:center">3.99</td>
         <td style="text-align:center">(300/1000) × 3.99 = 1.197</td>
         <td style="text-align:center" rowspan="3">1.26</td>
     </tr>
 		 <tr>
         <td style="text-align:center">音频</td>
         <td style="text-align:center">60 × 1 = 60</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">(60/1000) × 0.99 = 0.0594</td>
     </tr>
</table>


## 注意事项

本节提供更多注意事项以供参考。

### 价格计算器

请查看[TRTC价格计算器](https://intl.cloud.tencent.com/pricing/trtc/calculator)。

### 时长用量精度

TRTC 以秒为时长统计精度，以当月累计秒数转换成分钟数后进行计费。在每月底结算整月用量时，TRTC 会把当月产生的音频和各类型的视频用量（单位为秒）分别相加，然后除以 60，分别得出音频分钟数和各类型的视频分钟数，最后**向上**取整。例如一个月产生了 59 秒的音频时长用量，则音频用量数据计为 1 分钟；如果产生了 61 秒的视频时长用量，则视频用量数据计为 2 分钟。月用量误差在 1 分钟内。

### 双流分辨率

双流模式下，用户的分辨率计算方式如下：

-   如果订阅的是大流，则用户的集合分辨率根据发送端设置的大流分辨率计算。
-   如果订阅的是小流，则用户的集合分辨率根据用户实际收到的分辨率计算。

### 屏幕共享流的分辨率

如果你的场景中涉及屏幕共享，则屏幕共享流的视频单价以你在 `TRTCVideoEncParam` 中设置的视频分辨率为准。设置方法详见以下说明：

-   全平台 C++:[startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#ab1fc5a303726a666d30051c836e33fdd)
-   iOS：[startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf51acf26b2212192f7145468886b791) [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abebcd402e310d5d7dcbef9f6b601cfc4)
-   macOS: [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97)
-   Android:[startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aacbe76e164030701d261a2edbc43668f)

在 Web 端，由于设备和浏览器的限制，部分浏览器对设置的屏幕属性不一定能全部适配。这种情况下浏览器会自动调整分辨率，计费也将按照实际分辨率计算。详见[setScreenProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setScreenProfile)。

### 其他产品或服务计费

在你的场景中，如果除音视频通话、互动直播外还涉及其他 TRTC 产品或服务，如[云端录制](https://intl.cloud.tencent.com/document/product/647/45176)等，则需要额外收费。详见各 TRTC 产品或服务的计费说明。
