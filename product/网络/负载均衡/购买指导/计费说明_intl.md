## Billing Items
The private network-based CLB is free, and the public network-based CLB charges the rental fee only. The public network must be purchased for the CVM bound with public network CLB. For more information, please see [Public Network Billing Method](https://intl.cloud.tencent.com/document/product/213/10578).

## Pay-as-You-Go Mode
The rental fee for public network-based CLB goes on pay-as-you-go mode and a per-day basis, so that you don't need to prepay for the entire period of use. 
- You are charged for the days of the service every 24 hours.
- The billing starts when the CLB instance is successfully created and stops when you perform the termination.
- It will charge for at least one day even if the usage is less than one day.

>! The fee of one-day usage will be deducted in advance when creating a pay-as-you-go CLB instance, hence, please make sure your account balance is sufficient. After CLB is purchased, the rental fee will always be charged even though it is idle (no access and not bound with backend CVM).

## Price
The rental fees of the public network-based CLB instance domains are as follows.
|  Domain | Price<br>（USD/Day） |
|---------|---------|
| Guangzhou/Shenzhen Finance Zone/Shanghai/Shanghai Finance Zone/Beijing/Chengdu/Chongqing/Bangkok | 0.07 |  
| Hong Kong/Seoul/Bombay | 0.21 |
| Tokyo | 0.22 |
| Singapore/Frankfurt/Toronto/Moscow | 0.14 |
| Silicon Valley/Virginia | 0.12 |

## Arrear Isolation Policy

- When account is in arrears, the service will stop in 24 hours. You will be informed by SMS or email to top up your account within 24 hours in case of service suspension.
- If the account is not topped up within 24 hours, the service will stop, the instance will be **isolated** and the occupied instance will stop charging. The relevant configuration data of the instance will be retained for 7 days. The instance will be started up automatically if it has been topped up within 7 days. If the arrears are more than 7 days, the abandonment of the CLB will be seen as the action of the user's own initiative and the relevant configuration data will be released.
- Tencent Cloud will send you a notification message via SMS or email one day before the release. Once the instance is released, the relevant configuration data will be permanently deleted and no longer be recovered.

>! CLB and CVM can only be unbound manually, but they will be unbound by force when **CVM** is isolated (Pay-as-You-Go CVM is in arrears for over 2 hours).
