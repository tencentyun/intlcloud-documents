### How long does it take for an expired domain name to return to service after renewal?
Your domain name is in the "domain name renewal period" fo 30 days after expiration, during which you can still renew it using normal renewal price. For more information on how to renew a domain name, see [here](https://cloud.tencent.com/document/product/242/9644). If your domain name is expired for more than 30 days, it will go into the "domain name redemption period". For more information about this period, see the following description.  
On the second day upon domain name expiration, the domain name resolution will be suspended temporarily and your website cannot be accessed. If you successfully renew your domain name during the "domain name renewal period", the resolution will be resumed in 72 hours if the domain name uses Tencent Cloud DNS, or in 48-72 hours if the domain name does not use Tencent Cloud DNS.

### What is domain name redemption period?
When a domain name expires, there will be a renewal period of about 30 days, depending on the suffix of the domain name. If the domain name is not renewed in this period, it will go into the redemption period, which also varies with the suffix:

* For Chinese domain names: <Chinese>/<English>.cn, .com.cn, .net.cn, .ac.cn, .中国 domain names have a redemption period of 15 days, and .在线, .中文网 domain names have a redemption period of 30 days. If redemption is not performed during this period, the domain name will be opened for registration again.
* For international domain names: <Chinese>/<English>.com, <Chinese>/<English>.net, .org, .info, .me, <Chinese>/<English>.cc, .name, .mobi, <Chinese>/<English>.pw, <Chinese>/<English>.tv, .wang, .xyz, .club, .la (Chinese/English), .acia domain names have a redemption period of 30 days. If redemption is not performed during this period, the domain name will go into the "pending deletion period" of 5 days, during which you cannot perform renewal or redemption but wait for deletion. When 5 days pass, it will be opened for registration again.

![](//mc.qcloudimg.com/static/img/36bf19459493fea02b493fa06d2e8c30/image.png)

### How do I redeem a domain name?
Redemption is not required if your domain name is expired for not more than 30 days and is still in the renewal period. You only need to renew the domain name.
If your domain name is expired for more than 30 days but not more than 60 days, your domain name is in the "domain name redemption period", during which you can redeem the domain name at a price higher than renewal price.
Steps for domain name redemption:
1. Log in to the Tencent Cloud Domain Service Console.
2. Go to the **All Domains** page, select the domain name to be redeemed, and click the **Redeem** button from the domain name status bar.
3. Confirm your action in the pop-up window and complete the payment to finish the redemption operation.

For any other questions, [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=16&level2_id=17&level1_name=%E5%85%B6%E4%BB%96%E6%9C%8D%E5%8A%A1&level2_name=%E5%9F%9F%E5%90%8D) to contact the technical customer service.

>**Notes:**
1. To ensure your domain name stays functional, the system will inform you of the renewal of your domain name via SMS message, email or internal message before it expires. You will be informed 30, 15, 7, 5, 3 and 1 day(s) in advance before the expiration. Please check your notifications from time to time.
2. Domain name resolution is suspended during the redemption period. When a domain name is successfully redeemed, the DNS will be resumed immediately but you need to reconfigure the resolution record of the domain name. Once this is done, your domain name will be resumed in 48 hours generally.
3. To redeem a domain name during the "redemption period", you need to make a payment which is higher than normal renewal price. The price for redemption is determined by the registry.


### How long can I renew my domain name?
According to regulations of the registry, the valid period of a domain name cannot exceed 10 years (5 years for ".co" domain names). If you purchased a domain name with a usage period of 3 years, then you can renew it for another 7 years (for non-".co" domain names) or another 2 years (for ".co" domain names).
You can only renew a domain name for 1 year during redemption. Perform renewal action after the domain name is redeemed if you need to renew it for longer.

### Can I renew an expired domain name?
Yes. Generally, a domain name which just expired is still in the "domain name renewal period", which means you can renew it normally. For more information on how to renew a domain name, see [here](https://cloud.tencent.com/document/product/242/9644).

 * If your domain name is expired for not more than 30 days, the domain name should be in the renewal period, during which you can renew it normally, and it will be resumed upon successful renewal.
 * If your domain name is expired for more than 30 days, then it will be in the redemption period, and you need to redeem it using a higher price. It will be resumed upon successful redemption.
 * If the expired domain name is not in your account, then it can no longer be resumed (in most cases). You can register the domain name again after it is completely deleted.  

### Why can't my domain name be accessed after renewal?
After renewal, the domain name will take effect in 0-72 hours by default. Contact Tencent Cloud customer service if it takes more than 72 hours.

### How do I query my registrar and account?
If you forget your domain name registrar and account information, query the registrar from Whois and try to retrieve the corresponding account and password by using the registration information.

### What are the statuses for an expired domain name?
1. Within 1-30 days after domain name expiration, the domain name status displayed on Whois is "REGISTRAR HOLD" (held by registrar), i.e. the domain name renewal period.
2. When REGISTRAR HOLD status (domain name renewal period) ends, the domain name will go into 30 days of redemption period, during which the status displayed on Whois will be "REDEMPTION PERIOD" (grace period).
3. When the redemption period ends, the domain name will go into 5 days of pending deletion period (status on Whois is displayed as "PENDING Delete"), after which the domain name will be deleted. When a domain name is deleted, it will be opened for registration again.
4. The status REGISTRAR/REGISTRY LOCK means the domain name is locked by the registrar/registry to prevent registrar transfer after the domain name has expired.



