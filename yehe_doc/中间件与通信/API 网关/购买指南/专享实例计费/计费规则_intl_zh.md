专享实例是 API 网关提供的高阶实例，底层资源由用户独享，相较于共享实例可提供更高的性能和 SLA 保证，更适合生产环境使用，面向大型客户。关于共享实例与专享实例之间的对比选择请您参考 [实例选择指南](https://intl.cloud.tencent.com/document/product/628/40305)。

本文主要介绍专享实例的计费方式和计费规则。

## 计费项目

API 网关专享实例的计费项包括：实例费用和外网出流量费用。

### 实例费用

实例费用提供包年包月和按量计费两种方式，两种计费方式的对比如下：

| 实例计费模式 |              包年包月              |                           按量计费                           |
| ------------ | :--------------------------------: | :----------------------------------------------------------: |
| 付款方式     |               预付费               | 购买时 [冻结费用](https://intl.cloud.tencent.com/document/product/555/12039)，每小时结算 |
| 计费单位     |               美元/月                |                            美元/秒                             |
| 单价         |              单价较低              |                           单价较高                           |
| 最少使用时长 |           至少使用一个月           |      按秒计费，每小时整点进行一次结算，随时购买随时释放      |
| 使用场景     | 适用于设备需求量长期稳定的成熟业务 |         适用于电商抢购等设备需求量瞬间大幅波动的场景         |

### 外网出流量费用

外网出流量指的是 API 网关到客户端的出流量，根据使用的公网流量计费，付费模式为后付费，每小时结算一次。

> !若您购买了出流量资源包，在资源包有效期内将优先抵扣资源包中的出流量，超出的部分按照按量计费方式计费。详情参考 [资源包计费](https://intl.cloud.tencent.com/document/product/628/38407)。

流量走向：
![](https://main.qcloudimg.com/raw/8d816cd1a15d788a53a3eecb06eb94c4.png)

| 计费项     | 计费项含义                                                   | 计费说明                         |
| :--------- | :----------------------------------------------------------- | :------------------------------- |
| 内网出流量 | 数据通过腾讯云内网从 API 网关传输到后端服务产生的流量        | 免费                             |
| 内网入流量 | 数据通过腾讯云内网从客户端传输到 API 网关 产生的流量         | 免费                             |
| 外网出流量 | 数据通过互联网从客户端传输到 API 网关后，API 网关返回响应数据所产生的流量 | 按小时结算 每 GB 单价 * 小时累计 |
| 外网入流量 | 数据通过互联网从客户端传输到 API 网关产生的流量              | 免费                             |
