>The FL service is currently in beta test. If you want to try it out, please submit an application for beta eligibility.
>
1. Log in to the [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. On the left sidebar, click **Diagnostic Tools** > **Flow Logs** to create a flow log.
3. Click **+New** in the top-left corner and enter or confirm the following parameters in the pop-up box:
   1. Collection Type: it specifies the type of traffic to be collected by the flow log: all traffic, or the traffic rejected or accepted by security groups or ACL.
   2. Logset: it specifies the storage location in CLS for flow logs.
   3. Log Topic: it specifies the minimum dimension of log storage, which is used to distinguish between different types of logs, such as `Accept` log.
4. After selecting, click **OK** to create the flow log.
>
 >- You can view the records of a newly created flow log in CLS in 15 minutes after the creation (10 minutes for the capture window and 5 minutes for data publishing).
 >- FL is free of charge, but the data stored in CLS is charged at standard prices.

After the creation, you can view the flow log and search for log data in CLS by keyword. For more information, please see [Log Search](https://intl.cloud.tencent.com/document/product/614/16981).
![](https://main.qcloudimg.com/raw/027cb7ebdfa578c1c6c96fd88919da5a.png)
