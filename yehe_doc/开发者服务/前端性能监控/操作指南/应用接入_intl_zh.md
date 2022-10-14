前端性能监控支持 Web、小程序（微信、QQ）、Hippy、Weex、Rect Native 、Flutter 和 Cocos 应用类型接入。本文将为您介绍如何进行应用接入。

## 操作步骤
1. 登录 [前端性能监控](https://console.cloud.tencent.com/rum)。
2. 在右侧菜单栏中单击**数据总览**。
3. 在数据总览页中单击**应用接入**，根据下列表格配置创建应用信息。
<table>
<th>
 配置项
</th>
<th>
 说明
</th>
<tr>
<td>
 应用名称
</td>
<td>
 自定义应用名称，方便您在前端监控平台辨识该应用。
</td>
</tr>
<tr>
<td>
 应用描述
</td>
<td>
 填写应用描述 ，如应用用途、应用简介等，方便其它用户了解该应用。
</td>
</tr>
<tr>
<td>
 应用类型
</td>
<td>
 支持 Web、小程序（微信、QQ）、Hippy、Weex 、Rect Native 、 Flutter 和 Cocos 应用类型接入。
</td>
</tr>
<tr>
<td>
 应用仓库地址（可选）
</td>
<td>
 填写您的应用仓库地址，可不填写。
</td>
</tr>
<tr>
<td>
 所属业务系统
</td>
<td>
 该功能用于分类管理您接入的应用，您可以根据研发团队、业务逻辑、应用类别等进行应用分类管理。若您没有可用团队，您可以单击右侧的创建链接，填写完信息后，单击<b>确认</b>即创建成功。
</td>
</tr>
</table>

4.配置完后单击**下一步**，参考下列说明选择一种方式安装 SDK 。
- **npm**方式安装 SDK（所有应用类型均可使用该方式接入）。下列 Web 应用为例说明如何通过 npm 方式接入 SDK。
 i. 在接入指引页面中复制提供的首行命令，引入 npm 包。
![](https://qcloudimg.tencent-cloud.cn/raw/d0ac7f69cac4d5d4c1606e5f9c00a0e1.png)
 ii. 在接入指引页面中复制提供的代码初始化 SDK。
![](https://qcloudimg.tencent-cloud.cn/raw/0a2cb98c7362d8bb37b32d5ff7f13d86.png)
- **&lt;script&gt; 标签引入**方式接入 SDK（仅支持 Web 接入类型）。
 i. 在接入指引页面复制提供的 `<script>` 标签 代码。
ii. 把**&lt;script&gt; 标签引入**类型下的代码引入到 `<head></head>` 标签中即可。
![](https://qcloudimg.tencent-cloud.cn/raw/2fe67f1a420ba5d8f3c0a5a904022555.png)
<dx-alert infotype="explain" title="">
按照上述步骤接入后即可使用数据总览、页面性能、异常分析、页面访问（PV、UV）、API 监控和静态资源功能。如需使用日志查询、离线日志、自定义测速和自定义事件，需参考接入指引上报数据。
</dx-alert>
