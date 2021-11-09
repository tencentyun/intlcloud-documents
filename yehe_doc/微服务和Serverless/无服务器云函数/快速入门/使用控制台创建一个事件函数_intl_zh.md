本文向您介绍如何通过腾讯云控制台快速创建一个事件函数。



## 步骤1：注册腾讯云账号

如果您已在腾讯云注册，可忽略此步骤。

<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:13px;">点此注册腾讯云账号</a></div>

## 步骤2：在线充值

云函数服务用户每月可享受一定量的免费资源使用量及免费调用次数，外网出流量无免费额度。云函数按照实际使用云资源收费付费，采用后付费模式。如需通过云函数使用其他后付费云上资源，请参考 [在线充值](https://intl.cloud.tencent.com/zh/document/product/555/7425) 文档充值账号后进行购买。



## 步骤3：服务授权

在 [腾讯云控制台](https://console.cloud.tencent.com/) 中，选择**云产品** > **云函数**，进入 Serverless 控制台，按照界面提示为云函数授权。（如果您已为云函数授权，请跳过该步骤。）

<div style="background-color:#00A4FF; width: 150px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/scf/index?rid=1" target="_blank"  style="color: white; font-size:13px;">点此进行服务授权</a></div>



## 步骤4：创建函数

<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/scf/list-create?rid=1&ns=default" target="_blank"  style="color: white; font-size:13px;">点此进入创建函数页面</a></div>

<br>



1. 单击左侧导航栏**函数服务**，进入“函数服务”页面。
2. 在页面上方选择**广州**地域，单击**新建**。如下图所示：
![](https://main.qcloudimg.com/raw/718294ab42e0352407f5675ed50ade95.png)
3. 在“新建函数”页面填写函数基础信息，单击**下一步**。如下图所示： 
![](https://main.qcloudimg.com/raw/16bb5ab1368b418d67a07db7b5d142d0.png)
 - **创建方式**：选择 “模版函数”。
 - **模板搜索**：输入 helloworld 后按 “Enter” 进行搜索，选择 “helloworld” 模版。云函数支持多重运行环境，此函数以使用 Python2.7 为例。
4. 函数名称默认填充，可根据需要自行修改。函数配置保持默认，并单击**完成**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/1f97c60e8cffc2b089d41c187d7b4609.png)
函数创建完成后，自动进入创建成功函数的“函数配置”页面，可查看该云函数的函数配置信息。
5. 选择**函数代码**，查看或在线编辑函数代码。如下图所示：
![](https://main.qcloudimg.com/raw/80b6fbaccc151814b4fdfd9012929b3a.png)




## 步骤5：部署函数（含配置触发器）
1. 在进行函数代码在线编辑后，单击**部署**，函数会被部署。
2. 在已创建函数的详情页面，选择左侧**触发管理**，并单击**创建触发器**。
3. 在弹出的“创建触发器”窗口中，将“触发方式”设置为 “API网关触发器”，并取消勾选**启用集成响应**，其它参数保持默认配置。如下图所示：
![](https://main.qcloudimg.com/raw/3fd656b836b6892cea8aecff6feb5594.png)
4. 单击**提交**，即可完成函数部署及触发器配置。

## 步骤6：云端测试
<dx-tabs>
::: 函数部署测试
在“函数管理”页中，选择**函数代码**，单击**测试**，运行代码并返回测试结果。如下图所示：

<dx-alert infotype="explain" title="">
- 如果您需要更换测试模版或模版中的内容。可直接编辑函数内容，或者选择**当前测试模版**，更换后单击**保存**即可生效。
- 不同的测试模板分别模拟不同的触发器消息源，且不同的触发器和云函数之间传递的消息均为约定好的数据结构。具体详情可参考 [触发器介绍](https://intl.cloud.tencent.com/document/product/583/9705)。
</dx-alert>

![](https://main.qcloudimg.com/raw/3758f32893e46b38d94d25cb71666542.png)
返回结果如下所示：
![](https://main.qcloudimg.com/raw/7d5c5d7fc1b7b79f37861df7b3b8d1eb.png)
在本次测试过程中，云函数会在 `main_handler` 的 `event` 参数中，获取 “Hello World事件模版” 的数据结构。

```
{
  "key1": "test value 1",
  "key2": "test value 2"
}
```

:::
::: 触发器配置测试
在“触发管理”页中，查看触发器详情。

1. 触发器创建成功后，会在该函数的“触发管理”页面生成访问路径。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/1f97c60e8cffc2b089d41c187d7b4609.png)
2. 在浏览器里打开该访问路径，显示 “hello from scf”，则说明函数部署成功。
:::
</dx-tabs>


## 步骤7：查看日志与监控
<dx-tabs>
::: 查看日志
在已创建函数的详情页面，选择左侧的**日志查询**，即可查看函数详细日志。如下图所示：
![](https://main.qcloudimg.com/raw/d1150d2144bab8a023294554d3c1c170.png)
更多关于日志信息请参见 [函数日志](https://intl.cloud.tencent.com/document/product/583/32740)。

:::
::: 查看监控
在“函数管理”页中，选择已创建函数的**监控信息**，即可查看函数调用次数/运行时间等情况。如下图所示：

<dx-alert infotype="notice" title="">
监控统计的粒度最小为1分钟。您需要等待1分钟后，才可查看当次的监控记录。

</dx-alert>



![](https://qcloudimg.tencent-cloud.cn/raw/820ae3b24fc7a0ca30de878ea201599a.png)
更多关于监控信息请参见 [监控指标说明](https://intl.cloud.tencent.com/document/product/583/32739)。
:::
::: 配置告警
在已创建函数的详情页面，单击**前往新增告警**为云函数配置告警策略，对函数运行状态进行监控。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/34d0c93904c98c189cead318e9a7a090.png)
更多关于配置告警请参见 [告警配置说明](https://intl.cloud.tencent.com/document/product/583/32738)。

:::
</dx-tabs>


## 步骤8：删除函数
函数运行后即开始消耗资源，为避免产生不必要的费用，此步骤向您介绍如何清除所有资源。
1. 选择左侧导航栏中的**函数服务**，在“函数服务”页面选择需删除函数所在行右侧的**删除**。如下图所示：
![](https://main.qcloudimg.com/raw/1e01a23067cf71e0bf4dbc574f7d9ca2.png)
2. 在“删除函数”弹窗中确认信息后，单击**确定**即可删除函数。



## 遇到问题？
非常抱歉您在使用时出现问题，您可以通过 [提交工单](https://console.intl.cloud.tencent.com/workorder) 来寻求帮助。
