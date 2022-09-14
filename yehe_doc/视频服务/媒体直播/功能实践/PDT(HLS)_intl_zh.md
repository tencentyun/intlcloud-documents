您可以为HLS输出的Media Manifest设置EXT-X-PROGRAM-DATE-TIME标签，来关联具有绝对日期或时间的媒体段的第一个样本。具体格式为：

```
1  #EXT-X-PROGRAM-DATE-TIME:<date-time-msec>
```

其中 date-time-msec 是 ISO/IEC 8601:2004 [ISO_8601] 日期/时间， 表示，例如 YYYY-MM-DDThh:mm:ss.SSSZ。 它应该表明时区和秒的小数部分，精确到毫秒。

为HLS输出插入PDT，首先选择需要修改的**Channel**，并且进入到**Output Group Setting**编辑页面，只有当**Output Group Type**是如下类型时才能够设置：HLS、HLS_ARCHIVE、HLS_STREAM_PACKAGE 。
在**Segment Infomation**选择中，找到**PdtInsertion**开关，打开开关，并设置插入间隔，单位为秒，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/0863a6dc3e189d25d7c37c6e18d2af4d.png)
编辑完成后，启动频道。有输入后，即可在输出的M3u8中看到PDT标签，每600秒插入一次。





