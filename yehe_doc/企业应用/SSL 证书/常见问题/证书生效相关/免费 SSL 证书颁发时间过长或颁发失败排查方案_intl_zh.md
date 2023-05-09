本文将介绍您在腾讯云申请免费 SSL 证书时，验证域名所有权中超时导致颁发失败如何排查处理。

> **说明**
> 
>  免费 SSL 证书颁发时间一般不超过30分钟，若超过您可参考本文自行排查导致超时原因。
> 


## 排查 CAA 记录

无论是文件验证或 DNS 验证都需要检查 CAA 记录，无 CAA 记录或 CAA 记录中包含 `0 issuewild "sectigo.com"` 和 `0 issue "sectigo.com"` 均可通过 CAA 记录检查。

### dig 命令
``` bash
dig 域名名称 CAA
```

返回值为空或包含 `0 issuewild "sectigo.com"` 和  `0 issue "sectigo.com"` 即为正常。如下图所示：
![](https://write-document-release-1258344699.cos-internal.ap-guangzhou.tencentcos.cn/100022348635/41eb33ee37ee11ed8088525400463ef7.png?q-sign-algorithm=sha1&q-ak=AKIDCA0fRmLeWwTaqhIO9OHzbBdqvJVSwwpL23cSygO5PtfpzKsrhtEaC9BzhKxCx2a0&q-sign-time=1676448807;1676452407&q-key-time=1676448807;1676452407&q-header-list=&q-url-param-list=&q-signature=da40cd6c0faf7df1bc5b3d04960affc36d89336d&x-cos-security-token=67r0tZSRDKfWD4gGyrGFdccypdBtJHDa1b290d6aa035d9f4a97367adb087bcecbmx0skXjsUotRaaqcwAxxzLgF2TxF500kWRNlO1Sn4SvfZEIeCsBCOjmSF2pGt8DEI-AGrh0TY1b2BOCTDNV4iCKcu9wST9JCAdb9AuTOUrYS4VbAck8EfojQNVR8OORmGdX0z7ONOhSM8ySt8P7seDOPePUpbJtJ_apGxejL-17SbN56gLHiRyEtZcLNp9AeFBkTZUXPCRCLLXZCJ89RdkCynOs_SBDAwgJS0cHmLrWM3uw0XKrGotReUAGbt8osLswK1CI2fDJ2gi4jujm3odbs4M5gQuDY5exIpE8m4mzZpLtZFhwFbKSOtPy0TblJeBv-t5ZnTPYxMnHNvDAoW7n6LZnjsYoREC_jst966gZKMSTffanCfjAXaXYr1hS)

### DNS 诊断工具

前往 [DNS 诊断工具](https://myssl.com/dns_check.html?checking=caa#dns_check)，输入主域名并选择 CAA 记录后点击检测，返回值为空或包含 `0 issuewild "sectigo.com"` 和 `0 issue "sectigo.com"` 即为正常。

> **说明**
> 
>  若出现检测失败或只有部分地区可以正常检测的情况，请检查域名 DNS 解析设置。
> 


#### 解决方法

若返回检测结果不为空且不包含 `0 issuewild "sectigo.com"` 和 `0 issue "sectigo.com"`，请前往域名解析处添加以下记录：
<table>
<tr>
<td rowspan="1" colSpan="1" >主机记录</td>
<td rowspan="1" colSpan="1" >记录类型</td>
<td rowspan="1" colSpan="1" >线路类型</td>
<td rowspan="1" colSpan="1" >记录值</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >@</td>
<td rowspan="1" colSpan="1" >CAA</td>
<td rowspan="1" colSpan="1" >默认</td>
<td rowspan="1" colSpan="1" >0 issuewild "sectigo.com"</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >@</td>
<td rowspan="1" colSpan="1" >CAA</td>
<td rowspan="1" colSpan="1" >默认</td>
<td rowspan="1" colSpan="1" >0 issue "sectigo.com"</td>
</tr>
</table>


## 排查验证 DNS 记录

检查完 CAA 记录后请确认验证记录是否已经添加，若为自建 NS 或部分存在境外解析限制的 NS 请检查境外解析是否正常，可使用 DNS 诊断工具或 [DNSCHCKER](https://dnschecker.org/#CNAME/) 工具进行检测，一般情况下，所有监测点均能正常返回且返回值相同。
1. 确定检测域名。
检测域名应为`主机记录.域名`，例如，证书主机记录为`_26A56EBADCE479E******5D304C0D8.blog`，域名为 `dnspod.cn`，则要检测域名为 `_26A56EBADCE479E******5D304C0D8.blog.dnspod.cn`。


2. 前往 [DNS 诊断工具](https://myssl.com/dns_check.html?checking=caa#dns_check)，输入检测域名并选择 CNAME 记录后，单击**检测**，返回值为控制台提示的记录值即为正常。


## 排查服务器是否屏蔽验证 IP

使用文件验证方式通过后进入 “等待机构签发” 时，长时间不颁发证书的原因一般为服务器或机房屏蔽了 CA 的验证 IP，请将 CA 验证 IP 加白：`64.78.193.238`、`216.168.247.9`。