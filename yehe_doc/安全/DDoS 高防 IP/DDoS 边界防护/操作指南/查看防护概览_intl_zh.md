用户将业务接入 DDoS 边界防护服务，并且将业务流量切换至 DDoS 边界防护后，可在控制台查看 DDoS 攻击防护情况、CC 攻击情况、Web 攻击情况和业务流量情况 。
>?目前 DDoS 边界防护产品处于灰度优化中，如有需要，请 [联系我们](https://intl.cloud.tencent.com/contact-us) 申请。

## 查看 DDoS 攻击防护情况
1. 登录 [DDoS 边界防护管理控制台](https://console.cloud.tencent.com/ddos/antiddos-edge/overview/ddos) ，在左侧导航中，单击**防护概览**，并选择 **DDoS 攻击防护**。
2. 在 DDoS 攻击防护页面，单击切换“时间”，可以设置查询时间范围。
>?支持查询最多180天以内的攻击流量信息及 DDoS 攻击事件。

![](https://qcloudimg.tencent-cloud.cn/raw/d81f2ef90e98950154227f4a5e6b660f.png)
3. 在 DDoS 攻击防护页面的实例下拉框中，通过单击![](https://main.qcloudimg.com/raw/74853a065cabb2c2d5df9fccd42fe984.png)搜索边界防护实例，查看是否存在 DDoS 攻击。
![](https://qcloudimg.tencent-cloud.cn/raw/3f81e2e57dc682eaa4e178bac0267deb.png)
 - **攻击流量带宽**
查看该时间范围内所选择的实例遭受的攻击情况，包括网络攻击流量带宽 / 攻击包速率趋势。当遭受攻击时，在流量趋势图中可以明显看出攻击流量的峰值。
 ![](https://qcloudimg.tencent-cloud.cn/raw/6314869b3536ce5bf3b00f38ab817d38.png)
 - **攻击事件**
了解每一次攻击事件的攻击（开始）时间、持续时间、攻击类型以及攻击状态。
>!
>- 只能查询单个边界防护实例遭受攻击的攻击源信息。
>- 攻击源信息为抽样数据，即随机抓包统计的数据，在攻击结束后大约5分钟后才会显示数据。

 ![](https://qcloudimg.tencent-cloud.cn/raw/efb5a5d77f70cc2a61888d9eb00f9038.png)
 - **攻击统计**
通过查看攻击总流量、攻击包量和攻击总次数三个维度的数据，了解该时间范围内的攻击情况。
>?
>- 攻击总流量：查看该时间范围内，所选择的实例遭受攻击事件中各协议总攻击流量的占比情况。
>- 攻击包量：查询该时间范围内，所选择的实例遭受攻击事件中各协议攻击包总数的占比情况。
>- 攻击总次数：查询该时间范围内，所选择的实例遭受的各攻击类型总次数占比情况。

 ![](https://qcloudimg.tencent-cloud.cn/raw/59f8a2c0c90cf269479f0b464312edea.png)


## 查看 CC 攻击防护情况
1. 登录 [DDoS 边界防护管理控制台](https://console.cloud.tencent.com/ddos/antiddos-edge/overview/ddos) ，在左侧导航中，单击**防护概览**，并选择 **CC 攻击防护**。
2. 在 CC 攻击防护页面，单击切换“时间”，可以设置查询时间范围。
>?支持查询最多180天以内的攻击请求数信息及 CC 攻击事件。

![](https://qcloudimg.tencent-cloud.cn/raw/d5f5aaa806aada8fc9be8e06aa76418d.png)
3. 在 CC 攻击防护页面的实例下拉框中，通过单击![](https://main.qcloudimg.com/raw/74853a065cabb2c2d5df9fccd42fe984.png)搜索边界防护实例，查看是否存在 CC 攻击。
![](https://qcloudimg.tencent-cloud.cn/raw/860193f7a2d1f9570ff6ca6e9303cf61.png)

- **攻击流量带宽**
    - 用户可以选择**今天**查看所选择的边界防护实例的攻击请求数趋势。通过观察总请求值是否远高于正常情况下的业务访问量（QPS），并查看攻击 QPS 是否有数值且数值超大。
>?
>- 总请求峰值：统计遭受攻击时，被防护 IP 接收到的总请求流量峰值。
>- 攻击请求峰值：统计遭受攻击时， 由边界系统阻断的请求次数峰值。

![](https://qcloudimg.tencent-cloud.cn/raw/e9018d9bfc96d8c60692a7be8b2b0986.png)

- **CC 攻击记录**
如果存在 CC 攻击，系统会记录下攻击的开始时间、结束时间、被攻击域名、被攻击 url、总请求峰值、攻击请求峰值和攻击源等信息。


## 查看 Web 攻击防护情况
1. 登录 [DDoS 边界防护管理控制台](https://console.cloud.tencent.com/ddos/antiddos-edge/overview/ddos) ，在左侧导航中，单击**防护概览**，并选择 **Web 攻击防护**。
2. 在 Web 攻击防护页面，单击切换“时间”，可以设置查询时间范围。
>? 支持查询最多180天以内的攻击流量信息及 DDoS 攻击事件。

![](https://qcloudimg.tencent-cloud.cn/raw/8bac3facf58a7061fe7a3e1d4e6121b0.png)
3. 在 Web 攻击防护页面的实例下拉框中，通过单击![](https://main.qcloudimg.com/raw/74853a065cabb2c2d5df9fccd42fe984.png)搜索边界防护实例，查看是否存在Web 攻击。
![](https://qcloudimg.tencent-cloud.cn/raw/a353cea39b68f991b11e494e8238cf91.png)
 - **攻击趋势**
查看该时间范围内所选择的实例遭受的攻击情况，包括网络攻击峰值和攻击总次数。
![](https://qcloudimg.tencent-cloud.cn/raw/472470e7080f7f98d8ce2e4153bd6819.png)
 - **攻击事件**
了解每一次攻击事件的攻击（开始）时间、被攻击域名、被攻击 url 以及攻击类型。
![](https://qcloudimg.tencent-cloud.cn/raw/2e32e6ef07290c8d1b0e4adf97014fc1.png)
 - **攻击统计**
通过查看攻击总流量、攻击包量和攻击总次数三个维度的数据，了解该时间范围内的攻击情况。
>?
>- 攻击次数最多的域名 Top5：查看该时间范围内，所选择的实例遭受攻击最多的域名情况。
>- 攻击来源 ip Top5：查询该时间范围内，所选择的 实例遭受攻击事件中攻击来源 ip Top5 情况。
>- 攻击类型分布：查询该时间范围内，所选择的实例遭受的各攻击类型分布情况。

![](https://qcloudimg.tencent-cloud.cn/raw/93ee1a1a8af91cb8dd17dc3c1d4306a9.png)

## 查看业务流量情况
1. 登录 [DDoS 边界防护管理控制台](https://console.cloud.tencent.com/ddos/antiddos-edge/overview/ddos) ，在左侧导航中，单击**防护概览**，并选择**业务**。
2. 在业务页面，单击切换“时间”，可以设置查询时间范围。
>?支持查询最多180天以内的业务信息。

![](https://qcloudimg.tencent-cloud.cn/raw/fcabf582cd95fb9c6f721a61d568f2fc.png)
3. 在业务页面的实例下拉框中，通过单击![](https://main.qcloudimg.com/raw/74853a065cabb2c2d5df9fccd42fe984.png)搜索边界防护实例。
![](https://qcloudimg.tencent-cloud.cn/raw/3a646391dc4c86940e5a7769b0ade00d.png)

 - 查看该时间范围内的业务带宽峰值、业务连接数峰值和业务请求峰值。
 ![](https://qcloudimg.tencent-cloud.cn/raw/ea3c1c11a67a6d45cfdb9a708895fae1.png)

 - 查看所选择时间范围内的入/出业务流量带宽趋势、入/出业务包速率的趋势及活跃连接数和新建连接数的趋势。
![](https://qcloudimg.tencent-cloud.cn/raw/8f463bf3ebc782567a4403560cf47012.png)

 - 查看所选择时间范围内的活跃连接数、新建连接数和状态码的趋势。
>?
>- 活跃连接数：当前时间所有 established 状态的 TCP 连接数。
>- 新建连接数：客户端每秒内新增的与边界建立通信的 TCP 连接数。

 ![](https://qcloudimg.tencent-cloud.cn/raw/f8d93ebc6eb4576b2a99471f1dddc5c2.png)
