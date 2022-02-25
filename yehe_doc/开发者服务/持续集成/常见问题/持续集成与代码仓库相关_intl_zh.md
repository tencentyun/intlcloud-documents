[](id:push)
### 如何在持续集成中推送代码？

在某些场景下，您可能需要在持续集成阶段推送代码。CODING 的持续集成内置了 Git、SVN 等命令工具，您可以参考如下示例。

```groovy
pipeline {
  agent any
  stages {
    stage('检出') {
      steps {
        checkout([
            $class: 'GitSCM', 
            branches: [[name: env.GIT_BUILD_REF]], 
            userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]])
      }
    }
    stage('修改') {
        steps {
            sh "echo '# Hello CODING' > README.md"
            sh "git add ."
            sh "git commit -m 'add README.md' "

        }
    }
    stage('推送') {
        steps {
            // 使用了 CODING 持续集成系统预置的项目令牌环境变量 PROJECT_TOKEN_GK 和 PROJECT_TOKEN 来推送
            // 若希望推送到非本项目或第三方平台的代码仓库，需要自行换成有效的凭据信息
            sh "git push https://${PROJECT_TOKEN_GK}:${PROJECT_TOKEN}
              @e.coding.net/myteam/myrepo.git HEAD:master"
        }
    }
  }
}
```

[](id:svn)
### 如何调用 SVN 仓库？

在默认的持续集成计划的配置过程中，所运行的代码源默认是 Git 类型仓库。若希望使用 SVN 仓库 运行持续集成，下文给出了指引。

#### 前提条件
在开始之前，请先创建项目令牌与申请用户名+密码凭据。

#### 步骤1：创建项目令牌
1. 前往**项目设置** > **开发者选项** > **项目令牌**页面，单击**新建项目令牌**。设置过期时间后并勾选持续集成所有的权限。
![](https://qcloudimg.tencent-cloud.cn/raw/15f5b33ffdffc68786acfcb8ab35c254.png)
2. 创建完成后会给出用户名及密码。
![](https://qcloudimg.tencent-cloud.cn/raw/95f8baf22dd161d8d84acbcbc53782fd.png)

#### 步骤2：申请用户名和密码凭据
前往**项目设置** > **开发者选项** > **凭据管理**页面，单击**录入凭据**录入用户名和密码凭据。用户名和密码需要填写在创建项目令牌时给出的用户名及密码。
![](https://qcloudimg.tencent-cloud.cn/raw/faecc391d2d211dffa73ff85d1bef136.png)
创建完成后会给出凭据 ID，稍后需要将此 ID 录入至构建计划的流程配置中。

#### 步骤3：配置构建计划

1. 在**持续集成** > **构建计划**中单击**新建构建计划配置**，进入**选择构建计划模板** > **基础**页面，选择基础栏中的**空白模板**，这样可以自定义流程配置。
![](https://qcloudimg.tencent-cloud.cn/raw/44ad89ae71d2b39f55603c7fa0ac8c71.png)
2. 命名构建计划后，代码源选择**不使用**。
![](https://qcloudimg.tencent-cloud.cn/raw/0ed0c5885a0b96b69909e9443f7dd202.png)
3. 完成后在流程配置中填写相应的配置。
<dx-codeblock>
:::  groovy
pipeline {
    agent any
    stages {
    stage('检出 SVN 代码') {
      steps {
        checkout([$class: 'SubversionSCM',
                  // 此处可以添加额外认证
                  additionalCredentials: [],
                  excludedCommitMessages: '',
                  excludedRegions: '',
                  excludedRevprop: '',
                  excludedUsers: '',
                  filterChangelog: false,
                  ignoreDirPropChanges: false,
                  includedRegions: '',
                  locations: [[
                               // 输入上文中创建的凭据 ID
                               credentialsId: '5e25f6a9-675c-4b38-97b0-e907b5fe27cd',
                               // 检出代码时所取出代码的范围
                               depthOption: 'infinity',
                               // 是否将 SVN 上的外部引用一并检出
                               ignoreExternalsOption: true,
                               // SVN 的检出目录，此目录是该 Job 工作目录的相对路径
                               local: '.',
                               // SVN 代码仓库地址
                               remote: "svn://subversion.e.coding.net/StrayBirds/svn"]],
                  workspaceUpdater: [$class: 'UpdateUpdater']])
      }
    }
    }
}
:::
</dx-codeblock>

#### 步骤4：添加环境变量

在变量与缓存中添加环境变量，类别选择 CODING 凭据里的用户名 + 密码。
![](https://qcloudimg.tencent-cloud.cn/raw/3d14e719305c28d3bdb84afc19cf7ba5.png)

#### 步骤5：触发构建

您可以选择手动构建或配置触发方式进行自动构建，构建成功后如图所示。
![](https://qcloudimg.tencent-cloud.cn/raw/4debfde7e67ec3b1bd6736ecd40ba882.png)

[](id:mult-repo)
### 如何拉取多仓库？

1.  创建代码仓库项目令牌
在**项目设置** > **开发者选项** > **项目令牌**中，单击**新建项目令牌**，并勾选**读取**代码仓库权限。因涉及到两个仓库，需在代码仓库权限选择**统一配置所有代码仓库权限**，创建完成后获取用户名与密码。
![](https://qcloudimg.tencent-cloud.cn/raw/5db0d6f99280f8172e4c81e5746873ed.png)
2.  在持续集成配置中选择不使用代码源。
![](https://qcloudimg.tencent-cloud.cn/raw/75af7630e731e79030f95d14a061e923.png)
3.  编写 Jenkinsfile 配置文件，填写需拉取的代码仓库地址。
<dx-codeblock>
:::  groovy
pipeline {
    agent any
    stages {
    stage('检出1') {
      steps {
        sh 'git clone "https://${GIT_USER}:${GIT_PASSWORD}@e.coding.net/codes-farm/laravel-demo.git"'
        sh 'ls -la'
      }
    }
    stage('检出2') {
      steps {
        sh 'git clone "https://${GIT_USER}:${GIT_PASSWORD}@e.coding.net/codes-farm/laravel-demo/config.git"'
        sh 'ls -la'
      }
    }
    }
}
:::
</dx-codeblock>
4.  将第一步申请的项目令牌的用户名与密码添加至持续集成的环境变量中。
![](https://qcloudimg.tencent-cloud.cn/raw/e140093eef8545cbcc9004bfcb6e8e46.png)

[](id:git-submodule)
### 如何检出 Git Submodule 代码？

在持续集成构建计划中，若要将子仓库代码作为代码源，需通过流程配置检出 Git Submodule 子仓库代码。

在配置持续集成流程前，请先将子仓库添加至父仓库中。使用 `git submodule add` 命令添加拟跟踪项目的仓库地址作为子仓库，

```shell
git submodule add https://e.coding.net/test/git-sub-module.git
```

代码提交成功后，在父仓库页将看到此图标：
![](https://qcloudimg.tencent-cloud.cn/raw/63797d77925e8025e30efeeae1ca548a.png)

#### 步骤1：录入仓库访问凭据
通常情况下，子仓库的访问凭据与父仓库的凭据有差异，也为了避免在持续集成配置中暴露敏感信息，可以先行将父子仓库的访问凭据都录入至项目设置中。

1. 进入**项目设置** > **开发者选项** > **凭据管理**页面，单击**录入凭据**，在**凭据类型**选择**用户名 + 密码**或 **SSH 私钥**并在**凭据授权**下勾选**授权所有持续集成构建计划**。
![](https://qcloudimg.tencent-cloud.cn/raw/2474ec8d7c9acb51670b334b47bd1079.png)
2. 录入完成后获取两者的凭据 ID。
![](https://qcloudimg.tencent-cloud.cn/raw/74f56ec802addac826b768e4787fa145.png)

#### 步骤2：配置持续集成流程

参考使用以下 Jenkinsfile 配置：
<dx-codeblock>
:::  groovy
pipeline {
    agent any
        stages {
            stage('检出') {
              steps {
                checkout([
                $class: 'GitSCM',
                 branches: [[name: GIT_BUILD_REF]],
                  doGenerateSubmoduleConfigurations: false,
                  // 此处配置 Submodule 的检出规则
                  extensions: [[
                  $class: 'SubmoduleOption',
                   // 是否禁用检出 Submodule
                  disableSubmodules: false,
                  // 是否允许检出时使用 Parent Project 的用户凭据
                  parentCredentials: false,
                  // 是否递归检出所有 Submodule 的更新
                  recursiveSubmodules: true,
                  // 指定参考仓库的路径
                  reference: '',
                  // 是否追踪 .gitmodules 文件中配置的分支的最新提交
                  trackingSubmodules: false
                  ]],
                  submoduleCfg: [
                  ],
                  // 此处配置远程 Parent Project 和 Submodules的检出信息
                  userRemoteConfigs: [
                  [
                  // 此处配置远程 Parent Project 仓库 SSH 凭据和仓库地址
                  credentialsId: '93207d20-****-****-****-410850900d86',
                  url: 'https://e.coding.net/StrayBirds/Parent/parent.git'
                  ],
                  // 此处配置远程 Submodule 仓库凭 SSH 凭据和仓库地址
                  [
                  credentialsId: '560bdc1e-****-****-****-c8e3ccb3ccc6',
                  url: 'https://e.coding.net/StrayBirds/Submodule/sub.git'
                  ],
                  // 如果有更多的 Submodules ，可以在这里增加配置
                  ]
                  ])
              }
          }
      }
  }
:::
</dx-codeblock>

运行成功后的日志如下：
![](https://qcloudimg.tencent-cloud.cn/raw/af71fb714644a655c775457881689cfc.png)

[](id:checkout)
### 如何检出其它项目的代码仓库？

在持续集成中，您可以通过项目令牌的方式检出其它项目内的 CODING 仓库代码。

为了方便您区分即将要操作的两个不同项目，我们统一将：

-   需要被检出的代码仓库所在项目称为 “项目 A” 
-   执行检出持续集成任务所在的项目称为 “项目 B” 

#### 步骤1：在项目 A 内创建项目令牌

1.  进入项目 A **项目设置** > **开发者选项** > **项目令牌**页面，单击**新建项目令牌** 。
![](https://qcloudimg.tencent-cloud.cn/raw/f2b5e9469fc2375658ab95e06a3cf1a9.png)
2.  选择需要检出的代码仓库，按需求配置操作权限。
![](https://qcloudimg.tencent-cloud.cn/raw/8fc94b33e1b91d172bd3c7409df6be4e.png)
3.  单击**确定**后创建成功。

#### 步骤2：在项目 B 创建凭据[](id:step2)

1.  进入项目 B 进入**项目设置** > **开发者选项** > **凭据管理**页面，单击**录入凭据**。
![](https://qcloudimg.tencent-cloud.cn/raw/f2b5e9469fc2375658ab95e06a3cf1a9.png)
2.  回到之前创建好的项目 A 项目令牌页面，单击**查看密码**。
![](https://qcloudimg.tencent-cloud.cn/raw/2e2a1ac3996d04931d7ae5728b7119b2.png)
3.  在项目 B 的**录入凭据**窗口**凭据类型**选择**用户名 + 密码**，粘贴项目令牌对应信息。
![](https://qcloudimg.tencent-cloud.cn/raw/2cabd65470900b5f6970092c06dc3ff8.png)
4.  勾选授权的持续集成项目，单击**保存**。
![](https://qcloudimg.tencent-cloud.cn/raw/0733ac6d51d34859a0c54f8345a27692.png)

#### 步骤3：在项目 B 持续集成任务中配置对应的环境变量

1.  进入持续集成设置 > **流程配置**，添加**从代码仓库检出**步骤，单击**环境变量**。
![](https://qcloudimg.tencent-cloud.cn/raw/1c311af0420f7b522c4355a259b3f039.png)
也可以在添加检出流程之后，进入持续集成设置 > **变量与缓存**中单击**添加环境变量**。
![](https://qcloudimg.tencent-cloud.cn/raw/d125416a8350370a5f042225dfda976e.png)

2.  分别添加以下两个环境变量： 
<table>
<tr>
<th>变量名</th>
<th>默认值</th>
</tr>
<tr>
<td>GIT_REPO_URL</td>
<td>需要检出的仓库克隆地址（HTTPS）</td>
</tr>
<tr>
<td>CREDENTIALS_ID</td>
<td>在 <a href = "#step2">步骤2</a> 录入的凭据 ID</td>
</tr>
</table>
<ul><li>GIT_REPO_URL</li>
<img src = "https://qcloudimg.tencent-cloud.cn/raw/81be69a1baf0f9fe404c87ad125fc10c.png" style="width: 100%">
<li>CREDENTIALS_ID</li>
<img src = "https://qcloudimg.tencent-cloud.cn/raw/8bf73f2b050dfddc4d67d9748ec5022d.png" style="width: 100%">
</ul>

填好后的环境变量：
<img src = "https://qcloudimg.tencent-cloud.cn/raw/726d34013ec5cab13f4373ef6f9091e7.png" style="width: 100%">
</ul>

#### 步骤4：开始构建任务，成功检出代码
![](https://qcloudimg.tencent-cloud.cn/raw/a0b29d81fc914b2ac6a5115fda2e8031.png)

[](id:git-lfs)
### 如何检出使用 Git LFS 的仓库

在持续集成中用户可以通过流程配置检出使用 Git LFS (Large File Storage) 插件管理的代码仓库，实现带有大文件的 Git 仓库持续集成。

#### Git LFS 简介

Git LFS 插件加速了带有频繁变动的大文件（例如图片、视频等）的 `git clone` 和 `git fetch` 操作。

每当您在仓库中添加了大文件时，Git LFS 插件会将它储存在本地的 Git LFS cache 中，同时将代码仓库中的大文件内容代替为指向缓存地址的引用。当您提交代码时，本次提交所涵盖的所有大文件会被提交到远程 Git LFS cache 中，该缓存和您的远程仓库相关联。当您检出带有大文件引用的提交时，插件会将其替换为缓存中的文件实际内容。

因此，通过 Git LFS 插件的管理，大文件只会在 `git checkout` 的时候被加载。

#### 如何在构建计划中检出代码？

在 **构建计划设置** > **流程配置**页面，单击**从代码仓库检出**添加步骤，添加 Git-LFS-Pull 插件。
![](https://qcloudimg.tencent-cloud.cn/raw/7fa4d3d7d676fc99dded617c99bbb7a6.png)

#### Jenkinsfile
<dx-codeblock>
:::  groovy
pipeline {
  agent any
  stages {
    stage('检出') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: env.GIT_BUILD_REF]],
          extensions: [
            // 添加 GitLFSPull 插件
            [$class: 'GitLFSPull'],
          ],
          userRemoteConfigs: [[
            url: env.GIT_REPO_URL,
            credentialsId: env.CREDENTIALS_ID
          ]]
        ])
      }
    }
  }
}
:::
</dx-codeblock>

[](id:gongfeng)
### 关联的工蜂仓库无法同步至外部仓库列表

目前需在工蜂授权时选择**当前帐号**的授权范围才能成功同步到外部仓库列表，并在持续集成构建任务重被检出，如果您选择的授权范围是**项目组**或**项目**，则无法成功同步。
![](https://qcloudimg.tencent-cloud.cn/raw/c3ccbb676cc103c8d7d8389a0038c9c1.png)
