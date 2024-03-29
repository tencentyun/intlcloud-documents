腾讯云已提供全面升级后的 [边缘安全加速平台（TencentCloud EdgeOne，简称 EdgeOne）](https://intl.cloud.tencent.com/document/product/1145/45961)。EdgeOne 基于腾讯云遍布全球的边缘节点，可为用户同时提供内容分发网络加速和边缘安全防护能力，相比传统独立的安全防护和加速产品，EdgeOne 在边缘节点上提供了开箱即用的安全防护能力，构建了更加完善的 DDoS 防护、Web 防护、Bot 管理能力，支持各类丰富的自定义规则管控，为用户提供了更灵活、更强大的安全防护能力。

如果您现在已接入 CDN 并有安全防护需求，您可以参考以下步骤将当前服务迁移至 EdgeOne 平台，通过 EdgeOne 为您提供 CDN 加速及安全防护能力。

## 操作步骤

### 步骤一：确定当前需开启安全防护的域名

EdgeOne 将以 [站点](https://intl.cloud.tencent.com/document/product/1145/46435) 维度提供套餐购买和安全防护能力，如果您需要迁移至 EdgeOne，您需先确认当前需开启安全防护的域名对应的站点个数，来了解迁移至 EdgeOne 后需要使用多少个站点。您可以参照下表的示例进行评估：

| 需开启安全防护的 CDN 域名                                      | 对应 EdgeOne 站点         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------- | ------------------------------------------------------------ |
| `www.example.com`<br/>`test.example.com`<br/>`image.example.com` | `example.com`               | 主域名均一致，仅需要接入一个站点使用，针对全站所有域名开启安全防护 |
| `www.example.com`<br/>`test.example.com`<br/>`www.site.com`      | `example.com`<br />`site.com` | 主域名存在不一致，需要分别接入 `example.com` 和 `site.com` 两个站点，再分别针对对应站点域名开启安全防护 |


### 步骤二：前往EdegOne 控制台接入站点及加速域名

前往 [EdgeOne 控制台](https://console.cloud.tencent.com/edgeone)，根据步骤一中需开启安全防护的 CDN 域名，完成对应的 EdgeOne 站点接入，并添加加速域名。详细步骤可以参考 [从零开始快速接入 EdgeOne](https://www.tencentcloud.com/document/product/1145/54208)。

接入站点需购买 EdgeOne 套餐，推荐购买 EdgeOne 标准版套餐，套餐内资源已默认包含 DDoS 防护、Web 防护、CC 防护以及 BOT 管理能力，并赠送经防护后的 CDN 流量和请求数。详细套餐介绍可参考：[EdgeOne 套餐](https://intl.cloud.tencent.com/document/product/1145/48705)。

>?EdgeOne 提供了开箱即用的安全防护能力。添加加速域名后，域名将自动开启安全防护（包括 DDos 防护和 Web 防护）。如果您希望根据当前的业务情况，自定义调整安全防护的规则配置，您可以继续参考步骤三进行调整。


### 步骤三（可选）：个性化配置安全防护策略

如果您需要根据当前的业务个性化配置安全策略，例如：添加 IP 黑白名单、配置区域封禁、自定义 Web 防护规则。可参考以下文档了解如何进行配置。

- [DDoS 防护](https://intl.cloud.tencent.com/document/product/1145/47795)
- [Web 防护](https://intl.cloud.tencent.com/document/product/1145/46729)
- [Bot 管理](https://intl.cloud.tencent.com/document/product/1145/47912)


## CDN 资源包退费

如果您当前已购买 EdgeOne 套餐，并确认将服务迁移至 EdgeOne 平台内使用，CDN 内还存在未用完的资源包时，可以 [提交工单](https://console.intl.cloud.tencent.com/workorder/category)，提供相关购买记录后，按照资源包剩余用量的百分比为您提供资源包退款。
