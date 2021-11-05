> !
>
> -   本文档仅针对使用 [TRTC 提供的 MCU 集群进行云端混流转码](https://intl.cloud.tencent.com/document/product/647/34618) 产生的旁路转码费用作出相关说明。若您将 TRTC 的音视频流旁路推流到云直播后，再使用 [云直播提供的云端混流功能](https://intl.cloud.tencent.com/document/product/267/37665)，云直播将向您收取 [直播转码](https://intl.cloud.tencent.com/document/product/267/39604) 费用。
> -   若您将转码后输出的音视频流转推到云直播系统中，让观众 [实现 CDN 直播观看](https://intl.cloud.tencent.com/document/product/647/35242)，云直播将向您收取 [流量/带宽](https://intl.cloud.tencent.com/document/product/267/2818#.E6.B5.81.E9.87.8F.E5.B8.A6.E5.AE.BD) 费用。
> -   如果你已与我们的销售签约，则实际计费信息以合同为准。

<span id="Billing_items"></span>

## 单价

TRTC 云端混流转码服务的单价如下：

| 编码方式 | 计费项                   | 单价（美元/千分钟）（四舍五入至小数点后三位） |
| -------- | ------------------------ | --------------------------------------------- |
| 音频转码 | 旁路转码-语音            | 0.799                                         |
| H.264    | 旁路转码-H264-标清 SD    | 2.296                                         |
| H.264    | 旁路转码-H264-高清 HD    | 4.643                                         |
| H.264    | 旁路转码-H264-全高清 FHD | 8.990                                         |

<span id="Billing_method"></span>

## 用量统计方式

实时音视频 TRTC 按同一 [腾讯云账号](https://console.intl.cloud.tencent.com/trtc)下所有应用通过 MCU 混流转码后输出的**转码时长**来统计旁路转码服务的用量。转码时长根据编码方式和转码结果的不同，分为 [视频时长](#m_video) 和 [音频时长](#m_voice)。

> ! 时长统计精度为秒，按日累计秒数转换成分钟数后进行计费，不足一分钟按一分钟计。

<span id="m_video"></span>

### 视频时长

视频时长指转码结果中包含视频画面的时间。TRTC 会根据转码后输出的视频分辨率划分视频档位，然后分别对不同档位的视频时长进行计费。视频档位与分辨率的对应关系如下表所示：

| 视频档位           | 输出分辨率                                                |
| ------------------ | --------------------------------------------------------- |
| 标清 （SD）        | 输出分辨率 ≤ 307,200（640 × 480）                         |
| 高清 （HD）        | 307,200（640 × 480）＜ 输出分辨率 ≤ 921,600（1280 × 720） |
| 全高清 （Full HD） | 921,600（1280 × 720）＜ 输出分辨率                        |

-   转码后输出的同一条流在同一时间内，既有视频又有音频时，只按视频时长统计，不会重复计算音频时长。
-   转码后输出的同一条流的分辨率可能会发生变化，TRTC 将分段统计服务用量，通常情况下 60 秒更新一次，当分辨率发生变化时则立即上报更新。

<span id="m_voice"></span>

### 音频时长

音频时长指转码结果中只有纯音频的时间。

<span id="Fixed_price"></span>

## 计费示例

假设客户 A 在 01 月 01 日使用 TRTC 的 MCU 集群进行云端混流转码，使用 H.264 编码方式，输出 1920 × 1080、640 × 360 分辨率的视频各 100 分钟，同时使用音频转码，输出音频时长 100 分钟。

则 01 月 02 日用户 A 需要支付 01 月 01 日产生的旁路转码费用为

<table>
     <tr>
         <th style="text-align:center">输出分辨率</th>
         <th style="text-align:center">视频档位</th>
         <th style="text-align:center">时长（分钟）</th>
         <th style="text-align:center">单价（美元/千分钟）</th>
         <th style="text-align:center">各服务费用（美元）</th>
         <th style="text-align:center">总费用（美元）（四舍五入至小数点后两位）</th>
     </tr>
     <tr>
         <td style="text-align:center">1920 × 1080</td>
         <td style="text-align:center">全高清 FHD</td>
         <td style="text-align:center">100</td>
         <td style="text-align:center">8.990</td>
         <td style="text-align:center" >0.899</td>
         <td style="text-align:center" rowspan="3">1.44</td>
     </tr>
     <tr>
         <td style="text-align:center">640 × 360</td>
         <td style="text-align:center">高清 HD</td>
         <td style="text-align:center">100</td>
         <td style="text-align:center">4.643</td>
         <td style="text-align:center">0.464</td>
     </tr>
     <tr>
         <td style="text-align:center">音频</td>
         <td style="text-align:center">音频</td>
         <td style="text-align:center">100</td>
         <td style="text-align:center">0.799</td>
         <td style="text-align:center">0.0799</td>
     </tr>
</table>

## 注意事项

本节提供更多注意事项以供参考。

### 日结账单

即日结的支付方式。TRTC 云端混流转码服务仅支持**日结后付费**的方式，按日计费，每天上午 10 点扣除前一天产生的费用。

<span id="Billing_examples"></span>
