### I have already configured the DNS as required. Why did the validation fail?
It usually takes 10 minutes to synchronize the DNS. However, there may be a certain delay depending on your TTL. Please use a tool to check whether the configured DNS is correct. If there is no problem, please wait.

### Do I have to obtain the ICP filing for my domain to use SES?
You do not have to if you only use the domain to send emails. If the <b>A record</b> of your domain points to a Chinese mainland server, you must complete ICP filing for the domain.

### Can I use a corporate email domain as the SES email domain?
To avoid conflicts between SPF and MX records, do not use your corporate email domain as the SES email domain.
If necessary, you need to merge their SPF record.

### Can the subdomains under the same primary domain be used in SES?
Yes.

### How should I configure the DNS?
- If you are using Tencent Cloud DNS service, log in to the [Tencent Cloud console](https://console.cloud.tencent.com/cns) to configure.
- If you are using DNS service from another domain service provider, you can transfer your domain to Tencent Cloud for DNS resolution.
- In other cases, please configure it at your domain service provider.

### Is there any effects if different subdomains use different email services?
No.
