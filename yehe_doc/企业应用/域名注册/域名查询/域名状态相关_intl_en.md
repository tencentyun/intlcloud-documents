### Domain status in WHOIS

When viewing a domain's WHOIS information, you will see the **Status** column. Each domain may have one or multiple current status. Understanding the meaning of each domain status helps you identify the cause of a specific status and take actions promptly.

The following video shows the domain status in WHOIS:



The status is as listed below:

<table>
<tr>
<td rowspan="1" colSpan="1" >Status</td>
<td rowspan="1" colSpan="1" >Description</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Starting with `client`</td>
<td rowspan="1" colSpan="1" >Initiated by the registrar</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Starting with `server`</td>
<td rowspan="1" colSpan="1" >Initiated by the registry</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >ACTIVE (OK)</td>
<td rowspan="1" colSpan="1" >Normal status. This indicates that no action is required and no protection measure is configured. When the domain is in other statuses, `OK` is not displayed, but that does not definitely mean the domain is abnormal.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >addPeriod</td>
<td rowspan="1" colSpan="1" >New registration period for the domain set by the registry. This status will last for five days after domain registration without affecting the domain use. It will be automatically released after five days.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >INACTIVE</td>
<td rowspan="1" colSpan="1" >Inactive status, which indicates that DNS query cannot be performed as the domain server is not set during registration.</td>
</tr>
</table>




**When a domain is locked for security reasons, the following statuses may be displayed:**
- Status starting with `client`:

<table>
<tr>
<td rowspan="1" colSpan="1" >Starting with `client`</td>
<td rowspan="1" colSpan="1" >Description</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >clientDeleteProhibited</td>
<td rowspan="1" colSpan="1" >The domain is prohibited by the registrar from being deleted.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >clientUpdateProhibited</td>
<td rowspan="1" colSpan="1" >The domain is prohibited by the registrar from being modified (the domain information cannot be modified, but the DNS records can be set or modified).</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >clientTransferProhibited</td>
<td rowspan="1" colSpan="1" >The domain is prohibited by the registrar from being transferred (no transfer-out from the registrar).</td>
</tr>
</table>

- Status starting with `server`:

<table>
<tr>
<td rowspan="1" colSpan="1" >Starting with `server`</td>
<td rowspan="1" colSpan="1" >Description</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >serverDeleteProhibited</td>
<td rowspan="1" colSpan="1" >The domain is prohibited by the registry from being deleted.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >serverUpdateProhibited</td>
<td rowspan="1" colSpan="1" >The domain is prohibited by the registry from being modified (the domain information cannot be modified, but the DNS records can be set or modified).</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >serverTransferProhibited</td>
<td rowspan="1" colSpan="1" >The domain is prohibited by the registry from being transferred (some domains newly registered or transferred to a new registrar will be set to this status for 60 days by the registry, which will be automatically released after 60 days. Some domains are set to this status as they are involved in arbitration or lawsuit and will be released after such arbitration or lawsuit ends).</td>
</tr>
</table>


   **Other status regarding resolution and renewal prohibition includes:**

<table>
<tr>
<td rowspan="1" colSpan="1" >Certain Prohibition Status</td>
<td rowspan="1" colSpan="1" >Description</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >clientRenewProhibited</td>
<td rowspan="1" colSpan="1" >The domain is prohibited by the registrar from being renewed (the domain cannot be renewed). Possible causes of this status include:<br>- Unverified CNNIC domains will be in this status and need to complete the verification to be released. <br>- If domains with other suffixes are in this status, they are usually under arbitration or dispute. Contact your registrar to confirm the cause.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >clientHold</td>
<td rowspan="1" colSpan="1" >The DNS is suspended by the registrar. To release the domain, contact your registrar.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >serverRenewProhibited</td>
<td rowspan="1" colSpan="1" >The domain is prohibited by the registry from being renewed (the domain cannot be renewed). Possible causes of this status include:<br>- Unverified CNNIC domains will be in this status and need to complete the verification to be released. <br>- If domains with other suffixes are in this status, they are usually under arbitration or dispute. Contact your registrar to confirm the cause.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >serverHold</td>
<td rowspan="1" colSpan="1" >The DNS is suspended by the registry. This is often because the identity verification fails for a `.com`, `.cn`, or `.net` domain. The domain will be automatically released after the identity verification is approved.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >pendingTransfer</td>
<td rowspan="1" colSpan="1" >The registry sets the domain to pending transfer.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >pendingVerification</td>
<td rowspan="1" colSpan="1" >The registration information is being confirmed (if identity verification has not been completed or approved for the domain, its DNS query will be affected. If identity verification has not been completed for the domain within five days of registration, the domain will enter the `serverHold` status and cannot be resolved properly).</td>
</tr>
</table>


### Domain expiration status

Domain expiration status includes the following:
<table>
<tr>
<td rowspan="1" colSpan="1" >Domain Expiration Status</td>
<td rowspan="1" colSpan="1" >Description</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >REGISTRAR HOLD</td>
<td rowspan="1" colSpan="1" >Indicates the period of about 30 days after expiration of a domain, i.e., the so-called "renewal period".</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >REDEMPTION PERIOD</td>
<td rowspan="1" colSpan="1" >Indicates that a domain will enter the redemption period of about 30 days after its renewal period ends.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >AUTORENEWPERIOD</td>
<td rowspan="1" colSpan="1" >Indicates that a domain can be renewed within about 30 days after expiration.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >PENDING DELETE</td>
<td rowspan="1" colSpan="1" >Indicates that an international domain will enter the deletion waiting period of five days after its redemption period ends.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >REGISTRAR/REGISTRY LOCK</td>
<td rowspan="1" colSpan="1" >Indicates the registrar/registry lock status, which is used to prevent a domain from being transferred to another registrar after expiration.</td>
</tr>
</table>




