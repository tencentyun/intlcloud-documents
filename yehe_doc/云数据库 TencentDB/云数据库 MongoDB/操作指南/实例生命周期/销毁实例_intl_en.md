## Operation Scenarios
Based on your business needs, you can return pay-as-you-go instances in the console in a self-service manner.
- After a pay-as-you-go instance is returned, it will be directly terminated without a retention period; therefore, please do so with caution.

After an instance is returned, once its status changes to "Isolated", no fees related to it will be incurred.
>!
>- After an instance is terminated, its data will not be recoverable. Please back up the data in advance.
>- When the instance is terminated, its IP resources will be released simultaneously. If the instance has read-only instances or disaster recovery instances:
>  - Read-only instances will be terminated at the same time.
>  - Disaster recovery instances will disconnect their sync connections and be promoted to master instances automatically.
>- After the instance is terminated, the refund procedures will be as detailed below:
>  - The five-day guaranteed self-service refund amount will be refunded to your Tencent Cloud account.
>  - The normal self-service refund amount will be refunded to your Tencent Cloud account at the ratio of cash and gift vouchers paid upon purchase.
> 


## Directions



 ### Pay-as-You-Go instance
1. Log in to the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb), select **More** > **Terminate** in the **Operation** column in the instance list.
2. In the pop-up dialog box, confirm that everything is correct and click **OK**.
>!After you click **OK**, the instance will be directly terminated without a retention period; therefore, please do so with caution.
>
![](https://main.qcloudimg.com/raw/b0d642108a455149b47158c059521ea2.png)
