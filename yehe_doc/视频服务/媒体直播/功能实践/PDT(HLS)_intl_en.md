You can configure EXT-X-PROGRAM-DATE-TIME tags for the output media manifest of HLS streams to associate the first media segment with an absolute date and time. The format is as follows:

```
1  #EXT-X-PROGRAM-DATE-TIME:<date-time-msec>
```

The format of `date-time-msec` is ISO/IEC 8601:2004 [ISO_8601] (YYYY-MM-DDThh:mm:ss.SSSZ). It must specify the time zone and have a millisecond precision.

Insert PDT tags in HLS streams. Find the target channel and click **Edit** to go to the **Output Group Setting** page. You can configure EXT-X-PROGRAM-DATE-TIME tags only if the **Output Group Type** is HLS, HLS_ARCHIVE, or HLS_STREAM_PACKAGE.
In the **Segment Information** area, toggle on **PdtInsertion** and specify the interval (seconds) to insert the tags.
![](https://qcloudimg.tencent-cloud.cn/raw/0863a6dc3e189d25d7c37c6e18d2af4d.png)
After the configuration, start the channel. When input is available, you will see PDT tags in the output M3U8 streams, which are inserted every 600 seconds.





