---
title: Trigger Rules - CODING Help Center
pageTitle: Trigger Rules
pagePrevTitle: Graphical Editor
pagePrev: ci/process/visual-editor.html
pageNextTitle: Environment Variables
pageNext: ci/configuration/env.html
alias: 
- devops/ci/trigger.html
- ci/trigger.html
---

### [Function Overview](#intro)

In the process of configuring a continuous integration (CI) plan, you can set trigger rules as necessary for running the build plan. These include the run frequency and trigger conditions of the build plan. The following trigger methods can be used in every CI build plan.

- Manual trigger
- Triggered by code changes
- Scheduled trigger
- API trigger

You can combine these methods.

### [Manual trigger](#manually)

You can manually trigger a build plan by entering the build parameters, which will be added to the build environment in the form of environment variables.

On the build plans page, select "Build Now". In the pop-up window, select the build targets (tag, branch, or revision number), enter the required build parameters to complete the trigger build.

![](https://qcloudimg.tencent-cloud.cn/raw/c5169da46d16ca854a27c3b32bca1480.png)

### [Triggered by code changes](#code-changed)

For a build plan configured to be triggered by code changes, the code repository selected for the build plan will be monitored to trigger the build plan according to its changes.

![](https://qcloudimg.tencent-cloud.cn/raw/f33a34c343460ba7192ad51f7c2e5526.png)

#### [Code updates](#push)

- Trigger build when pushing to <branch>

    A build is triggered only when the code of the specified branch is updated.

- Trigger build when pushing a new tag

    A build is triggered only when a new Git tag is created.

- Trigger build when pushing to a branch

    A build is triggered when the code of any branch is updated.

- Build when branch or tag rules met

    Supports matches of regular expressions:

    1. If you want to trigger a build when the code of a master branch is updated, "refs/heads/master" and "master" both match the condition.

    2. If you want to trigger a build only when a master or dev branch is updated, use the following: ^refs/heads/(master|dev).

#### [Merge requests](#merge-request)

A merge request triggers a build in the following circumstances:

- When a merge request is initiated
- A change has occurred in the source branch of a merge request
- A change has occurred in the target branch of a merge request
- When a merge request is merged

> When a build is **triggered by a merge request**, the **result after the source branch and target branch is merged** is built, so integration errors can be identified at the earliest. This is not possible when a build is **triggered by code updates**.

![](https://qcloudimg.tencent-cloud.cn/raw/e973a7922ae15305bffa25621ea50ece.png)

#### [Automatically cancel identical builds](#auto-cancel)

In the settings, you can select "Automatically cancel identical version numbers" and "Automatically cancel identical merge requests" to cancel identical builds that are triggered (and only keep the latest one).

![](https://qcloudimg.tencent-cloud.cn/raw/99c6e09431782cdd9c136af0fca3bd94.png)

#### [Private GitLab](#gitlab)

In the case of [Bind Private GitLab](/docs/admin/service-integration/gitlab.html), GitLab Webhooks will be automatically created. Subsequently, CODING will be notified of events to match the above-set trigger rules. 

![](https://help-assets.codehub.cn/enterprise/20210818202005.png)

### [Scheduled trigger](#scheduled)

By configuring a scheduled trigger for a build plan, you can set the build plan to be triggered periodically or at specific times to generate build tasks.
You can add multiple scheduled triggers in no order of priority. If scheduled triggers overlap, multiple builds are triggered.

![](https://qcloudimg.tencent-cloud.cn/raw/ff1fdf393a49692edda087fc877f55a9.png)

- Trigger condition: Do not repeatedly trigger scheduled task if code is unchanged

    If the code of the selected branch has not changed since the last trigger, a build will not be triggered at the trigger time.

- Select Date

    You can select multiple days in a week.

- Repeatedly

    You can select a time range between 00:00 and 24:00 (accurate to the hour) to trigger tasks at the specified interval.

- Once

    You can select a trigger time between 00:00 and 24:00 (accurate to the minute).

### [API trigger](#api)

Before using this feature, select "Project Settings" > "Developer Options" > "Project Token" > "Create Token" to generate the token authorizing you to trigger the Continuous Integration API.

![](https://qcloudimg.tencent-cloud.cn/raw/19b634422035eebe34442aa9c2d41a5b.png)

With the token, you can call the API in a build plan. Select "Generate cURL command to test trigger" to generate the call command.

![](https://qcloudimg.tencent-cloud.cn/raw/efcacd80cec9a7c91b4b94336c6fd009.png)

#### [API](#api-detail)

When the project token calls the CODING Continuous Integration (CODING-CI) API, the authentication method is `Basic Auth`. See the API parameters below.

##### Trigger build task

```json
POST https://< TEAM_GK >.coding.net/api/cci/job/< JOB_ID >/trigger
```

##### Request body

```json
{
  "ref": "master",
  "envs": [
    {
      "name": "my-params-1",
      "value": "hello",
      "sensitive": 1
    },
    {
      "name": "my-params-2",
      "value": "world",
      "sensitive": 0
    }
  ]
}
```

##### Return body

```json
{
  "code": 0
}
```

##### Parameter descriptions

|  Parameter | Location  | Required?  | Type  | Default value  | Description
|---|---|---|---|---| ---
|  ref |  body |   No |   string | master  | Built target ref (`commit sha` / `tag` / `branch`), ignore if code repository isn't used in build plan
|  envs |  body |   No |   env[] | -    | Startup parameter of build plan

**envItem**

|  Parameter | Location  | Required?  | Type  | Default value  | Description
|---|---|---|---|---| ---
|  name |  envItem.name |   Yes |   string | master  | Name of startup parameter of build plan
|  value |  envItem.value |   No |   string | -    | Startup value of build plan
|  sensitive |  envItem.sensitive |   No |   number | 0  | Whether to keep startup parameters confidential and do not show startup parameters in log 1: confidential, 0: plaintext

==== 2021/08/24 ====
