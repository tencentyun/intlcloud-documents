---
title: Build Plan Templates - CODING Help Center
pageTitle: Build Plan Templates
pagePrevTitle: Group Management
pagePrev: ci/manage/group.html
pageNextTitle: Upload Generic Artifacts
pageNext: ci/plugins/generic.html
alias: 
- ci/node/overview.html
- ci/team-template.html
---

### [Function Overview](#intro)

In CODING Continuous Integration (CODING-CI), you can create unified **build plan templates**. Members in a team can reuse configured standard templates across projects to configure build processes more efficiently and centrally manage universal build plans.

### [New build plan template](#new)

Click the gear icon <img src ="https://help-assets.codehub.cn/enterprise/20210928153255.png" style ="margin:0"> in the upper-right corner of your team homepage to go to the team settings. Select "Feature Settings" > "Build Plan Templates" to create a new build template.

![](https://qcloudimg.tencent-cloud.cn/raw/cdb2aa9960ca23fd3be79a16805c8157.png)

### [Edit build plan template](#edit)

In a template, you can edit the process configuration, basic configurations, trigger rules, and variables and caches.

#### [Process configuration](#process)

Use the "Graphical Editor" or "Text Editor" to compose the execution process of the build template. The graphical editor allows you to view while writing a build process. You can add and delete steps in the graphical editor and convert the result to text. However, steps composed in the text editor may not be fully converted to graphics.

![](https://qcloudimg.tencent-cloud.cn/raw/0c3bb006a4c2a797d1f3bcb8274c5c2a.png)

#### [Basic configurations](#basic)

In "Basic Configurations", you can change the template name and icon. From the "Actions" dropdown menu on the right, you can select "Delete Template" or [Sync Template](#sync).

![](https://qcloudimg.tencent-cloud.cn/raw/bd43b35f8a4c44e89038fee4327fe14d.png)

If a template is updated, the creator of the template can click [Sync Template](#sync) to sync the updates to all build plans created from the template. Selecting "Sync Template" will overwrite the configurations in the related build plans. Refer to the [sample scenarios](#sync).

#### [Trigger rules](#trigger)

You can configure code source trigger, scheduled trigger, or manual trigger rules. The settings are the same as those of normal build plans. For more information, see [Trigger Rules](https://intl.cloud.tencent.com/document/product/1135/45430).

#### [Variables and caches](#variable)

You can add environment variables to a build plan. If you manually enable a build task, the environment variables will be used as the default values for startup parameters. For more information, see [Environment Variables](https://intl.cloud.tencent.com/zh/document/product/1135/45431).

### [Use build plan template](#using)

After a build template is created, members of the team can use the build plan template in any project.

![](https://qcloudimg.tencent-cloud.cn/raw/f80296b00fccf0f0b7c1dc947158fbf3.png)

"Template" will be shown in the upper-left corner of such a build plan. You can select the code source as required for a project.

![](https://qcloudimg.tencent-cloud.cn/raw/ad7c4bfb3e4cd2d142d9c1f3f0d6e429.png)

After you create the build plan, the build plan process, trigger configurations, environment variables, and default values are the same as the template, you can modify them according to the project. These modifications will not apply to the template. To modify the template, from your team settings, select "Feature Settings" > "Build Plan Templates".

### [Sync build plan template](#sync)

After a build plan template is modified, the creator of a template can sync the updates to all build plans created from the template.

**Sample scenario**: Team A implements continuous integration build specifications. Most build plans are created from a standard build plan template. After some time, the previous specifications need to be updated and the template creator simply needs to modify the build plan template and sync the updates to all build plans created from the template.

![](https://qcloudimg.tencent-cloud.cn/raw/bb3f08a7ac75fb25946485fd4b455176.png)

Syncing updates will not overwrite all contents in build plans. See the figure below for an example of "changes" that would be applied.

![](https://qcloudimg.tencent-cloud.cn/raw/8f044ebaf0f69fceca8a410bbfed01d2.png)

> ⚠️ Make sure you have known the effect before you perform the sync operation.

==== 2020/11/27 ====
