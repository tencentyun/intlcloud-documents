The delayed playback feature is useful if you want StreamLive to ingest input in real time, but do not want to process the content or generate an output immediately. Delayed playback allows you to hold an input for a specified period of time before it’s transcoded and packaged for output. Currently, this feature only works for RTMP_PUSH inputs. Follow the steps below to configure delayed playback:
1. Click the input for which you want to configure delayed playback. If the input is bound to a channel that is currently running, you need to stop the channel first.
![](https://qcloudimg.tencent-cloud.cn/raw/9b45272668f6d18330fc932df4c9a4d0.png)
2. Click **Edit**, toggle on **Delay Time**, and specify the delay time (10-600 seconds).
![](https://qcloudimg.tencent-cloud.cn/raw/65f41a79185c43c1a3c7ab76bd192f53.png)

Click **Confirm**. Now, instead of generating outputs immediately, the input will be processed only after the specified delay time.

