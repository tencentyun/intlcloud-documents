>! 
>- 即时通信 IM 原计费方案已于2022年12月26日下线。
>- 2022年12月26日前创建过 IM 应用的客户默认使用原计费方案，请参考[旧版价格说明](https://www.tencentcloud.com/document/product/1047/52470)，如果您想迁移到当前计费方案，请[联系销售](https://www.tencentcloud.com/contact-us)或[提交工单](https://console.tencentcloud.com/workorder)。迁移后不可恢复，请谨慎选择。
## IM 基础功能包
即时通信 IM 的基础功能包由 [基础服务资费](#jc) 和 [增值服务资费](#zz) 两部分组成。

### 基础服务资费[](id:jc)
基础服务资费包括：**套餐包费用**和**套餐包外超量费用**。
- 套餐包费用：IM 套餐包分为开发版、标准版和进阶版，创建应用后默认为开发版（免费）。您可以根据实际业务需求选择不同的套餐包，套餐包功能对比可参见 [套餐包功能对比](#tc)。
- 套餐外超量费用：超出标准版或进阶版套餐包免费额度以外所需支付的费用。


具体的计费和价格详情如下表所示：

<table >
<tbody>
 <tr>
<th colspan="2" rowspan="2" >计费项</td>

<th colspan="3">套餐包类型</td>
 </tr>
 <tr >
<th  >开发版</td>
<th  >标准版</td>
<th  >进阶版</td>
 </tr>
 <tr>
<td colspan="2" >套餐包费用</td>

<td  >免费</td>
<td  >399 USD/月</td>
<td  >699 USD/月</td>
 </tr>
 <tr  >
<td rowspan="2" >套餐外超量费用</td>
<td  >峰值 MAU</td>
<td rowspan="2" >-</td>
<td colspan="2"  >0.015 USD/用户/月</td>
 </tr>
 <tr >
<td  >峰值并发连接数（PCC）</td>
<td colspan="2"> <strike></strike> 限时免费</td>
 </tr>
</tbody></table>

>?
>- MAU 的计算方式为调用 IM SDK Login 操作与 IM 后台建立长链接后，MAU 将会加1，即单个用户当月登录即时通信 IM 计为1个 MAU，同一用户重复登录时，MAU 不累加。请根据业务场景合理使用 IM SDK Login 操作，避免出现 MAU 过高的情况。

## 增值服务资费[](id:zz)

<table>
<tr>
<th width="30%">计费项</th>
<th width="70%">说明</th>
</tr><tr>
<tr>
<td>音视频通话能力</td>
<td ><b>目前处于内测期，每个SDKAppID提供2次免费体验机会，每次有效期均为60天</b>。</td>
</tr></table>

>?更多增值服务建设中。如果您在使用即时通信 IM 有其他增值服务需求，请[联系我们](https://www.tencentcloud.com/document/product/1047/41676)。