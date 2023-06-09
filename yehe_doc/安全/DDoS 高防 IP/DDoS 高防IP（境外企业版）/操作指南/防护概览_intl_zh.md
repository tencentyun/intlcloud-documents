## 防护概览（总览）
用户将业务接入 DDoS 高防 IP（境外企业版） 服务，且将业务流量切换至 DDoS 高防 IP（境外企业版） 后，可在控制台查看业务流量情况和 DDoS 攻击防护情况。支持抓包下载攻击数据，便于用户分析与溯源。


### 查看攻击态势
1.	登录 [DDoS 高防 IP（境外企业版）](https://console.cloud.tencent.com/ddos/ddos-basic) 控制台，在左侧导航栏中，单击**防护概览** > **防护总览**。
![](https://qcloudimg.tencent-cloud.cn/raw/d43fa663afebd05e6807dde663b90258.png)
2.	在攻击态势模块中，可查看当前业务是否存在风险，和最近一次攻击的时间的攻击类型。当有攻击存在时，单击**升级防护**可进入购买页。

3. 在攻击态势模块中，还可以直观查看各项数据情况。
![](https://qcloudimg.tencent-cloud.cn/raw/4ecad368488ce05e5c54d6ac8b316fa4.png)
   **字段说明：**
    - 被攻击 IP 数：受到攻击的业务 IP 总数。包括基础防护被攻击 IP 数、接入高防包后被攻击的业务 IP 数、高防 IP 实例被攻击数。
    - 已防护 IP 数：接入高防包的业务 IP 和高防 IP 实例。
    - 被封堵 IP 数：被屏蔽所有外网访问的业务 IP 数。包括基础防护的业务 IP、接入高防包的业务 IP 和高防 IP 实例。
    - 被攻击域名数：高防 IP 被攻击的域名数、被攻击的端口所影响的域名数。
    - 已防护域名数：高防 IP 实例的域名接入数量。
    - 攻击峰值：当前攻击事件中的最高攻击带宽。


### 查看防御态势
1.	登录 [DDoS 高防 IP（境外企业版）](https://console.cloud.tencent.com/ddos/ddos-basic) 控制台，在左侧导航栏中，单击**防护概览** > **防护总览**。
2. 在防御态势模块的统计图中，展示业务 IP 状态数据，可以快速了解业务 IP 健康状态。
![](https://qcloudimg.tencent-cloud.cn/raw/7a88a800c181831dc4580e3dc923102f.png)
   **字段说明：**
    - IP 总数：当前全部业务 IP 总数，包括基础防护的业务 IP、接入高防包的业务 IP 和高防 IP 实例。
    - 已防护 IP 数：接入高防包的业务 IP 和高防 IP 实例。
    - 封堵 IP 数：被屏蔽所有外网访问的业务 IP 数。包括基础防护的业务 IP、接入高防包的业务 IP 和高防 IP 实例。
3. 在防御态势模块的防护趋势中，展示一周内全量业务受攻击总次数，可以快速了解近期攻击状态分布情况。
![](https://qcloudimg.tencent-cloud.cn/raw/63ed220cf237d856528e1f2b1a80e49e.png)
3. 在防御态势模块的防护建议中，展示基础防护状态下受到攻击的业务 IP，提示接入高级防护。方便用户快速为被攻击 IP 接入高级防护，保证业务安全。
![](https://qcloudimg.tencent-cloud.cn/raw/7cce1b85e81dab27cae83e03cfabeb13.png)

### 查看高防 IP 实例统计
1.	登录 [DDoS 高防 IP（境外企业版）](https://console.cloud.tencent.com/ddos/ddos-basic) 控制台，在左侧导航栏中，单击**防护概览** > **防护总览**。
2. 在高防实例统计模块中，展示高防 IP 资源的安全状态，可以快速全面了解风险业务分部。
![](https://qcloudimg.tencent-cloud.cn/raw/5a08a7115062914ecccf1674762a541a.png)

### 查看近期安全事件
1.	登录 [DDoS 高防 IP（境外企业版）](https://console.cloud.tencent.com/ddos/ddos-basic) 控制台，在左侧导航栏中，单击**防护概览** > **防护总览**。
2. 在近期安全事件模块中，展示最近全量的攻击事件。单击**查看详情**，进入事件详情页面，供用户进行 DDoS 攻击分析及溯源支撑。
![](https://qcloudimg.tencent-cloud.cn/raw/61528176e7f8297f3532901bca36c761.png)
3. 在事件详情页面的攻击信息模块，查看该时间范围内的 IP 遭受的攻击情况，包括被攻击 IP、状态、攻击类型（采样数据）、攻击带宽峰值和攻击包速率峰值、开始时间结束时间基础信息。
![](https://qcloudimg.tencent-cloud.cn/raw/4aa25f97c6f9dbaee1a1d747f315b428.png)
4. 在事件详情页面的攻击趋势模块，可查看网络攻击流量带宽或攻击包速率趋势。当遭受攻击时，在流量趋势图中可以明显看出攻击流量的峰值。
>?此处数据为该攻击时间段全量实时数据。

![](https://qcloudimg.tencent-cloud.cn/raw/1df1d09926470f122ea43afa351dcf7f.png)
5. 在事件详情页面的攻击统计模块，可通过攻击流量协议分布、攻击类型分布，查看这两个数据维度下的攻击分布情况。
>?此处数据为该攻击时间段内攻击采样数据，非全量数据。

![](https://qcloudimg.tencent-cloud.cn/raw/8c72fbac90522d2aa0eccda6a56d9e7d.png)
   **字段说明：**
   - 攻击流量协议分布：查看该时间范围内，所选择的高防 IP 实例遭受攻击事件中各协议总攻击流量的占比情况。
   - 攻击类型分布：查看该时间范围内，所选择的高防 IP 实例遭受的各攻击类型总次数占比情况。
6. 在事件详情页面 “TOP5 展示”模块，可查看攻击源 IP TOP5 和攻击源地区TOP5，准确把握攻击源的详细情况便于精准防护策略的制定。
>?此处数据为该攻击时间段内攻击采样数据，非全量数据。

![](https://qcloudimg.tencent-cloud.cn/raw/5e70e40264c9511b6357bce58ee1cc14.png)
7. 在事件详情页面的攻击源信息模块，可查看该攻击时间段内攻击详情的随机采样数据，尽可能详细的展示出此次攻击的细节，主要包括攻击源 IP、地域、累计攻击流量、累计攻击包量。
>?此处数据为该攻击时间段内攻击采样数据，非全量数据。

![](https://qcloudimg.tencent-cloud.cn/raw/146b6107c5ceac3a3d1afccd66798c01.png)

## DDoS 高防 IP 概览
将防护 IP 接入到 DDoS 高防 IP 服务后，当用户收到 DDoS 攻击提醒信息或发现业务出现异常时，需要快速了解攻击情况，包括攻击流量大小、防护效果等，可在控制台进行查看。在掌握足够信息后，才可以采取更有效的处理方式，第一时间保障业务正常。


### 查看 DDoS 攻击防护情况
1.	登录 [DDoS 高防 IP（境外企业版）](https://console.cloud.tencent.com/ddos/ddos-basic) 控制台。在左侧导航栏中，单击**防护概览** > **DDoS 高防 IP**。
![](https://qcloudimg.tencent-cloud.cn/raw/be67d057c2ece542e53b3730a5cf9945.png)
1. 在 DDoS 攻击页签，设置查询时间范围，单击选择**全部线路** > **Anycast**，查看是否存在攻击。默认展示全量资产的DDoS攻击数据。
>?支持查询最多180天以内的攻击流量信息及 DDoS 攻击事件。

![](https://qcloudimg.tencent-cloud.cn/raw/f35b004d7113c0874a569d0dcc7cdbdd.png)
2. 查看该时间范围内所选择的高防 IP 防护遭受的攻击情况，包括网络攻击流量带宽 / 攻击包速率趋势。
![](https://qcloudimg.tencent-cloud.cn/raw/7fa11d7c8ff40d20534259e9159134b7.png)
3. 在近期安全事件模块中，可展示所遭受的 DDoS 攻击事件。单击**查看详情**，可查看该事件的具体详情。
![](https://qcloudimg.tencent-cloud.cn/raw/61528176e7f8297f3532901bca36c761.png)
    - 支持查看攻击源信息、攻击源地区、产生的攻击流量及攻击包量大小等。供用户进行 DDoS 攻击分析及溯源支撑。
![](https://qcloudimg.tencent-cloud.cn/raw/4aa25f97c6f9dbaee1a1d747f315b428.png)
    - 单击**攻击包下载**，可看到该攻击时间段的攻击采样数据列表。
![](https://qcloudimg.tencent-cloud.cn/raw/5bcbb304872f4271d7c431bcecc37486.png)
    - 下载本次攻击计时间段的攻击包采样数据，了解攻击详情，为制定针对性的防护方案提供数据支撑。
    ![](https://qcloudimg.tencent-cloud.cn/raw/eab5a834b67e6d95e8283b54aeedb37c.png)
4. 在攻击统计模块中，可通过攻击流量协议分布、攻击包协议分布和攻击类型分布，查看这三个数据维度下的攻击分布情况。
![](https://qcloudimg.tencent-cloud.cn/raw/e065d87c5e7a90bc920f1658f4f45ad2.png)
   **字段说明：**
    - 攻击流量协议分布：查看该时间范围内，所选择的高防 IP 实例遭受攻击事件中各协议总攻击流量的占比情况。
    - 攻击包协议分布：查看该时间范围内，所选择的高防 IP 实例遭受攻击事件中各协议攻击包总数的占比情况。
    - 攻击类型分布：查看该时间范围内，所选择的高防 IP 实例遭受的各攻击类型总次数占比情况。
5. 在攻击来源模块中，可查看该时间范围内，所遭受 DDoS 攻击事件的攻击源在国内、全球的分布情况，便于用户清晰了解攻击来源情况，为进一步防护措施提供基础依据。
![](https://qcloudimg.tencent-cloud.cn/raw/ade8f4dcbcdd71e35af7116b2a7b8941.png)

### 查看 CC 攻击防护情况
1. 单击 **CC 攻击**防护页签，设置查询时间范围，单击选择**全部线路** > **Anycast**，查看是否存在 CC 攻击。
![](https://qcloudimg.tencent-cloud.cn/raw/0a53677659c3787cdc8664799aab047a.png)
2. 用户可以选择**今天**，查看所选择的高防包的请求数趋势和请求速率的相关数据。通过观察总请求速率、攻击请求速率、总请求数量、攻击请求次数相关数据判定业务受影响程度。
![](https://qcloudimg.tencent-cloud.cn/raw/1a4919ceb93c145acc3a4a80ff4c5dda.png)
   **字段说明：**
    - 总请求速率：统计当前，高防 IP 接收到的总请求流量的速率（QPS）。
    - 攻击请求速率：统计当前，攻击请求流量的速率（QPS）。
    - 总请求数量：统计当前，高防 IP 接收到的总请求数量。
    - 攻击请求次数：统计当前，高防 IP 接收到的攻击请求的次数。
3. 在近期安全事件模块中，如果存在 CC 攻击，系统会记录下攻击的开始时间、结束时间、被攻击域名、被攻击 URI	、总请求峰值、攻击请求峰值和攻击源等信息。单击**查看详情**，展示该事件的具体详情。支持查看攻击信息、攻击趋势、CC 详细记录。
![](https://qcloudimg.tencent-cloud.cn/raw/68b909b0b2d13eff52d6f1f1c7733bdc.png)
