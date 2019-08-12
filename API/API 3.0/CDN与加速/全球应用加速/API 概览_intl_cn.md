## 源站相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [AddRealServers](/document/api/608/37014) | 添加源站 |
| [DescribeRealServers](/document/api/608/37013) | 查询源站信息 |
| [DescribeRealServersStatus](/document/api/608/37012) | 查询源站绑定状态 |
| [ModifyRealServerName](/document/api/608/37011) | 修改源站名称 |
| [RemoveRealServers](/document/api/608/37010) | 删除源站 |

## 监听器相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [BindListenerRealServers](/document/api/608/37008) | 监听器绑定源站 |
| [CreateHTTPListener](/document/api/608/37007) | 创建HTTP监听器 |
| [CreateHTTPSListener](/document/api/608/37006) | 创建HTTPS监听器 |
| [CreateTCPListeners](/document/api/608/37005) | 创建TCP监听器 |
| [CreateUDPListeners](/document/api/608/37004) | 创建UDP监听器 |
| [DeleteListeners](/document/api/608/37003) | 删除通道监听器 |
| [DescribeHTTPListeners](/document/api/608/37002) | 查询HTTP监听器信息 |
| [DescribeHTTPSListeners](/document/api/608/37001) | 查询HTTPS监听器信息 |
| [DescribeListenerRealServers](/document/api/608/37000) | 查询监听器源站列表 |
| [DescribeTCPListeners](/document/api/608/36999) | 查询TCP监听器列表 |
| [DescribeUDPListeners](/document/api/608/36998) | 查询UDP监听器列表 |
| [ModifyHTTPListenerAttribute](/document/api/608/36997) | 修改HTTP监听器配置 |
| [ModifyHTTPSListenerAttribute](/document/api/608/36996) | 修改HTTPS监听器配置 |
| [ModifyTCPListenerAttribute](/document/api/608/36995) | 修改TCP监听器配置 |
| [ModifyUDPListenerAttribute](/document/api/608/36994) | 修改UDP监听器配置 |

## 规则相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [BindRuleRealServers](/document/api/608/36992) | 转发规则绑定源站 |
| [CreateDomain](/document/api/608/36991) | 创建HTTPS监听器的访问域名 |
| [CreateRule](/document/api/608/36990) | 创建监听器转发规则 |
| [DeleteDomain](/document/api/608/36989) | 根据域名删除转发规则 |
| [DeleteRule](/document/api/608/36988) | 删除7层监听器转发规则 |
| [DescribeRuleRealServers](/document/api/608/36987) | 查询转发规则相关源站信息 |
| [DescribeRules](/document/api/608/36986) | 查询转发规则信息 |
| [ModifyCertificate](/document/api/608/36985) | 修改域名对应的证书 |
| [ModifyDomain](/document/api/608/36984) | 更新监听器转发规则域名 |
| [ModifyRuleAttribute](/document/api/608/36983) | 修改转发规则信息 |
| [SetAuthentication](/document/api/608/36982) | 认证高级配置 |

## 证书相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [CreateCertificate](/document/api/608/36980) | 创建证书 |
| [DeleteCertificate](/document/api/608/36979) | 删除证书 |
| [DescribeCertificateDetail](/document/api/608/36978) | 查询证书详情 |
| [DescribeCertificates](/document/api/608/36977) | 查询服务器证书列表 |
| [ModifyCertificateAttributes](/document/api/608/36976) | 修改证书属性 |

## 通道相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [CheckProxyCreate](/document/api/608/36974) | 查询通道是否可以创建 |
| [CloseProxies](/document/api/608/36973) | 关闭通道 |
| [CloseSecurityPolicy](/document/api/608/36972) | 关闭安全策略 |
| [CreateProxy](/document/api/608/36971) | 创建通道 |
| [CreateSecurityPolicy](/document/api/608/36970) | 创建安全策略 |
| [CreateSecurityRules](/document/api/608/36969) | 添加安全策略规则 |
| [DeleteSecurityPolicy](/document/api/608/36968) | 删除安全策略 |
| [DeleteSecurityRules](/document/api/608/36967) | 删除安全策略规则 |
| [DescribeAccessRegions](/document/api/608/36966) | 查询加速区域 |
| [DescribeAccessRegionsByDestRegion](/document/api/608/36965) | 根据源站区域查询可用加速区域 |
| [DescribeDestRegions](/document/api/608/36964) | 查询源站区域 |
| [DescribeProxies](/document/api/608/36963) | 查询通道实例列表 |
| [DescribeProxiesStatus](/document/api/608/36962) | 查询通道状态列表 |
| [DescribeProxyAndStatisticsListeners](/document/api/608/36961) | 查询统计通道和监听器信息 |
| [DescribeProxyDetail](/document/api/608/36960) | 查询通道详情 |
| [DescribeSecurityPolicyDetail](/document/api/608/36959) | 获取安全策略详情 |
| [DestroyProxies](/document/api/608/36958) | 销毁通道 |
| [InquiryPriceCreateProxy](/document/api/608/36957) | 创建加速通道询价 |
| [ModifyProxiesAttribute](/document/api/608/36956) | 修改通道的属性 |
| [ModifyProxiesProject](/document/api/608/36955) | 修改通道所属项目 |
| [ModifyProxyConfiguration](/document/api/608/36954) | 修改通道配置 |
| [ModifySecurityRule](/document/api/608/36953) | 修改安全策略规则名 |
| [OpenProxies](/document/api/608/36952) | 开启通道 |
| [OpenSecurityPolicy](/document/api/608/36951) | 开启安全策略 |

## 通道组相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [CreateProxyGroup](/document/api/608/36949) | 创建通道组 |
| [CreateProxyGroupDomain](/document/api/608/36948) | 开通通道组域名 |
| [DeleteProxyGroup](/document/api/608/36947) | 删除通道组 |
| [DescribeCountryAreaMapping](/document/api/608/36946) | 获取国家地区编码映射表 |
| [DescribeGroupDomainConfig](/document/api/608/36945) | 获取通道组域名解析配置详情 |
| [DescribeProxyGroupDetails](/document/api/608/36944) | 查询通道组详情 |
| [DescribeProxyGroupList](/document/api/608/36943) | 拉取通道组列表 |
| [ModifyGroupDomainConfig](/document/api/608/36942) | 配置通道组就近接入域名 |
| [ModifyProxyGroupAttribute](/document/api/608/36941) | 修改通道组属性 |

## 其他接口

| 接口名称 | 接口功能 |
|---------|---------|
| [DescribeGroupAndStatisticsProxy](/document/api/608/37022) | 查询统计通道组和通道信息 |
| [DescribeListenerStatistics](/document/api/608/37021) | 查询监听器统计数据 |
| [DescribeProxyGroupStatistics](/document/api/608/37020) | 查询通道组统计数据 |
| [DescribeProxyStatistics](/document/api/608/37019) | 查询通道统计数据 |
| [DescribeRealServerStatistics](/document/api/608/37018) | 查询已绑定源站健康检查统计数据 |
| [DescribeRegionAndPrice](/document/api/608/37017) | 获取源站区域和带宽梯度价格 |
| [DescribeResourcesByTag](/document/api/608/37016) | 根据标签拉取资源列表 |

