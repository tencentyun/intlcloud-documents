TCM 提供网格升级服务， 用户可将低版本的网格升级到高版本。升级过程遵循灰度升级原则，分为以下几步：
1. TCM 部署新版本控制面，完成控制面升级。

2. 数据面灰度升级，用户重启业务，使存量业务 Pod 完成 Sidecar 更新。

3. 升级验证，验证升级后业务是否正常。

4. 老版本控制面下线，升级完成。

   在老控制面下线前，可以回滚到升级前的状态。升级流程如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/cc08d5a86ead7effe267e57de73ef03f.png)


## 操作步骤
1. 登录 [服务网格控制台](https://console.cloud.tencent.com/tke2/mesh)。

2. 当网格版本可升级时，网格界面将会提示有可升级的新版本，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/0cb5a5ef56615634eb42adbec8edb8dd.png)

3. 选择**更多 > 升级**后，根据引导进行升级。
升级将按照**控制面升级 > 数据面升级 > 旧控制面下线**三个阶段进行，在旧控制面下线前，可以回滚到升级前的状态。
    <dx-tabs>
   ::: 控制面升级
**控制面升级**，TCM 将部署新版本控制面组件：
![](https://qcloudimg.tencent-cloud.cn/raw/cc2119c2bfbf1e2e30059968d736ef38.png)
    :::
    ::: 数据面升级
**数据面升级**，分为业务数据面升级和 Gateway 升级。

其中业务数据面升级是用户将指定 Namespace 的 Sidecar 自动注入改为使用新版本，勾选后，该 Namespace 下**新创建**的业务 Pod 将注入新版本的 Sidecar ，**存量的业务 Pod 重建后才会更新为新版本**，由于重启涉及到业务可用性影响，平台不会自动重建业务 Pod，**需要用户手动重建**。

<dx-alert infotype="explain" title="">
- 您可以通过流水线重新发布业务或直接使用 kubectl patch、kubectl rollout restart 等命令行工具手工重建工作负载。
- 部分场景下 Sidecar 将被卸载而不是升级，例如：Namespace 曾开启过 Sidecar 注入，并且部分业务 Pod 已成功注入 Sidecar，之后又关闭了 Namepsace 级 Sidecar 注入，则重启业务 Pod 后，除非为 Pod 单独设置了 Sidecar 注入标记，否则 Sidecar 将被卸载。
</dx-alert>

![](https://staticintl.cloudcachetci.com/yehe/backend-news/hfMT559_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230111161121.png)

Gateway 升级，将所有需要升级的 Gateway 组件勾选到新版本并单击右侧的**升级**：

![](https://staticintl.cloudcachetci.com/yehe/backend-news/zZI4912_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230111161250.png)

所有数据面升级完成后，单击**升级**进入下一步。
:::
::: 升级验证
由于版本升级涉及到特性变更，可能存在兼容性问题，业务 Pod 重建后，您需要检查业务是否正常。如果发现升级导致业务异常，您可以在升级界面中选择回滚，将数据面 Sidecar 退回到原版本。
:::
</dx-tabs>

4. 选择**完成**或**取消升级**。在“数据面升级”中，单击**升级**或**回滚**将检查当前存量 Pod 是否满足进入下一步的条件。当所有 Namespace 均切换到新版本控制面，并且所有存量业务 Pod 中 Sidecar 均已更新到新版本后，可以选择**升级**，进入下一步**下线旧版本控制面**完成升级。或当所有的 Namespace 均切换回旧版本控制面，并且所有存量业务 Pod 中 Sidecar 均使用旧版本控制面时，可以单击**回滚**进入下一步将新版本控制面下线，取消升级。
![](https://qcloudimg.tencent-cloud.cn/raw/77047f18f8d37a68359511b188f34bdd.png)
