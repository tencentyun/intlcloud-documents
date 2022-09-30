进入控制台[Flow Management](https://console.tencentcloud.com/mdc/flow)页面，在列表中点击某一条Flow，即可查看该Flow的详细信息。

![](https://qcloudimg.tencent-cloud.cn/raw/8761f3d6e89cd2ef43c7a1531baceeb0.png)

## 基本信息 Information
![](https://qcloudimg.tencent-cloud.cn/raw/849236bd82f00c864ec0ba5a4a8e03bc.png)
在**Information**中，可以查看 Flow ID， Flow Name， Input Region，当前状态以及 最大带宽。

## 输入源信息 Input Source
![](https://qcloudimg.tencent-cloud.cn/raw/08335f06efbb8d4699a50b1acd7f86b5.png)
在**Input Source**中，可以查看 包括Input Source Name， Input地址，白名单配置，以及 协议相关的设置。

## 输出信息 Output
![](https://qcloudimg.tencent-cloud.cn/raw/900b528fbc1d55552c7c520d74c18a7a.png)
在**Output**中，可以查看所选Flow的所有Output，列表中会显示：

- **Name**: Output的名字。
- **Output ID**: Output的ID。
- **Output Region**： Output所在的区域，Flow会将流传输到此区域。
- **Output IP**：Output输出节点的IP地址。
- **Protocol**：Output的输出协议。
- **URL**： 若Output支持拉流，则可以在此获取拉流地址

另外，您可以在此页面对 Output 进行创建、编辑、删除等操作。

## 日志信息 Log
![](https://qcloudimg.tencent-cloud.cn/raw/2ed506e30a7bf706805ae2d29986454b.png)
在**Log**中，可以查看Flow运行过程中的各种事件信息，包括：推流、断流、拉流被IP白名单拒绝等等。

## 健康信息 Health
可以查看当前流的各项指标，包括：帧率、码率等等。
### 源 Input Source
可以查看近一个小时的推流、拉流质量。也可以在时间选择窗口选取其他时间段，来查看其它时间段的质量信息。
![](https://qcloudimg.tencent-cloud.cn/raw/f4f10f4d37873fce43c3d88def9eaef0.png)

在视频Video以及音频Audio曲线中，可以通过点击相应按钮来选择查看码率或者帧率。如果有多路音频，您可以在下拉选择框中选择不同的音频查看其码率或者帧率。
![](https://qcloudimg.tencent-cloud.cn/raw/ef3502d0afb338f4c64b673379dd25cf.png)

若是SRT协议，您还可以页面在最下方，查看SRT的链路质量，包括:
- **Packet Loss Rate**：SRT链路的丢包率，可以衡量链路的稳定性，若丢包率小于20% 一般还能正常流畅的传输。
- **Retransmission Rate**：SRT链路的重传率，若重传率远小于丢包率，则表明链路异常，这种情况下直播流会有卡顿甚至断流。
- **RTT**：RTT用于衡量链路延时，RTT越大链路延时越高，需要把SRT的Latency设置的越大。Latency 一般推荐为RTT的4倍。若RTT曲线抖动非常厉害，则说明链路质量不稳定，极端情况下可能会导致丢包严重。
- **Number Of Dropped Packets**：SRT 协议栈主动丢包数量，这种丢包的发生是因为协议栈认为当前包的延时已经超过设置的 Latency，再次传输已经没有意义，故此会丢掉。当出现这种丢包时，一般会导致画面花屏，说明推流侧带宽不够，或者链路RTT过高，需要调大Latency。

![](https://qcloudimg.tencent-cloud.cn/raw/720784ac0a25685da1c75d8a1aeeaea1.png)

### 输出 Output
Output下信息与Input大致相同，不过由于Output数量可能有很多，您可以在搜索框中选择您需要查看的Output。
![](https://qcloudimg.tencent-cloud.cn/raw/2563d297d6ee371f8f31b3010578a8b9.png)