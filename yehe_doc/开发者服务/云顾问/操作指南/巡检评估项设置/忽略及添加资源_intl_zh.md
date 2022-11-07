## 操作场景
云顾问支持设置忽略以下维度的资源，使其不参与巡检。
 - 已配置特定标签键和标签值的资源
 - 实例

在资源设置为“忽略”后，您可根据实际需求将资源重新添加至巡检中。

<dx-alert infotype="explain" title="">
若您需通过标签键及标签值添加或忽略资源，则需给资源添加标签。详情请参见 [创建标签并绑定资源](https://intl.cloud.tencent.com/document/product/651/41575)。
</dx-alert>




## 操作步骤

### 忽略资源
您可通过以下方式，指定不参与巡检的资源：

<dx-tabs>
::: 基于标签忽略资源
1. 登录云顾问控制台，选择左侧导航栏中的 **[评估设置](https://console.cloud.tencent.com/advisor/switch)**。
2. 在“评估设置”页面，选择**资源忽略**页签，并单击**+标签**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/3ec18201554a5f4a364b0f2c15050a4a.png)
3. 展开“标签键”及“标签值”下拉列表，选择需忽略的标签键及标签值。
4. 单击**保存**即可，已配置该标签键及标签值的资源将不参与巡检。


:::
::: 基于实例忽略资源
1. 登录云顾问控制台，选择左侧导航栏中的 **[风险评估](https://console.cloud.tencent.com/advisor/assess)**。
2. 展开评估项，选择**评估中的资源列表**，并勾选需忽略的实例。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/a320e03137f1a0e5ea5e043c7eb9491d.png)
3. 单击**忽略**，即可设置实例不参与巡检。

:::
</dx-tabs>





### 添加资源
您可通过以下方式，将已设置为忽略的资源重新添加至巡检：

<dx-tabs>
::: 基于标签添加资源

1. 登录云顾问控制台，选择左侧导航栏中的 **[评估设置](https://console.cloud.tencent.com/advisor/switch)**。
2. 在“评估设置”页面，选择**资源忽略**页签。
3. 您可根据实际需求，修改或删除已配置的标签键及标签值，以将对应资源添加至巡检：
  - **修改已有标签**：选择标签所在行右侧的**编辑**，并按需修改。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/5365bb3e9e6cfeafb8a366830af55ed8.png)
  - **删除已有标签**：单击标签所在行右侧的**删除**即可删除该标签。
![](https://qcloudimg.tencent-cloud.cn/raw/2401d97110d782660af8c2e2e5b0b8ce.png)

:::
::: 基于实例添加资源

1. 登录云顾问控制台，选择左侧导航栏中的 **[风险评估](https://console.cloud.tencent.com/advisor/assess)**。
2. 展开评估项，选择**被忽略的资源列表**，并勾选需添加的实例。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/4ca282c519b5b6b4091d9e42748b431a.png)
3. 单击**添加**，即可将实例添加至巡检。


:::
</dx-tabs>

