## Overview
StreamLink provides video content providers with stable, secure, quick, and low-latency media transport capabilities. The StreamLink service is managed at the flow level. Each flow corresponds to a transport connection. With StreamLink, you can quickly and stably transport streaming media and monitor various aspects of streaming quality throughout the transport process.

## Flow List
The StreamLink service is managed at the flow level. A flow transports a live stream to one or more destinations and generates playback URLs. You can manage all your flows in [Flow Management](https://console.tencentcloud.com/mdc/flow) of the StreamLink console. You can also add, view, edit, delete, start, or stop flows on this page.

![](https://qcloudimg.tencent-cloud.cn/raw/afd0fc995dafc79a23feb9ba2df91dae.jpg)

The **Flow Management** page displays the following information:
- **Status**: **IDLE** indicates the flow is not started. **RUNNING** indicates the flow has been started.
- **Source Protocol**: The input protocol.
- **Input Address**: The input address.
If a flow is running, you can edit the allowlist, delete an existing output, or create a new output. However, to perform other operations, you need to stop the flow first.