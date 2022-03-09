---
title: Docker - CODING 帮助中心
pageTitle: Docker
pagePrevTitle: 构建 Composer 制品
pagePrev: ci/artifacts/composer.html
pageNextTitle: 构建文件类型制品
pageNext: ci/artifacts/generic.html
alias: 
-   devops/ci/artifacts/docker.html
-   ci/artifacts/docker.html
---

### 功能介绍

本文将给出如何使用持续集成任务构建 Docker 镜像的示例 Jenkinsfile。构建完成后可以使用预置插件便捷的上传至 CODING 制品仓库中。在使用该功能之前，请确保您对 Docker 类型制品库有[初步了解](/docs/artifacts/quick-start/docker.html)。

### Jenkinsfile

```groovy
pipeline {
  agent any
  stages {
    stage('检出') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: env.GIT_BUILD_REF]],
          userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]
        ])
      }
    }
    stage('构建 Docker 镜像') {
      steps {
        script {
          ARTIFACT_VERSION = "1.2.0"
          // 注意：创建项目时链接标识不要使用下划线，而是连字符，比如 My Project 的标识应为 my-project
          // 请修改 build/my-api 为你的制品库名称和镜像名称
          CODING_DOCKER_IMAGE_NAME = "${env.PROJECT_NAME.toLowerCase()}/build/my-api"
          // 本项目内的制品库已内置环境变量 CODING_ARTIFACTS_CREDENTIALS_ID，无需手动设置
          docker.withRegistry("https://${env.CCI_CURRENT_TEAM}-docker.pkg.coding.net", "${env.CODING_ARTIFACTS_CREDENTIALS_ID}") {
            docker.build("${CODING_DOCKER_IMAGE_NAME}:${ARTIFACT_VERSION}").push()
          }
        }
      }
    }
  }
}
```

### 常见问题

1.  如何自动生成版本号？

请阅读：[自动生成版本号](/docs/ci/artifacts/version.html)
