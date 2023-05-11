This document describes how to troubleshoot a failure to issue the free SSL certificate due to domain ownership verification timeout when you apply for the certificate from Tencent Cloud.

>?
> 
>  It generally takes up to 30 minutes to issue a free SSL certificate, after which you can troubleshoot the timeout as instructed in this document.
> 


## Checking the CAA Record

CAA records need to be checked for both file validation and DNS validation. If there are no CAA records or they contain `0 issuewild "sectigo.com"` and `0 issue "sectigo.com"`, the check can be passed.

### `dig` command
``` bash
dig domain name CAA
```

Everything is normal if the returned value is empty or contains `0 issuewild "sectigo.com"` and `0 issue "sectigo.com"`, as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Jebr513_da1cd0e19bf8dffe3d14b229c3f7143f.png)

### DNS diagnosis tool

Go to the [DNS diagnosis tool](https://myssl.com/dns_check.html?checking=caa#dns_check), enter the primary domain, select **CAA**, and click **Check**. Everything is normal if the returned value is empty or contains `0 issuewild "sectigo.com"` and `0 issue "sectigo.com"`.

>?
> 
>  If the check fails or only certain regions can be checked, check the DNS settings of the domain.
> 


#### Solution

If the returned result is not empty and does not contain `0 issuewild "sectigo.com"` and `0 issue "sectigo.com"`, add the following records to the DNS settings:
<table>
<tr>
<td rowspan="1" colSpan="1" >Host</td>
<td rowspan="1" colSpan="1" >Record Type</td>
<td rowspan="1" colSpan="1" >Split Zone</td>
<td rowspan="1" colSpan="1" >Record Value</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >@</td>
<td rowspan="1" colSpan="1" >CAA</td>
<td rowspan="1" colSpan="1" >Default</td>
<td rowspan="1" colSpan="1" >0 issuewild "sectigo.com"</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >@</td>
<td rowspan="1" colSpan="1" >CAA</td>
<td rowspan="1" colSpan="1" >Default</td>
<td rowspan="1" colSpan="1" >0 issue "sectigo.com"</td>
</tr>
</table>


## Checking the DNS Record

After checking the CAA record, check whether the validation record has been added. For self-built NS servers or those with DNS query limits outside the Chinese mainland, check whether the DNS query outside the Chinese mainland is normal with the DNS diagnosis tool or [DNSCHCKER](https://dnschecker.org/#CNAME/). In general, all monitored points can return values and their returned values are the same.
1. Determine the domain to be checked.
The domain to be checked should be in the format of `host.domain`; for example, if the certificate's host is `_26A56EBADCE479E******5D304C0D8.blog` and the domain is `dnspod.cn`, the domain to be checked should be `_26A56EBADCE479E******5D304C0D8.blog.dnspod.cn`.


2. Go to the [DNS diagnosis tool](https://myssl.com/dns_check.html?checking=caa#dns_check), enter the target domain, select **CNAME**, and click **Check**. Everything is normal if the returned value is the record value prompted in the console.


## Checking Whether the Validation IP Is Blocked by the Server

If you wait a long time for the certificate to be issued by the CA after passing the file validation, it's possible that the server or data center has blocked the CA's validation IPs (`64.78.193.238` and `216.168.247.9`). In that case, add them to the allowlist.
