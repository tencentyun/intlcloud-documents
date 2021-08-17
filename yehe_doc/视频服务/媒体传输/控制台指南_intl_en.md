## Overview

StreamLink offers stable and secure real-time transfer capabilities, which meet the needs of video content providers for quick, stable, and low-latency video streaming media transfer. The StreamLink service is managed at the flow level in the StreamLink console, and each flow corresponds to a stream transfer linkage. You can quickly and stably transfer video streaming media and comprehensively monitor the quality of the video streams during the transfer in the console.

## Prerequisites

- You have an IP address used for push.
- You have logged in to the [StreamLink console](https://console.cloud.tencent.com/mdc/flow).

## Directions

### 1.   Select a region

Before creating a flow, you need to select the starting point of the new flow transfer linkage. Currently, you can select multiple nodes in East China, Asia, Hong Kong/Macao/Taiwan (China), West US, and Europe. If you need more nodes or technical support, please [contact us](https://intl.cloud.tencent.com/contact-sales).

![img](https://main.qcloudimg.com/raw/40f51b438e95684be5aa3a85293a612a.png)

### 2.   Create a flow

Click "Create Flow" to enter the creation page and configure the following settings.

1. Enter the basic information of the new flow.

- Enter a custom flow name.
- Select the maximum bandwidth, which can be 10 Mbps or 20 Mbps.

2. Enter the information of the input source.

- Enter the input source name.
- Select SRT, RTMP, or RTP as the protocol type of the input source.

>!
>- When you select SRT as the protocol type of the input source, you need to configure the latency setting. This parameter affects the size of buffers to save data sent and received by the server, and we recommend increasing this parameter if the network condition is poor. You can enter a value based on your actual business needs. The default value is 120 ms.
>- For the latency setting, you can perform a ping test on the IP address given after the creation to determine the optimal value. In addition, you can also directly use the default value and then adjust the latency value on the sender side to achieve the same goal.
>- StreamLink supports transfer encryption and decryption based on the SRT protocol. If the stream you push to StreamLink is an encrypted flow, you can enable "Decryption Configurations", enter the decryption key, and select the key length for StreamLink to decrypt your upstream.
![img](https://main.qcloudimg.com/raw/612a69af560cc583b9e2a420f83db35d.png)

- Set the IP allowlist (in CIDR format) of the input source, so that streams can be pushed to this flow only from IPs in the allowlist.
- You can also configure descriptive information for the flow's input source so that you can distinguish different input sources.

![img](https://main.qcloudimg.com/raw/9996153b4d81bff835b8a163366a9916.png)

After configuring the settings, click "Create" to create the flow.

### 3.   View a flow

Click a flow name on the flow management page to enter the flow details page, where you can view the basic information of the flow, basic information of the input source, output details, logs, and health data, as well as create and configure output nodes.

- #### Information

You can view the basic information of the flow, including the flow ID, flow name, input region, status, and maximum bandwidth. You can also click "Edit" to rename the flow.

![img](https://main.qcloudimg.com/raw/5ea936332f14daa6c2494a0e9077a825.png)

- #### Input Source

You can view the basic information and protocol type of the input source, including the input source ID, input source name, primary/backup input addresses, CIDR IP allowlist, and input source description. You can also click "Edit" to change the input source information.

>! If an output node has been configured for the flow, then the input source type cannot be modified.

![img](https://main.qcloudimg.com/raw/74538cf1cd523d1a98d71531305c61c2.png)

- #### Output

StreamLink supports the one-flow-multi-output mechanism, so you can configure output nodes in different regions for the same flow input source. You can view the information of all output nodes as well as create, delete, and edit output nodes here.

>! You cannot create, edit, or delete output nodes for running flows.

1. To create an output node, you need to enter the output name, output region, output protocol type (SRT, RTMP, or RTP), primary/backup destination IP addresses and ports, and output description.

2. StreamLink supports remuxing the transfer protocol. You can select the output protocol (SRT, RTMP, or RTP) when creating an output. If you select the SRT protocol, you need to enter the primary/backup destination IP addresses and ports. You can also set the latency according to your actual business needs, which is 120 ms by default.

3. Click "Confirm" to save the new output node.

>?
>- If the input protocol is SRT, the output protocol cannot be RTP.
>- The primary and backup pipelines of an output node are independent from each other and correspond to the primary and backup pipelines of the input source, respectively. This means that the stream you push to the primary pipeline of the flow will be output to the primary destination address after being transferred through StreamLink, while the stream pushed to the backup pipeline of the flow will be output to the backup destination address after being transferred through StreamLink.
>- The primary output address is required, while the backup output address is optional.
>- If you need to encrypt the output stream of the SRT protocol, you can toggle on "Enable Encryption" here. Then you need to enter the encryption key and select the key length.

![img](https://main.qcloudimg.com/raw/df0ba72d6c50b12fc37e2763513cf31f.png)

4. View the information of all output nodes under this flow, including the name, output ID, output region, protocol type, output destination IP, and destination.

![img](https://main.qcloudimg.com/raw/812429b52baa93b9b330a8b3b1104f2f.png)

5. You can edit and delete the information of an output node. The name, primary/backup destination IP addresses and ports, and output description of the output node can be changed, **but the output region and output protocol type cannot**.

![img](https://main.qcloudimg.com/raw/9d41cc9228d856869827be032433e12d.png)

- #### Log

You can view the information of events triggered during upstreaming and downstreaming in the log module and click "Confirm" to generate an event log which contains the following information:

- Time: the time when the event occurred.
- Type: event type. Valid values include input-primary, input-backup, output-primary, and output-backup, which can be filtered.
- Input/Output name: the name of the input/output that generated the event.
- Information: specific event information.

>?
>- You can change the time zone. The local time zone is selected by default.
>- You can query the log data for the last 5 days with a query time range of less than 24 hours.

![img](https://main.qcloudimg.com/raw/4418b689e88eb332b885677e43cbe5a6.png)

- #### Health

You can monitor the source and output quality of the flow during upstreaming and downstreaming in the health module. Select "Primary" or "Backup" to view the data of the primary or backup source or output and click "Confirm" to generate relevant data, including:

| Monitoring Source | Bandwidth                    | Video                      | Audio                         | SRT Protocol Metrics       |                               |                                                              |                 |
| ----------------- | ---------------------------- | -------------------------- | ----------------------------- | -------------------------- | ----------------------------- | ------------------------------------------------------------ | --------------- |
| Bitrate           | Frame Rate                   | Bitrate                    | Frame Rate                    | Packet Loss Rate           | Retransmission Rate           | RTT                                                          | Dropped Packets |
| Source            | Total input/output bandwidth | Input/Output video bitrate | Input/Output video frame rate | Input/Output audio bitrate | Input/Output audio frame rate | SRT protocol parameters, which are  displayed only when SRT protocol is selected |                 |
| Output            |                              |                            |                               |                            |                               |                                                              |                 |

>?
>- You can change the time zone. The local time zone is selected by default.
>- You can query the health data for the last 5 days with a query time range of less than 24 hours.
>- For the video and audio bitrate and frame rate metrics, you can select the specific channel of video and video for data display on the right.
>- If the protocol is SRT, you can choose to display the packet loss rate, retransmission rate, RTT, or number of dropped packets on the right.

![img](https://main.qcloudimg.com/raw/107263b0b3b1a1321222f891e24e136a.png)

![img](https://main.qcloudimg.com/raw/bc8dd565e63e74eb15e1f3868cdf9083.png)

### 4.   Start/Stop a flow

After creating the flow and output node, click "Start" to run the flow. When you are done using the flow, click "Stop" to stop it.

>! Flows that have no output nodes cannot be started.

![img](https://main.qcloudimg.com/raw/df397e7413a9d3bb91956de33f9c2130.png)

### 5.   Delete a flow

To delete a flow, click "Delete" to delete its configuration information.

![img](https://main.qcloudimg.com/raw/c5d2f2a49521be8d02f0a8cb2bb805b9.png)