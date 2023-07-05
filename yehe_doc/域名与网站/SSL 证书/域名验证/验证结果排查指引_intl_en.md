If you failed manual DNS validation, troubleshoot in either of the following ways:
- Tool diagnosis:
Click the [DNS diagnosis tool](https://myssl.com/dns_check.html#ssl_verify) and enter the content as prompted.

- Self-diagnosis:

  - Check the domain status.
Check whether the domain can be resolved properly. An unverified or newly purchased domain cannot be resolved properly.

  - Check the DNS server.
Check whether the record is added at the correct DNS service provider. For example, if the DNS server is from `www.net.cn`, it will not work to add the TXT record at DNSPod.

  - Check the DNS record.
If failure continues after you follow the steps above correctly, you may want to check for typos in the server name, record value, etc. Please confirm that TXT records are entered completely and correctly and wait for 24 hours.
    



      If the DNS record is not approved in 24 hours, [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance.
