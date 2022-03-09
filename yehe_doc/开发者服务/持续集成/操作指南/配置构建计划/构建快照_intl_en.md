---
title: Build Snapshots - CODING Help Center
pageTitle: Build Snapshots
pagePrevTitle: Environment Variables
pagePrev: ci/configuration/env.html
pageNextTitle: Cache Directory
pageNext: ci/configuration/cache.html
alias: 
- devops/ci/snapshot.html
- ci/snapshot.html
---

### [Function overview](#intro)

You may use different configuration files or build parameters for each build task in Continuous Integration. CODING Continuous Integration (CODING-CI) features build snapshots to allow you to review the execution process of a build task. Build snapshots clearly show the configuration parameters of every build record.

### [View build configuration](#view)

1. In a project, click "Continuous Integration" > "Build Plans". Select the title of a build plan to view all build records of the plan. Click a record to open it:

![](https://qcloudimg.tencent-cloud.cn/raw/1013edd241d6b0734d64bf5d1d0e4c35.png)

2. In a build record, you can click "Build Snapshot" to view the configuration snapshots of the build record—the startup parameters, environment variables, and process configuration file.

![](https://qcloudimg.tencent-cloud.cn/raw/0b41b49a9abb4d2943723d72a8ee35ff.png)

#### [Startup parameters](#start-variable)

The startup parameters are the parameters that you entered when starting a build task. They are incorporated into the run environment of the build task as environment variables.

![](https://qcloudimg.tencent-cloud.cn/raw/f8643d78c771d2867bec2260d56b4f5f.png)

After the build is completed, you can view the configured startup parameters in "Build Snapshot".

![](https://qcloudimg.tencent-cloud.cn/raw/af3afa4d46565ea0b5d425f081170135.png)

#### [Environment variables](#env-variable)

The environment variables only include those you configured when starting the task, and exclude all environment variables generated or dynamically set in the run process.

![](https://qcloudimg.tencent-cloud.cn/raw/1471a4a122f431ac87b791c290c7cf1b.png)

Select "Environment Variables" to view the environment variables set by the system and user for the build task when the task was started.

![](https://qcloudimg.tencent-cloud.cn/raw/d93c195a4739db963d1036b74c54df02.png)

#### [Process configuration file](#jenkinsfile)

Select the tab for the process configuration to view the configuration file (Jenkinsfile) used for the build record.

![](https://qcloudimg.tencent-cloud.cn/raw/95e7942bfcbeebc14e3e7cbd4dc5f3f5.png)

==== 2020/08/13 ====
