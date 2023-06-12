### WHOIS 中域名状态的解释说明

查看域名WHOIS 信息时，都有一项**域名状态**栏，每一个域名都有当前的状态，可能只有一个状态，也可能有多个状态。了解各种域名状态的含义，有助于您了解域名处于不同状态下的原因，可及时采取相应解决措施。

以下视频将为您介绍 WHOIS 中的域名状态：



分别有以下几种情况：

<table>
<tr>
<td rowspan="1" colSpan="1" >主要状态</td>
<td rowspan="1" colSpan="1" >说明</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >以 client 开头</td>
<td rowspan="1" colSpan="1" >由注册商发起。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >以 server 开头</td>
<td rowspan="1" colSpan="1" >由注册局发起。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >ACTIVE（OK）</td>
<td rowspan="1" colSpan="1" >普通状态（正常，没有需要立即进行的操作，也没有设置任何保护措施，当有其他状态时 OK 状态不显示，但并不代表不正常）。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >addPeriod</td>
<td rowspan="1" colSpan="1" >注册局设置的域名新注册期。域名新注册后5天内会出现该状态，不影响域名使用，5天后将自动解除该状态。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >INACTIVE</td>
<td rowspan="1" colSpan="1" >非激活状态（注册时未设置域名服务器，无法进行解析）。</td>
</tr>
</table>




**域名注册信息的保护，域名在进行某些安全锁定后，会出现以下状态：**
- 以 client 开头的状态：

<table>
<tr>
<td rowspan="1" colSpan="1" >client 开头</td>
<td rowspan="1" colSpan="1" >说明</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >clientDeleteProhibited</td>
<td rowspan="1" colSpan="1" >注册商设置禁止删除。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >clientUpdateProhibited</td>
<td rowspan="1" colSpan="1" >注册商设置禁止修改（不允许修改域名信息，可以设置或修改解析记录）。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >clientTransferProhibited</td>
<td rowspan="1" colSpan="1" >注册商设置禁止转移（注册商处设置不允许转出）。</td>
</tr>
</table>

- 以 server 开头的状态：

<table>
<tr>
<td rowspan="1" colSpan="1" >server 开头</td>
<td rowspan="1" colSpan="1" >说明</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >serverDeleteProhibited</td>
<td rowspan="1" colSpan="1" >注册局设置禁止删除。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >serverUpdateProhibited</td>
<td rowspan="1" colSpan="1" >注册局设置禁止修改（不允许修改域名信息，可以设置或修改解析记录）。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >serverTransferProhibited</td>
<td rowspan="1" colSpan="1" >注册局设置禁止转移（有的域名新注册及转移注册商在60天内会被注册局设置该状态，60天后自动解除；有的则是域名涉及仲裁或诉讼案被注册局设置，仲裁或诉讼案结束会被解除）。</td>
</tr>
</table>


   **还有一些禁止解析、禁止续费的状态：**

<table>
<tr>
<td rowspan="1" colSpan="1" >部分禁止状态</td>
<td rowspan="1" colSpan="1" >说明</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >clientRenewProhibited</td>
<td rowspan="1" colSpan="1" >注册商禁止续费（域名不能被续费）。出现该状态的原因有：<br>- 未实名的 CNNIC 域名会处于该状态，解除该状态需完成域名实名认证。<br>- 若是其他后缀的域名出现该状态，通常处于仲裁或法院争议期，请联系注册商确认原因。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >clientHold</td>
<td rowspan="1" colSpan="1" >注册商设置暂停解析，联系注册商解除该状态。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >serverRenewProhibited</td>
<td rowspan="1" colSpan="1" >注册局禁止续费（域名不能被续费）。出现该状态的原因有：<br>- 未实名的 CNNIC 域名会处于该状态，解除该状态需完成域名实名认证。<br>- 若是其他后缀的域名出现该状态，通常处于仲裁或法院争议期，请联系注册商确认原因。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >serverHold</td>
<td rowspan="1" colSpan="1" >注册局设置暂停解析（大多原因是.com、.cn、.net 等域名未进行实名认证，完成实名审核后自动解除该状态）。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >pendingTransfer</td>
<td rowspan="1" colSpan="1" >注册局设置转移过程中。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >pendingVerification</td>
<td rowspan="1" colSpan="1" >注册信息确认中（域名未完成实名审核，或实名审核未通过，期间会影响解析。如域名注册后 5 天内仍未完成实名，则将进入 serverHold 状态，无法正常解析）。</td>
</tr>
</table>


### 域名过期的状态

域名过期状态有以下几种情况：
<table>
<tr>
<td rowspan="1" colSpan="1" >域名过期状态</td>
<td rowspan="1" colSpan="1" >说明</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >REGISTRAR HOLD（注册商保留）</td>
<td rowspan="1" colSpan="1" >表示域名过期后30天左右，即俗称的 “域名续费期”。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >REDEMPTION PERIOD（赎回宽限期）</td>
<td rowspan="1" colSpan="1" >表示域名续费期结束后进入30天左右的 “域名赎回期”。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >AUTORENEWPERIOD（自动续费宽限期）</td>
<td rowspan="1" colSpan="1" >表示域名过期后30天左右，可以被续费。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >PENDING DELETE</td>
<td rowspan="1" colSpan="1" >表示国际域名在赎回期结束之后域名将进入5天的待删除期，5天期满后域名被删除。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >REGISTRAR/REGISTRY LOCK</td>
<td rowspan="1" colSpan="1" >表示注册商/局域名锁定状态，过期后防止被转移注册商。</td>
</tr>
</table>




