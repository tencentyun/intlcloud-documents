概览页面可浏览当前账户下 WAF 实例信息，攻击概览，安全分析等模块。

## 安全概览
1. 登录 [Web 应用防火墙控制台](https://console.cloud.tencent.com/guanjia/tea-overview)，在左侧导航栏中，选择**概览**，进入概览页面。
2. 在概览页面，左上角选择对应域名，即可查看该域名的概览信息。
![](https://qcloudimg.tencent-cloud.cn/raw/23dfbc23419f0245f479ef3af9c08a5d.png)

## 实例概览
在概览页面，左上角选择对应域名，单击**包含x个实例**，即可查看当前账户下已购实例过期信息。
 ![](https://qcloudimg.tencent-cloud.cn/raw/81f0cdb46e064821cc004276b9269b3c.png)

## 规则更新动态
在概览页面的规则更新动态模块，单击右上角的**查看更多**，即可查看当前 WAF 支持的 Web 规则库。
![](https://qcloudimg.tencent-cloud.cn/raw/54962f9ed88750627ca66efa4a273313.png)


## 攻击总览
#### 全部域名
1. 当安全概览为全部域名时，攻击总览统计数据为全局攻击数，统计周期可以通过筛选显示。
![](https://qcloudimg.tencent-cloud.cn/raw/83aa0ad35a197fd6cb27c3b660dbf224.png)
2. 同时，在页面下方可以查看域名 Web 攻击次数 TOP5(次)、攻击来源 IP TOP5(次) 、域名 CC 攻击次数 TOP5(次)等信息。
![](https://qcloudimg.tencent-cloud.cn/raw/fbab1ef15352085f9fe3f17b23fa3f37.png)

**字段说明：**
 - 域名 Web 攻击次数 TOP5(次)：展示全部实例中受到攻击最多的5个域名。
 - 攻击来源 IP TOP5(次) ：展示全部实例中受到攻击最多的5个 IP。
 - 域名 CC 攻击次数 TOP5(次) ：展示全部实例中受到攻击最多的5个域名。
 - 请求来源 IP TOP5(次) ：展示全部实例中访问最多的5个 IP。
 - 攻击来源区域分布(次)：展示全部实例中攻击来源分布的地区。
 - 攻击类型占比：展示全部实例中攻击类型的分布。
 - 浏览器类型占比：展示全部实例中浏览器类型的分布。



#### 单个域名
1. 当安全概览为单个域名时，攻击总览统计数据为单个域名收到攻击数，统计周期可以通过筛选显示。
![](https://qcloudimg.tencent-cloud.cn/raw/e0d1d9f2c98d03468dfe0b6e02f88f3f.png)
2. 同时，在页面下方可以查看攻击来源 IP TOP5(次)、请求来源 IP TOP5(次) 、攻击来源区域分布(次)等信息。
![](https://qcloudimg.tencent-cloud.cn/raw/37feb6d131391509a6ddf03eb9be6bdd.png)

**字段说明：**
 - 攻击来源 IP TOP5(次) ：展示全部实例中受到攻击最多的5个 IP。
 - 请求来源 IP TOP5(次) ：展示全部实例中访问最多的5个 IP。
 - 攻击来源区域分布(次)：展示全部实例中攻击来源分布的地区。
 - 攻击类型占比：展示全部实例中攻击类型的分布。
 - 浏览器类型占比：展示全部实例中浏览器类型的分布。

## 概览安全分析
- 基础安全：分析描述了当前选择的域名在统计周期内所受到的 Web 攻击次数。
![](https://qcloudimg.tencent-cloud.cn/raw/e2da627fcd6fc8a8cbdd34f497504493.png)
- 业务运营：分析描述了当前选择的域名在统计周期内的 QPS 及带宽详情，右侧统计了该域名统计周期内的响应及访问次数的 Top 值。
![](https://qcloudimg.tencent-cloud.cn/raw/1b5157b79a67dd09b4fa4bc270ce850a.png)
- BOT 与业务安全：描述了当前域名在统计周期内的 BOT 信息，单击前往 [BOT流量分析](https://console.cloud.tencent.com/guanjia/tea-flowanalysis) 即可查看 BOT 与业务安全的流量信息。
![](https://qcloudimg.tencent-cloud.cn/raw/faca16583c5cc20ac85c54ece1d59ce1.png)
