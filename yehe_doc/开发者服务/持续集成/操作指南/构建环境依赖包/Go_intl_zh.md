---
title: Go - CODING 帮助中心
pageTitle: Go
pagePrevTitle: 基于 CI 实现微信小程序的持续构建
pagePrev: ci/practice/quick/wechat-mini-program.html
pageNextTitle: 安装 Maven 依赖包
pageNext: ci/depend/maven.html
alias: ci/depend/go.html
---

Go 命令直接使用「代码仓库」存放依赖包，执行 `go get` 命令时会调用 `git clone` 命令拉取代码。如果使用私有包，则需配置私有代码库的用户名/密码。

### [导入代码仓库密码](#vcs-password)

在「项目设置」→「开发者选项」中导入用户名/密码，通过环境变量的方式调取能够防止敏感信息暴露在构建计划中。

![](https://qcloudimg.tencent-cloud.cn/raw/633ced86200765e4a5c0ed8930193c31.png)

### [使用环境变量](#Jenkins)

把用户名/密码填入持续集成的环境变量：

![](https://qcloudimg.tencent-cloud.cn/raw/59ee48d873ed2da46c10d2be5979b6d1.png)

在文本编辑器中中配置 git url，将环境变量填入其中：

```shell
pipeline {
  agent any
  stages {
    stage('检出') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: GIT_BUILD_REF]],
          userRemoteConfigs: [[
            url: GIT_REPO_URL,
            credentialsId: CREDENTIALS_ID
          ]]])
        }
      }
      stage('安装依赖') {
        steps {
          sh 'git config --global url."https://${GO_GET_USER}:${GO_GET_PASSWORD}@e.coding.net/codes-farm/go-demo/".insteadOf "https://e.coding.net/codes-farm/go-demo/"'
          sh 'go get e.coding.net/codes-farm/go-demo/labstack-echo'
        }
      }
    }
  }
```

在起始阶段配置依赖安装环节后，运行持续集成将自动进行代码拉取。

==== 2021/03/24 ====
