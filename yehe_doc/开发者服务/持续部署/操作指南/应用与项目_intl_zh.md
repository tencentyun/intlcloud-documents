本文为您详细介绍 CODING 持续部署中的应用与项目。

## 前提条件
使用 CODING 项目管理的前提是，您的腾讯云账号需要开通 CODING DevOps 服务。

## 进入项目
1. 登录 CODING 控制台，单击**立即使用**进入 CODING 使用页面。
2. 单击工作台首页左侧的 <img src ="https://main.qcloudimg.com/raw/12230547b45d5eae85ad1c4fa86fba68.png" width="15"style ="margin:0" data-nonescope="true" >，进入持续部署控制台。

## 功能介绍
CODING 持续部署中的应用和项目都是属于企业/团队的一级资源，它们之间为一对多关系，即一个项目包含多个应用，一个应用从属于多个项目。
![](https://qcloudimg.tencent-cloud.cn/raw/714889a702a966a1f24ecd2fb9704e9a.png)
在该设计下，运维人员可以专注于应用的持续部署管理（部署流程、基础设施等），而非运维人员（一般指开发）只需要在项目维度操作（提交发布单，查看发布详情)，使运维能够专注于在云的基础上做基础设施运维，开发在项目内就能够进行大部分业务运维并完成从需求到发布的完整闭环。

## 应用
应用是 CODING CD 中的基本部署单位。应用包含若干个应用集群，以及安全组和负载均衡器等。应用对部署的软件集合进行抽象，通常代表您想要部署的服务、配置、以及运行所需的基础设置。推荐的做法是一个应用对应微服务架构中的一个服务。
![](https://qcloudimg.tencent-cloud.cn/raw/0f80cb25c0e5b5be70c2b6a30c9a092b.png)

### 对应关系示例
在微服务架构下的微服务对应于一个 CODING 持续部署的应用，当然您也可以在了解对应关系的情况下依照自己的偏好来设定对应关系。下面是一个典型的团队、项目、应用、集群、云账号之间的关系示例：
<table>
    <tr>
        <th colspan="4">团队：XXX 科技有限公司</th>
    </tr>
    <tr>
        <td>云账号</td>
        <td><ul style="margin:0;list-style-type:disc;">
            <li>自建 Kubernetes Service Account</li>
            <li>腾讯云北京 TKE 集群 Service Account</li>
            <li>腾讯云中国香港 API Key</li></ul>
        </td>
    </tr>
    <tr>
        <td>项目1：车载用品电商站点项目</td>
        <td><ul style="margin:0;list-style-type:disc;">
            <li>应用1：车载电商后端</li>
            <li>应用2：车载电商前端</li>
            <li>应用3：物流管理服务</li></ul>
        </td>
    </tr>
    <tr>
        <td>项目2：服装电商站点项目</td>
        <td><ul style="margin:0;list-style-type:disc;">
            <li>应用1：服装电商后端</li>
            <li>应用2：服装电商前端</li>
            <li>应用3：物流管理服务</li></ul>
        </td>
    </tr>
    <tr>
        <td>部署控制台</td>
        <td><ul style="margin:0;list-style-type:disc;">
            <li>应用1：车载电商后端
                <ul><li>测试集群</li><li>生产集群</li></ul></li>
            <li>应用2：车载电商前端
                <ul><li>测试集群</li><li>生产集群</li></ul></li>
            <li>应用3：物流管理服务
                <ul><li>车载电商测试集群</li><li>车载电商生产集群</li><li>服装电商测试集群</li><li>服装电商生产集群</li></ul></li>
            <li>应用4：服装电商后端
                <ul><li>测试集群</li><li>生产集群</li></ul></li>
            <li>应用5：服装电商前端
                <ul><li>测试集群</li><li>生产集群</li></ul></li>
        </ul>
        </td>
    </tr>
</table>

## 云账号绑定
云账号是访问云资源的凭证，进入 CODING 部署控制台创建应用，单击导航栏**应用** > **创建应用**。在进行应用创建之前，请确保您已经完成了 [云账号绑定](https://intl.cloud.tencent.com/document/product/1137/45451)。
![](https://qcloudimg.tencent-cloud.cn/raw/174263bb417add3d117ef3f3753396ac.png)

## 应用创建
单击首页左侧的控制台，单击右上角**创建应用**。
![](https://qcloudimg.tencent-cloud.cn/raw/eaf08309ec593918a183be205b11e8c1.png)

## 与项目关联
在部署控制台内完成应用创建后，可以直接在控制台首页将应用与项目相关联。
![](https://qcloudimg.tencent-cloud.cn/raw/786ae80a6693a3983e2cf461f46611bc.png)

## 新建发布单
当运维人员完成对应用的 [部署流程配置](https://intl.cloud.tencent.com/document/product/1137/45455) 后，开发人员在项目内就可以实现从项目协同到应用发布的 DevOps 闭环。典型的场景是当有新版本需要发布时，开发人员在**持续部署** > **Kubernetes** 页面新建发布单，发布单自动触发部署流程执行，开发可随时查看发布状态和历史详情。
![](https://qcloudimg.tencent-cloud.cn/raw/28468af7631eab5b5fade4e4bd00e31a.png)

## 管理应用
在部署控制台新建应用后可以在应用的**配置**中调整应用属性与通知，或删除应用。
![](https://qcloudimg.tencent-cloud.cn/raw/81e64ce6c1f364038c30c364e989dae3.png)

### 应用通知
目前支持 CODING 站内通知、企业微信、钉钉和飞书四种通知方式。

### 显示 / 隐藏功能入口
对于不需要显示的功能入口，可以在**特性**栏将其禁用，这里的禁用并不会删除相应的数据，仅表示在控制台界面隐藏。可以隐藏部署流程、集群、负载均衡器和安全组功能入口：
![](https://qcloudimg.tencent-cloud.cn/raw/af92e7393d6069f86dd620ccde9cfe76.png)

### 添加实例的自定义属性链接
在**集群** > **服务组** > **实例详情**面板可以查看运行实例的自定义链接，自定义链接提供关于实例的简略信息，如：日志、健康状态等。
![](https://qcloudimg.tencent-cloud.cn/raw/d561cda1441048648539a19fcb2ce68e.png)
自定义链接对应的 IP 可以是公有或私有 IP，默认端口为 80；如果需要设置其他端口号，在 Path 文本框以`:`开头，如：`:7002/health`。

1. 在**链接**一栏，单击 **Add Section**。
2. **Section Heading** 输入自定义链接标题。
3. **Links** 输入自定义链接名称，以及 URL。

>?URL 字段支持使用表达式引用更多的实例属性。例如对于腾讯云实例，可以使用`{region}`引用实例的所在地域。

5. 单击 **Add Link** 在同一属性下添加更多链接。
6. 单击 **Add Section** 添加新的自定义属性链接。
7. 单击**撤销**取消添加操作。**撤销**不会删除已保存的自定义属性链接。
8. 单击**保存**完成操作。

### 流量保护
>? 流量保护旨在确保任何时间至少有一个实例处于正常运行状态。

启用流量保护功能后，如果用户或者脚本尝试删除、禁用或对服务组进行伸缩容操作，CODING 控制台会对操作进行验证以确保集群中至少有一个实例在正常运行，否则将会拒绝用户或脚本请求。
1. 在**流量保护**栏，单击**添加流量保护**。
2. 以下是需要填写的字段：

<table>
   <tr>
      <th width="0px" style="text-align:center">字段</td>
      <th width="0px" style="text-align:center">必填项</td>
      <th width="0px"  style="text-align:center">说明</td>
   </tr>
   <tr>
      <td>云账号</td>
      <td>是</td>
      <td>设置流量保护的云账号</td>
   </tr>
   <tr>
      <td>地域</td>
      <td>是</td>
      <td>可选的地域，`*` 表示选择所有地域</td>
   </tr>
   <tr>
      <td>分组</td>
      <td>否</td>
      <td>设置流量保护的集群分组，如果留空表示选择不属于任何分组的集群</td>
   </tr>
   <tr>
      <td>详情</td>
      <td>否</td>
      <td>详情是区分集群的三级字段，具有相同 `${Application}-${Stack}-${Detail}` 的服务组属于同一个集群</td>
   </tr>

</table>

3. 单击**保存**使配置生效。

### 应用删除
如果应用中有服务组，需要先删除服务组。
进入 [部署控制台](https://console.cloud.tencent.com/coding) 后，单击应用右下角**齿轮图标**，进入应用配置页后单击**删除**。
![](https://qcloudimg.tencent-cloud.cn/raw/f5d78c4b4527e0e98004e587814741a4.png)
