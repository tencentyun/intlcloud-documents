>!If you are a customer of a Tencent Cloud partner, the rules regarding resource lifecycle when there are overdue payments are subject to the agreement between you and the reseller.

## Pay-As-You-Go by Monthly 95th Percentile
### Overdue Payment Alert
1. Overdue alert: You will receive a notification when your account balance becomes negative.
2. Balance alert: This feature is disabled by default. To enable this feature, see [Balance Alert Guide](https://intl.cloud.tencent.com/document/product/555/9942).

### Overdue Policies
The following policies are applied from the moment when your account balance drops to 0. 
1. Within seven days, Cloud Connect Network (CCN) is still available for the account.
2. Seven days later, the CCN instance becomes unavailable and the cross-region bandwidth drops to 0 Kbps. However, the CCN instance retains and resumes service once the overdue payment is made. 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Wiau038_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224100938.png)

>?
>- If the non-stop feature is enabled, CCN is still available even your account becomes overdue, and the billing continues. To enable this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>- The pay-as-you-go CCN instance billed by monthly 95 percentile will be charged between 8 and 10 AM (UTC+8) on the first day of the next month.
>For example, if you use such a CCN instance in November 2019, you will be charged between 8 and 10 AM (UTC+8) on December 1, 2019.
>- All operations and status changes will be notified to Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, etc.
