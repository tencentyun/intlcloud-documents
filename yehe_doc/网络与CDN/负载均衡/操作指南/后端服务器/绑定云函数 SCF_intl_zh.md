您可以通过编写云函数 SCF 来实现 Web 后端服务，然后使用负载均衡 CLB 绑定云函数 SCF 并对外提供服务。

## 背景信息
[云函数（Serverless Cloud Function，SCF）](https://intl.cloud.tencent.com/document/product/583)是腾讯云为企业和开发者们提供的无服务器执行环境，帮助您在无需购买和管理服务器的情况下运行代码。在您创建完云函数后，可以通过创建 CLB 触发器将云函数与事件进行关联。CLB 触发器会将请求内容以参数形式传递给云函数，并将云函数返回作为响应返回给请求方。

## 使用场景
<dx-accordion>
::: 通用的\sHTTP/HTTPS\s接入
适用于电商、社交、工具等 App 应用程序，以及个人博客、活动页面等 Web 应用程序等场景。方案流程如下所示：
1. App、浏览器、H5、小程序等发起 HTTP/HTTPS 请求，通过 CLB 访问 SCF。
2. 由 CLB 做证书卸载，SCF 仅需提供 HTTP 服务。
3. 请求转给 SCF 后，继续后续处理，例如写入云数据库或调用其他 API。
![](https://main.qcloudimg.com/raw/534ca758662eaffdd40d243bd8384739.svg)
:::
::: CVM/SCF\s平滑切换
适用于 HTTP/HTTPS 服务从 CVM 迁移至 SCF 的场景，以及当 CVM（SCF）服务有问题时，快速迁移至 SCF（CVM）的故障切换场景。方案流程如下所示：
1. App、浏览器、H5、小程序等发起 HTTP/HTTPS 请求。
2. 通过 DNS 解析将请求解析到 CLB 的 VIP 上。
3. 一个 CLB 转发请求给 CVM，另一个 CLB 转发请求给 SCF。
4. 客户端无感知，即可完成后端服务在 CVM 和 SCF 之间的平滑切换。
![](https://main.qcloudimg.com/raw/d285c006b5945486a725936385d9dcb2.svg)
:::
::: CVM/SCF\s业务分流
适用于秒杀、抢购等场景，使用 SCF 处理高弹性服务、使用 CVM 处理日常业务。
1. 通过 DNS 解析将域名 A 解析到其中一个 CLB 的 VIP 上，将域名 B 解析到另外一个 CLB 的VIP 上。
2. 其中一个 CLB 转发请求给 CVM，另外一个 CLB 转发请求给 SCF。
![](https://main.qcloudimg.com/raw/96a77f06ecad23ddf13282aa2e6a496b.svg)
:::

</dx-accordion>



## 限制说明
- 仅广州、上海、北京、成都、中国香港、新加坡、孟买、东京、硅谷地域支持绑定 SCF。
- 仅标准账户类型支持绑定 SCF，传统账户类型不支持。建议升级为标准账户类型，详情可参见 [账户类型升级说明](https://intl.cloud.tencent.com/document/product/684/15246)。 
- 传统型负载均衡不支持绑定 SCF。
- 基础网络类型不支持绑定 SCF。
- CLB 默认支持绑定同地域下的所有 SCF，可支持跨 VPC 绑定 SCF，不支持跨地域绑定。
- 目前仅 IPv4、IPv6 NAT64 版本的负载均衡支持绑定 SCF，IPv6 版本的暂不支持。
- 仅七层（HTTP、HTTPS）监听器支持绑定 SCF，四层（TCP、UDP、TCP SSL）监听器和七层 QUIC 监听器不支持。
- CLB 绑定 SCF 仅支持绑定“Event 函数”类型的云函数。


## 前提条件
1. [创建负载均衡实例](https://intl.cloud.tencent.com/document/product/214/6149)
2. [配置 HTTP 监听器](https://intl.cloud.tencent.com/document/product/214/32515) 或 [配置 HTTPS 监听器](https://intl.cloud.tencent.com/document/product/214/32516)

## 操作步骤
![](https://main.qcloudimg.com/raw/eca21ba71ea22a6c240d3b4a05dfdce0.svg)

### 步骤一：创建云函数
1. 登录 [云函数控制台](https://console.cloud.tencent.com/scf)，在左侧导航栏单击【函数服务】。
2. 在“函数服务”页面，单击【新建】。
3. 在“新建”函数服务页面，创建方式选择“自定义创建”，输入函数名称，地域选择与 CLB 实例相同的地域，运行环境选择“Python3.6”，在函数代码输入框中输入如下代码（本文以 Hello CLB 为例），单击【完成】。
>!CLB 绑定 SCF 时，需按照特定响应集成格式返回，详情请参见 [集成响应](https://intl.cloud.tencent.com/document/product/583/39849)。
```plaintext
# -*- coding: utf8 -*-
import json
def main_handler(event, context):

    return {
        "isBase64Encoded": False,
        "statusCode": 200,
        "headers": {"Content-Type":"text/html"},
        "body": "<html><body><h1>Hello CLB</h1></body></html>"
   }
```

### 步骤二：部署云函数
1. 在“函数服务”页面的列表中，单击刚才创建的函数名。
2. 在“函数管理”页面，单击【函数代码】页签，在页签底部单击【部署】。
![]()

### 步骤三：绑定云函数
1. 登录 [负载均衡控制台](https://console.cloud.tencent.com/clb)，在左侧导航栏单击【实例管理】。
2. 在“实例管理”页面的“负载均衡”页签中，单击目标实例右侧“操作”列的【配置监听器】。
3. 在 HTTP/HTTPS 监听器列表中，选择需要绑定云函数 SCF 的监听器，分别单击目标监听器左侧的【+】和展开的域名左侧的【+】，然后选中展开的 URL 路径，单击【绑定】。
![]()
4. 在弹出的“绑定后端服务”对话框中，目标类型选择“云函数 SCF”，选择命名空间、函数名和版本/别名，设置权重后，单击【确认】。
![]()
5. 返回“监听器管理”页签，在“转发规则详情”区域显示负载均衡已绑定的云函数，即已创建 CLB 触发器。
![]()
>? 您还可以选择在 SCF 控制台创建 CLB 触发器，从而将负载均衡 CLB 与云函数 SCF 绑定，详情请参见 [创建触发器](https://intl.cloud.tencent.com/document/product/583/31441)。

## 结果验证
1. 登录 [云函数控制台](https://console.cloud.tencent.com/scf)，在左侧导航栏单击【函数服务】。
2. 在“函数服务”页面的列表中，单击刚才创建的函数名。
3. 在函数页面，单击左侧列表的【触发管理】。
4. 在“触发管理”页面的触发器中，单击访问路径。
![]()
5. 在浏览器里打开该访问路径，若显示 “Hello CLB”，则说明函数已成功部署。
![]()


## 相关文档
[创建 SCF 函数](https://intl.cloud.tencent.com/document/product/583/32742)
