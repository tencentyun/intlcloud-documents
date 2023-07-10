使用日志服务（Cloud Log Service，CLS）与使用 Elasticsearch Service 自建日志系统（如 ELK）费用对比，**将节省约84%费用**。以下为您进行详细对比。

## 费用对比
以日志规模为1亿条/天，每条日志100字节，保存15天，峰值 QPS 在4000为例子。

| 产品 | 刊例价 | 费用详情|
|---------|---------|---------|
| 日志服务 CLS | 38美元/月 | <ul  style="margin: 0;"><li>写流量费用：0.074美元/日</li><li>索引流量费用：0.694美元/日</li><li>日志存储费用：0.084美元/日</li><li>索引存储费用：0.403美元/日<br /> <li>服务请求费用：0.003美元/日</li><li>主题分区租用费用：0.014美元/日<br />详情可前往 [计费示例](https://intl.cloud.tencent.com/document/product/614/37509) 查看 |
| Elasticsearch Service 自建日志系统   |  244美元/月  | <li>节点机型费用：125美元/月<br /> <li>节点存储费用：119美元/月 |

## 费用说明

Elasticsearch Service 费用详情如下：
**节点机型选择**：
选购 ES.S1.MEDIUM8机型，2核4GB，三节点部署，费用为125美元/月。

**节点存储费用**：
 - 根据 [Elasticsearch Service](https://intl.cloud.tencent.com/document/product/845/19551) 官网文档建议，选择副本数量为1，增加数据可靠性；预留50%的存储空间，保证服务的稳定性。
 - 实际容量估算公式：
   存储容量 = 源数据 ×（1 + 副本数量）× 1.45 ×（1 + 预留空间）≈ 源数据 ×（1 + 副本数量）× 2.2 = 614.46GB
   每个节点选购210GB SSD 硬盘，三节点费用为119美元/月。
>?集群配置选购请参见 [集群规格和容量配置评估](https://intl.cloud.tencent.com/document/product/845/19551) 文档。





