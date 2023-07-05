## 操作场景
除了使用腾讯云提供的公共镜像，您还可以创建自定义镜像。创建自定义镜像后，您可以在腾讯云控制台快速创建与该镜像相同配置的腾讯云云服务器实例。


<dx-alert infotype="explain" title="">
由于镜像底层使用了云硬盘快照服务：
 - 在创建自定义镜像时会默认创建关联该镜像的快照，且保留自定义镜像会产生一定的快照费用，详情请参见 [快照计费概述](https://intl.cloud.tencent.com/document/product/362/32415)。
</dx-alert>




## 注意事项

- 每个地域暂支持10个自定义镜像。
- 若您的 Linux 实例具备数据盘，但您仅制作系统盘自定义镜像时，请确认 `/etc/fstab` 不包含数据盘配置，否则会导致使用该镜像创建的实例无法正常启动。
- 制作过程需要持续十分钟或更长时间，具体时间与实例的数据大小有关，请提前做好相关准备，以防影响业务。
- 裸金属云服务器暂不支持使用控制台及 API 创建自定义镜像，您可通过云服务器 CVM 进行创建。
- 若您的 Windows 实例需入域且使用域账号，则在创建自定义镜像前，请执行 Sysprep 操作以确保在实例入域后 SID 唯一。详情请参见 [通过 Sysprep 实现云服务器入域后 SID 唯一](https://intl.cloud.tencent.com/document/product/213/35876)。

## 操作步骤
<dx-tabs>
::: 使用控制台从实例创建

#### 关机实例（可选）
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm)，查看对应实例是否需进行关机。
<dx-alert infotype="notice" title="">
2018年7月之后基于公共镜像创建的实例（系统盘为云硬盘），支持在线制作镜像（即实例不关机的情况下制作镜像）。除此情况外的实例，请先将实例关机后再进行镜像制作，以确保镜像与当前实例部署环境完全一致。
</dx-alert>
  - 需要，则继续执行步骤。
  - 不需要，请执行 [制作自定义镜像](#createOS) 步骤。
2. 在实例的管理页面，根据实际使用的视图模式进行操作：
  - **列表视图**：选择实例所在行右侧的**更多** > **实例状态** > **关机**。如下图所示：
![](https://main.qcloudimg.com/raw/cc0bb1c82b96cca94cb7c1c011b664a7.png)
  - **页签视图**：选择实例详情页面中的**关机**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/bd0d10a80c75a653adee564105a9820b.png)


#### 制作自定义镜像[](id:createOS)
1. 在实例的管理页面，根据实际使用的视图模式进行操作：
   - **列表视图**：选择**更多** > **制作镜像**。如下图所示：
   ![](https://main.qcloudimg.com/raw/8e3fc28e1a0b1e9e337ff72e34a9fd01.png)
   - **页签视图**：选择右上角的**更多操作** > **制作镜像**。如下图所示：
   ![](https://qcloudimg.tencent-cloud.cn/raw/27d7f6f19bc115c501bb1157ebe37cab.png)
2. 在弹出的“制作自定义镜像”窗口中，参考以下信息进行配置：
  - **镜像名称**及**镜像描述**：自定义名称及描述。
  - **标签**：可按需增加标签，用于资源的分类、搜索和聚合。更多信息请参见 [标签](https://intl.cloud.tencent.com/document/product/651/13334)。
<dx-alert infotype="explain" title="">
若您需创建包含系统盘及数据盘的自定义镜像，则请 [提交工单](https://console.intl.cloud.tencent.com/workorder/category) 申请开通功能。 
</dx-alert>
3. 单击**制作镜像**即可。
您可单击左侧导航栏中的 **[镜像](https://console.cloud.tencent.com/cvm/image)**，在“镜像”页面中查看镜像的创建进度。


#### 使用自定义镜像创建实例（可选）
待镜像完成创建后，在镜像列表中选择您创建的镜像，单击其所在行右侧的**创建实例**，即可购买与之前相同镜像的服务器。如下图所示：
![](https://main.qcloudimg.com/raw/2d64df77d16b3c26d275770e03a1caf1.png)

:::
::: 使用\sAPI\s创建
您可以使用 CreateImage 接口创建自定义镜像。具体内容可以参考 [创建镜像 API](https://intl.cloud.tencent.com/document/product/213/33276)。
:::
</dx-tabs>

## 最佳实践

### 数据盘数据迁移

如果您需要在启动新实例时同时保留原有实例数据盘上的数据，您可以先对数据盘做 [快照](https://intl.cloud.tencent.com/document/product/362/31638)，并在启动新实例时使用该数据盘快照创建新的云硬盘数据盘。
更多相关信息，请参阅 [快照创建云硬盘](https://intl.cloud.tencent.com/document/product/362/5757)。
