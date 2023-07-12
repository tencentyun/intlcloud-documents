## 跨区域传输实践
### 场景描述
有一场直播活动在中国成都举行，现场信号会传送到中国上海进行制作。制作后的信号将传送给各个直播平台同步播出。直播平台分布在中国，欧洲，北美。
### 解决方案
![srt_cross_region](https://qcloudimg.tencent-cloud.cn/raw/4e5653f8e6f7c00200837decc23fceb9.png)
- 现场将信号通过 SRT 协议传送到演播室
- 演播室根据原始信号制作出最终播出的节目信号,然后通过 SRT 协议传送到各个直播平台
- 直播平台可以主动从 Stream Link 拉流，或者由 Stream Link 直接推送到直播平台
### 配置说明
假设有一路信号需要传送到位于上海的制作中心。
制作中心会有一路制作后的节目流需要传送给各个播出平台。
#### 创建一个 Event 
![create_event.png](https://qcloudimg.tencent-cloud.cn/raw/880e8b360176e700a1f1e9a6ffe00009.png)

创建一个Event，这样可以将此次活动用到的 Flow 都放置在此 Event 下，方便管理使用。

![step_into_flow_mgr](https://qcloudimg.tencent-cloud.cn/raw/e0ac5ac5f9a106686b3432f23bb60f27.png)

点击 **Flow management** 进入 Flow 管理页面，在其中进行配置。
#### 现场到演播室的 Flow 配置
现场到制作中心之间的延时要求比较低，所以这一段我们选择 SRT 传输协议。
由于原始信号十分重要，制作中心依赖源流才能成功制作最终的节目，因此这里创建两个单独的 Flow 用于传输。
##### 创建 SRT Main Flow
![select_region](https://qcloudimg.tencent-cloud.cn/raw/1f3fb2ee4d0ed271fabceecfa7a6e1dc.png)

因为现场在成都，创建 Flow 时需要选择 成都，使得 Input 和推流侧在同一个区域。
- **Region**:
选择**成都**，此区域就是 Input 的区域。
- **Max bandwidth**:
用于制作的原始信号码率较高，我们选择 **20Mbps**。
##### 添加 Input
![add_input_to_cd_main_src_flow](https://qcloudimg.tencent-cloud.cn/raw/8ca394bd8924076324d728d6be9a3f78.png)

选中 Flow 后，点击 **Add Input** 为 Flow 添加 Input

![create_input_of_cd_flow](https://qcloudimg.tencent-cloud.cn/raw/89ed5fd2205246e71c38cef26fc86052.png)
- **Input name**:
填写 `src_chengdu` 方便后面管理
- **Protocol type**:
选择 **SRT** 协议
- **Mode**:
模式选择 **Listener** ，现场直接推送信号到 Stream Link。
- **Latency setting**:
由于推流侧和Stream Link 在同一个城市，中国同城的传输 RTT 一般不超过 10ms，所以 Latency 我们设置为 60ms。
推流时，如果发现 RTT 较高，我们可以调整 推流侧的 Latency 设置，来增大 Latency。
- **Decryption Settings**:
由于推流侧有固定IP，本次推流不设置加密，转而使用 IP 白名单，保证安全性。
- **CIDR IP allowlist**:
填写推流侧使用的 IP，用于限制推到 Flow 的只能是本次活动的设备。

填充完毕后，点击 **Save** 保存 Input 配置。
##### 添加 Output
因为制作中心在上海，因此我们需要添加一个位于上海的 Output。
由于延迟的考虑，Output 我们仍然选择 SRT 协议。

![add_output_to_cd_flow](https://qcloudimg.tencent-cloud.cn/raw/64210224a58ec588287b70d8022e9509.png)
- **Output Name**:
填写 `shanghai_main_output` 方便后面管理。
- **Output region**:
由于延迟的考虑，此处选择**上海**。
- **Protocol type**:
选择 SRT 协议。
- **Mode**:
选择 **Listener** 模式，演播室从 Stream Link 拉流，方便操作。
- **Latency Setting**:
由于拉流侧和Stream Link 在同一个城市，中国同城的传输 RTT 一般不超过 10ms，所以 Latency 我们设置为 60ms。
推流时，如果发现 RTT 较高，我们可以调整 推流侧的 Latency 设置，来增大 Latency。
- **Enable encryption**:
由于拉流侧有固定IP，本次推流不设置加密，转而使用 IP 白名单，保证安全性。
- **CIDR IP allowList**:
填写拉流侧使用的 IP，用于限制可以拉流的设备。

填充以上信息后，点击 **Save** 保存output配置。

##### 创建 SRT Backup Flow
创建过程和配置与 Main Flow 相同，此处不在赘述。

#### 演播室到各个播出平台的 Flow 配置
演播室制作后的节目最终需要播出到各个平台，由于各个平台的播出对延迟并不十分敏感，所以这段传输使用 RTMP 协议。
##### 创建 RTMP Failover FLOW
![create_sh_pgm_flow](https://qcloudimg.tencent-cloud.cn/raw/26a66818ece8ee368bc2eb38f70146da.png)

因为演播室在上海，因此 Region 选择上海，使得 Input 和推流侧在同一个区域。
- **Region**:
选择**上海**，此区域就是 Input 的区域。
- **Max bandwidth**:
用于最终播出的流码率较低，我们选择 **10Mbps**。
![add_inpiut_to_sh_pgm](https://qcloudimg.tencent-cloud.cn/raw/600340d9cb6ee910bd038b34c5b5cf6c.png)
- **Protocol type**:
选择 **RTMP** 协议
- **Failover**:
打开 Failover
- **CIDR IP allowlist**:
填写推流侧使用的 IP，用于限制推到 Flow 的只能是演播室的设备。

填充以上信息后，点击 **Save** 保存 Input 配置。

##### 添加 Output
由于需要在美国、欧洲以及中国三个区域播出，我们每个区域至少需要创建一个 Output。Output 选择 RTMP_PULL 协议，让直播平台主动拉流，方便直播平台处理。
由于单个 Output 最多允许同时拉取 4 路流，若同一个地区有多个平台拉流，则建议创建多个 Output。
以欧洲为例，若同时有两个直播平台需要播出，则可以建立两个 Output，这样各平台使用独立的地址，不会互相影响。
此处只演示一个 Output 的创建，其他 Output 创建过程一致，不再赘述。

![add_output_to_sh_pgm](https://qcloudimg.tencent-cloud.cn/raw/85f5be6aeccc8b39b18867eb657a6fe8.png)
- **Output Name**:
填入 `eu_pgm_platform_a` 方便后续管理。
- **Output region**:
选择 **Frankfurt, Germany**.
- **Protocol type**:
选择 **RTMP_PULL**, 让直播平台主动拉流，方便直播平台处理。
- **CIDR IP allowlist**:
填写拉流侧使用的 IP，用于限制可以拉流的设备。

填充以上信息后，点击 **Save** 保存output配置。

#### 启动 Flow
![start_flow](https://qcloudimg.tencent-cloud.cn/raw/3f08277ee40bb2567f99aa606fa93059.png)

直播活动开始时，需要在 Stream Link 中启动 Flow.
#### 获取推拉流地址

推流地址可以在 Flow 页面获取。
- 进入推拉流地址信息页面

![show_flow_addr](https://qcloudimg.tencent-cloud.cn/raw/7e87a226706e6a2c491840ad332dc929.png)
- 从 Input Source Information 获取推流地址

![flow_addr](https://qcloudimg.tencent-cloud.cn/raw/44c00dbbcc8b9c88423b70acebb230c2.png)

#### 动态修改 Flow 配置
若直播过程中遇到突发情况，需要临时调整 Flow 配置，您可以在不用停止 Flow 的情况下直接操作。
- 修改 Input/Output 配置

![modify_input_output_setting](https://qcloudimg.tencent-cloud.cn/raw/67bdf2c97d0697a675634d03e7cf0b31.png)
- 删除某个 Output

![delete_output](https://qcloudimg.tencent-cloud.cn/raw/55f71eae74bbd2b043dc01cad167b961.png)
- 增加 Output

![create_output](https://qcloudimg.tencent-cloud.cn/raw/514c796335bb6a84fa4afba7296a3b1e.png)
