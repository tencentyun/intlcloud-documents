# 跨区域传输实践

## 场景描述
以一场直播活动为例，假设在中国成都举行，现场信号会传送到中国上海进行制作。制作后的信号将传送给各个直播平台同步播出。直播平台分布在中国，欧洲，北美。

## 解决方案
![](https://qcloudimg.tencent-cloud.cn/raw/62fd6a79371347984aa53930a465bcd0.jpeg)
- 现场将信号通过SRT协议传送到演播室。
- 演播室根据原始信号制作出最终播出的节目信号，然后通过SRT协议传送到各个直播平台。
- 直播平台可以主动从StreamLink拉流，或者由StreamLink 直接推送到直播平台。


## 配置说明
假设有一路信号需要传送到位于上海的制作中心。制作中心会有一路制作后的节目流需要传送给各个播出平台。


### 1. 现场到演播室的Flow配置
现场到制作中心之间的延时要求比较低，所以这一段我们选择SRT传输协议。由于原始信号十分重要，制作中心依赖源流才能成功制作最终的节目，因此这里创建两个单独的Flow用于传输。

#### 创建 SRT Main Flow
因为现场在成都，因此需要在页面左上角将Region切换为成都，使得Input和推流侧在同一个区域。
![](https://qcloudimg.tencent-cloud.cn/raw/c8e72acfc3666277ca4686e74feba235.png)
![](https://qcloudimg.tencent-cloud.cn/raw/51e1c324d0da25db355060a4ad7b89e5.png)

- **Name**：填写chengdu_main_ori_stream，方便后面管理。
- **Max Bandwidth**：用于制作的原始信号码率较高，我们选择20Mbps。
- **Protocol**：选择SRT协议。
- **Mode**：模式选择Listener，现场直接推送信号到StreamLink。
- **Latency**：由于推流侧和StreamLink 在同一个城市，中国同城的传输RTT一般不超过 10ms，所以Latency我们设置为 60ms。推流时，如果发现RTT较高，我们可以调整推流侧的 Latency设置，来增大Latency。
- **Decryption Settings**：由于推流侧有固定IP，本次推流不设置加密，转而使用IP白名单，保证安全性。
- **CIDR IP Allowlist**：填写推流侧使用的IP，用于限制推到Flow的只能是本次活动的设备。

填充完毕后，点击**Create**保存Flow 配置。

#### 添加 Output
因为制作中心在上海，因此我们需要添加一个位于上海的Output。由于延迟的考虑，Output 我们仍然选择SRT协议。
![](https://qcloudimg.tencent-cloud.cn/raw/57276bf97bce0d5032fd4d2691df7beb.png)

- **Output Name**：填写shanghai_main_output，方便后面管理。
- **Output Region**：由于延迟的考虑，此处选择上海。
- **Output Protocol**：选择SRT协议。
- **Mode**：选择Listener模式，演播室从StreamLink 拉流，方便操作。
- **Latency Setting**：由于拉流侧和StreamLink 在同一个城市，中国同城的传输RTT 一般不超过10ms，所以Latency我们设置为 60ms。推流时，如果发现RTT较高，我们可以调整 推流侧的Latency设置，来增大Latency。
- **Enable Encryption**：由于拉流侧有固定IP，本次推流不设置加密，转而使用 IP 白名单，保证安全性。
- **CIDR IP AllowList**：填写拉流侧使用的IP，用于限制可以拉流的设备。

填充以上信息后，点击**Confirm**保存output配置。

#### 创建 SRT Backup Flow
创建过程和配置与 Main Flow 相同，此处不在赘述。


### 2. 演播室到各个播出平台的Flow配置
演播室制作后的节目最终需要播出到各个平台，由于各个平台的播出对延迟并不十分敏感，所以这段传输使用RTMP协议。

#### 创建 RTMP Failover Flow
演播室上海，因此需要在页面左上角将Region切换为上海，使得Input和推流侧在同一个区域。
![](https://qcloudimg.tencent-cloud.cn/raw/3f2cc6be8882b2ef9f7ea3c2efa8a285.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0ece7d6ebe0c1062f3210c8354d2b3cf.png)

- **Name**：填写pgm_main，方便后面管理。
- **Max Bandwidth**：用于最终播出的流码率较低，我们选择10Mbps。
- **Protocol**：选择RTMP协议。
- **Failover**：打开Failover。
- **CIDR IP Allowlist**：填写推流侧使用的IP，用于限制推到Flow的只能是演播室的设备。

填充完毕后，点击**Create**保存Flow 配置。

#### 添加Output
由于需要在美国、欧洲以及中国三个区域播出，我们每个区域至少需要创建一个Output。Output选择RTMP_PULL协议，让直播平台主动拉流，方便直播平台处理。由于单个Output最多允许同时拉取4路流，若同一个地区有多个平台拉流，则建议创建多个Output。以欧洲为例，若同时有两个直播平台需要播出，则可以建立两个Output，这样各平台使用独立的地址，不会互相影响。此处只演示一个Output的创建，其他Output创建过程一致，不再赘述。
![](https://qcloudimg.tencent-cloud.cn/raw/edf53f502063c2f3c93ef8170256a1dc.png)

- **Output Name**：填入 eu_pgm_platform_a，方便后续管理。
- **Output Region**：选择Frankfurt, Germany。
- **Output Protocol**：选择RTMP_PULL, 让直播平台主动拉流，方便直播平台处理。
- **CIDR IP Allowlist**：填写拉流侧使用的IP，用于限制可以拉流的设备。

填充以上信息后，点击**Confirm**保存Output配置。

### 3. 获取推拉流地址
#### 推流地址
推流地址可以在Flow Management以及Input Source Information页面获取。
从Flow Management获取推流地址：
![](https://qcloudimg.tencent-cloud.cn/raw/685dd9818b72280ffc9d84cec9ab8c0a.png)
从Input Source Information获取推流地址：
![](https://qcloudimg.tencent-cloud.cn/raw/2098e9e325b6673ded79ab6843b7ad75.png)

#### 拉流地址
拉流地址可以在Output列表页获取：
![](https://qcloudimg.tencent-cloud.cn/raw/5f760430afe012ee26531294510de0bf.png)

### 4. 启动Flow
![](https://qcloudimg.tencent-cloud.cn/raw/d4e543da4000175587ec2d4d74e4775e.png)
直播活动开始时，需要在StreamLink中启动Flow。

### 5. 动态修改Flow配置
若直播过程中遇到突发情况，需要临时调整Flow配置，您可以在不用停止Flow的情况下直接操作。
修改Input CIDR Allowiplist：
![](https://qcloudimg.tencent-cloud.cn/raw/c4c642e542beed25a7cd134600a3ba62.png)
修改Output CIDR Allowiplist：
![](https://qcloudimg.tencent-cloud.cn/raw/de4ce1df26d2bff4b0ca9ca7312a70ba.png)
停止某个Output：
![](https://qcloudimg.tencent-cloud.cn/raw/13b2a0fe21b9d528bdee155135da9b5d.png)
增加Output：
![](https://qcloudimg.tencent-cloud.cn/raw/026591b6497dc6aa8411f3e19a2e42db.png)