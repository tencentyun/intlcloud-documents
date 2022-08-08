## 功能介绍
腾讯云通过标签工具及账单分账能力实现用户云资源账单在统计分析维度上的自定义管理，适配用户对账单及成本分析的多维管理分析诉求。如希望按 EMR 集群视角或集群中部分节点使用者视角进行账单拆分，可使用 [分账标签](https://intl.cloud.tencent.com/document/product/555/32276) 进行账单分拆。

- **集群维度账单应用场景**：可从部门维度查看集群的账单消费，在不同业务部门使用不同的 EMR 集群时，需按照部门的维度进行账单拆分。集群维度的标签将代表不同业务部门进行分账设置，并关联 EMR 集群内其他资源（如 EMR节点、云硬盘、元数据费用）。
- **集群内节点账单拆分应用场景**：可从部门维度查看节点的账单消费，在多个业务部门使用同一 EMR 集群，需按照不同部门使用的不同任务节点进行账单拆分。节点维度标签将代表不同业务部门分账设置，并关联 EMR 节点内的资源（如 CVM、系统盘、数据盘费用）。

## 前提条件
将标签设置成 [分账标签](https://intl.cloud.tencent.com/document/product/555/32276)，分账标签设置生效后，因数据缓存机制在账单中展示的时间存在有不超过24小时的延迟。

## 操作步骤
### 按集群维度分账
1. 配置分账标签
	- 新建集群配置分账标签
		- 创建集群：登录 [弹性 MapReduce 控制台](https://console.cloud.tencent.com/emr)，在集群列表页面中，选择创建集群。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/7402372e02b50580d7e430444aa473ff.png)

		- 选配分账标签：在**基础配置 > 高级设置**模块中，选择已经配置好的分账标签。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/e2fb8777b122379a6b263eb34523e49c.png)
	- 已有集群配置分账标签
		- 集群添加分账标签：登录 [弹性 MapReduce 控制台](https://console.cloud.tencent.com/emr)，在集群列表页面中，选择需要编辑标签的集群，单击顶部的**更多操作 > 编辑标签**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/93bb213f6e6c4b6947529a3fa3fb86f9.png)
		- 在弹出的“您已经选择2个云资源”窗口中，根据实际需求进行分账标签的添加、修改或者删除分账标签。
![](https://qcloudimg.tencent-cloud.cn/raw/f0af8b0ff374614d42dca5dfb59a687f.png)

>? 最多支持对20个集群进行标签的批量编辑操作。

2. 查看集群分账标签
	- 设置列表标签字段：在集群列表中单击**设置**图标。
![](https://qcloudimg.tencent-cloud.cn/raw/851508fd0c37c847f5744804e7eb0221.png)
勾选**标签**字段显示。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/d331f5321af853cac31f6e370ad5b3e6.png)
	- 查看集群分账标签。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/fb542f6be94dfb569e0a122d7cdf09ac.png)

3. 查看节点分账标签
对集群赋予的分账标签，会被集群中的 CDB（如云数据库）、CBS（系统盘、数据盘）、CVM（云服务器）自动继承。
	- 设置节点标签字段：集群列表 > 选择集群名称 > 资源管理 > 节点列表，单击**设置**图标。
![](https://qcloudimg.tencent-cloud.cn/raw/5fd76595e1fe389c499977f74eaa0e3f.png)
勾选标签字段显示，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/df84ccd0cb1a396199926398e68deca7.png)
	- 查看节点分账标签，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/63c9b964742c1d16a7444b712dbc632e.png)

4. 配置扩容资源分账标签
在创建集群之后，对于新增 MetaDB、手动/自动扩容节点不会自动继承集群维度的分账标签，需手动绑定，才能产生关联。
	- 配置扩容节点分账标签：单击**集群名称** > 资源管理 > 扩容 > 配置标签（集群维度标签），新增节点便可与集群维度分账标签产生联系。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/d9966b6cbcfb8575c2ec2f8cdbc44f4e.png)
	- 配置 MetaDB 分账标签：单击**集群名称** > 集群服务 > 新增组件 > 如选择Hive组件 > 选择分账标签（集群维度标签），新增 MetaDB 便可与集群维度分账标签产生联系。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/05a35054e9db5746258d0e49b5592bdd.png)

>? 集群费用 = 已有资源所产生费用 + 新增资源所产生费用 ，故新增资源需绑定集群维度分账标签，才能统计到集群费用。

5. 查看集群账单
前往 [费用中心](https://console.cloud.tencent.com/expense/bill/overview)  > 账单概览 > 选择所需月份账单 > 按标签汇总 > 选择集群维度分账标签，便可查看集群费用。
![](https://qcloudimg.tencent-cloud.cn/raw/2d4cef56755710fefb2f737e656fc42f.png)

>? 
>- 因为创建集群时，已选择 Hive 元数据存放位置 MetaDB 关联，故这里的费用组成由节点费用、云数据盘 CBS 、云数据库 MySql（CDB）组成。
>- 新建集群的按量计费模式，因按小时计费，故在1个小时后显示账单数据。

6. 账单下载
前往 [费用中心](https://console.cloud.tencent.com/expense/bill/overview)  > 费用账单 > 账单下载中心，可按 L0、L1、L2、L3不同类别下载不同月份的账单。
![](https://qcloudimg.tencent-cloud.cn/raw/7c9f987e12de7b78474178efc39e46f1.png)

>? 
>- L0：PDF 账单为 PDF 版电子账单，方便用户财务请款或留档。
>- L1：多维度汇总账单，提供按产品汇总、按项目汇总、按地域汇总、按标签汇总等视角的账单数据，方便您按类别查看账单。
>- L2：资源账单，提供按资源 id（实例）维度的账单数据。
>- L3：明细账单按最明细维度展示费用信息，例如小时结产品则每个组件每小时会呈现一条账单明细。（除 L3类型外，其他类型的账单仅能查询上月账单数据，本月数据需到下个月月1号查询）。

### 按节点维度分账
1. 配置节点分账标签
单击**资源管理** > 节点列表 > 选择节点 > 编辑标签。
![](https://qcloudimg.tencent-cloud.cn/raw/9705069ecff82539bbc045f46ee19b58.png)
可对节点进行添加、修改或者删除分账标签。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/cd81df662f930b488c949456fd447892.png)
2. 设置节点标签字段
集群列表 > 选择集群名称 > 资源管理 > 节点列表， 单击**设置**图标。
![](https://qcloudimg.tencent-cloud.cn/raw/aaff1123125d0f6e69c5f6a30c3eec57.png)
勾选标签字段显示，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/19af9c6bdb22fde097f8770f489e713d.png)
3. 查看节点分账标签，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/aebe90c2ab7af63ce88f35573b685442.png)
4. 查看节点账单
    前往费用中心  > 账单概览 > 选择所需月份账单 > 按标签汇总 > 选择扩容节点分账标签，便可查看节点费用。
    ![](https://qcloudimg.tencent-cloud.cn/raw/09d7b4a0014a474d08e0f30a8a47716b.png)
5. 账单下载
与集群维度的账单下载步骤一致。





