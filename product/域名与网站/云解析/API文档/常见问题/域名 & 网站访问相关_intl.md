### How to add a domain name resolution?
Add one and save it by following the steps in [Quick Addition of Domain Resolution](https://cloud.tencent.com/document/product/302/3446).
> **Note:** 
> It takes 0-72 hours for the modified DNS server to take effect globally. If you find that the record does not become effective in some regions, please check the time of modification. If it was less than 72 hours ago, please wait patiently.

### What should I do if the domain name resolution fails?
1. If the **default** line type is not selected, the record cannot be added correctly, and some users may not be able to visit the website.
Please set **Line type** to **Default**; otherwise, only the specified lines can access your website. If it is to resolve for two lines, it is recommended to enter a **China Telecom IP** for the **Default** line (but you can configure a different IP as needed).
2. If the domain name resolution was just added, the error may be due to a regional delay. It is recommended to wait patiently for 72 hours or try again later.
3. If the domain name resolution was added long ago, you can clear the local cache and try again.
4. If cleaning the local cache does not fix the issue, you can test it locally by the method below:
```
nslookup domain name
nslookup domain name 119.29.29.29 
```
If the test domain name 119.29.29.29 is resolved properly, it can be determined that the local DNS has been hijacked. In this case, you need to contact the ISP pointed to for help.
### What can I do in case of error 400, 503 or bad request?
If the page returns an error code including:
1. Website under construction
2. Object not found
3. Error 404
4. Access forbidden
5. Error 403
6. Forbidden

Basically, the issue is not related to the resolution. It is recommended that you consult with the server administrator of the domain name. For more error codes, see [here](https://cloud.tencent.com/document/product/302/19903).

### What should I do if the domain name resolution is successful but the website cannot be opened?
If pinging the domain name gets the correct IP, it means that the resolution is good. It is recommended that you consult with the server administrator of the domain name.

### What should I do if the domain name resolution is successful but neither the IP nor the domain name can be accessed when pinging CVM?
See the following documents:
- [Unable to Ping an Instance's IP Address](https://intl.cloud.tencent.com/document/product/213/14639)
- [Unable to Access a Website](https://intl.cloud.tencent.com/document/product/213/14633)

### What should I do if the website is temporarily inaccessible due to the fact that it hasn't obtained an ICP license or contains illegal content?
According to Chinese laws and regulations, all websites that provide non-operating Internet information services within the territory of the People's Republic of China are required to obtain an ICP license.
If a domain name points to a Tencent Cloud's server in mainland China, it must complete the ICP license filing process with Tencent Cloud before it can be accessed. For details, see [here](https://cloud.tencent.com/document/product/243/655).
If a domain name points to an Alibaba Cloud's server in mainland China, it must complete the ICP license filing process with Alibaba Cloud. For details, see Alibaba Cloud's relevant documentation.
If a domain name points to a server in Hong Kong or overseas, it can be accessed directly.

### What should I do if the SSL certificate expires and the webpage becomes inaccessible?
After the certificate expires, the browser will prompt for insecure connection, but users can choose to proceed anyway. If you want to continue to use HTTPS for access, please go to the certificate authority for certificate renewal as soon as possible, or purchase a new certificate and replace the expired one with it on the server. You can also remove the HTTPS-related configuration from the server and use the HTTP protocol for website access. For specific advice, consult with your SSL certificate service provider.

### What if the webpage is inaccessible as the website is under construction?
After purchasing a domain name, you need to build the website first to make it accessible. Please contact technical support to build the website and configure domain name resolution.
