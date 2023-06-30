<dx-alert infotype="explain" title="">
该功能目前处于内测阶段，如需使用请联系您的售前经理进行申请开通。
</dx-alert>


## 计费模式
- 对于已在专有预扣资源池中，但并未使用的实例，将按照 [按量计费](https://intl.cloud.tencent.com/document/product/213/2180) 的计费模式收取一定的资源空置费用。 

资源空置费用 = 同配置 [按量计费实例价格](https://intl.cloud.tencent.com/document/product/213/2176) × 0.3
<dx-alert infotype="explain" title="">
具体价格请以创建预扣资源包页面中的“空置费用”为准。
</dx-alert>




## 计费示例
您可根据以下示例，了解使用**单次抵扣包**及**循环抵扣包**时，预扣资源池的计费规则：

<dx-tabs>
::: 单次抵扣包
<table>
<tr>
<th width="11%">时间</th><th>操作</th><th>计费情况</th><th>备注</th>
</tr>
<tr>
<td>1月1日</td>
<td>创建包含3台实例的资源预扣包，时长1个月</td>
<td>创建成功后即对3台实例开始计费</td>
<td>按秒计费，并按小时结算</td>
</tr>
<tr>
<td>1月2日</td>
<td>创建1台相同配置实例，成功抵扣预扣资源</td>
<td rowspan=3>对其余2台实例进行按量计费，已被抵扣的实例不产生空置费用</td>
<td>- </td>
</tr>
<tr>
<td>1月3日</td>
<td>退还1月2日创建的1台实例</td>
<td>实例不会退还至预扣资源</td>
</tr>
<tr>
<td>···</td>
<td>无操作</td>
<td>-</td>
</tr>
<tr>
<td>2月1日</td>
<td>无操作</td>
<td>预扣包到期，不产生空置费用</td>
<td>未使用的2台实例将被退还</td>
</tr>
</table>
单次抵扣包使用过程示意图如下：
![](https://qcloudimg.tencent-cloud.cn/raw/cd41ffb0caea8b7b81a71e5d45d45333.png)

:::
::: 循环抵扣包
<table>
<tr>
<th width="11%">时间</th><th>操作</th><th>计费情况</th><th>备注</th>
</tr>
<tr>
<td>1月1日</td>
<td>创建包含3台实例的资源预扣包，时长1个月</td>
<td>创建成功后即对3台实例开始计费</td>
<td>按秒计费，并按小时结算</td>
</tr>
<tr>
<td>1月2日</td>
<td>创建1台相同配置实例，成功抵扣预扣资源</td>
<td>对其余2台实例进行按量计费，已被抵扣的实例不产生空置费用</td>
<td>可创建按量计费实例</td>
</tr>
<tr>
<td>1月3日</td>
<td>退还1月2日创建的1台实例</td>
<td>对3台实例开始计算空置费用</td>
<td>预扣包未过期，资源退回至预扣资源</td>
</tr>
<tr>
<td>1月4日</td>
<td>创建2台相同配置实例，成功抵扣预扣资源</td>
<td>对剩余1台实例进行按量计费，已被抵扣的实例不产生空置费用</td>
<td>可创建按量计费实例</td>
</tr>
<tr>
<td>···</td>
<td>无操作</td>
<td>-</td>
<td>-</td>
</tr>
<tr>
<td>2月1日</td>
<td>无操作</td>
<td>预扣包到期，不产生空置费用</td>
<td>未使用的1台实例将被退还</td>
</tr>
<tr>
<td>2月4日</td>
<td>1月4日创建的实例到期退还</td>
<td>预扣包到期，不产生空置费用</td>
<td>实例资源退还腾讯云</td>
</tr>
</table>
循环预扣包使用过程示意图如下：
![](https://qcloudimg.tencent-cloud.cn/raw/2647d27ef32cc19b7bb5737c7d58781b.png)


:::
</dx-tabs>



## 相关文档
- [专有预扣资源池概述](https://intl.cloud.tencent.com/document/product/213/43850)
- [创建预扣包](https://intl.cloud.tencent.com/document/product/213/43851)
- [查看专有预扣资源列表](https://intl.cloud.tencent.com/document/product/213/43852)
- [查看已创建的预扣包列表](https://intl.cloud.tencent.com/document/product/213/43853)
