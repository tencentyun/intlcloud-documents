Resource-level permissions specify which resources users can operate on. Most DNSPod APIs support resource-level authorization. With it, you can allow a user to use specific resources.

## Authorization Types Available in CAM for DNSPod Resources

| Resource Type | Six-Segment Resource Format |
|---------|---------|
| DNSPod | `qcs::dnspod::uin/${uin}:domain/{DomainId}` |

Where:
- `${uin}` is the root account ID of the resource owner, expressed as `uin/${uin}` (e.g., `uin/12345678`), or left empty.
- `$DomainId` is the ID of a specific domain. To authorize access to all resources, enter the wildcard `*`.

## DNSPod Actions Supporting Authorization in CAM

<table>
<thead>
  <tr>
    <th>API Operation</th>
    <th>Description</th>
    <th>Format</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>DescribeAccountNicknames</td>
    <td>Gets the information of the sharing user</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeBatchList</td>
    <td>Gets the bulk operation list</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeBatchResult</td>
    <td>Gets the bulk operation result</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeBatchTask</td>
    <td>Gets bulk operation details</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDNSSecKeys</td>
    <td>Queries whether DNSSEC is enabled</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDNSSecStatus</td>
    <td>Queries the DNSSEC status </td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomain</td>
    <td>Gets the information of a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainAcquireTxtValue</td>
    <td>Gets the TXT record value for reclaiming a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainAcquireValidateCode</td>
    <td>Gets the validation code for reclaiming a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainAliasList</td>
    <td>Gets the domain alias list</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainAnalytics</td>
    <td>Gets the DNS requests of the primary domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainBatchAccquireTXTValue</td>
    <td>Gets the TXT record value for reclaiming domains in bulk</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainCustomLineList</td>
    <td>Gets the custom split zone list of a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainExistRecordList</td>
    <td>Gets existing DNS records</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainGroupList</td>
    <td>Gets the domain group list</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainLogFile</td>
    <td>Downloads a domain log file</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainLogList</td>
    <td>Views a domain log file</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainPackageList</td>
    <td>Gets the domain plan list</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainPurview</td>
    <td>Gets domain permissions</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainRegistration</td>
    <td>Gets domain registration information</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainShareInfo</td>
    <td>Gets the sharing information of a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainStatusList</td>
    <td>Gets the domain status list</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainUnlockMail</td>
    <td>Sends a domain unlocking email</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeExcelRecords</td>
    <td>Exports a record in Excel format</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeLineGroupList</td>
    <td>Gets the split zone group list of a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeProductInfo</td>
    <td>Gets product information</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeRecord</td>
    <td>Gets a DNS record</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeRecordFilterList</td>
    <td>Filters the DNS record list</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeRecordGroupList</td>
    <td>Gets the DNS record group list</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeRecordImpactInfo</td>
    <td>Validates a DNS record conflict</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeRecordLineCategoryList</td>
    <td>Gets the list of split zone categories available to a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeRecordLineList</td>
    <td>Gets the list of split zones available to a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeRecordList</td>
    <td>Gets the DNS record list</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeRecordType</td>
    <td>Gets the DNS record types available in the plan</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeShareAccountValidation</td>
    <td>Validates the target account for domain sharing</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeShareSubdomainList</td>
    <td>Gets the list of shared subdomains</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeSubdomainAnalytics</td>
    <td>Gets the DNS requests of a subdomain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeSubdomainList</td>
    <td>Gets the subdomain list of a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeTXTRecords</td>
    <td>Exports a record in TXT format</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeUserDetail</td>
    <td>Gets user details</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeUserLogList</td>
    <td>Gets the user log list</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeZoneRecords</td>
    <td>Exports a record in Zone format</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
</tbody>
</table>

<table>
<thead>
  <tr>
    <th>API Operation</th>
    <th>Description</th>
    <th>Format</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>CreateCertificate</td>
    <td>Applies for a certificate</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateDNSSec</td>
    <td>Confirms to enable DNSSEC</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateDNSSecCancel</td>
    <td>Cancels the operation of enabling DNSSEC</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateDNSSecKeys</td>
    <td>Enables DNSSEC</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateDomain</td>
    <td>Adds a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateDomainAlias</td>
    <td>Adds a domain alias</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateDomainBatch</td>
    <td>Adds domains in bulk</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateDomainBatchAccquire</td>
    <td>Adds a backend task to obtain domains in bulk</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateDomainCustomLine</td>
    <td>Creates a custom split zone for a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateDomainGroup</td>
    <td>Adds a domain group</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateImportedRecords</td>
    <td>Adds a backend task to import records</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateLineGroup</td>
    <td>Creates a split zone group for a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateLineGroupCopy</td>
    <td>Creates a split zone group copy</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateRecord</td>
    <td>Adds a DNS record</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateRecordBatch</td>
    <td>Adds DNS records in bulk</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateRecordGroup</td>
    <td>Adds a record group</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>CreateShareDomains</td>
    <td>Adds domain sharing</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DeleteDNSSec</td>
    <td>Disables DNSSEC</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DeleteDNSSecCancel</td>
    <td>Cancels the operation of disabling DNSSEC</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DeleteDomain</td>
    <td>Deletes a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DeleteDomainAlias</td>
    <td>Deletes a domain alias</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DeleteDomainCustomLine</td>
    <td>Deletes a custom split zone of a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DeleteDomainGroup</td>
    <td>Deletes a domain group</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DeleteLineGroup</td>
    <td>Deletes a split zone group of a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DeleteRecord</td>
    <td>Deletes a DNS record</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DeleteRecordGroup</td>
    <td>Deletes a DNS record group</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DeleteShareDomain</td>
    <td>Deletes a shared domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DeleteShareDomains</td>
    <td>Deletes shared domains</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainAutoRenewStatus</td>
    <td>Sets auto-renewal for a domain plan</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainCameSpeedup</td>
    <td>Enables CNAME flattening</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainCustomLine</td>
    <td>Modifies a custom split zone of a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainDNS</td>
    <td>Modifies the DNS server of a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainDNSFixStatus</td>
    <td>Refreshes the DNS validity status of a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainGroup</td>
    <td>Modifies a domain group</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainLock</td>
    <td>Locks a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainOwner</td>
    <td>Transfers a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainOwnerByCodeValidate</td>
    <td>Validates the code to reclaim a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainOwnerByTxtValidate</td>
    <td>Validates the TXT record value for reclaiming a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainRemark</td>
    <td>Adds domain remarks</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainStatus</td>
    <td>Modifies the domain status</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainTTL</td>
    <td>Modifies the default domain TTL value</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainToGroup</td>
    <td>Modifies the domain group</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDomainUnlock</td>
    <td>Unlocks a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyDynamicDNS</td>
    <td>Updates dynamic DNS records</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyLineGroup</td>
    <td>Modifies a split zone group of a domain</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyRecord</td>
    <td>Modifies a DNS record</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyRecordBatch</td>
    <td>Modifies DNS records in bulk</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyRecordGroup</td>
    <td>Modifies the record group</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyRecordRemark</td>
    <td>Modifies record remarks</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyRecordStatus</td>
    <td>Modifies the status of a DNS record</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyRecordToGroup</td>
    <td>Modifies the DNS record group</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyShareDomainStatusPause</td>
    <td>Suspends domain sharing</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyShareDomainStatusResume</td>
    <td>Resumes domain sharing</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>ModifyShareDomains</td>
    <td>Modifies domain sharing</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>UploadDomainRecordsFile</td>
    <td>Uploads a DNS record file. If a domain does not exist when you import a zone file, this domain will be automatically added.</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
</tbody>
</table>

<table>
<thead>
  <tr>
    <th>API Operation</th>
    <th>Description</th>
    <th>Format</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>DescribeDomainAndRecordList</td>
    <td>Queries domain and DNS record lists</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainFilterList</td>
    <td>Filters the domain list</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainList</td>
    <td>Gets the domain list</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainListAndExport</td>
    <td>Exports the domain list</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeDomainVipList</td>
    <td>Gets the list of domains under paid plans</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeShareDomainList</td>
    <td>Gets the list of domains shared by me</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
  <tr>
    <td>DescribeUserLineGroupList</td>
    <td>Gets the list of all split zone groups under the account</td>
    <td>qcs::dnspod::uin/${uin}:domain/{DomainId}</td>
  </tr>
</tbody>
</table>


