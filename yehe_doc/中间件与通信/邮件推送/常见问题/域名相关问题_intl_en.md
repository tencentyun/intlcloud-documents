[](id:que1) 
### How should I configure the DNS?
- If you are using Tencent Cloud DNS service, log in to the [Tencent Cloud console](https://console.cloud.tencent.com/cns) to configure.
- If you are using a DNS service provided by another domain service provider, you can transfer your domain to Tencent Cloud for DNS resolution.
- In other cases, please configure it at your domain service provider.


[](id:que2) 
### Why would the validation fail after I have configured the DNS as required?
 It usually takes 10 minutes to synchronize the DNS. However, there may be a certain delay depending on your TTL. Please use a tool to check whether the configured DNS is correct. If there is no problem, please wait.

[](id:que3) 
### Do I have to obtain the ICP filing for my domain to use SES?
- You do not have to if you only use the domain to send emails.
- If the A record of your domain points to a Chinese mainland server, you must complete ICP filing for the domain.

[](id:que4) 
### Can I use an enterprise email domain as the SES email domain?
To avoid conflicts between SPF and MX records, do not use your enterprise email domain as the SES email domain.
If you have to use them together, you need to merge the SPF record. You can also create and use a second-level domain under your existing sender domain.

[](id:que5) 
### Can the subdomains under the same primary domain be used in SES?
Yes.

[](id:que6) 
### Are there any effects if different subdomains use different email services?
No.
