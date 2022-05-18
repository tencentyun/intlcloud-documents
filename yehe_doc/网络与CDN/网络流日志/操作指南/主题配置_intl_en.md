This document describes how to create logsets and log topics specific to FL. All of these logsets and log topics are marked with “Flowlog”. The dashboard can be created only for those logsets and log topics to view the FL data of ENIs.

## Procedure
<dx-steps>
- Role authorization
- Create a logset
- Create a log topic
- Search a log record/Delete a log topic
</dx-steps>

## Directions
#### Role authorization
If you are creating a logset and log topic on this page for the first time, please complete the role authorization as instructed.
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and select **Flow Logs** > **Logs** in the left sidebar. Click **Go to authorization** in the pop-up dialog box.
![]()
2. Click **Grant**.
![]()
3. Click **Authorization completed**.
![]()


### Creating a logset
>?Only one “flowlog_logset” logset can be created under a region.
>
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and select **Flow Log** > **Topic** in the left sidebar.
2. On the page that appears, click **Create a logset** and then click **OK**. The logset “flowlog_logset” is created automatically.
![]()
		
### Creating a log topic
1. Click **+ New** in the log topic section.
![]()
2. In the “Add a log topic” dialog box that pops up, configure the log topic.
![]()
Parameter description:
	+ Topic name: The custom log topic name.
	+ FL type: ENI.
	+ Retention period: The custom log retention period. At least one day is required.
3. Click **OK**.

### Searching a log record
1. Click **Search** on the right of the log topic.
![]()
2. You will be directed to the search and analysis page in CLS, where you can view the log records of the log topic.


### Deleting a log topic
>?The log topic can be deleted only when no record of the log topic exists.
>
1. Click **Delete** on the right of the log topic.
![]()
2. Click **OK** in the pop-up dialog box.
