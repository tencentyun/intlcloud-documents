## Overview

You can grant a user permissions to view and use specific resources in the TKE console by using a Cloud Access Management (CAM) policy. This document describes how to grant a sub-account the permissions for a cluster with the specified tag in the console.


## Directions
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy). Click **Create custom policy** in the upper-left corner.
2. On the **Select Policy Creation Method** page that pops up, select **Authorize by Tag**.
3. In the service and action addition area of the Visual Policy Generator, enter the following information, and edit an authorization statement.
	- **Service** (required): select TKE.
	- **Action** (required): select the actions you want to authorize.
4. In the tag selection area, select the tags to authorize. Authorized sub-accounts will have the full read/write permissions for the resources with the specified tag key and tag value.
5. Click **Next**. On the **Bind User/Group/Role** page displayed, enter the policy name and description. The policy name is `policygen` by default, which is generated automatically in the console. The suffix number is generated based on the creation date. This is customizable.
6. Authorize users/groups/roles. Authorized sub-accounts will have the full read/write permissions for the resources with the specified tag key and tag value.
 - **Authorized User**: select the target sub-accounts as required.
 - **Authorized User Group**: select the user group to which the target sub-accounts belongs.
 - **Authorized Role**: select the role to which the target sub-accounts belong.
7. Click **Complete**.
