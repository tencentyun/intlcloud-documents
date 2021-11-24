>? 本文为容器镜像服务 TCR 企业版产品动态，容器服务 TKE 产品动态请参见 [产品动态](https://intl.cloud.tencent.com/document/product/457/37358)。


## 2021年07月

<table>
	<tr><th style="width: 25%;">动态名称</th><th style="width: 50%;">动态描述</th><th style="width: 25%;">相关文档</th></tr>
<tr><td>支持跨主账号实例同步</td><td>实例同步功能支持跨主账号的目标实例，实现跨主账号的实例数据同步。</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35494">配置实例同步</a></td></tr>
<tr><td>支持镜像版本不可变</td><td>支持对托管在 TCR 的镜像开启版本不可变功能，可确保相同版本的镜像仅被成功推送一次。</td><td>配置镜像版本不可变</a></td></tr>
</table>


## 2021年06月
<table>
<tr><th style="width: 25%;">动态名称</th><th style="width: 50%;">动态描述</th><th style="width: 25%;">相关文档</th></tr>
<tr><td>TCR 控制台功能增强</td><td>原实例列表页升级为实例管理页，可查看实例概况、TCR 最新功能及产品动态。</td><td>-</td></tr>
<tr><td>支持批量添加/编辑公网访问白名单</td><td>TCR 控制台支持单次输入多个白名单或导入已有安全组。</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35491">公网访问控制</a></td></tr>
<tr><td>管理自动解析新增多个地域支持</td><td>新增支持南京、中国香港、新加坡、法兰克福、成都、重庆。</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35492">内网访问控制</a></td></tr>
<tr><td>支持镜像清理</td><td>TCR 支持设置自定义规则批量清理企业版实例内的冗余镜像数据，释放存储空间，且支持模拟运行。</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/41073">清理 COS 存储空间</a></td></tr>
</table>


## 2021年04月

<table>
	<tr><th style="width: 25%;">动态名称</th><th style="width: 50%;">动态描述</th><th style="width: 25%;">相关文档</th></tr>
<tr><td>支持查询审计日志</td><td>TCR 企业版内实例、命名空间、镜像仓库等资源的读写操作已接入云审计，通过控制台进入"审计日志"即可查看相关操作记录。</td><td>-</td></tr>
</table>


## 2021年03月
<table>
	<tr><th style="width: 25%;">动态名称</th><th style="width: 50%;">动态描述</th><th style="width: 25%;">相关文档</th></tr>
<tr><td>自定义域名</td><td>TCR 支持配置使用自定义域名，为企业版实例添加自定义域名和 SSL 证书，实现通过 HTTPS 协议访问实例。</td><td>配置自定义域名</td></tr>
</table>

## 2021年01月
<table>
	<tr><th style="width: 25%;">动态名称</th><th style="width: 50%;">动态描述</th><th style="width: 25%;">相关文档</th></tr>
	<tr><td>支持单实例全球多地域复制</td><td>高级版实例支持在多个地域创建复制实例，访问域名及访问凭证统一，底层镜像数据实时高速同步。单次上传，即可在多个地域就近内网高速下载。</td><td>配置实例复制</td></tr>
	<tr><td>兼容支持云原生应用制品及多架构镜像</td><td>企业版实例支持兼容云原生应用制品（OCI），镜像仓库可直接托管 Helm Chart、CNAB 等云原生应用制品。支持托管多架构容器镜像，如 amd64、arm 等，满足物联网及边缘计算使用场景。</td><td>-</td></tr>
	<tr><td>支持按需加载容器镜像</td><td>高级版实例支持开启按需加载容器镜像特性，集群批量拉取容器镜像时可按需加载，提高容器启动速度。</td><td>-</td></tr>
	<tr><td>内网访问功能优化</td><td>国内实例新建内网访问链路时，支持同时使用 VPCDNS 配置实例访问域名的内网解析，无需使用自建 DNS 或配置 Host。</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35492">内网访问控制</a></td></tr>
</table>
## 2020年12月

<table>
<tr><th style="width: 25%;">动态名称</th><th style="width: 50%;">动态描述</th><th style="width: 25%;">相关文档</th></tr>
<tr><td>企业版服务正式启动商业化收费</td><td>企业版实例由公测正式转入收费服务，提供SLA 保障，支持后付费购买使用。</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35483">计费概述</a></td></tr>
<tr><td>全量开放弗吉尼亚、法兰克福地域</td><td>全量开放弗吉尼亚、法兰克福地域，费用详情可参见计费概述。</td><td><ahref="https://intl.cloud.tencent.com/document/product/1051/35483">计费概述</a></td></tr>
</table>

## 2020年10月

<table>
	<tr><th style="width: 25%;">动态名称</th><th style="width: 50%;">动态描述</th><th style="width: 25%;">相关文档</th></tr>
	<tr><td>镜像构建功能新增多个代码源支持</td><td>新增支持私有 GitLab，腾讯工蜂代码源支持，并优化了代码源授权流程。</td><td>配置镜像构建</td></tr>
	<tr><td>交付流水线部署功能支持镜像过滤</td><td>新增支持使用本地推送镜像触发部署过程，同时支持配置过滤规则，仅部署符合规则的最新推送镜像。</td><td>使用交付流水线实现容器 DevOps</td></tr>
</table>

## 2020年09月

<table>
	<tr><th style="width: 25%;">动态名称</th><th style="width: 50%;">动态描述</th><th style="width: 25%;">相关文档</th></tr>
	<tr><td>新增镜像版本保留功能</td><td>支持定义命名空间内镜像版本自动清理规则，可定期执行，清理历史镜像版本。</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/38942">自动删除镜像版本</a></td></tr>
</table>


## 2020年08月

<table>
	<tr><th style="width: 25%;">动态名称</th><th style="width: 50%;">动态描述</th><th style="width: 25%;">相关文档</th></tr>
	<tr><td>TCR 专属插件上线容器服务 TKE</td><td>TKE 集群一键安装 TCR 企业版专属插件，即可实现内网免密拉取容器镜像及 Helm Chart，显著提升应用部署体验。</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/38386">TKE 集群使用 TCR 插件内网免密拉取容器镜像</a></td></tr>
  <tr><td>新增支持腾讯云标签</td><td>支持为企业版实例绑定腾讯云标签，可利用云标签实现实例资源过滤及权限管理。</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35486">创建企业版实例</a></td></tr>
</table>

## 2020年07月

<table>
	<tr><th style="width: 25%;">动态名称</th><th style="width: 50%;">动态描述</th><th style="width: 25%;">相关文档</th></tr>
	<tr><td>交付流水线上线</td><td>快速配置交付流水线，即可实现代码更新自动触发镜像构建、推送及应用更新，结合容器服务 TKE 快速实现容器 DevOps。</td><td>使用交付流水线实现容器 DevOps</td></tr>
  <tr><td>Helm Chart 功能更新</td><td>支持控制台上传、下载 Chart 包。TKE 支持使用 TCR 私有 Helm 仓库部署应用。</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35493">管理 Helm Chart</a></td></tr>
</table>

## 2020年06月

<table>
	<tr><th style="width: 25%;">动态名称</th><th style="width: 50%;">动态描述</th><th style="width: 25%;">相关文档</th></tr>
	<tr><td>企业版启动全量公测</td><td>正式启动全量公测，支持创建安全且独享的企业版实例、支持镜像安全扫描、跨地域同步及 Helm Chart。</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35480">容器镜像服务产品概述</a></td></tr>
</table>
