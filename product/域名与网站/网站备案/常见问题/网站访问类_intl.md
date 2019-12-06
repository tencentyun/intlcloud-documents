### Why is my website inaccessible?
There are three possible reasons and you need to troubleshoot accordingly.
#### Reason 1: The website has not obtained ICP filing yet
To use servers in mainland China to set up a website, you must first apply for ICP filing, and the website can be launched for access only after the ICP filing number is obtained from the Communications Administration Bureau.
To understand why ICP filing is required and the impacts of failure to obtain it, see [ICP Filing Overview](https://intl.cloud.tencent.com/document/product/1022/30453). You can submit an ICP filing application in the ICP filing system of the server provider. Guide for ICP filing application through Tencent Cloud:
[Document for website ICP filing application >>](https://intl.cloud.tencent.com/document/product/1022)

#### Reason 2: The website's ICP filing has not been transferred to Tencent Cloud
If your website has obtained an ICP filing through another access service provider and now you want to switch from your original provider to Tencent Cloud, you need to transfer the ICP filing to Tencent Cloud and only after that can you engage in website content services through Tencent Cloud.

#### Reason 3: Your website's ICP filing number has been deregistered.
Possible reasons why an ICP filing number is deregistered include the following. For the specific reason, please contact your local Communications Administration Bureau.
1. ICP filing entity applied for deregistration directly with the Communications Administration Bureau or via access provider:
   The domain name is no longer owned by the entity; the entity no longer engages in website business; or the entity is changed or dissolved.

2. The domain name has expired and the new domain name owner submitted an application for deregistration to the Communications Administration Bureau due to domain name conflict:
   The domain name with ICP filing number has expired, but the new domain name owner couldn't submit an application for ICP filing (due to domain name conflict), so they submitted the domain name certificate and explanatory note to the local Communications Administration Bureau to apply for deregistration of the ICP filing, which then deregistered the conflicting domain name's ICP filing after verifying the actual conditions.
> In this case, if there is only one website under the name of the entity, the entity will be deregistered; if there are multiple websites, only the website with the conflicting domain name will be deregistered, while the ICP filing information of other websites will be retained.

3. The website information is false or inaccurate, or some information is missing in the ICP filing:
   1. In most cases, the reason why the access provider cancels the access is that the user no longer engages in website content services on the registered platform and stops using the servers of the access provider; after the access is canceled, the website becomes an empty shell and will be deregistered by the Communications Administration Bureau.
   2. The website information is false or incorrect, for example, the phone number in the ICP filing information has been changed or canceled, and if this is found during the spot checks by the Communications Administration Bureau or MIIT, deregistration will be performed.
4. The website contains illegal information:
   The Communications Administration Bureau will deregister a website containing illegal information and its entity. In serious cases, the entity will be blacklisted and prohibited from re-applying for ICP filing with its identity document number or website name.

### What if my domain name is blocked?
Please verify whether your domain name has an ICP filing number:
- If yes, according to the Communications Administration Bureaus’ requirements, if you need to resolve your domain name to a Tencent Cloud CVM in mainland China, your website can be accessed only after the ICP filing is transferred to Tencent Cloud.
- If no, please apply for an ICP filing first. Your website can be accessed only after the ICP filing is obtained.

### What if my filed domain name is blocked?
If you are using a Tencent Cloud server, please confirm whether your domain name has obtained an ICP filing through Tencent Cloud.
According to the Communications Administration Bureaus’ requirements, if you use a server in mainland China, you need to apply for ICP filing through the server provider before your website can be accessed.
If you have already obtained ICP filing through another access provider, you need to transfer the ICP filing of the top-level domain name to Tencent Cloud. This doesn't affect your ICP filing information. 

### Can my website be accessed normally during the application for ICP filing?
- First-time ICP filing application or ICP filing application for new website: The website is not accessible before an ICP filing number is obtained.
- ICP filing information change application: The website that has obtained an ICP filing number can be accessed normally during the application for ICP filing change.
- ICP filing transfer application: The website can be accessed normally after Tencent Cloud preliminarily approves the application for ICP filing transfer.

### The application for ICP filing has already been submitted to the Communications Administration Bureaus for review. Can the access blockage be removed?
- First-time ICP filing application or ICP filing application for new website: The website is not accessible before an ICP filing number is obtained, so the access blockage cannot be removed.
- ICP filing information change application: The website that has obtained an ICP filing number can be accessed normally during the application for ICP filing change, so there is no access blockage.
- ICP filing transfer application: The domain name can be resolved for access after Tencent Cloud preliminarily approves the application for ICP filing transfer, so the access blockage can be removed.

### What if my website is still inaccessible on the day I receive a notification that my application for ICP filing has been approved?
It takes some time for the approval information to be synced from the Communications Administration Bureaus to the access provider's system, and after the synchronization, your website can be accessed normally. It is recommended that you wait for half an hour before retrying. If your website remains inaccessible for a prolonged time, please contact Tencent Cloud customer service at 4009-100-100 ext. 3 for assistance.

### The Communications Administration Bureau has approved my ICP filing application, but my website's resolution fails, why?
If an error occurs when accessing your domain name, try to ping your domain name resolution, and if the corresponding server IP is unpingable, it means that the registrar has suspended the resolution for your domain name. If the domain name suffix is .com or .net, you must verify your identity within 5 days after successfully registering the domain name before it can be resolved. If this is the case, please verify your identity accordingly.

### My domain name has already obtained an ICP filing through another access provider, but why can't it be accessed using a Tencent Cloud server?
You need to transfer the ICP filing of your top-level domain name to Tencent Cloud before you can use a Tencent Cloud server to access your website. Your website can be accessed after your application is preliminarily approved.

### Does the rejection of my application for ICP filing transfer affect my website accessibility?
Your website can be accessed only after your application for ICP filing transfer is preliminarily approved. In order to ensure normal access to your website, please complete the application process as soon as possible. 

### How long can my website be accessed after my application for ICP filing transfer is preliminarily approved if I do nothing?
After the preliminary approval, the ICP filing information will be retained for 45 days and then cleaned up. Please finish the subsequent steps in the application process within the 45-day period. 

### Can my website be accessed during the application for ICP filing transfer?
The website can be accessed normally after Tencent Cloud preliminarily approves the application for ICP filing transfer.

### My application for ICP filing transfer has been preliminarily approved, but my website still cannot be accessed, why?
Your domain name can be resolved and accessed around 10-30 minutes after the preliminary approval. If the website cannot be accessed, please troubleshoot as follows:
- If the CVM IP is pingable, it may be that permissions are configured on the server or the program is abnormal. Please contact your network administrator for network permission or configuration adjustment.
- If the CVM IP is unpingable, please contact Tencent Cloud customer service at 4009-100-100 ext. 3 for assistance.

### Can my website be accessed during the ICP filing application for new website?
No. The website is not accessible before an ICP filing number is obtained.  

### Does an application for ICP filing information change affect the website accessibility?
No.

### Can my website be used normally after ICP filing transfer is canceled?
- Cancellation of website ICP filing transfer is to unlink your ICP filing from Tencent Cloud, and after that, domain names pointing to Tencent Cloud cannot be accessed any longer.
- The ICP filing number of the website issued by MIIT still exists, and you should contact your new server provider and submit an application for ICP filing transfer as soon as possible so as to avoid any impact on the normal use of your website.

> After the transfer is canceled, if you don't switch to another access provider promptly, the ICP filing of the website may be deregistered by the competent Communications Administration Bureau.

### My domain name no longer points to a Tencent Cloud server. Will it be blocked if I don't apply for an ICP filing?
If your domain name points to a server outside mainland China, it will not be blocked.
If it points to a server in mainland China, it will be blocked, but the server won't be.

### Will a new top-level domain name that does not support ICP filing application be blocked?
Domain names with no ICP filing in mainland China will be blocked, but domain names outside mainland China don't require ICP filing and thus won't be blocked.

### What are the DNS server addresses of Tencent Cloud?
Tencent Cloud's DNS server addresses include:
- f1g1ns1.dnspod.net 
- f1g1ns2.dnspod.net

DNS change will take effect after 48 hours.
