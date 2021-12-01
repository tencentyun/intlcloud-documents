


## Overview
It takes about **5–7** business days to transfer your domain to DNSPod from another registrar, after which Tencent Cloud will provide domain services for your domain. This process is called domain transfer in.


## [Prerequisites](id:preconditions)
Domain transfer in is between registrars. The requirements for transfer in are as follows:
- The original registrar cannot be Tencent Cloud.  
- You must be the domain owner or authorized by the owner to manage the domain.
- The domain was registered at least 60 days ago and will expire in more than 15 days. For the domain expiration date, see [WHOIS Lookup](link).
- If an expired domain was renewed or redeemed at the original registrar less than 45 days ago, transferring it in is not recommended, as doing so may invalidate the renewal with the original registrar or shorten the renewal period.  
- The domain is in normal status and not involved in any disputes or overdue payments.  
- The domain is not being processed by judiciaries, arbitration institutions, or domain dispute resolution agencies. 
- During domain transfer in, the registry needs to verify again whether the naming of its prefix is valid. If the verification fails, the domain cannot be transferred in.
- Currently, different domain suffixes have different prices. For domain suffixes that can be transferred in, see [Domain Pricing](link). 

>!Domain management right and resolution right are independent of each other. If domain transfer in does not involve DNS server changes, the existing DNS will not be affected. If you want to use the DNSPod service, proceed as instructed in [Modifying DNS Server](https://docs.dnspod.com/dns/601105aaf5ab591fcad80d2d/).

## Billing Description

Domain transfer in is free of charge. As stipulated by the domain registry, a domain needs to be renewed for 1 year if transferred in.
>! 
>- If your domain has been renewed for 10 years (the upper limit), after you successfully pay for the transfer in order, the usage period will not be extended for one whole year.
>- The domain validity period is renewed by year. If the validity period of your domain is greater than 9 years and you successfully pay for a transfer order, the usage period will not be extended for one whole year.

## Directions

### Getting domain auth-code

Submit a domain transfer out application to the original registrar to get the domain auth-code.
>!
>- To transfer a domain, you must get an **auth-code** from the original registrar.
>- If you need to enter the name of the transfer target service provider when transferring out the domain from the original registrar, enter **DNSPod**.
>
- At registrars outside the Chinese mainland such as GoDaddy, generally you can directly click a button in the console to email an auth-code to the domain owner.
- Registrars in the Chinese mainland generally don't provide this feature. You need to contact the original registrar or its agent to manually request an auth-code or domain transfer out. Then, the registrar will generally provide processing directions.
- If you purchased the domain from an agent of a registrar such as www.net.cn and www.west.cn, and the agent refuses to provide an auth-code, you can directly make a complaint to the registrar. If the registrar also refuses to cooperate, you can make a complaint to registries such as ICANN or CNNIC.
- According to the regulations of applicable domain administrations (ICANN Domain Transfer Policy), the original registrar shall not reject, restrict, or charge for domain transfers for any reason. If the original registrar hinders your domain transfer or charges fees, you can make a complaint to [ICANN](http://www.icann.org/en/resources/compliance/complaints/transfer/form).


### Creating domain transfer in

1. Log in to the [Domains console](link) and enter the **My Domains** page.
3. Select **Transfer Domain** on the left sidebar to enter the **My Transfers** page.
4. Click **Transfer Domain** to start the domain transfer in process.

### Steps for domain transfer in
1. Enter the information, indicate your consent to the applicable agreements, and click **Submit** as shown below:
![](https://main.qcloudimg.com/raw/cb9f3256128436efcef92f3372bf88cb.png)
  - **Domain and auth-code**: enter them as required.
  - **Auto-Renewal**: the system will automatically renew your domain before it expires. Make sure that your account balance is sufficient.
<dx-alert infotype="explain" title="">
After auto-renewal is enabled, you can disable it in the [domain name list](link).
</dx-alert>
2. Domain transfer in requires to you renew the domain for one year. After the transfer order is generated, click **Pay** to make the payment as prompted as shown below:
![](https://main.qcloudimg.com/raw/906e5d6be733ab41a4f7bc7e434b974d.png)
3. After successful payment, you can return to the console, select **My Domains** > **Pending Transfer In** to view the status of your domain to be transferred in as shown below:
>!
> - Domain transfer in generally takes **5–7** business days, subject to the handling time of the registry. Please wait patiently.
>- After the domain is successfully transferred in, Tencent Cloud will send an SMS message to the mobile number bound to your account or an email to your bound email address.
>- To cancel transfer in, click **Cancel Transfer In**. For more information, see [How to Cancel Domain Transfer In](link).
>
![](https://main.qcloudimg.com/raw/848795cb2742e4c493bb53a7a0fffcef.png)


