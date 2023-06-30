## 简介
专有预扣资源池为用户大规模且长期的资源需求提供资源确定性保障。用户可通过主动**创建预扣资源包**的方式，将云服务器实例资源预扣至专属的资源池中。专有预扣资源池中的资源，不会被其他用户使用。当用户创建云服务器实例时，将优先抵扣专有预扣资源池内的资源。


## 预扣包类型[](id:type)
预扣包为**循环抵扣包**：
<table>
<tr>
<th>特性 </th>
<td>循环抵扣包</td>
</tr>
<tr>
<th>适用场景</th>
<td>主要面向长期周期性扩缩容的业务资源保障需求</td>
</tr>
<tr>
<th>重复抵扣<sup>*</sup></th>
<td>支持</td>
</tr>
<tr>
<th>可抵扣实例计费类型</th>
<td>支持按量计费实例</td>
</tr>
<tr>
<th>可选资源预留时长</th>
<td colspan=2>1个月、2个月、3个月</td>
</tr>
<tr>
<th>资源预留续期</th>
<td colspan=2>支持续期</td>
</tr>
<tr>
<th>资源空置费用</th>
<td colspan=2>循环抵扣包费用，详情请参见 <a href="https://intl.cloud.tencent.com/document/product/213/43857">专有预扣资源池计费说明</a></td>
</tr>
</table>

#### 重复抵扣定义[](id:repeatDeduction)

 已创建1台实例1个月时长的循环抵扣包，并抵扣该资源包成功创建实例，此时预扣包中可抵扣数量为0。由于循环抵扣包支持重复抵扣，若在使用一段时间后将该实例退还，且预扣包未过期，实例资源将资源退回预扣包，资源包的剩余资源量回复为1，若预扣包过期，资源将退回大盘。

## 使用限制
 - 循环抵扣包支持抵扣 [按量计费](https://intl.cloud.tencent.com/document/product/213/2180) 云服务器实例。
- 默认单个资源预扣包中可预扣100台实例。
- 预扣资源包创建成功后不支持退还。
- 创建预扣资源包时，若出现库存不足的情况，将以实际库存为准。
  例如，当用户需创建100台实例的预扣资源包，此时库存仅剩50台，则将成功创建50台实例的预扣资源包。



## 购买与使用
<table>
<tr>
<th>如果您需了解</th>
<th>则请参考</th>
</tr>
<tr>
<td>专有预扣资源池的计费规则</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/213/43857">专有预扣资源池计费说明</a>
</td>
</tr>
<tr>
<td>预扣云服务器实例资源至专属资源池</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/213/43851">创建预扣包</a>
</td>
</tr>
<tr>
<td>查看可预扣的资源信息</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/213/43852">查看专有预扣资源列表</a>
</td>
</tr>
<tr>
<td>查看已有的预扣资源包信息</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/213/43853">查看已创建的预扣资源包</a>
</td>
</tr>
<tr>
<td>预扣包续期</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/213/43854">续期预扣包</a>
</td>
</tr>
<tr>
<td>快速创建相同配置的预扣包</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/213/43855">创建相同配置预扣包</a>
</td>
</tr>
<tr>
<td>抵扣已有预扣包创建实例</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/213/43856">快速创建实例</a>
</td>
</tr>
</table>
