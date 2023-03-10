### What are domain security settings?

Tencent Cloud Domains supports the following domain security settings, which can be adopted as needed.

<table>
<tr>
<td rowspan="1" colSpan="1" >Domain Security Feature</td>
<td rowspan="1" colSpan="1" >Description</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Update prohibition lock</td>
<td rowspan="1" colSpan="1" >The domain update prohibition lock is a security service provided by the registrar as a layer of protection in addition to basic security. It effectively protects your domain information (including contact information, address, mobile number, email address, and DNS) from being modified by mistake or maliciously.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Transfer prohibition lock</td>
<td rowspan="1" colSpan="1" >The domain transfer prohibition lock is a security service provided by the registrar as a layer of protection in addition to basic security through technical means. It protects your domain from being transferred by mistake or maliciously.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >DNSSEC</td>
<td rowspan="1" colSpan="1" >As a feature of DNS, Domain Name System Security Extensions (DNSSEC) is a digital signature used to check the source domain reliability. It protects DNS data and makes such data trustworthy in other applications. Therefore, deploying DNSSEC for domains can enhance internet security and protect against attacks.</td>
</tr>
</table>


### What's the difference between the update prohibition lock and transfer prohibition lock?
- The update prohibition lock protects your domain information from being tampered with. When only this lock is enabled, you cannot enable or disable the transfer prohibition lock but can transfer domains.

- The transfer prohibition lock protects your domain from being transferred to another domain registrar. When only this lock is enabled, you can modify domain information.



### Why is there no deletion prohibition lock?

The deletion prohibition lock prevents domains from being deleted by mistake. Out of security considerations, Tencent Cloud does not provide the domain deletion feature and recommends that you enable the update prohibition lock and transfer prohibition lock and promptly renew your domain to secure it.