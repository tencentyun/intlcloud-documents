本文将引导您如何初步使用腾讯云传统型负载均衡：创建一个名为 `clb-test`的传统型公网负载均衡实例，并将来自客户端的请求转发到后端两台云服务器上。

## 前提条件
1. 负载均衡只负责转发流量，不具备处理请求的能力。因此，您需要有处理用户请求的云服务器实例。
在本示例中，只要具有两台云服务器实例即可，您也可以自行规划云服务器数量。本例中已经在广州地域下创建了云服务器实例 `rs-1` 和 `rs-2`。有关如何创建云服务器实例，请参见 [购买并启动云服务器实例](https://intl.cloud.tencent.com/document/product/213/4855)。
2. 本文以 HTTP 转发为例，云服务器上必须部署相应的 Web 服务器，如 Apache、Nginx、IIS 等。
为了验证结果，示例在 `rs-1` 上部署了 Apache 并返回一个带有 “Hello Tomcat! This is rs-1!” 的 HTML，在 `rs-2` 上部署了 Apache 并返回一个带有 “Hello Tomcat! This is rs-2!” 的 HTML。更多云服务器部署内容，请参见 [Linux（CentOS）下部署 Java Web](https://intl.cloud.tencent.com/document/product/214/32391) 及 [Windows 下安装配置 PHP](https://intl.cloud.tencent.com/document/product/213/10182)。
3. 访问云服务器的公网 IP+路径，若显示结果为您部署好的页面，则表示服务部署成功。
>!
> - 传统账户类型的云服务器上必须购买公网带宽，因为当前的带宽属性在 CVM 上，而非 CLB 上。若您无法确定账户类型，请参见 [账户类型](https://intl.cloud.tencent.com/document/product/214/36999)。
> - 示例中后端服务器部署的服务返回值不同，实际情况下，为保持所有用户均有一致体验，后端服务器上一般是部署完全相同的服务。

## 购买传统型负载均衡实例
1. 登录腾讯云 [负载均衡服务购买页](https://buy.cloud.tencent.com/lb)。
2. 本例地域选择与云服务器相同的【广州】，实例类型选择【传统型】，网络属性选择【公网】，网络选择【Default-VPC（默认）】，实例名称填写“clb-test”。
3. 单击【立即购买】，完成付款。有关负载均衡实例的更多内容，请参见 [产品属性选择](https://intl.cloud.tencent.com/document/product/214/13629) 。
4. 在“CLB 实例列表”页，选择对应的地域即可看到新建的实例。
![](https://main.qcloudimg.com/raw/183ac407a68c4aafe440aa2c111a154e.png)

## 创建负载均衡监听器
负载均衡监听器通过指定协议及端口来负责实际转发。本文以负载均衡转发客户端的 HTTP 请求配置为例。
1. 登录 [负载均衡控制台](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3)。
2. 在“CLB 实例列表”中，找到已创建的传统型的负载均衡实例 `clb-test`，单击实例 ID，进入负载均衡详情页。
3. 在“基本信息”部分，可以单击名称后的编辑修改实例名称。
4. 在“监听器管理”的【监听器】下，单击【新建】，新建负载均衡监听器。
![](https://main.qcloudimg.com/raw/df7de6ac8996718bc5176b14f25cd3cb.png)
5. 在弹出框中配置以下内容：
  - 名称自定义为“Listener1”。
  - 监听协议端口为 `HTTP：80`。
  - 后端端口为 `80`。
  - 均衡方式选择“加权轮询”。
  - 不勾选会话保持。
  - 开启健康检查。
  ![](https://main.qcloudimg.com/raw/41cbc18c096ed2f6c01a238dc426963e.png)
6. 单击【完成】，完成负载均衡监听器的创建。

有关负载均衡监听器的更多内容，请参见 [负载均衡监听器概述](https://intl.cloud.tencent.com/document/product/214/6151)。

## 绑定后端云服务器
1. 在“CLB 实例列表”中找到刚才创建的 `clb-test`，单击其 ID，进入负载均衡详情页。
2. 在“监听器管理”的“绑定后端服务”模块中，单击【绑定】。
![](https://main.qcloudimg.com/raw/a1c1ba2fa1b95a27a534a2446c381fc3.png)
3. 在弹出框中，选择与 CLB 同地域下的云服务器实例 `rs-1` 和 `rs-2`，权重均设置为默认值“10”。
4. 单击【确定】，完成绑定。
![](https://main.qcloudimg.com/raw/0c9f911e40621ff3615ac47d94651329.png)
5. 展开监听器【Listener1】，可以查看后端 CVM 的健康检查状态，当状态为“健康”时表示 CVM 可以正常处理负载均衡转发的请求。


## 配置安全组
创建完负载均衡后，您可以配置负载均衡的安全组来隔离公网流量，详情请参考 [配置安全组](https://intl.cloud.tencent.com/document/product/214/14733)。
安全组配置完成后，您可以选择开启或关闭安全组默认放通，不同选择配置如下所示。

### 方法一：开启安全组默认放通
>?目前该功能处于内测阶段，如果您需要体验该功能，请提交内测申请]。传统型内网负载均衡不支持安全组默认放通功能。
>
具体操作请参考 [配置安全组默认放通](https://intl.cloud.tencent.com/document/product/214/14733)。


### 方法二：在 CVM 安全组上放通客户端 IP
具体操作请参考 [配置安全组默认放通](https://intl.cloud.tencent.com/document/product/214/14733)。

## 验证负载均衡服务
1. 在浏览器中输入负载均衡的服务地址和端口 `http://vip:80`，测试负载均衡服务，如下图所示，表示本次请求被 CLB 转发到了 rs-1 这台 CVM 上，CVM 正常处理请求并返回。
![](https://main.qcloudimg.com/raw/5a7cb3e86d04149978b90050546a2983.png)
2. 此监听器的轮询算法是“按权重轮询”，且两台 CVM 的权重都是“10”，刷新浏览器，再次发送请求，可以看到本次请求被 CLB 转发到了 rs-2 这台 CVM 上。
![](https://main.qcloudimg.com/raw/8f9f5f667461a5d0efd3e6b2bbe859f3.png)
>!
> - 如果用户关闭会话保持功能，选择轮询的方式进行调度，则请求依次分配到不同后端服务器上。
> - 如果用户开启会话保持功能，或关闭会话保持功能但选择 ip_hash 的调度方式，则请求持续分配到同一台后端服务器上去。
