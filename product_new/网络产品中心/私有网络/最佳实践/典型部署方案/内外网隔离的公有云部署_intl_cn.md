## 应用场景
公有云多租户共享资源池，数据泄露的风险指数较高。用户希望在公有云上能有一个完全隔离的网络环境来部署云资源。
**用户关注重点**：
网络环境与其它租户完全隔离，规避多租户共享带来的安全风险。

## 解决方案
您可以通过腾讯云私有网络，创建一个隔离的网络环境来规避上述风险。私有网络（Virtual Private Cloud，VPC）是基于腾讯云构建的专属云上网络空间，为您在腾讯云上的资源提供网络服务，不同私有网络间完全逻辑隔离。作为您在云上的专属网络空间，您可以通过软件定义网络的方式管理您的私有网络 VPC，实现 IP 地址、子网、[路由表](https://intl.cloud.tencent.com/document/product/215/4954)、[网络 ACL ](https://intl.cloud.tencent.com/document/product/215/5132)、流日志等功能的配置管理。私有网络还支持多种方式连接 Internet，如 [弹性 IP](https://intl.cloud.tencent.com/document/product/215/4958) 、NAT 网关您也可以通过 VPN 连接或 [专线接入](https://intl.cloud.tencent.com/document/product/216) 连通腾讯云与您本地的数据中心，灵活构建混合云。
更多私有网络介绍详情，请参见 [产品概述](http://intl.cloud.tencent.com/document/product/215/535)。

## 操作步骤
1. 创建私有网络、初始化子网和路由表，详情请参见 [创建私有网络](http://intl.cloud.tencent.com/document/product/215/8113)。
2. 创建子网，详情请参见 [创建子网](http://intl.cloud.tencent.com/document/product/215/8114)。
3. 新建路由表并关联子网，详情请参见 [创建子网](http://intl.cloud.tencent.com/document/product/215/8115)。
4. 向子网中添加云服务器、数据库等，详情请参见 [添加云服务器](http://intl.cloud.tencent.com/document/product/215/8116)。
更多操作步骤说明，请参见 [快速入门](http://intl.cloud.tencent.com/document/product/215/8119)。
