First, please complete the registration process of a Tencent Cloud account.
### Adding a Domain Name
Log in to the Tencent Cloud DNS Console and add the domain name to be transferred to Tencent Cloud DNS. For more information, see [Adding a Domain Name](https://cloud.tencent.com/document/product/302/3446). If there is a lot of domain name data, you can select to batch import:
![](//mc.qcloudimg.com/static/img/a92554869b120029121faba523c1b438/image.png)
>**Note:**
>At this time, the domain name has only been successfully added to the Tencent Cloud DNS domain name list but not resolved by Tencent Cloud yet. You need to modify the DNS server at the domain name registrar, and after that, proceed with the subsequent steps.

### Upgrading Package (Optional)
You can upgrade the package as needed for minimum TTL, A record load balancing, subdomain name level and anti-attack traffic. For details, see [Purchasing Process](https://cloud.tencent.com/document/product/302/7808). If you want to use the free edition, you can ignore this step.
### Importing Resolution Records
If there are only a few of resolution records, you can choose to add them manually. For details, see [Adding an A Record](https://cloud.tencent.com/document/product/302/3449) and [Adding an CNAME Record](https://cloud.tencent.com/document/product/302/3450). If there are many resolution records, you can export them from the original DNS provider and import them into Tencent Cloud DNS using zone or .xls files:
![](//mc.qcloudimg.com/static/img/7bbaa544587436ca13b7741ee370ac55/image.png)
![](//mc.qcloudimg.com/static/img/f640781d89ca9f1625d71153cfb06074/image.png)
Key accounts can contact Tencent Cloud engineering team to verify whether the import is successful.
### Modifying a DNS Server
Go to the domain name registrar to modify the DNS server of the domain name. For details, see [Modifying DNS](https://cloud.tencent.com/document/product/302/5518).
### Waiting 72 Hours
Wait for the resolution to take effect globally, make sure it works and then add the resolution record.
### Verifying Whether the Resolution Works Properly
Visit a random domain name to verify whether the resolution is in effect.
### Domain Name Transfer (Optional)
After the resolution is stable, you can transfer the domain name to Tencent Cloud. For details, see [Domain Name Transfer](https://cloud.tencent.com/document/product/242/3645).
