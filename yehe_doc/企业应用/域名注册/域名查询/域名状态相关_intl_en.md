

### Domain status in WHOIS

When viewing a domain's WHOIS information, you will see the **Status** column. Each domain may have one or multiple current status. Understanding the meaning of each domain status helps you identify the cause of a specific status and take actions promptly.

The status is as listed below:
<table>
<tr>
<th style="width:25%">Main Status</th>
<th>Description</th>
</tr>
<tr>
<td>Starting with `client`</td>
<td>Initiated by the registrar.</td>
</tr>
<tr>
<td>Starting with `server`</td>
<td>Initiated by the registry.</td>
</tr>
<tr>
<td>ACTIVE (OK)</td>
<td>Normal status. This indicates that no action is required and no protection measure is configured. When the domain is in other status, OK is not displayed, which does not necessarily mean that the domain is exceptional.</td>
</tr>
<tr>
<td>addPeriod</td>
<td>New registration period for the domain set by the registry. This status will last for 5 days after domain registration without affecting the domain use. It will be automatically released after 5 days.</td>
</tr>
<tr>
<td>INACTIVE</td>
<td>Inactive status (as no DNS server was configured during registration, the domain cannot be resolved).</td>
</tr>
</table>

**When a domain is locked for security reasons, the following status may be displayed:**
- Status starting with `client`:
<table>
<tr>
<th style="width:25%">Status Starting with `client`</th>
<th>Description</th>
</tr>
<tr>
<td>clientDeleteProhibited</td>
<td>The domain is prohibited by the registrar from being deleted.</td>
</tr>
<tr>
<td>clientUpdateProhibited</td>
<td>The domain is prohibited by the registrar from being modified (the domain information cannot be modified, but the DNS records can be set or modified).</td>
</tr>
<tr>
<td>clientTransferProhibited</td>
<td>The domain is prohibited by the registrar from being transferred out.</td>
</tr>
</table>
- Status starting with `server`:
<table>
<tr>
<th style="width:25%">Status Starting with `server`</th>
<th>Description</th>
</tr>
<tr>
<td>serverDeleteProhibited</td>
<td>The domain is prohibited by the registry from being deleted.</td>
</tr>
<tr>
<td>serverUpdateProhibited</td>
<td>The domain is prohibited by the registry from being modified (the domain information cannot be modified, but the DNS records can be set or modified).</td>
</tr>
<tr>
<td>serverTransferProhibited</td>
<td>The domain is prohibited by the registry from being transferred (some domains newly registered or transferred to a new registrar will be set to this status for 60 days by the registry, which will be automatically released after 60 days. Some domains are set to this status as they are involved in arbitration or lawsuit and will be released after such arbitration or lawsuit ends).</td>
</tr>
</table>

**Other status regarding resolution and renewal prohibition includes:**
<table>
<tr>
<th style="width:25%">Partial Prohibition Status</th>
<th>Description</th>
</tr>
<tr>
<td>clientRenewProhibited</td>
<td>The domain is prohibited by the registrar from being renewed (the domain cannot be renewed, generally because it is under arbitration or dispute, and you need to contact the registrar to confirm the cause).</td>
</tr>
<tr>
<td>clientHold</td>
<td>The domain's DNS resolution is suspended by the registrar. Contact the registrar to release this status.</td>
</tr>
<tr>
<td>serverRenewProhibited</td>
<td>The domain is prohibited by the registry from being renewed (the domain cannot be renewed, generally because it is under arbitration or dispute, and you need to contact the registrar to confirm the cause).</td>
</tr>
<tr>
<td>serverHold</td>
<td>The domain's DNS resolution is suspended by the registry, generally because the identity verification for a .com/.cn/.net domain has not been completed. This status will be automatically released after identity verification is approved.</td>
</tr>
<tr>
<td>pendingTransfer</td>
<td>The domain is being transferred by the registry.</td>
</tr>
<tr>
<td>pendingVerification</td>
<td>The registration information is being confirmed (if identity verification has not been completed or approved for the domain, its DNS resolution will be affected. If identity verification has not been completed for the domain within 5 days of registration, the domain will enter the `serverHold` status and cannot be resolved properly).</td>
</tr>
</table>

### Domain expiration status
Domain expiration status includes the following:
<table>
<tr>
<th style="width:35%">Domain Expiration Status</th>
<th>Description</th>
</tr>
<tr>
<td>REGISTRAR HOLD</td>
<td>Indicates a period of about 30 days after domain expiration, i.e., "domain renewal period".</td>
</tr>
<tr>
<td>REDEMPTION PERIOD</td>
<td>Indicates that the domain entered the redemption period of about 30 days after the renewal period ends.</td>
</tr>
<tr>
<td>AUTORENEWPERIOD</td>
<td>Indicates that the domain can be renewed within about 30 days after expiration.</td>
</tr>
<tr>
<td>PENDING DELETE</td>
<td>Indicates that an international domain will enter the deletion waiting period of 5 days after its redemption period ends.</td>
</tr>
</tr>
<tr>
<td>REGISTRAR/REGISTRY LOCK</td>
<td>Indicates the registrar/registry lock status, which is used to prevent the domain from being transferred to another registrar after expiration.</td>
</tr>
</table>






