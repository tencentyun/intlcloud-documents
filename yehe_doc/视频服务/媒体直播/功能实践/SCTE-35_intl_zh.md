您可以配置StreamLive来处理SCTE-35消息。

在输入端，SCTE-35消息只能出现在包含MPEG-2 TS的输入中，这意味着只能选择如下几种类型的输入并开启透传SCTE-35功能才能有效：RTP_PUSH、UDP_PUSH、SRT_PUSH。

具体设置步骤为选择需要设置的Channel，通过编辑功能进入到**Output Group Setting**编辑页，找到需要设置SCTE-35透传的Outputs，打开**Scte 35 Setting**选项即可。

![](https://qcloudimg.tencent-cloud.cn/raw/d55fb61889552e9b005f23908c0fa0dc.png)

打开此功能后，并不代表在输出中就能看到SCTE-35信息了，还需要在Input输入中携带SCTE-35的PES负载才能实现传递。

在输出端，如果设置为传递，则可以在每个输出中使用来自SCTE-35的消息传递，为适合该输出类型的广告插播信息。


