您可以通过编写云函数 SCF 来实现 Web 后端服务，然后使用负载均衡 CLB 绑定云函数 SCF 并对外提供服务。
>? 负载均衡 CLB 绑定云函数 SCF 功能目前处于内测阶段，如需使用，请提交内测申请。
>

## 背景信息
[云函数（Serverless Cloud Function，SCF）](https://intl.cloud.tencent.com/document/product/583)是腾讯云为企业和开发者们提供的无服务器执行环境，帮助您在无需购买和管理服务器的情况下运行代码。在您创建完云函数后，可以通过创建 CLB 触发器将云函数与事件进行关联。CLB 触发器会将请求内容以参数形式传递给云函数，并将云函数返回作为响应返回给请求方。

## 使用场景

#### 典型场景一：秒杀/抢购活动
秒杀&抢购活动中，对整体资源的应用弹性的要求较高，而且和业务的主干场景联系较为紧密。云函数 SCF 一般是业务系统中较为独立的模块，便于迁移和改造。您可以通过负载均衡 CLB 无缝支持云函数，对于按调用次数的收费场景，整体计费和迁移成本都会比较低。同域名下，还可以轻松解决跨资源共享（CORS）跨域问题。
![](https://main.qcloudimg.com/raw/531e9819590d5a23dff69ec559945a31.png)

#### 典型场景二：辅助系统架构
企业的非主干 WEB 业务，例如订单系统、采集系统、BI 分析等对削峰填谷比较敏感的非主干场景，使用云函数 SCF 结合负载均衡 CLB ，整体迁移成本会比较低且迁移收益大。
![](https://main.qcloudimg.com/raw/4e92487155661da83aeb6c85f1b88462.png)

#### 典型场景三：动静态业务分离
当业务请求量较大时，可以通过区分网站的静态和动态请求，有针对性地对其进行分发处理，有效减少后端负载压力。其中动态请求可以通过单独部署负载均衡及关联云函数 SCF 服务进行处理，静态内容可以通过接入 CDN 服务，结合对象存储进行优化，提升加载速度。
![](https://main.qcloudimg.com/raw/1026b5217e6e288b4dca1381723defb6.png)

#### 典型场景四：同域名的地域级访问服务
业务对地域要求较高时，可以通过负载均衡 CLB 对云函数 SCF 做地域级访问划分。


## 限制说明
- 仅广州、上海、北京、成都、中国香港、新加坡、孟买、东京、硅谷地域支持绑定 SCF。
- 仅标准账户类型支持绑定 SCF，传统账户类型不支持。建议升级为标准账户类型，详情可参见 [账户类型升级说明](https://intl.cloud.tencent.com/document/product/684/15246)。 
- 传统型负载均衡不支持绑定 SCF。
- 基础网络类型不支持绑定 SCF。
- 仅支持跨 VPC 绑定 SCF，不支持跨地域绑定。
- 目前仅 IPv4、IPv6 NAT64 版本的负载均衡支持绑定 SCF，IPv6 版本的暂不支持。
- 仅七层（HTTP、HTTPS）监听器支持绑定 SCF，四层（TCP、UDP、TCP SSL）监听器和七层 QUIC 监听器不支持。

## 前提条件
1. [创建负载均衡实例](https://intl.cloud.tencent.com/document/product/214/6149)
2. [配置 HTTP 监听器](https://intl.cloud.tencent.com/document/product/214/32515) 或 [配置 HTTPS 监听器](https://intl.cloud.tencent.com/document/product/214/32516)

## 操作步骤
1. 登录 [负载均衡控制台](https://console.cloud.tencent.com/clb)。
2. 在“实例管理”页面的“负载均衡”页签中，单击目标实例右侧“操作”列的【配置监听器】。
3. 在 HTTP/HTTPS 监听器列表中，选择需要绑定云函数 SCF 的监听器，分别单击目标监听器左侧的【+】和展开的域名左侧的【+】，然后选中展开的 URL 路径，单击【绑定】。

4. 在弹出的“绑定后端服务”对话框中，目标类型选择“云函数 SCF”，选择命名空间、函数名和版本/别名，设置权重后，单击【确认】。

5. 返回“监听器管理”页签，在“转发规则详情”区域单击函数名。

6. 在“函数代码”页签，编辑函数代码。需要按照特定响应集成格式返回，详情请参见 [集成响应](https://intl.cloud.tencent.com/document/product/583/39849)。

>? 您还可以选择在 SCF 控制台创建 CLB 触发器，从而将负载均衡 CLB 与云函数 SCF 绑定，详情请参见 [创建触发器](https://intl.cloud.tencent.com/document/product/583/31441)。

## 相关文档
[创建 SCF 函数](https://intl.cloud.tencent.com/document/product/583/32742)
