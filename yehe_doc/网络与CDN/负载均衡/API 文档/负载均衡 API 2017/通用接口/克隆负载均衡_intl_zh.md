## 接口描述
CloneLB 接口用来克隆 CLB 的所有相关配置，包含 CLB 属性、安全组、监听器属性以及绑定的后端主机的克隆。
接口访问域名：`lb.api.qcloud.com`
>!
- 如果 CLB 的配置较多，该接口容易超时，此为正常现象，耐心等待克隆完成即可。
- 该接口不支持并发调用。
- 目前不支持传统型负载均衡的克隆。
- 所有克隆出来的新的 CLB 均为按量收费, 一旦克隆失败会自动删除。
- 克隆的 CLB 的名字统一为 cloneFrom-lb-xxx (来自 lb-xxx 的克隆)。

## 请求参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/214/11594) 页面。其中，此接口的 Action 字段为 CloneLB。

| 参数名称	 | 必选 | 类型 |描述 |
|---------|---------|---------|---------|
|loadBalancerId |	是 |	String |	负载均衡实例 ID。 |
|cloneType |	是	 |String	 |克隆类型：<li>all 克隆监听器和后端 RS 绑定关系。</li><li>onlyListener 仅克隆监听器，不克隆后端 RS 绑定关系。</li> |
|zone |	否	 |String |	克隆 CLB 的可用区，和 [购买参数](https://intl.cloud.tencent.com/document/product/214/1254) 相同。 |

## 返回参数
|参数名称|	类型|	描述|
|---------|---------|---------|
|cloneLBId|		String|	克隆产生的新的负载均衡实例 ID。|

## 示例
输入
```
https://lb.api.qcloud.com/v2/index.php?Action=CloneLB
&<公共请求参数>
&loadBalancerId=lb-xxx
&cloneType=all
```
输出
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "cloneLBId": "lb-sss"
}
```


