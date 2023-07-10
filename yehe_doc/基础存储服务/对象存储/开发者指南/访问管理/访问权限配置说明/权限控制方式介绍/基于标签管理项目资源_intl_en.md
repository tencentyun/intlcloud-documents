## Overview

>? This document describes how to use tags and tag authentication to manage project resources in the tag system. It is applicable to scenarios where a user used projects in the legacy console and granted sub-accounts access through project authentication.
>

Project management is the process of centrally managing resources based on projects. You can add Tencent Cloud product resources that support project management to a project. Then, select **Policies** > **Create Custom Policy** > **Create by Product Feature or Project Permission** in the [CAM console](https://console.cloud.tencent.com/cam) to generate a project policy. You can associate the project policy with project-related users or user groups, so that they can get the permission to manipulate project resources.

The legacy COS console enables permission management operations based on projects. However, a project policy grants the full access to all resources under all products included in the project. It **cannot meet the needs for multi-dimensional tagging and categorization** or **manage permissions in a refined manner**. In the new COS console, COS only supports tag-based permission management for project resources.

COS uses the tag service for compatibility with the legacy project feature. In the tag service system, a project is a special tag with the tag key being `project`. You can still create a project and then create a bucket under it in the project console. COS will automatically double-write the project association of a bucket during bucket creation to the tag service, so that the association can be displayed in the console.

> ?
> - If you need to manage buckets in a categorized manner, we recommend you directly use tags instead of projects to implement tasks such as permission control and cost allocation. For more information on how to add tags in the console, see [Setting Bucket Tags](https://intl.cloud.tencent.com/document/product/436/30928).
> - For more information on projects, see [Cloud Access Management](https://www.tencentcloud.com/document/product/598). For more information on the tag service, see [Tag](https://www.tencentcloud.com/document/product/651).
> - For more information on benefits of tags, see [Cloud Access Management](https://www.tencentcloud.com/document/product/598).
> 

## Granting a Sub-Account Access to a Project

You can grant a sub-account access to a project by following the steps below:

1. Log in to the [Project console](https://console.cloud.tencent.com/project), create a project, name it, and submit it. Then, create a resource such as a bucket or CVM instance under it.
    If you already have a project with storage or computing resources, you can skip this step.
2. After you create a project and bind a resource to it, enter the [Policy Management](https://console.cloud.tencent.com/cam/policy) page, click **Create Custom Policy** > **Authorize by Tag**, select COS and the operation permission to be granted, select the corresponding project tag, and grant the sub-account access to all resources under it.
3. Click **Next**, grant the permission to the selected user/user group/role, and click **Complete**.
>?
> - The default policy is to grant the sub-account access to all resources under the project tag. If you want the sub-account to perform only specified operations on certain resources under the tag, you can change the `action` (for specifying operations) and `resource` (for specifying resources) in the policy syntax as instructed in [Syntax Structure](https://intl.cloud.tencent.com/document/product/598/10604).
> - If you want the sub-account to be able to create buckets, you also need to grant it the `PUT Bucket` permission. On the [Policy Management](https://console.cloud.tencent.com/cam/policy) page, click **Create Custom Policy** > **Create by Policy Generator** and grant the sub-account the corresponding permission.
