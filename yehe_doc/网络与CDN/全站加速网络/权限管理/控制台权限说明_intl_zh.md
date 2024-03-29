腾讯云提供的访问管理 Web 服务，用于帮助客户安全地管理腾讯云账户的访问权限，资源管理和使用权限。通过访问管理，您可以创建、管理和销毁用户（组），并通过身份管理和策略管理控制哪些人可以使用哪些腾讯云资源，详情请参见 [用户指南](https://intl.cloud.tencent.com/document/product/598/17848)。

ECDN 支持资源级授权，通过指定 Action 和 Resource 创建自定义策略，可直接调用 API 接口对加速域名等资源进行操作。控制台功能点与 Action 映射关系见下文说明。

## 概览

| 功能模块                                                     | 授权 Action            | 注意事项                   |
| ------------------------------------------------------------ | ---------------------- | -------------------------- |
| 我的服务-接入域名                                            | DescribeDomains        | 展示已授权域名总数量       |
| 我的服务<li>本月总请求数</li><li>本月总流量</li><li>本月平均带宽峰值</li> | DescribeEcdnStatistics | 展示已授权域名本月访问数据 |
| 今日数据                                                     | DescribeEcdnStatistics | 展示已授权域名今日访问数据 |
| 请求数本月趋势                                               | DescribeEcdnStatistics | 展示本月请求数趋势曲线图   |

## 域名管理

| 功能模块         | 授权 Action                                  | 注意事项                                                     |
| ---------------- | -------------------------------------------- | ------------------------------------------------------------ |
| 域名列表及查询   | DescribeDomains                              | 查询 / 展示域名基础配置<br/>全量详细配置需要授权 DescribeDomainsConfig |
| 添加域名         | AddEcdnDomain                                | -                                                            |
| 关闭全站加速     | StopEcdnDomain                               | -                                                            |
| 启动全站加速     | StartEcdnDomain                              | -                                                            |
| 删除域名         | DeleteEcdnDomain                             | -                                                            |
| 修改域名所属项目 | UpdateDomainConfig                           | 域名所属项目属于域名配置一部分<br/>授权后可修改域名所有配置  |
| 域名配置管理     | UpdateDomainConfig<br/>DescribeDomainsConfig | 授权后可查看 / 修改域名所有配置                              |

## 统计分析

| 功能模块   | 授权 Action                                            | 注意事项                           |
| ---------- | ------------------------------------------------------ | ---------------------------------- |
| 使用量统计 | DescribeEcdnDomainStatistics<br>DescribeEcdnStatistics | 授权后可查询域名所有访问数据指标   |
| 状态码统计 | DescribeEcdnStatistics                                 | 授权后可查询域名所有状态码数据指标 |

## 缓存刷新

| 功能模块     | 授权 Action        |
| ------------ | ------------------ |
| URL 刷新提交 | PurgeUrlsCache     |
| 目录刷新提交 | PurgePathCache     |
| 查询刷新记录 | DescribePurgeTasks |

## 证书管理

| 功能模块     | 授权 Action           | 注意事项                 |
| ------------ | --------------------- | ------------------------ |
| 查询证书列表 | DescribeDomainsConfig | 授权后可查看域名所有配置 |
| 配置证书     | UpdateDomainConfig    | 授权后可修改域名所有配置 |
| 批量配置证书 | UpdateDomainsHttps    | 用于批量配置证书         |

## 日志服务

| 功能模块         | 授权 Action            |
| ---------------- | ---------------------- |
| 查询日志下载链接 | DescribeEcdnDomainLogs |
