---
title: Go - CODING Help Center
pageTitle: Go
pagePrevTitle: Continuous Build System for WeChat Mini Programs Based on CI
pagePrev: ci/practice/quick/wechat-mini-program.html
pageNextTitle: Install Maven Dependency
pageNext: ci/depend/maven.html
alias: ci/depend/go.html
---

The go command directly uses "Code Repositories" to store dependencies. Run the `go get` command to call the `git clone` command, which will pull code. If you are using a private package, you will need to configure the username and password of the private code repository.

### [Import code repository password](#vcs-password)

In "Project Settings" > "Developer Options", import the username and password. Invoke them by using environment variables to avoid exposing sensitive information in the build plan.

![](https://qcloudimg.tencent-cloud.cn/raw/633ced86200765e4a5c0ed8930193c31.png)

### [Using environment variables](#Jenkins)

Enter the username and password in the CI environment variables:

![](https://qcloudimg.tencent-cloud.cn/raw/59ee48d873ed2da46c10d2be5979b6d1.png)

Configure the git URL in the text editor and fill in the environment variables:

```shell
pipeline {
  agent any
  stages {
    stage('Check out') {
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
      stage('Install dependency') {
        steps {
          sh 'git config --global url."https://${GO_GET_USER}:${GO_GET_PASSWORD}@e.coding.net/codes-farm/go-demo/".insteadOf "https://e.coding.net/codes-farm/go-demo/"'
          sh 'go get e.coding.net/codes-farm/go-demo/labstack-echo'
        }
      }
    }
  }
```

After you configure the dependency installation in the initial stage, running Continuous Integration will automatically pull code.

==== 2021/03/24 ====
