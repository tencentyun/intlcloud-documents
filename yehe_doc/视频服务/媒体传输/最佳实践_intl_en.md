# Cross-Region Transport

## Scenario
An event taking place in Chengdu, China, will be streamed live. The live stream is sent to Shanghai, China, where it will be processed. The processed video will then be sent to live streaming platforms in China, Europe, and North America.

## How It Works
![](https://qcloudimg.tencent-cloud.cn/raw/62fd6a79371347984aa53930a465bcd0.jpeg)
- The video captured live on-premises is sent to the studio in Shanghai using the SRT protocol.
- The studio processes the video and distributes the video to live streaming platforms using the SRT protocol.
- Live streaming platforms pull streams from StreamLink, or StreamLink pushes the stream to live streaming platforms.


## StreamLink Configuration
The live stream needs to be sent to the studio in Shanghai. After processing the video, the studio needs to send the stream to different live streaming platforms.


### 1. Configuring flows to send the stream captured on-premises to the studio
Given the high latency requirements of live events, the SRT protocol is used. To ensure source availability, two flows are created to transport the live video to the studio.

#### Creating an SRT main flow
Because the event is taking place in Chengdu, select Chengdu as the region so that the input address is in the same region.
![](https://qcloudimg.tencent-cloud.cn/raw/c8e72acfc3666277ca4686e74feba235.png)
![](https://qcloudimg.tencent-cloud.cn/raw/51e1c324d0da25db355060a4ad7b89e5.png)

- **Name**: The flow is named `chengdu_main_ori_stream`.
- **Max Bandwidth**: Because the bitrate of the source video is high, **20Mbps** is selected.
- **Protocol**: Select **SRT**.
- **Mode**: Select **Listener**. The live video will be sent to StreamLink directly.
- **Latency**: The push end is in the StreamLink AZ used. In China, the RTT for same-city transport is usually less than 10 ms. Therefore, **Latency** is set to 60 ms. If the actual RTT is higher than expected, you can increase the latency at the push end.
- **Decryption Settings**: Given that the push end uses a fixed IP address, instead of encryption, IP allowlist is used to ensure security.
- **CIDR IP Allowlist**: Enter the IP address used by the push end. This ensures that only the device of the event can push streams to the flow.

Click **Create**.

#### Adding an output
Because the studio is in Shanghai, we need to create an output in Shanghai. To keep the latency low, SRT is used for the output as well.
![](https://qcloudimg.tencent-cloud.cn/raw/57276bf97bce0d5032fd4d2691df7beb.png)

- **Output Name**: The output is named `shanghai_main_output`.
- **Output Region**: To keep the latency low, Shanghai is selected.
- **Output Protocol**: Select **SRT**.
- **Mode**: Select **Listener**. The studio will pull the stream from StreamLink.
- **Latency Setting**: The studio is in the StreamLink AZ used. In China, the RTT for same-city transport is usually less than 10 ms. Therefore, **Latency** is set to 60 ms. If the actual RTT is higher than expected, you can increase the latency at the push end.
- **Enable Encryption**: Because the studio has a fixed IP address, instead of encryption, IP allowlist is used to ensure security.
- **CIDR IP AllowList**: Enter the IP address of the studio. This ensures that only the studio’s device can pull streams from StreamLink.

Click **Confirm**.

#### Creating an SRT backup flow
The steps of creating a backup flow are the same as those for the main flow.


### 2. Configuring a flow to send the stream from the studio to live streaming platforms
After processing the video, the studio needs to distribute it to live streaming platforms. Because live streaming platforms normally do not have high requirements for latency, RTMP is used for the transport.

#### Creating an RTMP failover flow
Because the studio is in Shanghai, select Shanghai as the region so that the input address is in the same region.
![](https://qcloudimg.tencent-cloud.cn/raw/3f2cc6be8882b2ef9f7ea3c2efa8a285.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0ece7d6ebe0c1062f3210c8354d2b3cf.png)

- **Name**: The flow is named `pgm_main`.
- **Max Bandwidth**: Because the bitrate of the processed video is lower, **10Mbps** is selected.
- **Protocol**: Select **RTMP**.
- **Failover**: Toggle this on.
- **CIDR IP Allowlist**: Enter the IP address of the studio. This ensures that only the studio’s device can push streams to the flow.

Click **Create**.

#### Adding an output
Because the video will be distributed in the US, Europe, and China, we need to create at least one output for each of the three regions. Select **RTMP_PULL** as the **Output Protocol**, which means live streaming platforms will need to pull the stream from StreamLink. Each output allows the pulling of four streams at the same time. If more than one platform in a region pull streams from StreamLink at the same time, we recommend you create multiple outputs. For example, if two live streaming platforms in Europe will pull the stream from StreamLink at the same time, create two outputs so that the two platforms can use separate URLs. The following shows how to create such outputs.
![](https://qcloudimg.tencent-cloud.cn/raw/edf53f502063c2f3c93ef8170256a1dc.png)

- **Output Name**: The output is named `eu_pgm_platform_a`.
- **Output Region**: Select **Frankfurt, Germany**.
- **Output Protocol**: Select **RTMP_PULL**. Live streaming platforms will need to pull the stream from StreamLink.
- **CIDR IP Allowlist**: Enter the IP address of the live streaming platform. This ensures that only the platform’s device can pull streams from StreamLink.

Click **Confirm**.

### 3. Obtaining the playback URL
#### Push URL
You can view the URL for pushing the stream to live streaming platforms on the **Flow Management** page or the **Input Source Information** page.
From **Flow Management**:
![](https://qcloudimg.tencent-cloud.cn/raw/685dd9818b72280ffc9d84cec9ab8c0a.png)
From **Input Source Information**:
![](https://qcloudimg.tencent-cloud.cn/raw/2098e9e325b6673ded79ab6843b7ad75.png)

#### Playback URL
You can view the playback URL in the output list:
![](https://qcloudimg.tencent-cloud.cn/raw/5f760430afe012ee26531294510de0bf.png)

### 4. Starting the flows
![](https://qcloudimg.tencent-cloud.cn/raw/d4e543da4000175587ec2d4d74e4775e.png)
When the event begins, start the flows in the StreamLink console.

### 5. Dynamically changing the flow settings
During live streaming, you can change the settings of a flow without stopping the flow.
Modifying the input CIDR allowlist:
![](https://qcloudimg.tencent-cloud.cn/raw/c4c642e542beed25a7cd134600a3ba62.png)
Modifying the output CIDR allowlist:
![](https://qcloudimg.tencent-cloud.cn/raw/de4ce1df26d2bff4b0ca9ca7312a70ba.png)
Deleting an output:
![](https://qcloudimg.tencent-cloud.cn/raw/13b2a0fe21b9d528bdee155135da9b5d.png)
Adding an output:
![](https://qcloudimg.tencent-cloud.cn/raw/026591b6497dc6aa8411f3e19a2e42db.png)