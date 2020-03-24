## Billing Items
Private network-based Cloud Load Balance (CLB) is free of charge. Public network-based CLB has an instance rental charge, and public network must be purchased for its servers. For more information, see [Public Network Billing Method](https://intl.cloud.tencent.com/document/product/213/10578).

## Pay-as-You-Go
Instance rental for public network-based CLB is based on pay-as-you-go mode and calculated on a daily basis (every 24 hours), so you don't need to pay your usage upfront.
- You will be billed every 24 hours.
- Billing is based on your actual days of use.
- Billing starts after the creation of CLB instance and stops upon termination.
- Usage less than a day will be billed as one day.

> We will withhold one day instance fee when pay-as-you-go CLB instance is created, so make sure you have sufficient account balance. After the purchase, a daily instance configuration charge applies even if the instance remains idle (no access and not bound with backend CVM).

## Price
The rental fees of the public network-based CLB instance domains are as follows.

|  Domain | Price<br>(USD/Day) |
|---------|---------|
| Guangzhou, Shenzhen Finance Zone, Shanghai, Shanghai Finance Zone, Beijing, Chengdu & Chongqing   | 0.07 |  
| Hong Kong, Bangkok, Seoul & Mumbai| 0.21 |
| Tokyo | 0.22 |
| Singapore, Frankfurt, Toronto & Moscow | 0.14 |
| Silicon Valley & Virginia | 0.12 |

## Arrear Isolation Policy

- Service will stop in 24 hours when your account is in arrears. You will get SMS/email notifications to top up your account within 24 hours. Your service will not be affected if you top up your account within 24 hours. 
- If you do not top up your account within 24 hours, instance will be stopped and **isolated**, and billing of used CLB instances will be stopped. Instance-related configuration data will be kept for 7 days. If your balance is positive, service will automatically resume. If your balance remains negative more than 7 days, it will be taken that you no longer wish to continue the service and relevant configuration data will be deleted permanently.
- Tencent Cloud will send you notifications via SMS/email one day before deletion. Once deleted, relevant configuration data cannot be recovered.

> CLB and CVM can only be unbound manually, but they can unbind forcibly when **CVM** is isolated (when Pay-as-You-Go CVM account is in arrears for over 2 hours).
