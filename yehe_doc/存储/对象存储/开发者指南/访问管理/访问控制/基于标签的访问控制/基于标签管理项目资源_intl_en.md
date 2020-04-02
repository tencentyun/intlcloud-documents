## Overview

> This document describes how to use tags and tag authentication to manage project resources in the tag system. It is applicable to the scenario where a user used projects in the legacy console and granted sub-accounts access through project authentication.

Project management is centralized management of resources in the project dimension. You can add Tencent Cloud product resources that support project management to a project. Then, select **Policy** > **Create Custom Policy** > **Create by Product Feature or Project Permission** in the [CAM Console](https://console.cloud.tencent.com/cam) to generate a project policy. You can associate the project policy with project-related users or user groups, so that they can get the permission to manipulate project resources.

The legacy COS Console enables permission management operations based on projects. However, a project policy grants the full access to all resources under all products included in the project. It **cannot meet the needs for multi-dimensional tagging and categorization**, **nor can it manage permissions in a refined manner**. In the new COS Console, COS only supports tag-based permission management for project resources.

COS uses the tag service to be compatible with the legacy project feature. In the tag service system, a project is a special tag with the tag key being `project`. You can still create a project and then create a bucket under it in the project console. COS will automatically double-write the project affiliation of a bucket during bucket creation to the tag service, so that the affiliation can be displayed in the console.

>
> - If you need to manage buckets in a categorized manner, you are recommended to directly use tags instead of projects to implement tasks such as permission control and bill splitting. For more information on how to add tags in the console, please see [Setting Bucket Tags](https://intl.cloud.tencent.com/document/product/436/30928).
> - For more information on the tag service, please see [Tag](https://intl.cloud.tencent.com/document/product/651).

## Granting a Sub-account Access to a Project

You can grant a sub-account access to a project by following the steps below:

1. Log in to the [project console](https://console.cloud.tencent.com/project), create a project, name it, and submit it. Then, create a resource such as a bucket or CVM instance under it. If you already have a project with storage or computing resources, you can skip this step.
2. After you create a project and bind a resource to it, enter the [Policy Management](https://console.cloud.tencent.com/cam/policy) page and click **Create Custom Policy** > **Authorize by Tag**. You can select the tag authentication method. Then, select the corresponding project tag and grant the sub-account access to all resources under it.
   ![](https://main.qcloudimg.com/raw/ab3400287f8e6509382d95842b0b840d.png)
3. The default policy is to grant the sub-account access to all resources under the project tag. If you want the sub-account to perform only specified operations on certain resources under the tag, you can change the `action` (for specifying operations) and `resource` (for specifying resources) in the policy syntax as instructed in [Syntax Structure](https://intl.cloud.tencent.com/document/product/598/10604) and click **Complete**.
![](https://main.qcloudimg.com/raw/434821bcb0169d9bcd64da5a2c816646.png)
4. If you want the sub-account to be able to create buckets, you also need to grant it the `PUT Bucket` permission. On the [Policy Management](https://console.cloud.tencent.com/cam/policy) page, click **Create Custom Policy** > **Create by Policy Generator** and grant the sub-account the corresponding permission.
![](https://main.qcloudimg.com/raw/4f2b3beb3bad2085fa1480ea9137b62d.png)
