## Balance Notifications
To send you timely balance information and help ensure the continuity of your resources, the system provides three types of balance notifications: custom balance alert, available credit alert, and credit change notification.

### Custom Balance Alerts
Alert rules
- Intended for all customers.
- Alerts are triggered when your account balance is below the specified threshold.
- Only one alert is sent daily (00:00–24:00) and the alerts stop after five days.

1. Log in to the console, go to <b>Billing Center > Payment Management > [Payment](https://console.intl.cloud.tencent.com/expense/recharge)</b>, and click **Balance alert**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EtbN280_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16758228888075.png)
2. Select **Receive balance alerts**, enter an alert threshold (up to nine integer digits and two decimal digits; negative numbers are supported), and click **Confirm**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/GVVn161_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16758229454494.png)

### Available Credit Alerts
Alert rules
- Intended for customers that have applied for a credit limit through a Tencent Cloud sales representative.
- Alerts are automatically triggered when the used credit reaches 70% of the available credit.
- Alerts are sent at four levels: 70–79%, 80–89%, 90–99%, and ≥ 100%.
- Only one alert is sent daily (00:00–24:00) and the alerts stop after five days.

### Temporary Credit Expiration Alerts
Alert rules
- Intended for customers that have applied for a temporary credit limit through a Tencent Cloud sales representative.
- Alerts are triggered 7 days before your temporary credit limit expires. If the credit limit takes effect for less than 7 days, alerts will be sent according to the actual number of effective days. To ensure the normal use of your cloud resources, please top up your account or contact the sales rep to assess whether to increase the credit limit.
- Only one alert is sent daily (00:00–24:00), and multiple expiration records are sent in one alert together. The alerts are sent until the expiration date.

### Credit Change Notifications
- Intended for customers that have applied for a credit limit through a Tencent Cloud sales representative.
- Notifications are triggered when a sales rep allocates, repossesses, or cancels credit for a customer.
- Only one notification is sent in real time.

### Specifying recipients and delivery methods
- The default recipients are the account creator, global resource collaborators, and the finance administrator.
- The default method for delivering notifications is via SMS.
- To modify the recipients and notification delivery methods, go to the [Message Subscription](https://console.cloud.tencent.com/messageCenter/messageConfig) page in the console.

1. Select **Balance Warning Notice** and click **Add recipient** or **Modify Message Recipient**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/T2y9994_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16758224335152.png)
2. In the pop-up window, modify the recipients and the notification delivery methods, and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/NDNY651_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16758224502703.png)

### Disabling notifications
If you do not want to receive balance notifications anymore, unselect **Receive balance alerts**.
