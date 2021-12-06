This document describes how to query and manage stacks.


## Directions


1. Log in to the [TIC console](https://console.cloud.tencent.com/tic).
2. In the left sidebar, choose **Orchestration** -> **Stacks** to go to the **Stacks** page. You can view existing stacks and the following information about each stack:
	- **Region**: region where a stack resides.
	- **Created time**: time when the stack was created. UTC is used.
	- **Status**: status of a stack.
	- **Version**: current version of a stack.
![](https://main.qcloudimg.com/raw/30bb9e1f6f893781bb8a4f349899a34c.png)
3. On this page, you can perform the following stack operations:
 - **Destroy a stack**: release all resources under the stack. Its status will change from **APPLY_COMPLETED** to **DESTROY_COMPLETED**.
 - **Delete a stack**: delete a stack only after the stack is destroyed.
4. Click on the **ID/Name** of any stacks to query the following details:
 - **Property** displays basic information about the stack.
 - **Version** allows you to query and manage the version history of the stack. You can create, export and compare versions, and save a version as a template.
 >!Each stack can have only one version draft. If you have selected a version when creating a new one, the specified version will be used as the basis. If you do not specify a version, the new version will be created based on the version in **VERSION_EDITING** status by default. If no version is in the **VERSION_EDITING** status, the current running version will be used as the basis.
 - **Resource** displays all resources in the stack.
 - **Event** displays all events related to the stack version.


 
