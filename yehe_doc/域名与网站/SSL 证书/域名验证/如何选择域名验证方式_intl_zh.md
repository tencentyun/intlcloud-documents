本文档将指导您在证书管理控制台申请证书或新增域名资料时，如何选择域名验证方式。

## 域名验证方式

腾讯云 SSL 证书支持以下域名验证方式：
<table>
<tr>
<td rowspan="1" colSpan="1" >验证方式</td>
<td rowspan="1" colSpan="1" >使用场景</td>
<td rowspan="1" colSpan="1" >使用限制</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" ><a href="https://www.tencentcloud.com/document/product/1007/53635">自动添加 DNS</a></td>
<td rowspan="1" colSpan="1" >申请 SSL 证书时，需要进行域名所有权验证的情况下，可选择自动添加 DNS。</td>
<td rowspan="1" colSpan="1" >须使用腾讯云 DNS 解析 DNSPod 的域名。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1007/45895">DNS 验证</a></td>
<td rowspan="1" colSpan="1" >申请 SSL 证书时，需要进行域名所有权验证的情况下，可选择 DNS 验证。</td>
<td rowspan="1" colSpan="1" >需具备域名的解析权限，适用于在任何平台进行解析的域名。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1007/43542">文件验证</a></td>
<td rowspan="1" colSpan="1" >申请 SSL 证书时，需要进行域名所有权验证的情况下，可选择文件验证。</td>
<td rowspan="1" colSpan="1" >操作过程比较复杂，需要一定的建站基础。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" ><a href="https://www.tencentcloud.com/document/product/1007/53635">自动 DNS 验证</a></td>
<td rowspan="1" colSpan="1" >仅支持申请多年期的国际标准证书，具体可查看<a href="https://www.tencentcloud.com/document/product/1007/53630">支持多年期的国际标准证书</a></td>
<td rowspan="1" colSpan="1" >需具备域名的解析权限。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" ><a href="https://intl.cloud.tencent.com/document/product/1007/44061"></a>支持多年期的国际标准证书</td>
<td rowspan="1" colSpan="1" >仅支持申请多年期的国际标准证书，具体可查看 <a href="https://www.tencentcloud.com/document/product/1007/53630">自动文件验证</a></td>
<td rowspan="1" colSpan="1" >操作过程比较复杂，需要一定的建站基础。<br>不支持通配符域名。</td>
</tr>
</table>
