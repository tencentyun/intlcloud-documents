---
title: Error - CODING Help Center
pageTitle: Error
pagePrevTitle: Update Images in K8s Clusters
pagePrev: ci/plugins/html-report.html
pageNextTitle: Push to CODING Docker Artifact Repository
pageNext: ci/plugins/cci-push-docker.html
alias: devops/ci/plugins/api-doc.html
---

In a sense, the "errorl" in Continuous Integration is a terminator to stop the remaining steps and suspend the build process.

![](https://qcloudimg.tencent-cloud.cn/raw/2ed70d3a927cc662ce4eedbdbc6ecc88.png)

In Continuous Integration, add "Catch incorrect substep". The result will serve as a signal for whether to suspend the continuous integration task. If the result is successful, the remaining steps are run. Even if the result fails, the remaining steps are still run, but the build task is deemed to have failed.

![](https://qcloudimg.tencent-cloud.cn/raw/2b60bd310995968219e246bb54a8fbbc.png)

==== 2021/06/30 ====
