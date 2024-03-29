Go to the [Flow Management](https://console.tencentcloud.com/mdc/flow) page of the StreamLink console and click **Create Flow**.
![](https://qcloudimg.tencent-cloud.cn/raw/b7ea1765ad2384f3b2c5ceeef2a76ce7.png)

Enter a flow name, specify the max bitrate, and enter the input information.
- **Name**: The flow name, which helps you identify a flow.
- **Max Bandwidth**: Select a max bitrate for your stream. The allocation of network resources will be based on this value.
- **Source Name**: The source name, which helps you identify a source.
- **Protocol Type**: The push protocol. Currently, RTMP, SRT, RTP, and RTSP are supported.

## RTMP
If you select RTMP, you need to push your stream to the input address generated by StreamLink. You can view the address on the **Flow Management** page.
![](https://qcloudimg.tencent-cloud.cn/raw/74cf0e4bb392f4474261703eec7974ea.png)

- **Failover**: If you enable failover, StreamLink will generate two input addresses. You can push streams to both addresses. The stream that arrives first will be used as the primary source. If the primary source is down, StreamLink will automatically switch to the backup stream.
- **CIDR IP Allowlist**: The IP allowlist, which specifies the IP addresses (example: `203.3.3.3/28`) that are allowed to push streams. This makes for improved security. Separate multiple addresses with semicolons, as in `203.3.3.3/28;202.3.3.3/28`.


## RTMP_PULL
If you select RTMP_PULL, StreamLink will pull streams from the address you specify.
![](https://qcloudimg.tencent-cloud.cn/raw/751d78b56498ba5d9eafaddb8bdccf57.png)

- **Source Address**: The RTMP URL, such as `rtmp://example.com/live`.
- **Source Key**: The RTMP stream key, such as `e18c3c4dd05aef020946e6afbf9e04ef`.
- **Failover**: Currently, failover is not yet supported for this protocol type. It will be made available in the future.

## SRT Listener
![](https://qcloudimg.tencent-cloud.cn/raw/30760bb8411f2a14bb630b3eb3cd8637.png)
- **Mode**: Select **Listener**. In this mode, you need to use the SRT caller mode to request to send your stream to the StreamLink input address. You can view the input address on the **Flow Management** page.
- **Latency Setting**: The SRT latency. If the push end is in the same country as your StreamLink AZ, we recommend you set this to 120 ms. If the push end is not in the same country as your StreamLink AZ, we recommend you set this to 200 ms. If the push end is not in the same continent as your StreamLink AZ, we recommend you set this to 1,000 ms. You can determine the value of this parameter based on the IP address assigned.
- **Decryption Settings**: You can toggle this on if you want to improve your transmission security. Specify the **Decryption Key** and **Key Length**. You need to configure the same parameters at the push end, or you will fail to push the stream.
  - **Decryption Key**: The encryption/decryption key. You need to configure the same key at the push end.
  - **Key Length**: The key length. You need to specify the same key length at the push end.
- **Failover**: Currently, failover is not yet supported for this protocol type. It will be made available in the future.
- **CIDR IP Allowlist**: The IP allowlist, which specifies the IP addresses (example: `203.3.3.3/28`) that are allowed to push streams. This makes for improved security. Separate multiple addresses with semicolons, as in `203.3.3.3/28;202.3.3.3/28`.

## SRT Caller
![](https://qcloudimg.tencent-cloud.cn/raw/b8a8ae4e50e6375b635795c4d60e2577.png)
- **Mode**: Select **Caller**. In this mode, StreamLink will request the source stream from the address you provide using the caller mode.
- **Source IP**: The IP address or domain of the source stream.
- **Source Port**: The port number of the source IP address.
- **Latency Setting**: The SRT latency. If the source address is in the same country as your StreamLink AZ, we recommend you set this to 120 ms. If the source address is not in the same country as your StreamLink AZ, we recommend you set this to 200 ms. If the source address is not in the same continent as your StreamLink AZ, we recommend you set this to 1,000 ms. You can determine the value of this parameter based on the IP address assigned.
- **Decryption Settings**: If you enable encryption for the source stream, you need to toggle this on and specify the decryption key and key length. Otherwise, StreamLink will fail to pull the stream.
  - **Decryption Key**: The decryption key. This is required if you enable encryption for the source stream.
  - **Key Length**: The key length, which must be the same as that configured for the source stream.
- **Failover**: Currently, failover is not yet supported for this protocol type. It will be made available in the future.

## RTP
If you select RTP, you need to push your stream to the input address generated by StreamLink. You can view the address on the **Flow Management** page.
![](https://qcloudimg.tencent-cloud.cn/raw/1e91a938d681e46e48ec8bb7405df2c4.png)

- **Failover**: Currently, failover is not yet supported for this protocol type. It will be made available in the future.
- **CIDR IP Allowlist**: The IP allowlist, which specifies the IP addresses (example: `203.3.3.3/28`) that are allowed to push streams. This makes for improved security. Separate multiple addresses with semicolons, as in `203.3.3.3/28;202.3.3.3/28`.