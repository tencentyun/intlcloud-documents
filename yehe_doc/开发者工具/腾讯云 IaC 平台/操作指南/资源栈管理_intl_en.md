This document describes how to view and manage stacks.


## Directions


1. Log in to the [TIC console](https://console.cloud.tencent.com/tic).
2. In the left sidebar, choose **Orchestration** -> **Stacks** to go to the **Stacks** page. You can view the existing stacks and the following information about each stack:
	- **Region**: region to which a stack belongs.
	- **Create time**: time when the stack was created. The time is displayed in UTC.
	- **Status**: status of a stack.
	- **Version**: current version of a stack.
![](https://main.qcloudimg.com/raw/755ff5bb43b0e9a87dfacd8d6bb3f282.png)
3. On this page, you can perform the following operations on each stack:
 - **Destroy a stack** to release resources in the stack. After a stack is destroyed, its status changes from **APPLY_COMPLETED** to **DESTROY_COMPLETED**.
 - **Delete a stack**. You can delete a stack only after the stack is destroyed.
4. Find a stack, and click **Details** in the **Operation** column to view the following stack details:
 - **Property** tab: displays basic information about the stack.
 - **Version** tab: allows you to view and manage the version history of the stack. You can create, export, and compare versions, and save a version as a template.
 >!Each stack can have only 1 version draft. If you do not specify a base version when you create a version, the new version will be created on the basis of the version in the **VERSION_EDITING** state. If no version in the **VERSION_EDITING** state exists, the current live version will be used as the basis. If you specify a base version, the specified version will be used as the basis.
 - **Resource** tab: displays all resources in the stack.
 - **Event** tab: displays all version-related events.


 
