## [新建验证](id:xjyz)
1. 登录 [验证码控制台](https://console.cloud.tencent.com/captcha/graphical)，左侧导航栏选择**图形验证** > **验证管理**。
2. 在验证管理页面，单击**新建验证**。
>? 验证码控制台新建验证上限为50个，您可以基于不同业务需求创建多个验证，每个验证配置不同的客户端类型、安全策略等。验证码接入流程请参见 [快速入门](https://intl.cloud.tencent.com/document/product/1159/49678) 文档。

3. 在新建验证弹窗中，根据业务场景需求，设置验证名称等参数，单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/4c04773a196a37f0ab3d755ba64c0dec.png)
4. 完成新建验证后，即可在验证管理页查看到已创建的验证：
![](https://qcloudimg.tencent-cloud.cn/raw/b34c8320ef661440fd8b109f3650c415.png)
操作说明：
 - 单击**基础配置**，可修改验证名称，标注验证场景、域名等，详情请参见 [基础配置](#jcpz)。
 - 单击**外观配置**，可配置验证提示语言等，详情请参见 [外观配置](#ygpz)。
 - 单击**安全配置**，可更新风控等级等安全策略，详情请参见 [安全配置](#aqpz)。
 - 单击**统计详情**，可查看请求量、验证通过量、验证拦截量等统计数据，详情请参见 [数据统计](#sjtj)。

## [数据统计](id:sjtj)
- 在 **[图形验证](https://console.cloud.tencent.com/captcha/graphical)** > **验证统计**页面，支持查看所有验证的统计数据。
![](https://qcloudimg.tencent-cloud.cn/raw/bc017cc74c15f80454f5315da65135bb.png)
- 在 **[图形验证](https://console.cloud.tencent.com/captcha/graphical)** > **验证管理**页面，到要查看的验证，单击**数据统计**，进入**验证详情** > **数据统计**页签，即可查看单个验证的统计数据。
  ![](https://qcloudimg.tencent-cloud.cn/raw/c898f461b84ee966689158c42cd9fa63.png)

- 验证码支持查看如下指标数据：
<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky">指标名称</th>
    <th class="tg-0pky">指标说明</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">请求量</td>
    <td class="tg-0pky">客户端加载验证的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">验证量</td>
    <td class="tg-0pky">用户回答验证问题后，发起验证的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">验证通过量</td>
    <td class="tg-0pky">验证通过的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">验证拦截量</td>
    <td class="tg-0pky">验证未通过，被拦截的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">答案错误拦截量</td>
    <td class="tg-0pky">因答案错误导致验证被拦截的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">安全策略打击拦截量</td>
    <td class="tg-0pky">因安全策略打击导致验证被拦截的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">票据校验量</td>
    <td class="tg-0pky">服务端发起票据校验的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">票据校验通过量</td>
    <td class="tg-0pky">票据校验通过的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">票据校验拦截量</td>
    <td class="tg-0pky">票据校验未通过的次数</td>
  </tr>
</tbody>
</table>

## [安全配置](id:aqpz)
1. 登录 [验证码控制台](https://console.cloud.tencent.com/captcha/graphical)，左侧导航栏选择**图形验证** > **验证管理**。
2. 在验证管理页面，选择要配置的验证，单击**安全配置**。
3. 在安全配置页签，配置相关参数，单击**保存修改**。
    ![](https://qcloudimg.tencent-cloud.cn/raw/c80269cac802ef1af9c91a210f6330ac.png)

    参数说明：
  - 验证方式：当前仅可选择滑动拼图验证方式。
  - 风控等级：可选择三个风控等级，体验优先、平衡、安全优先。
  - 智能免验证：可选择开启、关闭。

## [外观配置](id:ygpz)
1. 登录 [验证码控制台](https://console.cloud.tencent.com/captcha/graphical)，左侧导航栏选择**图形验证** > **验证管理**。
2. 在验证管理页面，选择要配置的验证，单击**外观配置**。
3. 在外观配置页签，可配置验证码提示语言，单击**保存修改**。
    ![](https://qcloudimg.tencent-cloud.cn/raw/ac055652129a1c228fabf8cd6fda592f.png)
4. 另外，验证码还支持配置隐藏帮助按钮等，需要在客户端代码接入时配置，详情请参见 [Web 客户端接入](https://intl.cloud.tencent.com/document/product/1159/49680)。

## [基础配置](id:jcpz)
1. 登录 [验证码控制台](https://console.cloud.tencent.com/captcha/graphical)，左侧导航栏选择**图形验证** > **验证管理**。
2. 在验证管理页面，选择要配置的验证，单击**基础配置**。
3. 在基础配置页签，单击**编辑**可修改验证名称，标注验证场景、域名等信息，单击**保存**即可。
![](https://qcloudimg.tencent-cloud.cn/raw/61ba4b683ee944a87ebd290848643b1d.png)

## 更多信息
您可以登录 [验证码控制台](https://console.cloud.tencent.com/captcha/graphical) ，在页面右上角单击**快速咨询**，了解更多详细信息。
