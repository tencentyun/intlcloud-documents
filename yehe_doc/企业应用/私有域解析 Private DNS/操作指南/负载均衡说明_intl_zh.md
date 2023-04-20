## 负载均衡介绍

基于私有域解析 Private DNS 实现的负载均衡，原理是相同主机记录、记录类型下设置不同的记录值，根据权重值随机轮询返回对应记录值。如果在同一主机记录、记录类型下有多个记录值，需要将访问流量分摊到各个记录值上，可以使用私有域的负载均衡来实现。

>?
> 解析返回得到的记录值是轮询随机得到的记录值，不会根据服务器负载和运行状况进行分配。
> 


## 负载均衡示例

负载均衡支持 A  与 CNAME 记录，各记录设置示例如下：

### A 记录负载均衡

<table>
<tr>
<td rowspan="1" colSpan="1" >主机记录</td>
<td rowspan="1" colSpan="1" >记录类型</td>
<td rowspan="1" colSpan="1" >记录值</td>
<td rowspan="1" colSpan="1" >权重</td>
<td rowspan="1" colSpan="1" >TTL</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >www</td>
<td rowspan="1" colSpan="1" >A</td>
<td rowspan="1" colSpan="1" >1.1.1.1</td>
<td rowspan="1" colSpan="1" >50</td>
<td rowspan="1" colSpan="1" >300</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >www</td>
<td rowspan="1" colSpan="1" >A</td>
<td rowspan="1" colSpan="1" >2.2.2.2</td>
<td rowspan="1" colSpan="1" >50</td>
<td rowspan="1" colSpan="1" >300</td>
</tr>
</table>


### CNAME 记录负载均衡

<table>
<tr>
<td rowspan="1" colSpan="1" >主机记录</td>
<td rowspan="1" colSpan="1" >记录类型</td>
<td rowspan="1" colSpan="1" >记录值</td>
<td rowspan="1" colSpan="1" >权重</td>
<td rowspan="1" colSpan="1" >TTL</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >www</td>
<td rowspan="1" colSpan="1" >CNAME</td>
<td rowspan="1" colSpan="1" >www.dnspod.com</td>
<td rowspan="1" colSpan="1" >50</td>
<td rowspan="1" colSpan="1" >300</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >www</td>
<td rowspan="1" colSpan="1" >CNAME</td>
<td rowspan="1" colSpan="1" >www.dnspod.cn</td>
<td rowspan="1" colSpan="1" >50</td>
<td rowspan="1" colSpan="1" >300</td>
</tr>
</table>


## 负载均衡使用限制

超出额度后不能进行正常添加。若您需添加负载均衡条数，您可购买 [增值服务优惠包](https://intl.cloud.tencent.com/document/product/1097/50828) 进行使用。
<table>
<tr>
<td rowspan="1" colSpan="1" >记录类型</td>

<td rowspan="1" colSpan="1" >“负载均衡” 条数</td>

<td rowspan="1" colSpan="1" >备注</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >A</td>

<td rowspan="1" colSpan="1" >10</td>

<td rowspan="1" colSpan="1" >-</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >AAAA</td>

<td rowspan="1" colSpan="1" >10</td>

<td rowspan="1" colSpan="1" >-</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXT</td>

<td rowspan="1" colSpan="1" >20</td>

<td rowspan="1" colSpan="1" >TXT 负载均衡不支持权重设置。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >CNAME</td>

<td rowspan="1" colSpan="1" >5</td>

<td rowspan="1" colSpan="1" >-</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >MX</td>

<td rowspan="1" colSpan="1" >50</td>

<td rowspan="1" colSpan="1" >-</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PTR</td>

<td rowspan="1" colSpan="1" >PTR 记录不支持负载均衡。</td>

<td rowspan="1" colSpan="1" >-</td>
</tr>
</table>


