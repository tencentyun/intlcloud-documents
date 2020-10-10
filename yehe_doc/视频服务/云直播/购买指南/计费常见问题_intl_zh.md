## 直播计费相关

<span id="live_que1"></span>
### 云直播有哪些计费项？如何知道我需要支付哪些费用？
云直播的计费项包含基础计费和增值计费。

- 基础费用：流量/带宽为基础计费，即您与加速源站建立连接产生的下行费用，可理解为只要您的直播内容有用户观看就会产生流量/带宽费用。
>?流量计费和带宽计费二选一，详细单价请参见 [结算明细](https://intl.cloud.tencent.com/document/product/267/2818#traffic-and-bandwidth)，切换方式请参见 [账单方式变更](https://intl.cloud.tencent.com/document/product/267/30411)。
- 增值计费：包括转码、录制、截图、鉴黄，上述四项功能默认关闭，您开启并使用后即会产生相应的费用，详细单价请参见 [结算明细](https://intl.cloud.tencent.com/document/product/267/2818#lvb-transcoding)。

<span id="live_que2"></span>
### 如何知道我是否欠费？
登录 [腾讯云直播控制台](https://console.cloud.tencent.com/live)，通过单击右上方的【费用】可进入费用概览页面，若您的可用余额小于0＄，则为欠费状态。请您及时充值，以免影响云直播和其他服务。

<span id="live_que3"></span>
### 直播上行推流收费吗？
云直播上行推流不收取费用，仅收取下行的流量费用。

<span id="live_que4"></span>
### 增值服务费用什么时候开始计算？
录制、截图、鉴黄、水印等关联推流域名的增值服务，在开启后推流即开始计费。转码等关联播放域名的增值服务，在开始拉流播放时开始计费（即创建并关联了转码模板，不拉流播放就不会产生转码费用），云端混流则在开启混流任务的时候开始计费。当您已开启添加水印或云端混流功能时，将可能产生标准转码费用，分辨率以您输出的直播流分辨率为准。



## 转码计费相关

<span id="tran_que1"></span>
### 直播转码是怎么收费的？如何预估转码费用？
云直播转码根据实际转码的编码方式、分辨率和相应时长进行计费，直播混流和添加水印亦是经由转码模块处理，会产生转码费用，详细请参考 [转码计费](https://intl.cloud.tencent.com/document/product/267/2818#lvb-transcoding)。
同一直播流、同一码率在多人观看情况下仅收取一份转码费用。

<span id="tran_que2"></span>
### 我并没有使用直播转码，为什么会产生转码账单？
云直播转码包括直播实时转码、云端混流和添加水印三种，若您使用了混流或水印功能亦会产生转码账单。

<span id="tran_que3"></span>
### 直播混流是不是必须产生转码费用？
是，会按照混流后的输出直播流收取转码费用。由于混流任务成功后不播放也消耗转码资源，混流的转码费用会按照混流时长进行收费，跟普通转码的播放时长计费有区别。



## 录制计费相关
<span id="record_que1"></span>
### 云直播的录制费用是如何收取的？
云直播的录制功能计费是以当月并发录制峰值为计费值的，在一个统计周期内录制路数的总和为并发峰值路数。单条直播流录制为一种文件，记为一路录制，若您录制为两种格式（MP4 和 HLS）则记为两路录制。

<span id="record_que2"></span>

### 直播录制路数峰值如何计算？
一路直播流（一个流 ID）录制一种格式文件，即为一路直播录制任务，每5分钟查询一次当前录制任务数，取当月取样点的最大值作为录制计费的路数月峰值。
**示例：**

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">流 ID</th>
<th rowspan=2 width="10%" style="text-align:center;">录制文<br>件格式</th>
<th colspan=7 width="50%" style="text-align:center;">当月（01日 - 30日）</th>
</tr><tr>
<td style="text-align:center;">01日</td><td style="text-align:center;">02日</td><td style="text-align:center;">03日</td>
<td style="text-align:center;">……</td>
<td style="text-align:center;">28日</td><td style="text-align:center;">29日</td><td style="text-align:center;">30日</td>
</tr><tr>
<td rowspan=4 style="text-align:center;">A</td>
<td style="text-align:center;">HLS</td><td></td><td></td><td></td>
<td rowspan=13 style="text-align:center;">没有进行录制</td>
<td id="ye"></td><td id="ye"></td>
<td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td>
</tr><tr>
<td rowspan=4 style="text-align:center;">B</td>
<td style="text-align:center;">HLS</td><td></td><td id="gr"></td><td id="gr"></td><td id="gr"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td id="gr"></td><td id="gr"></td><td></td><td id="gr"></td><td id="gr"></td><td></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td></td><td id="gr"></td><td></td><td id="gr"></td><td></td><td id="gr"></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td></td><td id="gr"></td><td></td><td id="gr"></td><td></td><td></td>
</tr><tr>
<td rowspan=4 style="text-align:center;">C</td>
<td style="text-align:center;">HLS</td><td id="br"></td><td></td><td id="br"></td><td id="br"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td></td><td></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td></td><td></td><td></td><td id="br"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td></td><td></td><td></td><td></td><td></td><td id="br"></td>
</tr><tr>
<td colspan=2 style="text-align:center;">录制路数</td>
<td style="text-align:center;">5</td><td style="text-align:center;">7</td><td style="text-align:center;">6</td><td style="text-align:center;">11</td><td style="text-align:center;">6</td><td style="text-align:center;">5</td>
</tr><tr>
<td colspan=2 style="text-align:center;">录制路数峰值</td><td colspan=7 style="text-align:center;">11</td>
</tr>
</table>

>? 
>- 黄色：代表流 ID **A** 下的录制任务。
>- 绿色：代表流 ID **B** 下的录制任务。
>- 蓝色：代表流 ID **C** 下的录制任务。


