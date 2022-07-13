开启智能防护后，AI 智能防护基于腾讯云的大数据能力，能够自学习网站业务流量基线，结合算法分析攻击异常，并自动下发精确的防护规则，动态调整业务防护模型，帮助您及时发现并阻断恶意攻击。
>?该功能为灰度上线阶段，部分用户暂无法使用敬请期待全量上线。

## 前提条件
- 您需要已成功 [购买 DDoS 高防 IP](https://intl.cloud.tencent.com/document/product/297/37241)，并设置防护对象。
- 智能 CC 防护当前仅支持域名接入的规则生效。

## 操作步骤
1. 登录 [DDoS 高防 IP（新版）管理控制台](https://console.cloud.tencent.com/ddos/antiddos-advanced/config/port)，在左侧导航中，单击**防护配置** > **CC 防护**。
2. 在 CC 防护页面的左侧列表中，选中高防 IP 的 ID 下面的域名。
![](https://qcloudimg.tencent-cloud.cn/raw/91440456fbdd3f9d56b9ed0c23943223.png)
3. 在 CC 防护开关及清洗阈值卡片中，单击![](https://qcloudimg.tencent-cloud.cn/raw/9795d7ce17dc03f5be0daae4ef488f98.png)开启 CC 防护开关，当防护开启后必须设置清洗阈值，否则无法使用智能 CC 防护。
>?
>- 清洗阈值是高防产品启动清洗动作的阈值，当指定域名收到的 HTTP 请求超过阈值时，将触发 CC 防护。
>- 当高防包的 IP 为“Web 应用防火墙” 的 IP 时，需要先到 [Web 应用防火墙控制台](https://console.cloud.tencent.com/guanjia/tea-baseconfig) 为此 IP 开启 CC 防护，详情请参见 [CC 防护规则设置](https://intl.cloud.tencent.com/document/product/627/11709)。

![](https://qcloudimg.tencent-cloud.cn/raw/9ebf3f22e757352b303cc1b0183080d2.png)
4. 在智能 CC 防护卡片中，单击![](https://qcloudimg.tencent-cloud.cn/raw/9795d7ce17dc03f5be0daae4ef488f98.png)开启智能防护。
![](https://qcloudimg.tencent-cloud.cn/raw/7eab58ff66f68d1c3b156b017aefbe47.png)
5. 开启智能 CC 防护后，基于每次攻击，智能防护自动生成防护规则。智能防护下发的规则存在**单次有效期**，单次攻击结束后，防护规则自动失效并清除。若需要针对下一次攻击调整。请单击右侧**查看**进行智能防护规则编辑。
![](https://qcloudimg.tencent-cloud.cn/raw/46c4a1943a9d0d8852aa76522afb4ede.png)
6. 智能防护规则基于单次攻击自动生成与生效。智能防护下发的规则存在单次有效期，单次攻击结束后，防护规则自动失效并清除。根据防护需求，可单击**删除**，删除对应防护规则。
![](https://qcloudimg.tencent-cloud.cn/raw/58151e5f35b23c82fe6a35c390857316.png)
