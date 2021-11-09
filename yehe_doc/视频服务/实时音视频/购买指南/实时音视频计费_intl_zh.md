# 实时音视频计费

本文介绍 TRTC 如何按月统计使用[语音通话](https://intl.cloud.tencent.com/document/product/647/36064)、[视频通话](https://intl.cloud.tencent.com/document/product/647/36063)、[音视频互动直播](https://intl.cloud.tencent.com/document/product/647/36059)的费用。

如果你已与我们的销售签约，则实际计费信息以合同为准。

## 费用组成

每月结束时，TRTC 会统计你 [腾讯云账号](https://console.intl.cloud.tencent.com/trtc)下所有项目当月产生的音频和视频时长用量（单位为分钟）。需注意，视频时长用量按照集合分辨率分为三个档位，分档定价。扣除 TRTC 为每个开发者账号提供的[每月一万分钟免费分钟数](https://intl.cloud.tencent.com/document/product/647/42735)后，TRTC 将剩余的音频时长用量和视频时长用量乘以对应的单价，最后相加得出本月总费用。

基础的计费公式如下：

**月度费用** = **音频时长用量** × **音频单价** + **各档位视频的时长用量** × **相应视频单价**

### 时长用量

每个会话的时长用量，是这个会话中**所有用户产生的时长用量之和**。

-   **视频时长用量**：如果用户成功订阅了视频流，则产生视频用量。注意，如果同时订阅音频流和视频流，只计算视频用量。
-   **音频时长用量**：如果用户没有订阅视频流，则无论其是否订阅了音频流，都会产生音频用量。

### 单价

音视频时长用量的单价如下：

| 用量类型          | 单价（美元/千分钟） |
| :---------------- | :------------------ |
| 音频              | 0.99                |
| 标清（SD）        | 1.99                |
| 高清（HD）        | 3.99                |
| 全高清（Full HD） | 14.99               |

TRTC 根据用户接收到的所有视频的集合分辨率，将视频分为如下三个类型并分别计算各类型视频的费用：

| 视频用量类型      | 用户订阅视频的集合分辨率                                  |
| :---------------- | :-------------------------------------------------------- |
| 标清（SD）        | 集合分辨率 ≤ 307,200（640 × 480）                         |
| 高清（HD）        | 307,200（640 × 480）＜ 集合分辨率 ≤ 921,600（1280 × 720） |
| 全高清（Full HD） | 921,600（1280 × 720）＜ 集合分辨率                        |

例如，用户 A 同时订阅 2 路分辨率为 960 × 720 的视频流，则该用户订阅的视频集合分辨率为 960 × 720 + 960 × 720 = 1,382,400，其视频用量按全高清（Full HD）类型的单价计费。

## 预付费套餐包

TRTC 为您提供音视频通用[套餐包](https://intl.cloud.tencent.com/document/product/647/42736)，可按照**1:2:4:15**分别抵扣语音、标清 SD、高清 HD 和全高清 FHD 时长，例如 1 分钟高清 HD 视频时长扣除 4 分钟通用套餐包时长。

通用套餐包定价如下表所示：

<table>
     <tr>
         <th style="text-align:center">套餐包类型</th>  
         <th style="text-align:center">套餐包时长（千分钟）</th> 
         <th style="text-align:center">刊例价（美元/千分钟）</th> 
         <th style="text-align:center">套餐内单价（美元/千分钟）</th> 
         <th style="text-align:center">套餐包价格（美元）</th> 
          <th style="text-align:center">折扣</th> 
     </tr>
     <tr>
         <td style="text-align:center" rowspan="4">固定套餐包</td>   
         <td style="text-align:center">25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center">24</td>   
         <td style="text-align:center">3% off</td>     
     </tr> 
     <tr>
         <td style="text-align:center">250 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center">227</td>   
         <td style="text-align:center">8% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center">856</td>   
         <td style="text-align:center">13.5% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center">3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center">2416</td>   
         <td style="text-align:center">18.7% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="5">自定义套餐包</td>   
         <td style="text-align:center">0 ＜ T ＜ 25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center" rowspan="5">套餐内单价*套餐包时长 T</td>   
         <td style="text-align:center"> original </td>    
     </tr> 
     <tr>
         <td style="text-align:center">25 ≤ T ＜ 250</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center">3% off</td>    
     </tr> 
     <tr>
         <td style="text-align:center">250 ≤ T ＜ 1000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center">8% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 ≤ T ＜ 3000</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center">13.5% off</td>   
     </tr> 
     <tr> 
         <td style="text-align:center">T ≥ 3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center">18.7% off</td>   
     </tr> 
</table>

> ?
>-   表格中套餐内单价按每千分钟单价向上取整精确到小数点后 3 位，实际计费按每分钟单价精确到小数点后 8 位。详情说明
>-   目前使用 TRTC 预付费服务需要进行白名单审核，请[联系我们](https://intl.cloud.tencent.com/contact-us)进行开通。
>-   如果您的月均分钟数超过 3M 分钟，并希望获得进一步的支持与报价服务，请[联系销售](https://intl.cloud.tencent.com/contact-us)。

## 计费示例

本节说明 TRTC 如何计算视频的集合分辨率、每种服务类型的时长用量以及相关费用。

假设有 5 位用户同时加入一个频道，并且进行了 60 分钟的视频互动直播。 在视频互动直播中，有 3 位主播（主播 A、B 和 C），A 主播的视频分辨率为 960 × 720，B 和 C 主播的视频分辨率为 640 × 480。2 位观众订阅了所有主播的视频流。 此外，主播 A 向频道中的所有其他用户共享了自己的屏幕。 发送和接收的屏幕共享流的分辨率均为 1920 × 1080。

### 计算视频的集合分辨率

下表展示了如何计算每位用户订阅视频流的集合分辨率，以确定各用户视频用量的类型和单价：

| 用户              | 订阅的视频流                 | 视频的集合分辨率                              | 总分辨率  | 视频用量类型 |
| :---------------- | :--------------------------- | :-------------------------------------------- | :-------- | :----------- |
| 主播 A + 屏幕共享 | 2 位主播                     | 640 × 480 × 2                                 | 614,400   | 高清 (HD)    |
| 主播 B            | 2 位主播 + 主播 A 共享的屏幕 | (960 × 720) + (640 × 480) + (1920 x 1080)     | 3,072,000 | 全高清 (FHD) |
| 主播 C            | 2 位主播 + 主播 A 共享的屏幕 | (960 × 720) + (640 × 480) + (1920 x 1080)     | 3,072,000 | 全高清 (FHD) |
| 观众 1            | 3 位主播 + 主播 A 共享的屏幕 | (960 × 720) + (640 × 480 × 2) + (1920 x 1080) | 3,379,200 | 全高清 (FHD) |
| 观众 2            | 3 位主播 + 主播 A 共享的屏幕 | (960 × 720) + (640 × 480 × 2) + (1920 x 1080) | 3,379,200 | 全高清 (FHD) |

### 计费

下表展示了如何计算视频互动直播中产生的总费用：

<table>
     <tr>
         <th style="text-align:center">收费服务（视频用量类型）</th>
         <th style="text-align:center">总时长用量（分钟） = 各用户时长用量总和</th>
         <th style="text-align:center">单价（美元/千分钟）</th>
         <th style="text-align:center">各服务费用（美元）</th>
         <th style="text-align:center">总费用（美元） （四舍五入至小数点后两位）</th>
     </tr>
     <tr>
         <td style="text-align:center">高清 (HD)</td>
         <td style="text-align:center">60</td>
         <td style="text-align:center">3.99</td>
         <td style="text-align:center">(60/1000) × 3.99 = 0.2394</td>
         <td style="text-align:center" rowspan="2">13.68</td>
     </tr>
     <tr>
         <td style="text-align:center">全高清 (FHD)</td>
         <td style="text-align:center">60 × 4 = 240</td>
         <td style="text-align:center">14.99</td>
         <td style="text-align:center">(240/1000) × 14.99 = 13.44</td>
     </tr>
</table>

## 注意事项

本节提供更多注意事项以供参考。

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

在你的场景中，如果除视频通话、互动直播外还涉及其他 TRTC 产品或服务，如[云端混流转码](https://intl.cloud.tencent.com/document/product/647/38929)等，则需要额外收费。详见各 TRTC 产品或服务的计费说明。
