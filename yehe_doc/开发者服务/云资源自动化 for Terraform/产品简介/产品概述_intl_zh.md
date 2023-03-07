云资源自动化 for Terraform（Tencent Infrastructure Automation for Terraform）是腾讯云基于全球备受欢迎的基础设施即代码（Infrastructure as Code）工具 Terraform 插件扩展体系下，提供云资源部署、实施和管理的自动化能力，旨在将 Terraform 完善成熟的基础设施自动化工具能力和腾讯云的云资源服务能力相互联接，让客户可以方便地实施 DevOps 和多云部署等模式。示意图如下：

![](https://qcloudimg.tencent-cloud.cn/image/document/76036968d48021e6577e022565a8c685.png)

[腾讯云 Provider](https://github.com/tencentcloudstack/terraform-provider-tencentcloud.git) 通过腾讯云 API 提供的 [Go SDK](https://github.com/TencentCloud/tencentcloud-sdk-go) 实现腾讯云产品管理，目前已经提供超过272个 Resource 和194个 Data Source，覆盖计算、存储、网络、容器服务、负载均衡、中间件、数据库、云监控等40款产品，已经支持多个海内外大客户的上云需求。

您可以通过腾讯云提供的完整的[ Terraform 文档](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs) 和 [Terraform 样例](https://github.com/tencentcloudstack/terraform-provider-tencentcloud/tree/master/examples)，来快速了解并开始使用 Terraform。