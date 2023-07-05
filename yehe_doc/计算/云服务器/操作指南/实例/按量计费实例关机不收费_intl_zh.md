## 操作场景
实例关机不收费是指按量计费实例通过关机操作使实例进入**已关机**状态后，不再收取实例（CPU、内存）费用，云盘（系统盘和数据盘）、公网带宽和镜像等组件将继续计费。

<dx-alert infotype="notice" title="">
启用关机不收费功能后，实例的 CPU 和内存将**不再保留**，公网 IP 地址会**自动释放**，更多功能说明、使用限制和影响请参见 [按量计费实例关机不收费说明](https://intl.cloud.tencent.com/document/product/213/19918)。
</dx-alert>



## 操作步骤
<dx-tabs>
::: 通过控制台操作

#### 关机单个实例
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm)。
2. 在实例的管理页面，根据实际使用的视图模式进行操作：
  - **列表视图**：选择需要关机的实例，并在右侧操作栏中，选择**更多** > **实例状态** > **关机**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/6bc11c552db35a4882506449573cf239.png)
   - **页签视图**：在需关机的实例页面中，选择右上角的**关机**。如下图所示：
 ![](https://qcloudimg.tencent-cloud.cn/raw/8602dbbdc2f30d072fe53d62e40963e4.png)
3. 勾选“**关机不收费**”，单击**确定**。
    如不支持会在实例列表显示不支持关机不收费。



#### 关机多个实例
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm)。
2. 勾选所有需要关机的实例，在列表顶部，单击**关机**，即可批量关机实例。如下图所示：
不能关机的实例会显示原因。
![](https://qcloudimg.tencent-cloud.cn/raw/7c3e7ab231472f3fe8fa8d0bdd7ff685.png)
2. 勾选“**关机不收费**”，单击**确定**。
如不支持会在实例列表显示不支持关机不收费。
:::
::: 通过云\sAPI\s操作
可使用 StopInstances 接口进行关机，参考文档 [关闭实例](https://intl.cloud.tencent.com/document/product/213/33235)。增加以下参数：

| 参数名称    | 必选 | 类型   | 描述                                                         |
| ----------- | ---- | ------ | ------------------------------------------------------------ |
| StoppedMode | 否   | String | 是否关机不收费，仅对按量计费云硬盘实例生效<br>**取值范围：**<br>KEEP_CHARGING：关机后继续收费<br>STOP_CHARGING：关机不收费<br>**默认取值：**<br>KEEP_CHARGING |

:::
</dx-tabs>
