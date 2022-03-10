---
title: 错误信号 - CODING 帮助中心
pageTitle: 错误信号
pagePrevTitle: 将镜像更新至 K8s 集群
pagePrev: ci/plugins/html-report.html
pageNextTitle: 推送到 CODING Docker 制品仓库
pageNext: ci/plugins/cci-push-docker.html
alias: devops/ci/plugins/api-doc.html
---

持续集成的「错误信号」步骤可以理解为构建的终止符，运行至此步骤后将停止余下步骤，直接中断构建过程。

![](https://qcloudimg.tencent-cloud.cn/raw/2ed70d3a927cc662ce4eedbdbc6ecc88.png)

在持续集成中添加「捕获错误子步骤」，能够将运行结果作为是否中断持续集成任务的信号。若成功运行，则继续执行余下步骤；即使失败也将执行余下步骤，但构建任务会被判断为失败。

![](https://qcloudimg.tencent-cloud.cn/raw/2b60bd310995968219e246bb54a8fbbc.png)

==== 2021/06/30 ====
