## What is CAA?

Certification Authority Authorization (CAA) is designed to avoid SSL certificates from being issued wrongly, which was approved by the Internet Engineering Task Force (IETF) as [RFC 6844](https://datatracker.ietf.org/doc/html/rfc6844). In March 2017, the CA/Browser Forum passed Ballot 187, which requires mandatory CAA checking from September 8, 2017.

## How Does CAA Work?
The domain name holder can set the CAA record to authorize a specific CA to issue an SSL certificate for it. The CA will mandatorily check the domain name’s CAA record under the regulations. If it’s not authorized, CA will reject issuing an SSL certificate for it to avoid certificate misissuance and security risks.

>?
>- If a CAA record is not configured for the domain, any CA can issue an SSL certificate for this domain.
>- If your domain is hosted with DNSPod, see [CAA Record](https://docs.dnspod.cn/dns/5f3b337aab35dc34f57913e4/).
>- If a CAA record for a non-Tencent Cloud CA is configured for the domain name, an SSL certificate cannot be issued for the domain properly. Before domain validation, check whether a CAA record is added for the domain and remove it if there is any.


