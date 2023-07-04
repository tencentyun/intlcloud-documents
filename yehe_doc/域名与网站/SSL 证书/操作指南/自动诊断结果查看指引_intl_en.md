If manual DNS verification fails, you can solve this problem by using one of the following methods:
- Tool-based check method:
  Click [DNS Diagnostic Tool](https://myssl.com/dns_check.html#ssl_verify) and enter the information as prompted.
- Self-diagnosis method:
 - Check the status of the domain name.
Make sure the domain name can be resolved. The resolution process may fail if identity verification has not been completed for the domain name or if the domain name is newly purchased.
 - Check the DNS server.
Make sure you have assigned the resolution process to the correct resolution provider. For example, if the DNS server is a Wanwang server, adding a TXT resolution to Tencent Cloud DNS will not work.
 - Check the resolution records.
If this problem persists after you correctly perform the steps above, check for typos in the server name, record value, and other information. After ensuring that TXT records are entered completely and correctly, wait for 24 hours.

If verification still fails after 24 hours, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

