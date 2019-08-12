
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), and select **Products** -> **Cloud Compute & Network** -> [**Virtual Private Cloud**](https://console.cloud.tencent.com/vpc/vpc?rid=8) -> **Flow Logs**.
<!-- >**Note:** 
>Flow Log is under internal trial. You can contact your business manager .<!--[You can apply for it now](https://cloud.tencent.com/act/apply/VPCFlowLogs).-->
2. Click **New** to go to "Create flow logs" page.
![](
https://main.qcloudimg.com/raw/72bbbbf536f688ce136c96bdd127c688.png)
>**Note:**
> For more information on how to create a logset and a log topic object, see [Create a logset and a log topic](https://intl.cloud.tencent.com/document/product/682/18967).
3. Enter or confirm the following parameters in the pop-up box. Click **OK** to complete the flow log creation.
 **Collection Type**: Specify the type of the traffic to be collected by flow logs: the traffic rejected/accepted by security groups or ACL, or all traffic.
 - **Logset**: Specify the storage set of the flow logs in CLS.
 - **Topic**: Specify the minimum dimension of log storage, which is used to distinguish different types of logs, such as Accept log.

![](https://main.qcloudimg.com/raw/83f8fc1b1c59582333620a4a5d3c9e5b.png)
>**Notes:**
>- You can view the records of a newly created flow log in CLS after 15 minutes upon the creation (capture window is 10 minutes, and it takes 5 minutes for data pushing).
>- Flow Logs service itself is free of charge, but the data stored in CLS is charged according to the standards set for CLS.

