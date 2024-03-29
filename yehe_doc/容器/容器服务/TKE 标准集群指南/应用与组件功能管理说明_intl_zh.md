 

## 组件管理说明

腾讯云容器服务 TKE 提供多种组件，以丰富集群功能，增强集群性能，提升整体稳定性。腾讯云提供三种不同类型的组件：

| 组件类型 | 组件说明 | 相关文档 |
|---------|---------|---------|
|系统组件|用户使用集群默认的必备核心组件：例如 CBS-CSI，IPAMD，监控，日志等，若这些组件异常将可能导致集群故障。|-|
|增强组件|增强组件即扩展组件，是腾讯云容器服务 TKE 提供的扩展功能包，您可以根据业务诉求选择部署所需的扩展组件。|[扩展组件](https://intl.cloud.tencent.com/document/product/457/33988)|
|应用市场|应用市场是腾讯云容器服务 TKE 集成的 [Helm 3.0](https://helm.sh/) 相关功能，为您提供创建 Helm Chart、容器镜像、软件服务等各种产品和服务的能力。| [应用市场](https://intl.cloud.tencent.com/document/product/457/37706)|



<dx-alert infotype="notice" title="">
- **免责声明**：针对应用市场中的应用，腾讯云会保障用户在应用支持的集群类型和 Kubernetes 版本里正常安装应用。除此之外的部分（如运行过程中遇到的应用问题；因为自定义配置的修改导致应用异常；应用不支持指定的集群类型和 Kubernetes 版本）由用户自行负责。
- 腾讯云售后团队向您提供的应用市场里的应用只针对有经验的系统管理员或其他相关 IT 人员，同时腾讯云不提供这些应用的调试及建议实施的 SLA 保障。您在使用应用中如遇到的任何问题，请到应用详情里的参考链接和应用官网反馈。
- 腾讯云容器服务（Tencent Kubernetes Engine，TKE）提供的服务等级协议请参考 [腾讯云容器服务服务等级协议](https://intl.cloud.tencent.com/document/product/457/12356)。
</dx-alert>

三种不同类型组件管理方式如下：

| 组件类型                       | 包含范围                                                     | 服务支持力度                                                 | 升级方式                                                     |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 系统组件<br>（默认安装，无法删除） | CBS-CSI，IPAMD，监控，日志等                                 | TKE 会优先保障系统组件稳定性，会在后台及时更新和修复涉及到安全和兼容的问题。 | 某些拥有特殊功能的版本，TKE 不会后台自动更新，您可以根据实际需要自行更新，详情见 [组件版本维护说明](https://intl.cloud.tencent.com/document/product/457/49395)。 |
| 增强组件<br>（用户自定义安装）     | 完整列表请 [查看](https://intl.cloud.tencent.com/document/product/457/33988) | TKE 会保障增强组件稳定性，会在后台及时更新和发布修复涉及到安全和兼容问题。每个增强组件有支持的版本列表，若您没有及时更新，组件可能会失效。 | 某些拥有特殊功能的版本，TKE 不会后台自动更新，您可以根据实际需要自行更新，详情见 [组件版本维护说明](https://intl.cloud.tencent.com/document/product/457/49395)。 |
| 应用市场<br>（用户自定义安装）     | 完整列表请 [查看](https://console.cloud.tencent.com/tke2/market) | TKE 仅保障应用在支持的集群类型和 Kubernetes 版本里安装部署。 | 提供应用更新升级的方式，会不定期推送应用的新 Chart，操作详情见 [更新应用](https://intl.cloud.tencent.com/document/product/457/30683)。 |



## 功能管理说明

针对部分功能，TKE 会在功能的文档和控制台上标识：“预览版”，表示该功能为抢先体验版，不在 [腾讯云容器服务服务等级协议](https://intl.cloud.tencent.com/document/product/457/12356) 保障范围内。
