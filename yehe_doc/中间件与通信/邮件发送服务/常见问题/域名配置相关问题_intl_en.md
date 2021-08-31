## Domain Name Configuration
#### What are the limits for domain name creation?
-   Each Tencent Cloud account can verify up to five sender domains. We recommend you create two different domain names for triggered emails and batch emails, respectively.
    
-   We recommend you use a sub-domain name to avoid affecting the primary domain name by issues such as emailing reputation. You can create a sub-domain name of your organizational email domain as the sender domain.
    
-   A domain name passing all verification items cannot be deleted.
    
-   A primary domain name and all its sub-domain names can be used by only one Tencent Cloud account as the sender domain.

#### Why do I need to verify the domain name? What are the purposes of each configuration item?
Domain name verification is to verify your ownership of the domain name so as to prevent others from forging it to send spam emails. It also verifies the sender identity for the email service provider to improve the email deliverability.

SPF, DKIM, and DMARC verification methods are mainly used to guarantee the emailing security. The MX verification method is used to receive replies from recipients. Their specific features are as follows:
-   SPF verification  
    Sender Policy Framework (SPF) is an email verification standard designed to prevent email spoofing. The domain owner uses SPF to notify the email service provider of which servers are allowed to send emails from the domain.
    
-   DKIM verification
	DomainKeys Identified Mail (DKIM) is a standard that allows the sender to use an encrypted key as the email signature, which can be used by the email service provider to check whether the email is tampered with by any third party during delivery.
	
-   DMARC verification
	Domain-based Message Authentication, Reporting, and Conformance (DMARC) is an email authentication protocol that uses SPF and DKIM to detect email spoofing. To meet the DMARC standards, emails must be authenticated through SPF and/or DKIM.

-   MX verification  
    A mail exchanger (MX) record points to an email server and is used by the email system to locate the email server based on the recipient address suffix during emailing.

#### How do I configure a domain name on the DNS server?
This section describes how to bind DNS to DMS on the DNS server.

First, log in to the [DMS Console](https://console.cloud.tencent.com/dms), create a domain name to be verified, and click **Configure** for the domain name to view the domain name configuration information.

Then, log in at your domain name registrar's website and add the queried domain name resolution records for your domain name.

The steps to update a DNS record vary by DNS or web hosting service provider. The table below lists links to documents of some popular providers. It is not exhaustive and does not endorse or recommend any products or services of any providers.
| DNS/Hosting Service Provider | Document Link |
|--|--|
| Tencent Cloud | [TXT Record](https://cloud.tencent.com/document/product/302/12648) (only Chinese is supported) |
| AWS | [Values for basic records](https://docs.aws.amazon.com/zh_cn/Route53/latest/DeveloperGuide/resource-record-sets-values-basic.html) (external link) |
| GoDaddy | [Add a TXT record](https://www.godaddy.com/help/add-a-txt-record-19232) (external link) |
| DreamHost | [How do I add custom DNS records?](https://help.dreamhost.com/hc/en-us/articles/215414867-How-do-I-add-custom-DNS-records-) (external link) |
| Cloudflare | [Managing DNS records in Cloudflare](https://support.cloudflare.com/hc/en-us/articles/360019093151) (external link) |
| HostGator | [Manage DNS Records with HostGator/eNom](https://www.hostgator.com/help/article/manage-dns-records-with-hostgatorenom) (external link) |
| Namecheap | [How do I add TXT/SPF/DKIM/DMARC records for my domain?](https://www.namecheap.com/support/knowledgebase/article.aspx/317/2237/how-do-i-add-txtspfdkimdmarc-records-for-my-domain) (external link) |
| Names.co.uk | [Changing your domain's DNS settings](https://www.names.co.uk/support/1156-changing_your_domains_dns_settings.html) (external link) |
| Wix | [Adding or Updating TXT Records in Your Wix Account](https://support.wix.com/en/article/adding-or-updating-txt-records-in-your-wix-account) (external link) |


#### Can I modify a DNS record configured for the domain name?
After a sender domain is successfully verified, its DNS record cannot be modified or deleted; otherwise, some incoming mail servers may reject emails, affecting the email delivery.