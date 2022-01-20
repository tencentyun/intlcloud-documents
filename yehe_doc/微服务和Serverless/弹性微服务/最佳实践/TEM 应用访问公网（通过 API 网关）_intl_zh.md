
## 操作场景

运行在 TEM 上的应用，由于业务需求等原因，通常会有访问公网的需求。而许多场景下，都是这些请求都是 HTTP/HTTPS 请求。您可以使用 API 网关，轻松的通过简单的配置，访问公网的 HTTP/HTTPS 请求。
>?如您的访问公网需求不只包含 HTTP/HTTPS 时，请参见 [TEM 应用访问公网](https://intl.cloud.tencent.com/zh/document/product/1094/41888) 来通过配置 NAT 网关实现。

## 前提条件

请先完成 [环境创建](https://intl.cloud.tencent.com/document/product/1094/40358) 和 [创建并部署应用](https://intl.cloud.tencent.com/document/product/1094/40362)。

## 操作步骤

### 步骤1：在 API 网关中关联公网 HTTP/HTTPS 请求

1. 前往 [API网关控制台](https://console.cloud.tencent.com/apigateway)，在左侧导航栏，单击**服务**，进入服务列表页。
2. 选择与部署TEM应用相同的地域，单击页面左上角的**新建**，新建一个服务。
    新建服务时，前端类型可选择 HTTP、HTTPS、HTTP 与 HTTPS 任一种，访问模式选择选择 VPC 内网，实例类型选择共享型。
    <img src = "https://qcloudimg.tencent-cloud.cn/raw/5f95e38cc91b5a4854c2048a93a7fe06.png" style="width: 100%">  
3. 单击 API 网关服务 ID 进入 API 管理页面。单击**新建 API**。
4. 在前端配置中填写 API 名称，前端类型选择 HTTP&amp;HTTPS，路径为“/”，请求方法选择 ANY 以包含所有请求，鉴权类型选择“免认证”，单击**下一步**。
![](https://qcloudimg.tencent-cloud.cn/raw/a945e3e3bd7d60383c47be24b7d884a5.png)
5. 在后端配置中，选择 公网URL/IP，配置您需要访问的公网域名以及路径（此处以腾讯云官网为例），单击**下一步**。
![](https://qcloudimg.tencent-cloud.cn/raw/b695295cda52de71705b973c2de5a6ab.png)
6. 设置应用的返回类型，此处为 HTML，RESTful 服务可选择为 JSON，单击完成。发布服务。

### 步骤2：验证公网请求连通性

1. 前往 API 网关服务基础配置页面，复制服务的内网 VPC 访问地址。
![](https://qcloudimg.tencent-cloud.cn/raw/c7132945c851609b3c559295a9968925.png)
2. 打开部署好的 TEM 应用页面，进入应用实例的 webshell，访问 API 网关内网 VPC 访问地址验证网络连通性。
![](https://qcloudimg.tencent-cloud.cn/raw/8bd3f68e322495c0416c68cdbccecf23.png)
