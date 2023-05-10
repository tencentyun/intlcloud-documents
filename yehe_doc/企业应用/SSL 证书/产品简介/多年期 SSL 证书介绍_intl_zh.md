### 什么是多年期证书
- 多年期证书是用户可一次性购买多年证书，每年证书临近到期时，腾讯云会自动将证书信息提交给CA机构审核，无需用户主动发起申请。

- 简化 SSL 证书产品申请和续费时的繁琐流程，为您自动化管理 SSL 证书申请、验证、审核、签发、续费的整个生命周期。

- 在腾讯云购买1年以上多年期证书并完成审核后，腾讯云将在前一个 SSL 证书有效期**到期前30个自然日内**为您自动申请第二张 SSL 证书，若您的组织及域名审核在有效期内，则会签发第二张证书，无需您进行重新申请操作。
  

   > **说明**
   > 
   >   - 证书自动审核通过后相当于重新颁发证书，您需要将新证书替换现有证书。
   >   - “-” 表示当前未售卖该类证书。


### 支持多年期的国际标准证书
<table>
<tr>
<td rowspan="1" colSpan="1" >证书品牌</td>
<td rowspan="1" colSpan="1" >企业型(OV) </td>
<td rowspan="1" colSpan="1" >企业型专业版(OV Pro) </td>
<td rowspan="1" colSpan="1" >域名型(DV)</td>
<td rowspan="1" colSpan="1" >域名型免费版(DV)</td>
<td rowspan="1" colSpan="1" >增强型(EV) </td>
<td rowspan="1" colSpan="1" >增强型专业版(EV Pro)</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >SecureSite</td>
<td rowspan="1" colSpan="1" >支持</td>
<td rowspan="1" colSpan="1" >支持</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >支持</td>
<td rowspan="1" colSpan="1" >支持</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >GeoTrust</td>
<td rowspan="1" colSpan="1" >支持</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >支持</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >TrustAsia</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >GlobalSign</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Wotrus</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
</table>


### 什么是自动提交审核

腾讯云 SSL 证书提供的自动提交功能，即指您可以通过 [证书管理控制台](https://console.cloud.tencent.com/certoverview) > **我的资料**中预填写企业资料和域名等申请信息并完成域名验证操作和公司信息审核。当您申请 SSL 证书时，腾讯云将帮助您自动完成特定品牌 SSL 证书的域名验证操作并提交审核，达到简易管理的效果。
自动审核将会向根 CA 机构提交 SSL 证书 OV 企业型和 EV 增强型证书、代码签名证书 CS 型和 EV_CS 增强型证书，审核通过后在腾讯云申请相应证书和类型时将跳过公司信息审核（如果审核不通过，会有专员主动联系该证书预留的联系方式）

### 支持自动提交审核的国际标准证书

以下表格为支持自动提交审核的国际标准证书。

> **说明**
> 
>  申请国密证书与不支持自动提交审核的国际标准证书时，不能跳过域名验证操作与自动提交审核。但您可以使用**我的资料**中已有的企业信息进行快速填写。
> 

<table>
<tr>
<td rowspan="1" colSpan="1" >证书品牌</td>
<td rowspan="1" colSpan="1" >企业型(OV) </td>
<td rowspan="1" colSpan="1" >企业型专业版(OV Pro) </td>
<td rowspan="1" colSpan="1" >域名型(DV)</td>
<td rowspan="1" colSpan="1" >域名型免费版(DV)</td>
<td rowspan="1" colSpan="1" >增强型(EV) </td>
<td rowspan="1" colSpan="1" >增强型专业版(EV Pro)</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >SecureSite</td>
<td rowspan="1" colSpan="1" >支持</td>
<td rowspan="1" colSpan="1" >支持</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >支持</td>
<td rowspan="1" colSpan="1" >支持</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >GeoTrust</td>
<td rowspan="1" colSpan="1" >支持</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >支持</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >TrustAsia</td>
<td rowspan="1" colSpan="1" >支持</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >支持</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >GlobalSign</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Wotrus</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >-</td>
<td rowspan="1" colSpan="1" >不支持</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
</table>


