Go to the [Flow Management](https://console.tencentcloud.com/mdc/flow) page of the StreamLink console. Click a flow to view its details.

![](https://qcloudimg.tencent-cloud.cn/raw/8761f3d6e89cd2ef43c7a1531baceeb0.png)

## Basic Information
![](https://qcloudimg.tencent-cloud.cn/raw/849236bd82f00c864ec0ba5a4a8e03bc.png)
Under the **Information** tab, you can view the flow ID, flow name, input region, flow status, and max bandwidth.

## Input Source
![](https://qcloudimg.tencent-cloud.cn/raw/08335f06efbb8d4699a50b1acd7f86b5.png)
Under the **Input Source** tab, you can view the source name, source address, allowlist, and protocol settings.

## Output
![](https://qcloudimg.tencent-cloud.cn/raw/900b528fbc1d55552c7c520d74c18a7a.png)
Under the **Output** tab, you can view the information of a flow’s outputs.

- **Name**: The output name.
- **Output ID**: The output ID.
- **Output Region**: The output region, which is the region a stream is sent to.
- **Output IP**: The IP address where the output is sent.
- **Protocol**: The output protocol.
- **URL**: The playback URL (if an output supports playback).

You can also create, edit, or delete an output on this page.

## Log
![](https://qcloudimg.tencent-cloud.cn/raw/2ed506e30a7bf706805ae2d29986454b.png)
Under the **Log** tab, you can view the events that occurred while a flow is running, such as stream pushed, stream interrupted, and IP address blocked.

## Health
Under the **Health** tab, you can view stream performance indicators such as frame rate and bitrate.
### Input source
You can view transport quality in the past hour. You can also view quality data in a specified time range.
![](https://qcloudimg.tencent-cloud.cn/raw/f4f10f4d37873fce43c3d88def9eaef0.png)

In the **Video** and **Audio** sections, you can view the bitrate and frame rate of the stream by selecting the corresponding tab. If the stream has more than one audio track, you can view the information of a specific audio track by selecting it from the drop-down list.
![](https://qcloudimg.tencent-cloud.cn/raw/ef3502d0afb338f4c64b673379dd25cf.png)

If the input protocol is SRT, you can also view performance indicators of the SRT transmission at the bottom of the page.
- **Packet Loss Rate**: The packet loss rate of the SRT transmission. This measures the stability of a transmission. Normally, to ensure smooth transmission, the packet loss rate must be lower than 20%.
- **Retransmission Rate**: The retransmission rate of the SRT transmission. A retransmission rate that is markedly lower than the packet loss rate usually indicates stutter or even stream interruption.
- **RTT**: RTT measures the latency of the transmission. High RTT indicates high latency, which means you need to set the SRT latency value high as well. The recommended SRT latency value is four times the RTT. If the RTT changes dramatically, it indicates unstable transmission and may lead to severe packet loss in some cases.
- **Number Of Dropped Packets**: The number of packets dropped by the SRT stack. The SRT stack drops packets when the transmission latency exceeds the SRT latency configured. This indicates insufficient bandwidth for push or high RTT and usually results in pixelation. You need to increase the latency value.

![](https://qcloudimg.tencent-cloud.cn/raw/720784ac0a25685da1c75d8a1aeeaea1.png)

### Output
The information displayed under the **Output** tab is largely the same as that under the **Input source** tab. A flow may have multiple outputs. You can select or search for an output to view its information.
![](https://qcloudimg.tencent-cloud.cn/raw/2563d297d6ee371f8f31b3010578a8b9.png)