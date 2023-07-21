
## 广告插入功能
随着音视频在互联网技术和应用中的发展，视频广告已经是目前一种主流的广告投放方式，在腾讯云音视频产品Stream Service上，可以实现基于SCTE-35和SSAI的动态广告插入，SSAI的完整大致流程如下：

![](https://qcloudimg.tencent-cloud.cn/raw/3d7f3f8f5ba9186e284d96458364a2b3.png)

1）推流端推送直播流到StreamLive进行转码、封装和广告SCTE-35事件标识的插入，并传输到StreamPackage。如果没有后续的流程，1）已经完成了CSAI中关于服务端的所有步骤。
2）播放端请求manifest(m3u8/mpd)，StreamPackage收到回源相关信息同时解析m3u8/mpd，检查scte-35标签。
3）StreamPackage请求Ad Decision Server，解析VAST/VMAP响应并获取广告视频地址。
4）下载广告视频、转码并存储。
5）将转码后的广告分片地址通过插入和替换更新到m3u8/mpd中并分发。
6）StreamPackage在客户端播放广告时上报至广告Tracking服务进行跟踪（Track）。

如果使用此广告插入功能，将产生[广告插入费用](https://www.tencentcloud.com/document/product/1063/50091)。

### 1. 开启广告替换功能
对于需要配置广告替换功能的频道，点击此频道进入到详情页面，StreamPackage的广告替换功能是基于Endpoint维度进行配置的：

![](https://qcloudimg.tencent-cloud.cn/raw/e820b2dda085733f139fc685ad6a016b.png)

点击**AD Configuration**，进入配置页面，页面中主要包括这几种配置：

- **Ad decision server**：ADS（ad decision server）服务的访问地址。
- **Configuration aliases**：个性化广告中，用于动态参数替换的规则。
- **Personalization details**：个性化广告中断时，用于兜底的默认广告播放方案。
- **Advanced settings**：其它高级配置。


### 2. 配置ADS地址模板
![](https://qcloudimg.tencent-cloud.cn/raw/16cdc5256cb736d949af14e5a84e1eb2.png)
ADS服务在此是指为StreamPackage提供广告内容的源站服务，ADS将决定每次的广告播放内容。请输入以http://或者https://开头的地址，最长支持25000个字符。

### 3. 配置个性化替换参数
可以通过点击右侧的按钮来添加参数、删除参数。参数名词可以支持数字、字母、下划线(_)、连字符(-)，最长32个字符。
![](https://qcloudimg.tencent-cloud.cn/raw/db2f8ab197d1741e60b0fdda12b6d5c8.png)

创建参数后，可以在参数下维护**alias key**、**alias value**。当为获取广告内容，向ADS发起访问请求时，StreamPackage会将访问请求中的**alias key**值，替换成相应的**alias value**值，以实现个性化广告。

一个具体的使用案例如下：
#### 1）ADS地址模板配置
```
https://my.ads.com/path?ad_type=[player_params.ad_type]&region=[player_params.region]
```

#### 2）个性化替换参数配置
```
"ConfigurationAliases": {
    "player_params.ad_type": {
        "customized": "abc",
        "default": "default"
    },
    "player_params.region": {
        "india": "ap-mumbai",
        "japan": "ap-tokyo"
    },
}
```

#### 3）在对StreamPackage的请求URL中，添加对应的key-value值
```
<master>.m3u8?ad_type=customized&region=india
```

#### 4）此时，StreamPackage向ADS发送的request url为
```
https://my.ads.com/path?ad_type=abc&region=ap-mumbai
```

### 4. 配置兜底广告播放方案
针对个性化广告不足以填充预留广告时长的场景，例如：个性化广告时长太短、由于网络或者其它原因未成功获取到个性化广告，您可以在**Slate ad** 设置兜底的默认广告，请输入以http://或者https://开头的地址，最长支持25000个字符。

![](https://qcloudimg.tencent-cloud.cn/raw/c06a36db8c817361e6a298331b95a98a.png)

如果不设置**Slate ad**，在遇到以上意外情况下，系统为了保障用户体验，将跳过广告播放环节，继续播放原视频流。您还可以通过设置**Personalization threshold**来设定时间阈值，如果广告空白的时间达到此阈值，即切换到播放原视频流。


### 5. 其它高级配置
![](https://qcloudimg.tencent-cloud.cn/raw/da1325577ee521b3c158fbd15d36991c.png)
- **Ad marker passthrough**：开启或者关闭广告标记透传功能。
- **DASH mpd location**：开启或者关闭DASH的一致性HTTP重定向。
- **SCTE-35 ad message type**：配置将输入视频流中的哪些标记信息作为广告标记进行处理。

### 6. 替换前后的manifest示例
下面示例提供了源流manifest和替换后的个性化manifest对比

#### 源流manifset示例
StreamPackage从源流中获取到的HLS master manifest示例：
```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-INDEPENDENT-SEGMENTS
#EXT-X-STREAM-INF:PROGRAM-ID=0,BANDWIDTH=500000,RESOLUTION=640x360
tx_ssai_temp1.m3u8
#EXT-X-STREAM-INF:PROGRAM-ID=0,BANDWIDTH=2000000,RESOLUTION=960x540
tx_ssai_temp2.m3u8
#EXT-X-STREAM-INF:PROGRAM-ID=0,BANDWIDTH=3000000,RESOLUTION=1280x720
tx_ssai_temp3.m3u8
```
StreamPackage从源流中获取到的插入了SCTE-35标签的HLS media manifest：
```
#EXTM3U
#EXT-X-VERSION:5
#EXT-X-MEDIA-SEQUENCE:3835222
#EXT-X-TARGETDURATION:6
#EXTINF:6.000, no desc seq 3835223
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907362016.ts?&3835223
#EXTINF:2.333, no desc seq 3835224
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907368016.ts?&3835224
#EXT-OATCLS-SCTE35:/AAgAAHwulfuAAAADwUAAACcAPCAAA27oAAAAAAAAPKrLtw=
#EXT-X-CUE-OUT:10
#EXTINF:3.667, no desc seq 3835225
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907370349.ts?&3835225
#EXT-X-CUE-OUT-CONT:ElapsedTime=3.667,Duration=10,SCTE35=/AAgAAHwulfuAAAADwUAAACcAPCAAA27oAAAAAAAAPKrLtw=
#EXTINF:6.000, no desc seq 3835226
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907374016.ts?&3835226
#EXT-X-CUE-OUT-CONT:ElapsedTime=9.667,Duration=10,SCTE35=/AAgAAHwulfuAAAADwUAAACcAPCAAA27oAAAAAAAAPKrLtw=
#EXTINF:0.333, no desc seq 3835227
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907380016.ts?&3835227
#EXT-X-CUE-IN
#EXTINF:5.667, no desc seq 3835228
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907380349.ts?&3835228
#EXTINF:6.000, no desc seq 3835229
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907386016.ts?&3835229
#EXTINF:6.000, no desc seq 3835230
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907392016.ts?&3835230
```
#### 个性化manifest示例

StreamPackage生成的个性化的HLS master manifest：
```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-INDEPENDENT-SEGMENTS
#EXT-X-STREAM-INF:PROGRAM-ID=0,BANDWIDTH=500000,RESOLUTION=640x360
tx_ssai_temp1.m3u8?session_id=fd320a4d99ba7df952f5a214ed901935&type=manifest
#EXT-X-STREAM-INF:PROGRAM-ID=0,BANDWIDTH=2000000,RESOLUTION=960x540
tx_ssai_temp2.m3u8?session_id=fd320a4d99ba7df952f5a214ed901935&type=manifest
#EXT-X-STREAM-INF:PROGRAM-ID=0,BANDWIDTH=3000000,RESOLUTION=1280x720
tx_ssai_temp3.m3u8?session_id=fd320a4d99ba7df952f5a214ed901935&type=manifest
```

StreamPackage生成的个性化的HLS media manifest：
```
#EXTM3U
#EXT-X-VERSION:5
#EXT-X-MEDIA-SEQUENCE:3835222
#EXT-X-TARGETDURATION:6
#EXTINF:6.000, no desc seq 3835223
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907362016.ts?&3835223
#EXTINF:2.333, no desc seq 3835224
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907368016.ts?&3835224
#EXT-X-DISCONTINUITY
#EXTINF:2.000,
segment?type=segment&session_id=fd320a4d99ba7df952f5a214ed901935&manifest_num=tx_ssai_temp3.m3u8&seq_num=3835224
#EXTINF:2.000,
segment?type=segment&session_id=fd320a4d99ba7df952f5a214ed901935&manifest_num=tx_ssai_temp3.m3u8&seq_num=3835225
#EXTINF:2.000,
segment?type=segment&session_id=fd320a4d99ba7df952f5a214ed901935&manifest_num=tx_ssai_temp3.m3u8&seq_num=3835226
#EXTINF:2.000,
segment?type=segment&session_id=fd320a4d99ba7df952f5a214ed901935&manifest_num=tx_ssai_temp3.m3u8&seq_num=3835227
#EXTINF:2.000,
segment?type=segment&session_id=fd320a4d99ba7df952f5a214ed901935&manifest_num=tx_ssai_temp3.m3u8&seq_num=3835228
#EXT-X-DISCONTINUITY
#EXTINF:5.667, no desc seq 3835228
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907380349.ts?&3835228
#EXTINF:6.000, no desc seq 3835229
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907386016.ts?&3835229
#EXTINF:6.000, no desc seq 3835230
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907392016.ts?&3835230
```