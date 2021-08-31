## API Description

This API is used to query the price of CLB instances. For more information about the prices, see [Billing Description](https://intl.cloud.tencent.com/document/product/214/8848).

Domain name for API calls: `lb.api.qcloud.com`

## Request Parameters
The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `InquiryLBPriceAll`.


| Parameter | Required | Type | Description |
|-------- |-------- |-------- |-------- |
| loadBalancerType | Yes | Int | CLB type. <li>2: public network CLB</li><li>3: private network CLB</li> |
| lbChargeType | Yes | String | Billing mode of the CLB instance.<li>POSTPAID_BY_HOUR: pay-as-you-go on an hourly basis. Keep the default value.</li> |
| goodsNum | No | Int | Number of instances. Default value: 1 |
| internetAccessible | No | Array | Network billing mode of the CLB instance, such as maximum bandwidth. This field is required for public network CLB. |
| loadBalancerId | No | String | This field is required only when you renew an instance or modify its configuration. |


- `internetAccessible` type
<table class="t"><tbody><tr>
<th><b>Parameter</b></th>
<th><b>Required</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> internetChargeType</td> <td>Yes</td> <td> String</td> <td>Network billing mode.<li style="margin-left:15px;padding-left:5px">TRAFFIC_POSTPAID_BY_HOUR: bill-by-traffic on an hourly pay-as-you-go basis</li><li style="margin-left:15px;padding-left:5px">BANDWIDTH_POSTPAID_BY_HOUR: bill-by-bandwidth on an hourly pay-as-you-go basis</li><li style="margin-left:15px;padding-left:5px">BANDWIDTH_PACKAGE: bill by bandwidth package (only for specified ISPs currently)</li></td>
</tr>
<tr>
<td> internetMaxBandwidthOut </td> <td> Yes</td> <td> Int </td> <td> Maximum outbound bandwidth, in Mbps. Valid ranges: 0-2048 Mbps. This field is only effective for public network CLB instances.</td>
</tr>
</tbody></table>

## Response Parameters
| Parameter | Type | Description |
|--------- |--------- |--------- |
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/214/11602#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81). |
| message | String | API-related module error message description. |
| codeDesc | String | Error code. For a successful operation, "Success" is returned. For a failed operation, a message describing the failure is returned. |
| price| Array | Prices of the CLB instances, in USD. |


## Example
Querying the price of a public network CLB instance.
```
https://lb.api.qcloud.com/v2/index.php?Action=InquiryLBPriceAll
&<Common request parameters>
&loadBalancerType=2
&lbChargeType=PREPAID
&goodsNum=1
&inquiryType=2
&internetAccessible.internetChargeType=BANDWIDTH_PREPAID
&internetAccessible.internetMaxBandwidthOut=1
&lbChargePrepaid.period=1
```

Successful response:
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
