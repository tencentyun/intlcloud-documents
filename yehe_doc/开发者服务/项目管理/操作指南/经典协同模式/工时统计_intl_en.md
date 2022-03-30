This document describes workload statistics in classic project management.


## Open Project

1. Log in to the CODING Console and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, click **Project Collaboration**.

## Feature Overview

When a team is collaborating, there are often requirements for the working time of the issue. CODING allows you to set the estimated time when creating an issue (requirement, task, or bug). After you have created the issue, you can log time, add task progress, and perform other operations. After you enter the spent time (amount of time worked) and estimated remaining time, the system will automatically generate a complete worklog, which is helpful for team reviews and efficiency analytics after iterations have been completed. The following example uses a requirement to demonstrate how you can set and edit the **time**.
![](https://qcloudimg.tencent-cloud.cn/raw/ffada2e2fc61fba1241d39ad51826167.jpeg)

## Estimated Time[](#predict)

When creating an issue, you can enter the **Estimated Time** in hours for the issue (must be no more than 10,000 and 2 decimal places) on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/b71ec33058a51fcf4c9be31fb983696d.jpeg)

## Record Time[](#register)

1. On the issue details page, you can record time in **Worklog** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/074bbe067cf927380ad719a24225eb70.jpeg)
2. On the **Record Time** details page, you can enter or modify the spent time, and the remaining time will increase or decrease in real time. Alternatively, you can manually modify the remaining time.
![](https://qcloudimg.tencent-cloud.cn/raw/12eafa6743ed52ccf9d4ff9d8199c0ad.jpeg)
3. By default, the start time is the current time. You can also modify it according to the actual situation. The start time is accurate to the minute.
![](https://qcloudimg.tencent-cloud.cn/raw/8132344125f46a39387a358edb9de311.jpeg)
4. The description is optional. You can briefly sum up and describe the work to facilitate reviews after the iteration is completed.
![](https://qcloudimg.tencent-cloud.cn/raw/4680fdabf24be74d69697b83a61a00a8.jpeg)
5. After entering the information, select **Record**. The remaining time of the issue will be updated and a new record will be automatically added to **Worklog**.
![](https://qcloudimg.tencent-cloud.cn/raw/263c64bf7476e0b3dbe7ebb3e6d60e19.jpeg)

## Progress Statistics[](#progress)

On the Create Issue or issue details page, you can enter data in **Progress** on the right and adjust the issue progress. Take note that the current progress cannot be modified if the requirement includes sub-issues. The progress is automatically calculated using the following formula: Parent issue progress = SUM (Direct sub-issue progress) ÷ SUM (Number of direct sub-issues).
![](https://qcloudimg.tencent-cloud.cn/raw/e3986d993b2f4d3a7e6cc386208151fe.jpeg)

### Automatically update progress[](#automatically-update )

Progress statistics allow the progress to be automatically updated to 100% when the issue transitions to **Completed**. You will need to configure the **workflow** of the requirement/task separately in **Project Settings** > **Project Collaboration**. Select **Change Field Value** in **Configuration Rules**, set the current step as **Any Status > Completed**, and set the field being changed to **Progress**. Enter a progress of **100** and the progress will be automatically updated after the configuration is applied.

![](https://qcloudimg.tencent-cloud.cn/raw/5f9eea688f0ed9e5b6813940fb0999a0.png)
>! Only members of user groups with **Management Permissions** enabled can modify or add custom statuses. See [Custom Workflows](https://intl.cloud.tencent.com/document/product/1133/44768) for details.
>
## Manage Worklogs[](#management)

### View worklog[](#check)

In **Worklog**, you can select **View Worklog** and switch between the **action log and worklog** on the Issue Details page. The worklog shows previous operations on the current issue worklog and is sorted by the **start time** entered in Record Time. You can view the member that recorded the time, start time, and description.
![](https://qcloudimg.tencent-cloud.cn/raw/fa1e72308989bfa6bc5f60b8f23adf5d.jpeg)

### Delete worklog[](#delete)

1. A worklog can be deleted by the member that recorded it. In **Worklog**, select **Delete** below the specific worklog.
![](https://qcloudimg.tencent-cloud.cn/raw/94f231f8f2e6fd0cc9287de7ae2f65ba.png)
2. When deleting a worklog, the deleted time will be added to the remaining time if you select Adjust Remaining Time.
![](https://qcloudimg.tencent-cloud.cn/raw/206a75f35ec0da845dce605a478907aa.jpeg)
For example, 69 hours have been recorded for a worklog being deleted and the remaining time is 26.92 hours. If **Adjust Remaining Time** is selected, the remaining time will be updated as follows: 26.92 + 69 = 95.92 hours. If you do not select the checkbox, the remaining time will be unchanged at 26.92 hours.
>! Deleted worklog cannot be restored. Proceed with caution.

