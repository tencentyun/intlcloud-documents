### The domain name is in serverHold state and the registrar has suspended the resolution. What can I do?
* Please check whether the identity verification for domain name has been completed. If not, this issue may occur. After the identity verification is completed, the domain name should be resolved normally.  
* If you have already completed the identity verification, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.  

### Why does a monitoring project report that the domain name cannot be resolved?
Third-party monitoring is different from the normal resolution process.
**Normal resolution process:**
1. A regular local DNS server will send requests to multiple NS server addresses simultaneously and take the fastest return value. (Every NS address in Tencent Cloud contains at least 3 servers, and each package contains 2 NS addresses with a total of more than 5 servers; as long as one server has a return, the resolution works);
2. Multiple retries (usually 3) will be performed when a connection error occurs.         
**Third-party monitoring project's monitoring process:**
1. Only one of the NS server addresses is captured for request, and other addresses are not tested;
2. No or only one retry is performed in case an error occurs.
![](https://main.qcloudimg.com/raw/e4f6d6bdf386ad92c55ea3f839d5b039.png)
Although the monitoring project keeps reporting errors, the users can be properly resolved to the IP.  

### When adding a domain name resolution, why am I prompted that "You have not registered as a Tencent Cloud DNS user"?
You have not provided the complete qualification information on the cloud platform. At present, you must verify your qualification before you can use Tencent Cloud DNS. Simply go to **User Center** -> **Account Information**, enter your complete information and upload the relevant documents. After your qualification is verified, you can start using the service.

### After a dot is automatically added after the domain name in a CNAME record, the resolution does not work. Why?
When a CNAME record is added, the record value is the domain name pointed to by CNAME. Only a domain name can be entered. After the record is generated, a "." is automatically added after the domain name, which is normal and will not affect the resolution. Please check whether other parts are correctly entered or configured. For details, see the tutorial for [CNAME Record](https://cloud.tencent.com/document/product/302/3450). If you have any further questions, please contact us for assistance.

### Why does Tencent Cloud DNS report error 4100?  
This may be due to Chinese transcoding. It is recommended that you rectify the signature generation process by referring to [PHP-based SDK](https://intl.cloud.tencent.com/document/sdk/php) or try with English.

