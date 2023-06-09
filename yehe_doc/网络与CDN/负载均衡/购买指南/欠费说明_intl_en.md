## Pay-as-You-Go
>?
>- **Delete unnecessary pay-as-you-go resources** to stop billing.
>- Since your actual resource consumption is constantly changing, some slight discrepancies may exist for your stated balance.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/2rFT108_6GWe135_PRELIM__%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US.png)

### Balance Alert
The system estimates the time that your account balance is about to run out based on the current balance and your usage in the past 24 hours. If the estimated time is within 5 days, an alert is sent to the Tencent Cloud account owner and collaborators subscribed to the alert in the specified method (email, SMS, and the Message Center).

### Overdue Payment Alert
Pay-as-you-go resources are billed on an hourly basis. When the account balance becomes negative (Point 1 in the figure above), an alert is sent to the Tencent Cloud account owner and collaborators subscribed to the alert in the specified method (email, SMS, and the Message Center).

### Overdue Policies
- Starting from the point when your account balance becomes negative, the pay-as-you-go load balancers are still available for the next 2 hours, and the billing continues. 2 hours later (Point 2 in the figure above), the load balancers will be isolated and suspended. The billing stops. 
- Isolated and suspended CLBs will be released seven days later, and cannot be recovered.

>! A CLB instance will NOT be unbound from the CVM instance automatically. When a CVM instance is isolated, it **will NOT be unbound** from the CLB instance either.
>

