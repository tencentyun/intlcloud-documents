This document describes how to select a proper domain validation method when you apply for a certificate or add a domain in the SSL Certificate Service console.

## Domain validation method

SSL Certificate Service supports the following domain validation methods:
<table>
<tr>
<td rowspan="1" colSpan="1" >Validation Method</td>
<td rowspan="1" colSpan="1" >Use Cases</td>
<td rowspan="1" colSpan="1" >Use Limits</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >[Automatic DNS addition](https://www.tencentcloud.com/document/product/1007/53635)</td>
<td rowspan="1" colSpan="1" >You can select automatic DNS addition for the required domain ownership verification when you apply for an SSL certificate.</td>
<td rowspan="1" colSpan="1" >You must use a DNSPod domain.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >[DNS validation](https://intl.cloud.tencent.com/document/product/1007/45895)</td>
<td rowspan="1" colSpan="1" >You can select DNS validation for the required domain ownership verification when you apply for an SSL certificate.</td>
<td rowspan="1" colSpan="1" >You need to have the DNS permission for the domain. This is applicable to domains resolved on any platform.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >[File validation](https://intl.cloud.tencent.com/document/product/1007/43542)</td>
<td rowspan="1" colSpan="1" >You can select file validation for the required domain ownership verification when you apply for an SSL certificate.</td>
<td rowspan="1" colSpan="1" >This process is complex and requires a basic knowledge of website development.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >[Automatic DNS validation](https://www.tencentcloud.com/document/product/1007/53635)</td>
<td rowspan="1" colSpan="1" >You can apply for multi-year international standard certificates only. For more information, see [Available Multi-Year International Standard Certificates](https://www.tencentcloud.com/document/product/1007/53630).</td>
<td rowspan="1" colSpan="1" >You need to have the DNS permission for the domain.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >[Automatic file validation](https://intl.cloud.tencent.com/document/product/1007/44061)</td>
<td rowspan="1" colSpan="1" >You can apply for multi-year international standard certificates only. For more information, see [Available Multi-Year International Standard Certificates](https://www.tencentcloud.com/document/product/1007/53630).</td>
<td rowspan="1" colSpan="1" >This process is complex and requires a basic knowledge of website development.<br>Wildcard domains are not supported.</td>
</tr>
</table>


