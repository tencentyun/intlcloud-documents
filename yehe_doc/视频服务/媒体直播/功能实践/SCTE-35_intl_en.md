You can configure StreamLive to pass through SCTE-35 messages.

SCTE-35 messages are only carried by MPEG-2 TS inputs. Therefore, StreamLive can only pass through SCTE-35 messages for RTP_PUSH, UDP_PUSH, or SRT_PUSH inputs.

Find the target channel and click **Edit** to go to the **Output Group Setting** page. Find the output for which you want to configure SCTE-35 pass-through, and toggle on **Scte 35 Setting**.

![](https://qcloudimg.tencent-cloud.cn/raw/d55fb61889552e9b005f23908c0fa0dc.png)

It’s not enough to just enable SCTE-35 pass-through. For SCTE-35 messages to be visible in the output, you must also include PES payloads of the SCTE-35 messages in the input.

After enabling pass-through, you can use SCTE-35 messages to insert ads into different outputs.


