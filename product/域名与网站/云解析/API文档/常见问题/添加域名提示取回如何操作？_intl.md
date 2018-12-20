## Problem Description
When I tried to add a domain name, I was prompted that the domain name had already been added by another user, as shown in the following figure. How to retrieve the domain name?
![1](//mc.qcloudimg.com/static/img/d8bf385c475f6bee85c55c4d63794d54/image.png)  
## Solution
### Method 1: Retrieving with Whois Email Verification
First, confirm that you own the email address filed with Whois. If yes, click OK and a verification email valid for half an hour will be sent to the email address.
When using Whois email verification for retrieval, check whether the following figure appears:
![3](//mc.qcloudimg.com/static/img/452b533f0e7e9d4d0a3694d4bad0894e/image.png)
If the displayed email address is "whoisprotect@dnspod.com", please first go to your domain name registrar's console and turn off "Privacy Protection" and then try again.
>**Note:**
>Domain names registered with Tencent Cloud can only be retrieved using Whois email verification.

### Method 2: Retrieving by Adding a TXT Record 
This method only applies to domain names whose DNS server is not DNSPod. You can set the following record to retrieve the domain name at the service provider for which to add a resolution.
![5](//mc.qcloudimg.com/static/img/5a5534e4d61aeccd4476c5787aa8f93c/image.png)
>**Note:**
>Domain names resolved by VIPs cannot be retrieved by yourself. Please contact customer service for assistance.

If you have any questions, you can [submit a ticket](https://console.cloud.tencent.com/workorder/create?level1_id=16&level2_id=17&level1_name=%E5%85%B6%E5%AE%83%E6%9C%8D%E5%8A%A1&level2_name=%E5%9F%9F%E5%90%8D) to contact customer service for help.
