## 防护说明
CC 防护根据访问特征和连接状态判定恶意行为， 阻断黑客的攻击。可根据不同的攻击场景配置相应的防护策略，保证业务稳定。清洗阈值是高防产品启动清洗动作的阈值。
>? CC 防护开关是控制是否启用 CC 防护的总开关，开启后下方的防护策略才能生效。

## 前提条件
您需要成功 [购买 DDoS 高防包](https://intl.cloud.tencent.com/document/product/1029/36115) ，并设置防护对象。

## 操作步骤
1. 登录 [DDoS 高防（新版）管理控制台](https://console.cloud.tencent.com/ddos/antiddos-native/config/port) ，在左侧导航中，单击**防护配置** > **CC 防护**。
2. 在 CC 防护页面的左侧列表中，选中高防包的 ID，如“bgp-00xxxxxx”。
![](https://qcloudimg.tencent-cloud.cn/raw/48b33703155d1418b3a1c3aab979e8f4.png)
3. 在 CC 防护开关及清洗阈值卡片中，单击![](https://qcloudimg.tencent-cloud.cn/raw/b56da8e70914bb5f6fce1900bcf81ef5.png)开启 CC 防护开关，当防护开启后必须进行清洗阈值设置否则无法使用 CC 防护。
>?清洗阈值是高防产品启动清洗动作的阈值，当指定域名收到的 HTTP 请求超过阈值时，将触发 CC 防护。

![](https://qcloudimg.tencent-cloud.cn/raw/48b33703155d1418b3a1c3aab979e8f4.png)
4. 在 CC 防护开关和清洗阈值卡片中，单击**设置**，进入 CC 防护开关和清洗阈值规则列表。
5. 在 CC 防护开关和清洗阈值规则列表中，单击左上角**新建**，输入所需参数和清洗阈值。
>?
>- 新建规则时，默认 CC 防护开关为打开状态。
>- 清洗阈值为默认，业务刚接入的 DDoS 高防包实例的清洗阈值采用默认值，并随着接入业务流量的变化规律，系统自动学习形成一个基线值。并支持对单个域名维度进行清洗阈值自定义设置。

![](https://qcloudimg.tencent-cloud.cn/raw/9ff82f6f7a954a392a39de161655875d.png)
6.	单击**保存**，添加规则。
>!精细化的规则优先级高于高防包实例全局维度下的规则。

7. 新建完成后，在 CC 防护开关及清洗阈值列表中，将新增一条 CC 防护域名规则。在自定义模式下，单击![](https://qcloudimg.tencent-cloud.cn/raw/5034a8bab40f77233b1c6e7654414019.png)和![](https://qcloudimg.tencent-cloud.cn/raw/7655c41673eb4d876ab44f11c5ade35f.png) ，支持修改 CC 防护域名开关和清洗阈值。
![](https://qcloudimg.tencent-cloud.cn/raw/33ef39ad86b2400066b9d908cc2516c0.png)



