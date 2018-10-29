
### What's the billing mode for VPN connections?
- VPN tunnels and customer gateways are free of charge.
- VPN gateways are charged by month. The cost of IDC bandwidth is included in the charges, so you need not to purchase network bandwidth for your CVM. Both pay-as-you-go and pay-by-month are supported for VPN gateways. For more information, see [Billing Overview](/document/product/215/4956?&_ga=1.243861126.2021346868.1522395796#.E8.AE.A1.E8.B4.B9.E6.A8.A1.E5.BC.8F)..

For the billing of VPC, see [Pricing List](/doc/product/215/3079).
### Why can't I renew or upgrade VPN gateways?
The renewal and upgrade of VPN gateway cannot be carried out at the same time. If there is any renewal or upgrade order pending for payment, it's not possible to perform further renewal or upgrade operation. The system will put all unpaid orders for renewal or upgrade into invalid status at 00:00 every day. You need to reorder the service.
### Will I receive a reminder when my VPN gateway expires?
- Upon the expiry of your VPN gateway, you can use it for a further period of 7 days. During this period, you can renew the VPN gateway. New validity period will be calculated starting from the last expiry time. In other words, you need to pay the fees for the use of VPN gateway between the last expiry time and the renewal.
- If you fail to make the payment within 7 days after the expiry of your VPN gateway, it will be automatically terminated, along with all the entries associated with this gateway in the route table.


### How long will the prepaid VPN gateway be retained after it expires and how do I renew it?
The prepaid VPN gateway will be frozen for 7 days after it expires. You can renew it for use. After 7 days, its resources will be released and cannot be retrieved. Please pay attention to the expiration time of the VPN gateway.

You can enable the automatic renewal feature for the VPN connection in [VPC Console](https://console.cloud.tencent.com/vpc/vpnGw?rid=1). This will automatically renew your VPN gateway service to ensure that the business is running stably without interruption, if your account balance is sufficient.

### Is the switch between Prepaid and Postpaid billing methods allowed?
You can switch the billing method of a VPN gateway from Prepaid to Postpaid. Please note that:
1. The Postpaid billing method will take effect after the current gateway expires.
2. In postpaid mode, VPN gateway fees and traffic fees are billed separately.
3. The gateway and traffic fees are charged on an hourly basis. When a VPN gateway is deleted, the usage period less than an hour is billed as 1 hour.
4. After the switch, the gateway can't be switched back to Prepaid billing method.

### Is SSL-VPN supported?
No. Only IPSec VPN is supported. If SSL-VPN is needed, it's recommended that you purchase [SSL-VPN](https://market.cloud.tencent.com/search/SSLVPN) products from the cloud market.


### How do I request a refund for my VPN gateway?
Use the following steps to get a refund for your VPN gateway:
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), and click **Ticket** in navigation bar.
![Picture Description](
https://main.qcloudimg.com/raw/84849f9c32afc5bf1458119482117096.png)
2. Go to the **Submit Ticket** page, choose the proper product and click **Application for Refund**.
![Picture Description](https://main.qcloudimg.com/raw/5c1551814fdd0921252dc8705e7c4757.png)
![](https://main.qcloudimg.com/raw/429d039eb79c9a0e6027e00a64f8fdd5.png)
3. Go to the **Application for Refund** page, enter proper information and click **Submit Ticket**.
![](
https://main.qcloudimg.com/raw/fb44c67fa01b77d236b06f464267250c.png)

Tencent Cloud customer service personnel will deal with your application within two working days. You can track your refund order generated after the refund is completed successfully.

**Notes:**
- Refund amount
 - Non-discount orders: The non-coupon amount actually paid by the user (including cash, bonus, voucher amount, rebate) is returned to your account, but coupons are not returned.
 - Discounted orders: The fees for the consumed resources are calculated based on the non-discounted original price and deducted from the refund, and the remaining amount is returned to the user.
- Notes about return of product
 - Prepaid products can be returned only if you apply for the return and confirm it by giving a reply within 5 days (inclusive) after the purchase of product. Any application and confirmation for return beyond this five-day period will be rejected.
 - For a single account, only one instance can be returned under each product. For example, for the CVM product involving 20 services, only one service can be returned for the account.
 - The device purchased as postpaid product cannot be returned after being changed to a postpaid product.
 - If you change the network billing method from bill-by-bandwidth to bill-by-traffic within the 5 days of unconditional return, only the remaining fees for the CVM and network are returned after the change.
 - Tencent Cloud has the right to reject the application for any suspected abnormal or malicious return of product.
>**Note:**
>Before request a return, check against the above five conditions and verify that you're eligible for the return, and ensure that your data has been migrated. After the return, the system will immediately clear the returned CVM and cloud database resources.



