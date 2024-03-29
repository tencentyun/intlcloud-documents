## 接口描述

InquiryLBPriceAll 接口用于查询负载均衡实例的价格。负载均衡实例的具体价格可以参考产品说明的 [计费说明](https://intl.cloud.tencent.com/document/product/214/8848)。

接口访问域名：`lb.api.qcloud.com`

## 请求参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/214/11594) 页面。其中，此接口的 Action 字段为 InquiryLBPriceAll。


|参数名称 |必选 |类型 |描述 |
|-------- |-------- |-------- |-------- |
| loadBalancerType | 是 | Int | 负载均衡的类型：<li>2：公网</li><li>3：内网</li> |
| lbChargeType | 是 | String| CLB 实例的计费类型：<li>POSTPAID_BY_HOUR：按小时后付费，即按量计费，默认是按量计费</li> |
| goodsNum | 否 | Int | 商品数量，默认为1 |
| internetAccessible | 否 | Array | CLB 实例的网络计费模式（公网属性的负载均衡必须传此字段），如最大带宽等 |
| loadBalancerId | 否 | String | 仅续费和修改配置时才需要传此字段 |


- internetAccessible 类型
<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>必选</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> internetChargeType</td> <td> 是</td> <td> String</td> <td> 网络计费方式：<li style="margin-left:15px;padding-left:5px">TRAFFIC_POSTPAID_BY_HOUR 按流量按小时后计费</li><li style="margin-left:15px;padding-left:5px">BANDWIDTH_POSTPAID_BY_HOUR 按带宽按小时后计费</li><li style="margin-left:15px;padding-left:5px">BANDWIDTH_PACKAGE 按带宽包计费（当前，仅指定运营商时才支持此种计费模式）</li></td>
</tr>
<tr>
<td> internetMaxBandwidthOut </td> <td> 是</td> <td> Int </td> <td> 最大出带宽，单位：Mbps，支持范围：0 - 2048，仅对公网属性的 CLB 生效</td>
</tr>
</tbody></table>

##  返回参数
|参数名称 |类型 |描述 |
|--------- |--------- |--------- |
| code	|Int	| 公共错误码，0 表示成功，其他值表示失败。详见错误码页面的 [公共错误码](https://intl.cloud.tencent.com/document/product/214/11602#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81) 。|
| message	| String	| 模块错误信息描述，与接口相关。|
| codeDesc	| String	| 英文错误码，成功返回 Success，失败有相应的英文说明。|
| price	| Array |负载均衡的价格详情，价格单位为美元。|


## 示例
查询类型为公网属性的负载均衡实例的价格：
```
https://lb.api.qcloud.com/v2/index.php?Action=InquiryLBPriceAll
&<公共请求参数>
&loadBalancerType=2
&lbChargeType=PREPAID
&goodsNum=1
&inquiryType=2
&internetAccessible.internetChargeType=BANDWIDTH_PREPAID
&internetAccessible.internetMaxBandwidthOut=1
&lbChargePrepaid.period=1
```

请求返回正确的输出：
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "price": {
        "lbIdPrice": {
            "originalPrice": 37.4, 
            "discountPrice": 11.22
        }
    }
}
```
