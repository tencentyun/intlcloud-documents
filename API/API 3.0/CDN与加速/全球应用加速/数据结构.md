## AccessRegionDetial

根据源站查询的可用加速区域信息及对应的可选带宽和并发量

被如下接口引用：DescribeAccessRegionsByDestRegion。

| 名称 | 类型 |  描述 |
|------|------|-------|
| RegionId | String | 区域ID |
| RegionName | String | 区域的中文或英文名称 |
| ConcurrentList | Array of Integer | 可选的并发量取值数组 |
| BandwidthList | Array of Integer | 可选的带宽取值数组 |

## AccessRegionDomainConf

域名就近接入配置

被如下接口引用：ModifyGroupDomainConfig。

| 名称 | 类型 | 必选 | 描述 |
|------|------|----------|------|
| RegionId | String | 是 | 地域ID。 |
| NationCountryInnerList | Array of String | 否 | 就近接入区域国家内部编码，编码列表可通过DescribeCountryAreaMapping接口获取。 |

## BandwidthPriceGradient

带宽梯度价格

被如下接口引用：DescribeRegionAndPrice、InquiryPriceCreateProxy。

| 名称 | 类型 |  描述 |
|------|------|-------|
| BandwidthRange | Array of Integer | 带宽范围。 |
| BandwidthUnitPrice | Float | 在对应带宽范围内的单宽单价，单位：元/Mbps/天。 |

## BindRealServer

已绑定的源站信息

被如下接口引用：DescribeListenerRealServers、DescribeRuleRealServers、DescribeRules、DescribeTCPListeners、DescribeUDPListeners。

| 名称 | 类型 |  描述 |
|------|------|-------|
| RealServerId | String | 源站ID |
| RealServerIP | String | 源站IP或者域名 |
| RealServerWeight | Integer | 该源站所占权重 |
| RealServerStatus | Integer | 源站状态，异常状态包括IP连接不上和域名解析失败（源站为域名）。其中：<br/>0，源站正常；<br/>1，IP异常；<br/>2，域名解析异常。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| RealServerPort | Integer | 源站的端口号<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| DownIPList | Array of String | 当源站为域名时，域名被解析成一个或者多个IP，该字段表示其中异常的IP列表。 |

## BindRealServerInfo

添加源站的源站信息返回值

被如下接口引用：DescribeRealServers。

| 名称 | 类型 |  描述 |
|------|------|-------|
| RealServerIP | String | 源站的IP或域名 |
| RealServerId | String | 源站ID |
| RealServerName | String | 源站名称 |
| ProjectId | Integer | 项目ID |
| TagSet | Array of [TagPair](#TagPair) | 标签列表<br/>注意：此字段可能返回 null，表示取不到有效值。 |

## Certificate

服务器证书

被如下接口引用：DescribeCertificates。

| 名称 | 类型 |  描述 |
|------|------|-------|
| CertificateId | String | 证书ID |
| CertificateName | String | 证书名称（旧参数，请使用CertificateAlias）。 |
| CertificateType | Integer | 证书类型 |
| CertificateAlias | String | 证书名称。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| CreateTime | Integer | 证书创建时间，采用unix时间戳的方式，表示从1970年1月1日（UTC/GMT的午夜）开始所经过的秒数。 |
| BeginTime | Integer | 证书生效起始时间，采用unix时间戳的方式，表示从1970年1月1日（UTC/GMT的午夜）开始所经过的秒数。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| EndTime | Integer | 证书过期时间，采用unix时间戳的方式，表示从1970年1月1日（UTC/GMT的午夜）开始所经过的秒数。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| IssuerCN | String | 证书签发者通用名称。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| SubjectCN | String | 证书主题通用名称。<br/>注意：此字段可能返回 null，表示取不到有效值。 |

## CertificateDetail

证书详情，包括证书ID， 证书名字，证书类型，证书内容以及密钥内容。

被如下接口引用：DescribeCertificateDetail。

| 名称 | 类型 |  描述 |
|------|------|-------|
| CertificateId | String | 证书ID。 |
| CertificateType | Integer | 证书类型。 |
| CertificateAlias | String | 证书名字。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| CertificateContent | String | 证书内容。 |
| CertificateKey | String | 密钥内容。仅当证书类型为SSL证书时，返回该字段。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| CreateTime | Integer | 创建时间，采用unix时间戳的方式，表示从1970年1月1日（UTC/GMT的午夜）开始所经过的秒数。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| BeginTime | Integer | 证书生效起始时间，采用unix时间戳的方式，表示从1970年1月1日（UTC/GMT的午夜）开始所经过的秒数。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| EndTime | Integer | 证书过期时间，采用unix时间戳的方式，表示从1970年1月1日（UTC/GMT的午夜）开始所经过的秒数。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| IssuerCN | String | 证书签发者通用名称。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| SubjectCN | String | 证书主题通用名称。<br/>注意：此字段可能返回 null，表示取不到有效值。 |

## CountryAreaMap

国家地区映射关系（名称和编码）

被如下接口引用：DescribeCountryAreaMapping。

| 名称 | 类型 |  描述 |
|------|------|-------|
| NationCountryName | String | 国家名称。 |
| NationCountryInnerCode | String | 国家编码。 |
| GeographicalZoneName | String | 地区名称。 |
| GeographicalZoneInnerCode | String | 地区编码。 |
| ContinentName | String | 大洲名称。 |
| ContinentInnerCode | String | 大洲编码。 |

## DomainAccessRegionDict

域名解析就近访问配置详情

被如下接口引用：DescribeGroupDomainConfig。

| 名称 | 类型 |  描述 |
|------|------|-------|
| NationCountryInnerList | Array of [NationCountryInnerInfo](#NationCountryInnerInfo) | 就近接入区域 |
| ProxyList | Array of [ProxyIdDict](#ProxyIdDict) | 加速区域通道列表 |
| RegionId | String | 加速区域ID |
| GeographicalZoneInnerCode | String | 加速区域内部编码 |
| ContinentInnerCode | String | 加速区域所属大洲内部编码 |
| RegionName | String | 加速区域别名 |

## DomainRuleSet

按照域名分类的7层监听器转发规则信息

被如下接口引用：DescribeRules。

| 名称 | 类型 |  描述 |
|------|------|-------|
| Domain | String | 转发规则域名。 |
| RuleSet | Array of [RuleInfo](#RuleInfo) | 该域名对应的转发规则列表。 |
| CertificateId | String | 该域名对应的服务器证书ID，值为default时，表示使用默认证书（监听器配置的证书）。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| CertificateAlias | String | 该域名对应服务器证书名称。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| ClientCertificateId | String | 该域名对应的客户端证书ID，值为default时，表示使用默认证书（监听器配置的证书）。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| ClientCertificateAlias | String | 该域名对应客户端证书名称。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| BasicAuthConfId | String | 该域名对应基础认证配置ID。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| BasicAuth | Integer | 基础认证开关，其中：<br/>0，表示未开启；<br/>1，表示已开启。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| BasicAuthConfAlias | String | 该域名对应基础认证配置名称。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| RealServerCertificateId | String | 该域名对应源站认证证书ID。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| RealServerAuth | Integer | 源站认证开关，其中：<br/>0，表示未开启；<br/>1，表示已开启。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| RealServerCertificateAlias | String | 该域名对应源站认证证书名称。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| GaapCertificateId | String | 该域名对应通道认证证书ID。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| GaapAuth | Integer | 通道认证开关，其中：<br/>0，表示未开启；<br/>1，表示已开启。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| GaapCertificateAlias | String | 该域名对应通道认证证书名称。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| RealServerCertificateDomain | String | 源站认证域名。<br/>注意：此字段可能返回 null，表示取不到有效值。 |

## Filter

过滤条件

被如下接口引用：DescribeProxies、DescribeProxyGroupList、DescribeRealServers。

| 名称 | 类型 | 必选 | 描述 |
|------|------|----------|------|
| Name | String | 是 | 过滤条件 |
| Values | Array of String | 是 | 过滤值 |

## GroupStatisticsInfo

可以显示统计数据的通道组和对应通道信息

被如下接口引用：DescribeGroupAndStatisticsProxy。

| 名称 | 类型 |  描述 |
|------|------|-------|
| GroupId | String | 通道组ID |
| GroupName | String | 通道组名称 |
| ProxySet | Array of [ProxySimpleInfo](#ProxySimpleInfo) | 通道组下通道列表 |

## HTTPListener

HTTP类型监听器信息

被如下接口引用：DescribeHTTPListeners。

| 名称 | 类型 |  描述 |
|------|------|-------|
| ListenerId | String | 监听器ID |
| ListenerName | String | 监听器名称 |
| Port | Integer | 监听器端口 |
| CreateTime | Integer | 监听器创建时间，Unix时间戳 |
| Protocol | String | 监听器协议 |
| ListenerStatus | Integer | 监听器状态 |

## HTTPSListener

HTTPS类型监听器信息

被如下接口引用：DescribeHTTPSListeners。

| 名称 | 类型 |  描述 |
|------|------|-------|
| ListenerId | String | 监听器ID |
| ListenerName | String | 监听器名称 |
| Port | Integer | 监听器端口 |
| Protocol | String | 监听器协议， HTTP |
| ListenerStatus | Integer | 监听器状态 |
| CertificateId | String | 监听器服务器SSL证书ID |
| ForwardProtocol | String | 监听器后端转发源站协议 |
| CreateTime | Integer | 监听器创建时间，Unix时间戳 |
| CertificateAlias | String | 服务器SSL证书的别名<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| ClientCertificateId | String | 监听器客户端CA证书ID<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| AuthType | Integer | 监听器认证方式。其中，<br/>0，单向认证；<br/>1，双向认证。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| ClientCertificateAlias | String | 客户端CA证书别名<br/>注意：此字段可能返回 null，表示取不到有效值。 |

## ListenerInfo

内部接口使用，返回可以查询统计数据的监听器信息

被如下接口引用：DescribeGroupAndStatisticsProxy、DescribeProxyAndStatisticsListeners。

| 名称 | 类型 |  描述 |
|------|------|-------|
| ListenerId | String | 监听器ID |
| ListenerName | String | 监听器名称 |
| Port | Integer | 监听器监听端口 |
| Protocol | String | 监听器协议类型 |

## MetricStatisticsInfo

单指标的统计数据

被如下接口引用：DescribeListenerStatistics、DescribeProxyGroupStatistics、DescribeProxyStatistics。

| 名称 | 类型 |  描述 |
|------|------|-------|
| MetricName | String | 指标名称 |
| MetricData | Array of [StatisticsDataInfo](#StatisticsDataInfo) | 指标统计数据 |

## NationCountryInnerInfo

就近接入的国家地区详情

被如下接口引用：DescribeGroupDomainConfig。

| 名称 | 类型 |  描述 |
|------|------|-------|
| NationCountryName | String | 国家名 |
| NationCountryInnerCode | String | 国家内部编码 |

## NewRealServer

新添加源站信息

被如下接口引用：AddRealServers。

| 名称 | 类型 |  描述 |
|------|------|-------|
| RealServerId | String | 源站ID |
| RealServerIP | String | 源站ip或域名 |

## ProxyGroupDetail

通道组详情信息

被如下接口引用：DescribeProxyGroupDetails。

| 名称 | 类型 |  描述 |
|------|------|-------|
| CreateTime | Integer | 创建时间 |
| ProjectId | Integer | 项目ID |
| ProxyNum | Integer | 通道组中通道数量 |
| Status | Integer | 通道组状态：<br/>0 正常运行<br/>1 创建中<br/>4 销毁中<br/>11 迁移中 |
| OwnerUin | String | 归属Uin |
| CreateUin | String | 创建Uin |
| GroupName | String | 通道名称 |
| DnsDefaultIp | String | 通道组域名解析默认IP |
| Domain | String | 通道组域名<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| RealServerRegionInfo | [RegionDetail](#RegionDetail) | 目标地域 |
| IsOldGroup | Boolean | 是否老通道组，2018-08-03之前创建的通道组为老通道组 |
| GroupId | String | 通道组ID |
| TagSet | Array of [TagPair](#TagPair) | 标签列表<br/>注意：此字段可能返回 null，表示取不到有效值。 |

## ProxyGroupInfo

通道组详情列表

被如下接口引用：DescribeProxyGroupList。

| 名称 | 类型 |  描述 |
|------|------|-------|
| GroupId | String | 通道组id |
| Domain | String | 通道组域名<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| GroupName | String | 通道组名称<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| ProjectId | Integer | 项目ID |
| RealServerRegionInfo | [RegionDetail](#RegionDetail) | 目标地域 |
| Status | String | 通道组状态。<br/>其中，<br/>0，运行中；<br/>1，创建中；<br/>4，销毁中；<br/>11，通道迁移中。 |
| TagSet | Array of [TagPair](#TagPair) | 标签列表。 |

## ProxyIdDict

通道ID

被如下接口引用：DescribeGroupDomainConfig。

| 名称 | 类型 | 必选 | 描述 |
|------|------|----------|------|
| ProxyId | String | 是 | 通道ID |

## ProxyInfo

通道信息

被如下接口引用：DescribeProxies、DescribeProxyDetail。

| 名称 | 类型 |  描述 |
|------|------|-------|
| InstanceId | String | （旧参数，请使用ProxyId）通道实例ID。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| CreateTime | Integer | 创建时间，采用unix时间戳的方式，表示从1970年1月1日（UTC/GMT的午夜）开始所经过的秒数。 |
| ProjectId | Integer | 项目ID。 |
| ProxyName | String | 通道名称。 |
| AccessRegion | String | 接入地域。 |
| RealServerRegion | String | 源站地域。 |
| Bandwidth | Integer | 带宽，单位：Mbps。 |
| Concurrent | Integer | 并发，单位：个/秒。 |
| Status | String | 通道状态。其中：<br/>RUNNING，运行中；<br/>CREATING，创建中；<br/>DESTROYING，销毁中；<br/>OPENING，开启中；<br/>CLOSING，关闭中；<br/>CLOSED，已关闭；<br/>ADJUSTING，配置变更中；<br/>ISOLATING，隔离中（欠费触发）；<br/>ISOLATED，已隔离（欠费触发）；<br/>UNKNOWN，未知状态。 |
| Domain | String | 接入域名。 |
| IP | String | 接入IP。 |
| Version | String | 通道版本号：1.0，2.0，3.0。 |
| ProxyId | String | （新参数）通道实例ID。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| Scalarable | Integer | 1，该通道可缩扩容；0，该通道无法缩扩容。 |
| SupportProtocols | Array of String | 支持的协议类型。 |
| GroupId | String | 通道组ID，当通道归属于某一通道组时，存在该字段。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| PolicyId | String | 安全策略ID，当设置了安全策略时，存在该字段。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| AccessRegionInfo | [RegionDetail](#RegionDetail) | 接入地域详细信息，包括地域ID和地域名。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| RealServerRegionInfo | [RegionDetail](#RegionDetail) | 源站地域详细信息，包括地域ID和地域名。<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| ForwardIP | String | 通道转发IP |
| TagSet | Array of [TagPair](#TagPair) | 标签列表，不存在标签时，该字段为空列表。<br/>注意：此字段可能返回 null，表示取不到有效值。 |

## ProxySimpleInfo

内部接口使用，返回可以查询统计数据的通道和对应的监听器信息

被如下接口引用：DescribeGroupAndStatisticsProxy、DescribeProxyAndStatisticsListeners。

| 名称 | 类型 |  描述 |
|------|------|-------|
| ProxyId | String | 通道ID |
| ProxyName | String | 通道名称 |
| ListenerList | Array of [ListenerInfo](#ListenerInfo) | 监听器列表 |

## ProxyStatus

通道状态信息

被如下接口引用：DescribeProxiesStatus。

| 名称 | 类型 |  描述 |
|------|------|-------|
| InstanceId | String | 通道实例ID。 |
| Status | String | 通道状态。<br/>其中：<br/>RUNNING，运行中；<br/>CREATING，创建中；<br/>DESTROYING，销毁中；<br/>OPENING，开启中；<br/>CLOSING，关闭中；<br/>CLOSED，已关闭；<br/>ADJUSTING，配置变更中；<br/>ISOLATING，隔离中；<br/>ISOLATED，已隔离；<br/>UNKNOWN，未知状态。 |

## RealServer

查询监听器或者规则相关的源站信息，不包括tag信息

被如下接口引用：DescribeListenerRealServers、DescribeRuleRealServers。

| 名称 | 类型 |  描述 |
|------|------|-------|
| RealServerIP | String | 源站的IP或域名 |
| RealServerId | String | 源站ID |
| RealServerName | String | 源站名称 |
| ProjectId | Integer | 项目ID |

## RealServerBindSetReq

RealServerBindSetReq

被如下接口引用：BindListenerRealServers、BindRuleRealServers。

| 名称 | 类型 | 必选 | 描述 |
|------|------|----------|------|
| RealServerId | String | 是 | 源站id |
| RealServerWeight | Integer | 是 | 源站权重 |
| RealServerPort | Integer | 是 | 源站端口 |
| RealServerIP | String | 是 | 源站IP |

## RealServerStatus

源站绑定信息查询，BindStatus， 0: 未被绑定 1：被规则或者监听器绑定

被如下接口引用：DescribeRealServersStatus。

| 名称 | 类型 |  描述 |
|------|------|-------|
| RealServerId | String | 源站ID。 |
| BindStatus | Integer | 0: 未被绑定 1：被规则或者监听器绑定。 |
| ProxyId | String | 绑定此源站的通道ID，没有绑定时为空字符串。 |

## RegionDetail

区域信息详情

被如下接口引用：DescribeAccessRegions、DescribeDestRegions、DescribeProxies、DescribeProxyDetail、DescribeProxyGroupDetails、DescribeProxyGroupList、DescribeRegionAndPrice。

| 名称 | 类型 |  描述 |
|------|------|-------|
| RegionId | String | 区域ID |
| RegionName | String | 区域英文名或中文名 |

## RuleCheckParams

7层监听器转发规则健康检查相关参数

被如下接口引用：CreateRule、DescribeRules、ModifyRuleAttribute。

| 名称 | 类型 | 必选 | 描述 |
|------|------|----------|------|
| DelayLoop | Integer | 是 | 健康检查的时间间隔 |
| ConnectTimeout | Integer | 是 | 健康检查的响应超时时间 |
| Path | String | 是 | 健康检查的检查路径 |
| Method | String | 是 | 健康检查的方法，GET/HEAD |
| StatusCode | Array of Integer | 是 | 确认源站正常的返回码，可选范围[100, 200, 300, 400, 500] |
| Domain | String | 否 | 健康检查的检查域名。<br/>当调用ModifyRuleAttribute时，不支持修改该参数。 |

## RuleInfo

7层监听器转发规则信息

被如下接口引用：DescribeRules。

| 名称 | 类型 |  描述 |
|------|------|-------|
| RuleId | String | 规则信息 |
| ListenerId | String | 监听器信息 |
| Domain | String | 规则域名 |
| Path | String | 规则路径 |
| RealServerType | String | 源站类型 |
| Scheduler | String | 转发源站策略 |
| HealthCheck | Integer | 是否开启健康检查标志，1开启，0关闭 |
| RuleStatus | Integer | 源站状态，0运行中，1创建中，2销毁中，3绑定解绑源站中，4配置更新中 |
| CheckParams | [RuleCheckParams](#RuleCheckParams) | 健康检查相关参数 |
| RealServerSet | Array of [BindRealServer](#BindRealServer) | 已绑定的源站相关信息 |
| BindStatus | Integer | 绑定源站状态，0正常，1源站IP异常，2源站域名解析异常 |
| ForwardHost | String | 通道转发到源站的请求所携带的host，其中default表示直接转发接收到的host。<br/>注意：此字段可能返回 null，表示取不到有效值。 |

## SecurityPolicyRuleIn

安全策略规则（入参）

被如下接口引用：CreateSecurityRules。

| 名称 | 类型 | 必选 | 描述 |
|------|------|----------|------|
| SourceCidr | String | 是 | 请求来源IP或IP段。 |
| Action | String | 是 | 策略：允许（ACCEPT）或拒绝（DROP） |
| AliasName | String | 否 | 规则别名 |
| Protocol | String | 否 | 协议：TCP或UDP，ALL表示所有协议 |
| DestPortRange | String | 否 | 目标端口，填写格式举例：<br/>单个端口: 80<br/>多个端口: 80,443<br/>连续端口: 3306-20000<br/>所有端口: ALL |

## SecurityPolicyRuleOut

安全策略规则（出参）

被如下接口引用：DescribeSecurityPolicyDetail。

| 名称 | 类型 |  描述 |
|------|------|-------|
| Action | String | 策略：允许（ACCEPT）或拒绝（DROP） |
| SourceCidr | String | 请求来源Ip或Ip段 |
| AliasName | String | 规则别名 |
| DestPortRange | String | 目标端口范围<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| RuleId | String | 规则ID |
| Protocol | String | 要匹配的协议类型（TCP/UDP）<br/>注意：此字段可能返回 null，表示取不到有效值。 |

## StatisticsDataInfo

统计数据信息

被如下接口引用：DescribeListenerStatistics、DescribeProxyGroupStatistics、DescribeProxyStatistics、DescribeRealServerStatistics。

| 名称 | 类型 |  描述 |
|------|------|-------|
| Time | Integer | 对应的时间点 |
| Data | Float | 统计数据值<br/>注意：此字段可能返回 null，表示取不到有效值。 |

## TCPListener

TCP类型监听器信息

被如下接口引用：DescribeTCPListeners。

| 名称 | 类型 |  描述 |
|------|------|-------|
| ListenerId | String | 监听器ID |
| ListenerName | String | 监听器名称 |
| Port | Integer | 监听器端口 |
| RealServerPort | Integer | 监听器转发源站端口，仅对版本为1.0的通道有效<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| RealServerType | String | 监听器绑定源站类型 |
| Protocol | String | 监听器协议， TCP |
| ListenerStatus | Integer | 监听器状态 |
| Scheduler | String | 监听器源站访问策略，其中：<br/>rr，轮询；<br/>wrr，加权轮询；<br/>lc，最小连接数。 |
| ConnectTimeout | Integer | 源站健康检查响应超时时间，单位：秒 |
| DelayLoop | Integer | 源站健康检查时间间隔，单位：秒 |
| HealthCheck | Integer | 监听器是否开启健康检查，其中：<br/>0，关闭；<br/>1，开启 |
| BindStatus | Integer | 监听器绑定的源站状态， 其中：<br/>0，异常；<br/>1，正常。 |
| RealServerSet | Array of [BindRealServer](#BindRealServer) | 监听器绑定的源站信息<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| CreateTime | Integer | 监听器创建时间，Unix时间戳 |

## TagPair

标签键值对

被如下接口引用：AddRealServers、CreateProxy、CreateProxyGroup、DescribeProxies、DescribeProxyDetail、DescribeProxyGroupDetails、DescribeProxyGroupList、DescribeRealServers。

| 名称 | 类型 | 必选 | 描述 |
|------|------|----------|------|
| TagKey | String | 是 | 标签键 |
| TagValue | String | 是 | 标签值 |

## TagResourceInfo

标签对应资源信息

被如下接口引用：DescribeResourcesByTag。

| 名称 | 类型 |  描述 |
|------|------|-------|
| ResourceType | String | 资源类型，其中：<br/>Proxy表示通道，<br/>ProxyGroup表示通道组，<br/>RealServer表示源站 |
| ResourceId | String | 资源ID |

## UDPListener

UDP类型监听器信息

被如下接口引用：DescribeUDPListeners。

| 名称 | 类型 |  描述 |
|------|------|-------|
| ListenerId | String | 监听器ID |
| ListenerName | String | 监听器名称 |
| Port | Integer | 监听器端口 |
| RealServerPort | Integer | 监听器转发源站端口，仅V1版本通道或通道组监听器有效<br/>注意：此字段可能返回 null，表示取不到有效值。 |
| RealServerType | String | 监听器绑定源站类型 |
| Protocol | String | 监听器协议， UDP |
| ListenerStatus | Integer | 监听器状态 |
| Scheduler | String | 监听器源站访问策略 |
| BindStatus | Integer | 监听器绑定源站状态， 0正常，1IP异常，2域名解析异常 |
| RealServerSet | Array of [BindRealServer](#BindRealServer) | 监听器绑定的源站信息 |
| CreateTime | Integer | 监听器创建时间，Unix时间戳 |

