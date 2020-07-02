>The FL service is currently in beta test. If you want to try it out, please [submit an application](https://console.cloud.tencent.com/workorder/category) for beta eligibility.
>
1. Log in to the [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Diagnostic Tools** > **Flow Logs** on the left sidebar.
2. Click **+ New** and the window "Create Flow Log Rule" will pop up.
>For more information on how to create logsets and log topics, please see [Creating Logsets and Log Topics](https://cloud.tencent.com/document/product/682/18967).
3. Enter the parameters below and click **OK** to complete the creation.
 - **Collection Type** specifies the type of traffic to be collected by flow logs: all traffic, the traffic rejected or accepted by security groups or ACL.
 - **Logset** specifies the storage location in CLS for flow logs.
 - **Log Topic** specifies the minimum dimension of log storage, which is used to distinguish different types of logs, such as Accept log.

![](https://main.qcloudimg.com/raw/8aa8ccfea284896ff569da02f5fa178d.png)
>?
>- You can view the record of a newly created flow log in CLS after 15 minutes upon the creation (10 minutes for the capture window and 5 minutes for data publishing).
>- Flow Logs service is free of charge, but the data are stored in CLS and charged by CLS. For the billing details, please see [CLS Purchase Guide](https://intl.cloud.tencent.com/document/product/614/30012).
