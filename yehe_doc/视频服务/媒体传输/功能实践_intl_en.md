## Cross-Region Transport
### Scenario
An event taking place in Chengdu, China, will be streamed live. The live stream is sent to Shanghai, China, where it will be processed. The processed video will then be sent to live streaming platforms in China, Europe, and North America.
### How It Works
![srt_cross_region](https://qcloudimg.tencent-cloud.cn/raw/4e5653f8e6f7c00200837decc23fceb9.png)
- The video captured live on-premises is sent to the studio in Shanghai using the SRT protocol.
- The studio processes the video and distributes the video to live streaming platforms using the SRT protocol.
- Live streaming platforms pull streams from StreamLink, or StreamLink pushes the stream to live streaming platforms.
### StreamLink Configuration
The live stream needs to be sent to the studio in Shanghai. After processing the video, the studio needs to send the stream to different live streaming platforms.
#### Creating an event
![create_event.png](https://qcloudimg.tencent-cloud.cn/raw/880e8b360176e700a1f1e9a6ffe00009.png)

Create an event, so that all the flows used in this activity can be placed under this event for easy management and use. 

![step_into_flow_mgr](https://qcloudimg.tencent-cloud.cn/raw/e0ac5ac5f9a106686b3432f23bb60f27.png)

Click **Flow management** to configure the flows.
#### Configuring flows to send the stream captured on-premises to the studio

Given the high latency requirements of live events, the SRT protocol is used. To ensure source availability, two flows are created to transport the live video to the studio.
##### Creating an SRT main flow
![select_region](https://qcloudimg.tencent-cloud.cn/raw/1f3fb2ee4d0ed271fabceecfa7a6e1dc.png)

Because the event is taking place in Chengdu, select Chengdu as the region so that the input address is in the same region.
- **Region**: Select **Chengdu**, which is the Input region.
- **Max bandwidth**: Because the bitrate of the source video is high, **20Mbps** is selected.
##### Adding an input
![add_input_to_cd_main_src_flow](https://qcloudimg.tencent-cloud.cn/raw/8ca394bd8924076324d728d6be9a3f78.png)

Select a flow in the flow list, click **Add input** to add an input to the flow.

![create_input_of_cd_flow](https://qcloudimg.tencent-cloud.cn/raw/89ed5fd2205246e71c38cef26fc86052.png)
- **Input name**: The input is named `src_chengdu`.
- **Protocol type**: Select **SRT**.
- **Mode**: Select **Listener**. The live video will be sent to StreamLink directly.
- **Latency setting**: The push end is in the StreamLink AZ used. In China, the RTT for same-city transport is usually less than 10 ms. Therefore, Latency is set to 60 ms. If the actual RTT is higher than expected, you can increase the latency at the push end.
- **Decryption settings**: Given that the push end uses a fixed IP address, instead of encryption, IP allowlist is used to ensure security.
- **CIDR IP allowlist**: Enter the IP address used by the push end. This ensures that only the device of the event can push streams to the flow.

Click **Save**. 
##### Adding an output
Because the studio is in Shanghai, we need to create an output in Shanghai. To keep the latency low, SRT is used for the output as well.

![add_output_to_cd_flow](https://qcloudimg.tencent-cloud.cn/raw/64210224a58ec588287b70d8022e9509.png)
- **Output Name**: The output is named `shanghai_main_output`.
- **Output region**: To keep the latency low, **Shanghai** is selected.
- **Protocol type**: Select **SRT**.
- **Mode**: Select **Listener**. The studio will pull the stream from StreamLink.
- **Latency setting**: The studio is in the StreamLink AZ used. In China, the RTT for same-city transport is usually less than 10 ms. Therefore, Latency is set to 60 ms. If the actual RTT is higher than expected, you can increase the latency at the push end.
- **Enable encryption**: Because the studio has a fixed IP address, instead of encryption, IP allowlist is used to ensure security.
- **CIDR IP allowList**: Enter the IP address of the studio. This ensures that only the studio's device can pull streams from StreamLink.

Click **Save**. 

##### Creating an SRT backup flow
The steps of creating a backup flow are the same as those for the main flow.

#### Configuring a flow to send the stream from the studio to live streaming platforms
After processing the video, the studio needs to distribute it to live streaming platforms. Because live streaming platforms normally do not have high requirements for latency, RTMP is used for the transport.
##### Creating an RTMP failover flow
![create_sh_pgm_flow](https://qcloudimg.tencent-cloud.cn/raw/26a66818ece8ee368bc2eb38f70146da.png)

Because the studio is in Shanghai, select Shanghai as the region so that the input address is in the same region. 
- **Region**: Select **Shanghai**, which is the input region. 
- **Max bandwidth**: Because the bitrate of the processed video is lower, **10Mbps** is selected.
![add_inpiut_to_sh_pgm](https://qcloudimg.tencent-cloud.cn/raw/600340d9cb6ee910bd038b34c5b5cf6c.png)
- **Protocol type**: Select **RTMP**.
- **Failover**: Toggle this on.
- **CIDR IP allowlist**: Enter the IP address of the studio. This ensures that only the studio's device can push streams to the flow.


Click **Save**. 

##### Adding an output
Because the video will be distributed in the US, Europe, and China, we need to create at least one output for each of the three regions. Select RTMP_PULL as the output protocol, which means live streaming platforms will need to pull the stream from StreamLink. Each output allows the pulling of four streams at the same time. If more than one platform in a region pull streams from StreamLink at the same time, we recommend you create multiple outputs. For example, if two live streaming platforms in Europe will pull the stream from StreamLink at the same time, create two outputs so that the two platforms can use separate URLs. The following shows how to create such outputs. 

![add_output_to_sh_pgm](https://qcloudimg.tencent-cloud.cn/raw/85f5be6aeccc8b39b18867eb657a6fe8.png)

- **Output Name**: The output is named `eu_pgm_platform_a`.
- **Output region**: Select **Frankfurt, Germany**.
- **Protocol type**: Select **RTMP_PULL**. Live streaming platforms will need to pull the stream from StreamLink.
- **CIDR IP allowlist**: Enter the IP address of the live streaming platform. This ensures that only the platform's device can pull streams from StreamLink.

Click **Save**. 

#### Starting a flow
![start_flow](https://qcloudimg.tencent-cloud.cn/raw/3f08277ee40bb2567f99aa606fa93059.png)

When the event begins, start the flows in the StreamLink console.
#### Obtaining the push and playback URL

You can view the push URL on the flow page. 
- Click **Addresses**.

![show_flow_addr](https://qcloudimg.tencent-cloud.cn/raw/7e87a226706e6a2c491840ad332dc929.png)
- Obtain the push address from input source information.

![flow_addr](https://qcloudimg.tencent-cloud.cn/raw/44c00dbbcc8b9c88423b70acebb230c2.png)

#### Dynamically changing the flow settings
During live streaming, you can change the settings of a flow without stopping the flow. 
- Modifying the input/output configuration: 

![modify_input_output_setting](https://qcloudimg.tencent-cloud.cn/raw/67bdf2c97d0697a675634d03e7cf0b31.png)
- Deleting an output:

![delete_output](https://qcloudimg.tencent-cloud.cn/raw/55f71eae74bbd2b043dc01cad167b961.png)
- Adding an output: 

![create_output](https://qcloudimg.tencent-cloud.cn/raw/514c796335bb6a84fa4afba7296a3b1e.png)
