对于在采集日志并配置了仪表盘、告警资源的用户，想要开放日志服务的日志检索查询、监控告警、仪表盘等能力给其他人，同时又想避免维护众多访问管理（Cloud Access Management，CAM）账号带来的管理成本。在不做开发工作的前提下，快捷方便的独立部署控制台是一个合适的方案。


## 独立部署控制台介绍

独立部署控制台不需要开发工作，便可免腾讯云账号登录使用日志服务。但其权限管理与安全能力较弱，只提供简单的密码鉴权。建议部署在内网中使用。

| 使用方式         | 功能支持        | 是否支持免腾讯云账号登录       | 开发工作量      | 账号权限管理       | 是否有登录态挤压 |
| ----------------- | ----------------- | --------------------------- | ---------------------- | ------------------------- | -------------------------- |
| [腾讯云控制台](https://console.cloud.tencent.com/cls/overview) | 支持日志服务（Cloud Log Service，CLS）全部功能                           | 不支持                                                   | 无                                       | 腾讯云 CAM         | 无                          |
| iframe 嵌入控制台-普通嵌入 | 支持 CLS 全部功能                           | 支持，iframe 嵌入到企业内的运维系统，通过企业鉴权系统登录 | 少，需要前端 iframe 嵌入                   | 企业鉴权系统              | 会挤压                     |
| iframe 嵌入控制台-SDK 嵌入 | 只支持 CLS 日志检索分析与仪表盘查看功能     | 支持，iframe 嵌入到企业内的运维系统，通过企业鉴权系统登录 | 多，需要前端 iframe 嵌入和后端接入层转发 | 企业鉴权系统              | 不会挤压                   |
| [独立部署控制台](https://www.tencentcloud.com/document/product/614/50280)                                           | 支持 CLS 全部功能                           | 支持，独立部署，免密登录或密码鉴权登录                   | 无                                       | 无/密码鉴权               | 会挤压                     |
| [Grafana 插件](https://intl.cloud.tencent.com/document/product/614/39592) | 只支持 Grafana 的仪表盘功能，不支持告警功能 | 支持，数据接入 Grafana 使用                                | 无                                       | Grafana 自身的权限管理系统 | 不会挤压                   |


## 独立部署控制台使用

CLS 在容器服务公有镜像仓库提供独立部署控制台的镜像，可在 [腾讯云容器服务](https://console.cloud.tencent.com/tke2) 拉取镜像部署使用。

### 前提条件

以在 TKE 标准集群部署镜像为使用案例，需要有一个可用集群。若无可用集群，可参考 [创建集群](https://intl.cloud.tencent.com/document/product/457/30637) 文档，创建一个新集群，或者参考 [创建容器实例](https://intl.cloud.tencent.com/document/product/457/47857) 文档，直接在容器实例上部署。

### 操作步骤

1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)，在集群列表中，单击一个可用集群的名称/ID，进入集群管理页面。

2. 在左侧导航栏中，选择**工作负载 > Deployment**，单击**新建**。

3. 在新建 Deployment 页面，配置如下主要信息，其他配置使用默认值即可。

 - 镜像：单击**选择镜像 > 公有镜像**，搜索并选择"**cls_iframe**"镜像。
 - 镜像版本：**最新的镜像版本**。
 - 环境变量：
 <table>
<thead>
<tr><th>环境变量</th><th>描述</th></tr>
</thead>
<tbody>
<tr><td>SecretId</td><td>前往 <a href="https://console.cloud.tencent.com/cam/capi">云 API 密钥</a> 获取 SecretId。</td></tr>
<tr><td>SecretKey</td><td>前往 <a href="https://console.cloud.tencent.com/cam/capi">云 API 密钥</a> 获取 SecretKey。</td></tr>
<tr><td>RoleArn</td><td><a href="https://intl.cloud.tencent.com/document/product/1150/49456">AssumeRole</a> 接口请求参数。 角色的资源描述，可在 <a href="https://console.cloud.tencent.com/cam/role">访问管理</a>，单击角色名获取。推荐使用 CLS 的只读角色。</br>若无角色，可参见 <a href="https://intl.cloud.tencent.com/document/product/598/19381">创建角色</a> 文档，为腾讯云主账号创建一个策略为<b>日志服务只读访问权限</b>的角色。</td></tr>
<tr><td>password</td><td>跳转服务密码，输入后即可以配置的身份访问控制台</td></tr>
</tbody></table>
 - 端口映射：容器端口和服务端口设置为**3000**。
>? 案例中选择了公网 LB 访问，实际业务操作中，建议**选择更安全的内网 LB 访问**。
>
5. 单击**创建Workload**，完成创建。
6. 完成工作负载创建后，单击**服务与路由**，查看刚才工作负载绑定的 LB 访问地址。

7. 复制 LB 访问 IP 地址，加**3000**的端口，在浏览器**输入密码**访问部署的日志服务控制台。


