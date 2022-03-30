This document describes how to configure custom issue fields in the CODING Project Management.

## Open Project

1. Log in to the CODING Console and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. Click **Project Collaboration** in the menu on the left.

## Feature Overview[](#intro)

Fields are used to **describe** the current status, due date, assignee, priority and other information of the issue.
![](https://qcloudimg.tencent-cloud.cn/raw/5d13380329bc007c05f7f1a8ae3d9cf3.png)

This document describes how to configure custom issue fields through ****Global Field Settings**** (which determines the issue type field of your team) and ****Project Field Configuration****. The steps are as follows:

1.  Create global fields and then select the fields for your project as needed.
2.  After the configuration, the fields will be available for all the issues (such as epics, requirements, tasks, and bugs).

## Global Field Settings[](#global)

Since all the issue fields of your team are determined by global field settings, only members who have **management permissions** in the user group can modify or add custom fields. Go to **Team Management** > **Permission Configuration** > **User Group** to view details.
![](https://qcloudimg.tencent-cloud.cn/raw/fc0253f4b720f2f004cfce24292623c9.png)
If you have management permissions, go to the homepage of your team, and then select **Feature Settings** from the menu on the left.

Click **Project Collaboration** > **Issue Field** to go to the field settings page.
![](https://qcloudimg.tencent-cloud.cn/raw/e2ebe585c10959547363130f73eda741.png)

### Create field[](#create)

Fields are divided into system fields and custom fields. Click **Create Field** in the upper-right corner of the issue field settings page and select a field type.
![](https://qcloudimg.tencent-cloud.cn/raw/9cc4707333cc7c0c9918dfef30cf592a.png)

Enter a field name, description (optional), and one or more menu options to create a custom field. The name of a custom field cannot be the same as that of a system field. The following example is a custom single select field and how to use this field in the project is demonstrated in a later section.
![](https://qcloudimg.tencent-cloud.cn/raw/af734131f0f7712d7485bada23c14806.png)

### Modify or delete field[](#edit)

You can **Configure Menu Options**, **Configure Basic Info**, and **Delete** custom fields in **Action**. Make sure no project is using the field before deleting it. System fields cannot be deleted.
![](https://qcloudimg.tencent-cloud.cn/raw/db526f1355788d7097306c3c8ba344c9.png)

## Project Field Configuration[](#project)

Project field configuration only applies to a single project.

1. In a project, select **Project Settings** > **Project Collaboration** > **Issue Types** in the menu on the left, and click **Fields** to the right of the issue to configure its fields.
![](https://qcloudimg.tencent-cloud.cn/raw/0ced510507c9a7c5050aeb35231c4cf9.png)
2. On the field configuration page, select **+ Add Field** in the upper-right corner to open the drop-down list **Add from existing fields**. Then, select the above single select field and whether to set the field to required. Then, click **Add**.
![](https://qcloudimg.tencent-cloud.cn/raw/42bef0fffd40db7e3df038d53341d5ff.png)
3. You can drag the fields to change their display priority, set default field values, and enable or disable the Required and Display on creation page options as needed. Besides, you can configure the field menu or delete fields in **Action**.
![](https://qcloudimg.tencent-cloud.cn/raw/a8266290c2fb6494cee1825e881bc669.png)
4. After you confirm all the field settings, select **Apply Configuration**.
![](https://qcloudimg.tencent-cloud.cn/raw/9b7021b4135b6c07480f047408abee94.png)

## Use Project Fields[](#attributes)

For example, when you create a requirement in a project, **a new field** added above is shown on the creation page.
![](https://qcloudimg.tencent-cloud.cn/raw/fe6108aaad848e6d69f625d45dc1e8aa.png)
