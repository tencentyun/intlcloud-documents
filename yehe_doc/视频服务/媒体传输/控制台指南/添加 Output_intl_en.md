## Output Management
On the [Flow Management](https://console.tencentcloud.com/mdc/flow) page of the StreamLink console, you can click a flow to view its details.
![](https://qcloudimg.tencent-cloud.cn/raw/6e157c3ffc610bcf01c247a441a538cd.png)
Under the **Output** tab of the flow details page, you can create, delete, or edit an output.
![](https://qcloudimg.tencent-cloud.cn/raw/ddfed18e28122e9198549541d3ebfd70.png)


## Create an Output
To create an output, click **Create Output**, complete the required settings in the pop-up window, and click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/e9b1da7a805b27d5dcfa452775e7461d.png)

- **Output Name**: The output name. Output names facilitate output management.
- **Output Region**: The output region, which is the region you want to send your stream to.
- **Output Protocol**: The output protocol. Different protocols require different settings.

  | Input Protocol | Output Protocol Options |
  | -----------| ---------------|
  | RTMP, RTMP_PULL       | RTMP, RTMP_PUSH, RTMP_PULL|
  | SRT         | SRT, RTMP_PUSH|
  | RTP         | RTP        |
  | RTSP        | RTSP       |
  

### RTMP_PUSH
If you select this protocol, the stream will be relayed to the address you specify.
![](https://qcloudimg.tencent-cloud.cn/raw/1a379f8a32e9ca1bd5341ade3a24912b.png)

- **Destination URL**: The RTMP destination URL, such as `rtmp://example.com/live`.
- **Flow Key**: The RTMP stream key, such as `e18c3c4dd05aef020946e6afbf9e04ef`.


### RTMP_PULL
If you need to play the stream from an output, select this protocol. After creating an RTMP_PULL output, you can view the playback URL in the output list.
![](https://qcloudimg.tencent-cloud.cn/raw/678b8da18059dec35579f1515c91e1ff.png)

- **CIDR IP Allowlist**: The IP allowlist, which specifies the IP addresses (example: `203.3.3.3/28`) that are allowed to push streams. This makes for improved security. Separate multiple addresses with semicolons, as in `203.3.3.3/28;202.3.3.3/28`.

### SRT listener
![](https://qcloudimg.tencent-cloud.cn/raw/13071f72fe033f1a82b1bba87c7b7a56.png)
- **Mode**: Select **Listener**. In this mode, you need to use the SRT caller mode at the receiving end to request the stream from StreamLink. You can view the playback URL in the output list.
- **Latency Setting**: The SRT latency. If the push end is in the same country as your StreamLink AZ, we recommend you set this to 120 ms. If the push end is not in the same country as your StreamLink AZ, we recommend you set this to 200 ms. If the push end is not in the same continent as your StreamLink AZ, we recommend you set this to 1,000 ms. You can determine the value of this parameter based on the IP address assigned.
- **Enable Encryption**: If you toggle this on, you also need to enable encryption at the receiving end and specify the encryption key and key length. Otherwise, you will fail to pull the stream.
  - **Encryption Key**: The encryption key.
  - **Key Length**: The key length.
- **Failover**: Currently, failover is not yet supported for this protocol type. It will be made available in the future.
- **CIDR IP Allowlist**: The IP allowlist, which specifies the IP addresses (example: `203.3.3.3/28`) that are allowed to push streams. This makes for improved security. Separate multiple addresses with semicolons, as in `203.3.3.3/28;202.3.3.3/28`.

### SRT caller
![](https://qcloudimg.tencent-cloud.cn/raw/254cb4af2ca2e3d27be2f0ff724b02f4.png)
- **Mode**: Select **Caller**. In this mode, StreamLink will use the SRT caller mode to send the stream to the address you specify.
- **Destination**: The IP address or domain to which the SRT stream is sent.
- **Port**: The port number of the destination IP address.
- **Latency Setting**: The SRT latency. If the source address is in the same country as your StreamLink AZ, we recommend you set this to 120 ms. If the source address is not in the same country as your StreamLink AZ, we recommend you set this to 200 ms. If the source address is not in the same continent as your StreamLink AZ, we recommend you set this to 1,000 ms. You can determine the value of this parameter based on the IP address assigned.
- **Enable Encryption**: If you enable encryption at the receiving end, you need to toggle this on and specify the encryption key and key length. Otherwise, you will fail to push the stream.
  - **Encryption Key**: The encryption key.
  - **Key Length**: The key length, which must be the same as that configured at the receiving end.
- **Failover**: Currently, failover is not yet supported for this protocol type. It will be made available in the future.


### RTP
If you select this protocol, the stream will be pushed to the address you specify.
![](https://qcloudimg.tencent-cloud.cn/raw/4cca576a3a1da76f0e2a2a4ab7d80b48.png)

- **Destination**: The address to send the stream to.
- **Output Protocol**: The drop-down list changes depending on the input protocol used.