

为满足不同使用场景下的用户需求，TDMQ Pulsar 提供了`专业集群`和`虚拟集群`两种产品形态。当您在购买 Pulsar 集群时，建议综合业务应用场景、产品能力、使用成本等因素，做出产品选型判断。


## 产品系列

一图了解消息队列 TDMQ Pulsar 版的产品系列。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/3mS4348_PRELIM__%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20Pulsar%20%E7%89%88_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.jpg)

## 建议选型流程

建议您根据以下流程进行产品选型。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/a7Gg310_PRELIM__%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20Pulsar%20%E7%89%88_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-2.jpg)

## 产品选型分析

以下从不同维度对比 TDMQ Pulsar 两种不同集群类型的特性：

<table>
  <tr>
    <th class="align-left">对比项</th>
    <th class="align-left">虚拟集群</th>
    <th class="align-left">专业集群</th>
  </tr>
  <tr>
    <td>实例类型</td>
    <td>物理共享，逻辑多租</td>
    <td>物理隔离</td>
  </tr>
  <tr>
    <td>面向客群和场景</td>
    <td>面向入门级客户，业务量适中、短期测试、峰值和均值流量差异较大</td>
    <td>头部客户，对于稳定性和资源隔离性要求高、业务流量大的生产环境</td>
  </tr>
  <tr>
    <td>付费模式</td>
    <td>按量付费-后付费</td>
    <td>包年包月-预付费</td>
  </tr>
  <tr>
    <td>计费项</td>
    <td>API调用费，消息存储费，分区主题资源占用费</td>
    <td>按支持的集群规格，主要包括 TPS 、带宽计费</td>
  </tr>
  <tr>
    <td>收发 TPS 限制</td>
    <td>单集群单 Topic 限制生产、消费各 5000 TPS</td>
    <td>按照不同的计算和存储规格按需自由购买（2000 TPS起）</td>
  </tr>
  <tr>
    <td>SLA</td>
    <td><li>数据可靠性：8个9</li><li>服务可用性：99.95%</li></td>
    <td><li>数据可靠性：10个9</li><li>服务可用性：99.99%</li></td>
  </tr>
  <tr>
    <td>Pulsar 引擎版本</td>
    <td>2.7.2</td>
    <td>2.9.2</td>
  </tr>
    <tr>
    <td>扩容上限</td>
    <td>一定范围弹性扩容、弹性使用</td>
    <td>自由度高，最大支持百万级 TPS</td>
  </tr>

  <tr>
    <td>高可用能力</td>
    <td>不支持同城跨可用区部署</td>
    <td>支持同地域自定义多可用区部署，提升容灾能力</td>
  </tr>
  <tr>
    <td>护航&专家服务</td>
    <td>提供腾讯云标准的工单服务</td>
    <td>提供保驾护航服务，如产品升级、新业务上线、大促营销活动等，保障业务平稳运行</td>
  </tr>

</table>


## 容量评估

在明确所选择的集群类型之后，您需要评估业务实际运行所需的实例规格，包括计算规格和存储规格。

- **计算规格**：TDMQ Pulsar 专业版的计算规格指该集群实例的消息收发 TPS 上限、带宽上限，您需要根据业务实际运行选择合适的计算规格。
- **存储规格**：您可根据业务量预估消息量和消息大小，计算需要的存储空间。

TDMQ Pulsar 专业版的消息存储默认为`3 副本`模式，评估时请注意。


### 购买集群

选择地域，并创建/购买集群。[立即前往](https://buy.cloud.tencent.com/tdmq)。



