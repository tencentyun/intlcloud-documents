## API 网关介绍

腾讯云 API 网关（API Gateway）是腾讯云推出的一种 API 托管服务，能提供 API 的完整生命周期管理，包括创建、维护、发布、运行、下线等。详细介绍请参见 [API 网关官网文档](https://intl.cloud.tencent.com/zh/document/product/628)。

## 操作场景

本文档主要介绍如何快速使用腾讯云 API 网关访问 TEM 应用并管理 TEM 应用的 API。使用 API 网关和 TEM 结合，可使 TEM 的用户享受到 API 网关提供的限流、认证、缓存等高级能力，助力业务获得成功。
<img src="https://qcloudimg.tencent-cloud.cn/raw/a353d0a3340323f948920a02a71ec0ab.png">

## 前提条件

请登录 [弹性微服务 TEM 控制台](https://console.cloud.tencent.com/tem)，先完成 [环境创建](https://intl.cloud.tencent.com/document/product/1094/40358) 和 [创建并部署应用](https://intl.cloud.tencent.com/document/product/1094/40362)。

## 操作步骤

### 步骤1：为 TEM 应用配置 VPC 内网访问

1. 登录 [TEM 控制台](https://console.cloud.tencent.com/tem)，在左侧导航栏单击**应用管理**，单击您想要配置的应用进入应用详情页。
2. 单击访问配置栏的**编辑并更新**，进入应用访问配置页。
3. 选择 VPC 内网访问（四层转发），选择子网、协议、容器端口和应用监听端口，并单击**提交**。此时 TEM 会为您自动创建四层转发的 VPC 内网应用型 CLB。


### 步骤2：创建 API 网关服务并绑定 TEM 应用[](id:step2)

1. 登录 [API 网关控制台](https://console.cloud.tencent.com/apigateway/service)，在左侧导航栏，单击**服务**，进入服务列表页。
2. 选择与部署 TEM 应用相同的地域，单击页面左上角的**新建**，新建一个服务。
   新建服务时，前端类型可选择 HTTP、HTTPS、HTTP 与 HTTPS 任一种，访问模式选择可以选择 VPC 内网和公网，实例类型选择共享性、专享型。
	 <img src="https://qcloudimg.tencent-cloud.cn/raw/5f95e38cc91b5a4854c2048a93a7fe06.png">
3. 单击 API 网关服务 ID 进入 API 管理页面。单击**新建 API**。
4. 在前端配置中填写 API 名称，前端类型选择 HTTP&HTTPS，路径为“/”，请求方法选择 ANY 以包含所有请求，鉴权类型选择“免认证”，单击**下一步**。
   ![](https://qcloudimg.tencent-cloud.cn/raw/a945e3e3bd7d60383c47be24b7d884a5.png)
5. 在后端配置中，选择 VPC 内资源，选择 TEM 应用部署环境所在的 VPC。设置后端域名，选择 TEM 应用自动创建的 CLB（名字为“cls-xxxdefault{TEM应用名}”），选择相应的监听器（即上一步中所设置的端口映射），填写后端地址为“/”，完成 API 的创建。
   ![](https://qcloudimg.tencent-cloud.cn/raw/37a8a5b7bc18613de223419c978b7f8e.png)
6. 此时您可看到您所配置的 API。并可以通过 API 网关提供的默认域名访问您的 TEM 应用。


### 步骤3：通过 API 网关访问 TEM 应用

访问 [步骤2](#step2) 中创建的 API 网关 API，即可通过 API 网关访问到 TEM 应用。
   ![](https://main.qcloudimg.com/raw/70ca90f3a189c79f09f0c8e334507b22.png)

## 注意事项

- 为保证应用无侵入的接入 API 网关，我们建议一个 API 网关服务只绑定一个 TEM 应用，前端地址和后端地址保持一致，同为“/”可以拦截所有 API，您也可以在服务中为您应用的某些 API 进行单独的配置。
- 您可以参考 [API 网关插件使用文档](https://intl.cloud.tencent.com/zh/document/product/628/40214)，为后端对接 TEM 的 API 网关 API 绑定插件，以享受 API 网关提供的高级功能。
