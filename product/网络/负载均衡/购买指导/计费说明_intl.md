## Billing Items
Private network-based Cloud Load Balance (CLB) is free of charge. Public network-based CLB has an instance rental charge, and public network must be purchased for its servers. For more information, see [Public Network Billing Method](https://intl.cloud.tencent.com/document/product/213/10578).

## Pay-as-You-Go
Instance rental for public network-based CLB is based on pay-as-you-go mode and calculated on a daily basis (every 24 hours), so you don't need to pay your usage upfront.
- You will be billed for services used every 24 hours.
- The billing starts when the CLB instance is successfully created and stops when you perform the termination.
- Usage that is less than a day will be billed as one day.

> We will deduct a day's fee in advance when you create a pay-as-you-go CLB instance. Please ensure you have sufficient balance in your account. After purchase, there will be a daily rental fee charge, even if the instance is idle (not accessed and not bound with backend CVM).

## Price
The rental fees of the public network-based CLB instance domains are as follows.

|  Domain | Price<br>(USD/Day) |
|---------|---------|
| Guangzhou/Shenzhen Finance Zone/Shanghai/Shanghai Finance Zone/Beijing/Chengdu/Chongqing/Bangkok | 0.07 |  
| Hong Kong/Seoul/Mumbai| 0.21 |
| Tokyo | 0.22 |
| Singapore/Frankfurt/Toronto/Moscow | 0.14 |
| Silicon Valley/Virginia | 0.12 |

## Arrear Isolation Policy

- When your account is in arrears, the service will stop in 24 hours. You will be informed by SMS or email to top up your account within 24 hours. If you top up your account within 24 hours, your service will not be interrupted. 
- If the account is not topped up within 24 hours, the service will stop, the instance will be **isolated** and the occupied CLB instance will stop incurring fees. The relevant configuration data of the instance will be retained for 7 days. The instance will automatically start up if the account is topped up within 7 days. If the account remains in arrears for over 7 days, it will be taken that the user no longer wishes to continue the CLB service and the relevant configuration data will be permanently deleted. Tencent Cloud will send you a notification message via SMS or email one day before deletion. Once deleted, the relevant configuration data will not be recoverable.

> CLB and CVM can only be unbound manually, but they will be unbound by force when **CVM** is isolated (this happens when the Pay-as-You-Go CVM account is in arrears for over 2 hours).
