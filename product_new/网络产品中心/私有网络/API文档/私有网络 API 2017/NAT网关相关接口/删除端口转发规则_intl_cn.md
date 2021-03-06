## 1. 接口描述
本接口（DeleteDnaptRule）用于删除 NAT 网关端口转发规则
接口请求域名：`vpc.api.qcloud.com`

使用该接口前请前往<a href="https://intl.cloud.tencent.com/doc/product/215/1682" title="网关说明" >NAT网关说明</a>了解NAT网关特性

## 2. 输入参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见 [公共请求参数](https://intl.cloud.tencent.com/doc/api/229/6976) 页面。其中，此接口的 Action 字段为 DeleteDnaptRule。

| 参数名称 | 必选  | 类型 | 描述 |
|---------|---------|---------|---------|
| vpcId | 是 | String | 私有网络 ID，如：vpc-8e0ypm3z |
| natId | 是 | String | NAT 网关 ID，如：nat-dqbak2vy |
| dnatList | 是 | Array | 要删除的端口转发规则列表 |
| dnatList.N.proto | 是 | String | 协议，可选值：tcp、udp |
| dnatList.N.eip | 是 | String | 外部 IP，即关联弹性 IP |
| dnatList.N.eport | 是 | String | 外部端号 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| code | int | 错误码。0：成功, 其他值：失败|
| message | string | 错误信息|

## 4. 错误码表
该接口没有业务逻辑错误码，更多公共错误码详见<a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC错误码">VPC 错误码</a>。

## 5. 示例
输入
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=DeleteDnaptRule
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">公共请求参数</a>>
&vpcId=vpc-d8vg6rev
&natId=nat-k6npdayk
&dnatList.0.proto=tcp
&dnatList.0.eip=139.199.232.178
&dnatList.0.eport=303
</pre>
输出
```
{
    "code":"0",
    "message":""
}
```
