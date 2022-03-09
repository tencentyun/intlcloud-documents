---
title: 构建快照 - CODING 帮助中心
pageTitle: 构建快照
pagePrevTitle: 环境变量
pagePrev: ci/configuration/env.html
pageNextTitle: 缓存目录
pageNext: ci/configuration/cache.html
alias: 
-   devops/ci/snapshot.html
-   ci/snapshot.html
---

### [功能介绍](#intro)

您在持续集成的每一个构建任务，都有可能使用到不同的配置文件或构建参数，为了方便您回顾构建任务的执行过程，CODING 持续集成提供了构建任务的构建快照查看功能。构建快照功能让您能清晰地了解到每次构建记录的配置参数。

### [查看构建配置](#view)

1.  在项目中点击【持续集成】->【构建计划】，点击单次构建计划的标题即可查看该计划的所有构建记录，点击进入任一一条构建记录：

![](https://qcloudimg.tencent-cloud.cn/raw/1013edd241d6b0734d64bf5d1d0e4c35.png)

2.  在构建记录中，点击【构建快照】就可以看到每次构建记录的配置快照：启动参数、环境变量、流程配置文件。

![](https://qcloudimg.tencent-cloud.cn/raw/0b41b49a9abb4d2943723d72a8ee35ff.png)

#### [启动参数](#start-variable)

启动参数是您在启动构建任务时，输入的参数内容，会以环境变量的形式注入到构建任务的运行环境中。

![](https://qcloudimg.tencent-cloud.cn/raw/f8643d78c771d2867bec2260d56b4f5f.png)

在构建完成后，您可以在构建快照中看到配置的启动参数。

![](https://qcloudimg.tencent-cloud.cn/raw/af3afa4d46565ea0b5d425f081170135.png)

#### [环境变量](#env-variable)

这里仅包含启动任务时配置的环境变量，不包含所有在运行过程中产生或者动态设置的环境变量。

![](https://qcloudimg.tencent-cloud.cn/raw/1471a4a122f431ac87b791c290c7cf1b.png)

在环境变量选项卡内，用户可以参看到任务启动时，系统和用户为构建任务设置的环境变量。

![](https://qcloudimg.tencent-cloud.cn/raw/d93c195a4739db963d1036b74c54df02.png)

#### [流程配置文件](#jenkinsfile)

通过流程配置选项卡，您可以看到此次构建记录使用的配置文件（Jenkinsfile）。

![](https://qcloudimg.tencent-cloud.cn/raw/95e7942bfcbeebc14e3e7cbd4dc5f3f5.png)

==== 2020/08/13 ====
