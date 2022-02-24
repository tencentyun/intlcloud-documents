[](id:push)
### How do I push code during continuous integration?

In some scenarios, you may have to push code during continuous integration (CI). CODING Continuous Integration (CODING-CI) provides built-in command tools, including Git and SVN. You can refer to the example below.

```groovy
pipeline {
  agent any
  stages {
    stage('check out') {
      steps {
        checkout([
            $class: 'GitSCM', 
            branches: [[name: env.GIT_BUILD_REF]], 
            userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]])
      }
    }
    stage('modification') {
        steps {
            sh "echo '# Hello CODING' > README.md"
            sh "git add ."
            sh "git commit -m 'add README.md' "

        }
    }
    stage('push') {
        steps {
            // The CODING-CI system's preset project token environment variables PROJECT_TOKEN_GK and PROJECT_TOKEN are used to push
            // To push to the code repository of another project or a third-party platform, you must manually replace this with valid credential information
            sh "git push https://${PROJECT_TOKEN_GK}:${PROJECT_TOKEN}
              @e.coding.net/myteam/myrepo.git HEAD:master"
        }
    }
  }
}
```

[](id:svn)
### How do I call SVN repositories?

In the default CI plan configuration process, the code source is a Git repository by default. To use an SVN repository for continuous integration, follow the instructions below.

#### Prerequisites
Before starting, create a project token and apply for username + password credentials.

#### Step 1: Create project token
1. Go to **Project Settings** > **Developer Options** > **Project Token** and click **Create Project Token*. Set the expiration date and select all CI permissions.
![](https://qcloudimg.tencent-cloud.cn/raw/15f5b33ffdffc68786acfcb8ab35c254.png)
2. Once the token is created, you will receive a username and password.
![](https://qcloudimg.tencent-cloud.cn/raw/95f8baf22dd161d8d84acbcbc53782fd.png)

#### Step 2: Apply for username and password credentials
Go to **Project Settings** > **Developer Options** > **Credential Management**, click **Enter Credential**, and enter your username and password. You must enter the username and password generated upon project token creation.
![](https://qcloudimg.tencent-cloud.cn/raw/faecc391d2d211dffa73ff85d1bef136.png)
After your credentials are created, you will receive a credential ID. Later, you must input this ID in the build plan process configuration.

#### Step 3: Configure build plan

1. Go to **Continuous Integration** > **Build Plans**, click **New Build Plan Configuration**, and go to **Select Build Plan Template** > **Basic**. On this page, select **Blank Template** in the Basic field. This allows you to customize the process configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/44ad89ae71d2b39f55603c7fa0ac8c71.png)
2. After naming the build plan, select **Not use** for the code source.
![](https://qcloudimg.tencent-cloud.cn/raw/0ed0c5885a0b96b69909e9443f7dd202.png)
3. Then, enter the relevant settings in the process configuration.
<dx-codeblock>
:::  groovy
pipeline {
    agent any
    stages {
    stage('check out SVN code') {
      steps {
        checkout([$class: 'SubversionSCM',
                  // You can add additional credentials here
                  additionalCredentials: [],
                  excludedCommitMessages: '',
                  excludedRegions: '',
                  excludedRevprop: '',
                  excludedUsers: '',
                  filterChangelog: false,
                  ignoreDirPropChanges: false,
                  includedRegions: '',
                  locations: [[
                               // Enter the credential ID created above
                               credentialsId: '5e25f6a9-675c-4b38-97b0-e907b5fe27cd',
                               // The range of code to check out
                               depthOption: 'infinity',
                               // Whether to check out SVN external references as well
                               ignoreExternalsOption: true,
                               // SVN checkout directory, which is a relative path of the job's work directory
                               local: '.',
                               // SVN code repository URL
                               remote: "svn://subversion.e.coding.net/StrayBirds/svn"]],
                  workspaceUpdater: [$class: 'UpdateUpdater']])
      }
    }
    }
}
:::
</dx-codeblock>

#### Step 4: Add environment variable

Add an environment variable in Variables and Caches. As the type, select Username + Password in CODING Credential.
![](https://qcloudimg.tencent-cloud.cn/raw/3d14e719305c28d3bdb84afc19cf7ba5.png)

#### Step 5: Trigger build

You can choose manual build or configure a trigger method for auto building. After a successful build, you will see the following:
![](https://qcloudimg.tencent-cloud.cn/raw/4debfde7e67ec3b1bd6736ecd40ba882.png)

[](id:mult-repo)
### How do I pull multiple repositories?

1.  Create a code repository project token
Go to **Project Settings** > **Developer Options** > **Project Token**, click **Create Project Token*, and select **Read** in Code Repository Permissions. As we need to read two code repositories, select **Configure all the code repository permissions** in Code Repository Permissions. When you create the token, you will receive a username and password.
![](https://qcloudimg.tencent-cloud.cn/raw/5db0d6f99280f8172e4c81e5746873ed.png)
2.  In the CI configuration, select **Not use** for the code source.
![](https://qcloudimg.tencent-cloud.cn/raw/75af7630e731e79030f95d14a061e923.png)
3.  Write a Jenkinsfile configuration file and enter the URLs of the code repositories to pull from.
<dx-codeblock>
:::  groovy
pipeline {
    agent any
    stages {
    stage('checkout 1') {
      steps {
        sh 'git clone "https://${GIT_USER}:${GIT_PASSWORD}@e.coding.net/codes-farm/laravel-demo.git"'
        sh 'ls -la'
      }
    }
    stage('checkout 2') {
      steps {
        sh 'git clone "https://${GIT_USER}:${GIT_PASSWORD}@e.coding.net/codes-farm/laravel-demo/config.git"'
        sh 'ls -la'
      }
    }
    }
}
:::
</dx-codeblock>
4.  Add the username and password generated when you applied for a project token in the CI environment variables.
![](https://qcloudimg.tencent-cloud.cn/raw/e140093eef8545cbcc9004bfcb6e8e46.png)

[](id:git-submodule)
### How do I check out Git submodule code?

To set a submodule of a repository as the code source in a CI build plan, you must use the process configuration to check out the Git submodule repository code.

Before configuring the CI process, add the sub-repository to the parent repository. Use the `git submodule add` command to add the repository URL of the project to be tracked as a sub-repository.

```shell
git submodule add https://e.coding.net/test/git-sub-module.git
```

After a successful code commit, you will see this icon on the parent repository page:
![](https://qcloudimg.tencent-cloud.cn/raw/63797d77925e8025e30efeeae1ca548a.png)

#### Step 1: Enter repository access credentials
Generally, the credentials for accessing a sub-repository are different from those of the parent repository. To avoid exposing sensitive information in CI configurations, you can enter the access credentials of the parent and sub-repositories in the project settings first.

1. Go to **Project Settings** > **Developer Options** > **Credential Management** and click **Enter Credential**. For the **Credential Type** select **Username + Password** or **SSH Private Key**. Under **Credential Authorization**, select **Authorize all the CI build plans**.
![](https://qcloudimg.tencent-cloud.cn/raw/2474ec8d7c9acb51670b334b47bd1079.png)
2. After entering the necessary information, you will receive two credential IDs.
![](https://qcloudimg.tencent-cloud.cn/raw/74f56ec802addac826b768e4787fa145.png)

#### Step 2: Configure CI process

Refer to the following Jenkinsfile configuration:
<dx-codeblock>
:::  groovy
pipeline {
    agent any
        stages {
            stage('check out') {
              steps {
                checkout([
                $class: 'GitSCM',
                 branches: [[name: GIT_BUILD_REF]],
                  doGenerateSubmoduleConfigurations: false,
                  // Configure submodule checkout rules here
                  extensions: [[
                  $class: 'SubmoduleOption',
                   // Whether to prohibit submodule checkout
                  disableSubmodules: false,
                  // Whether to allow the use of parent project user credentials for checkout
                  parentCredentials: false,
                  // Whether to recursively check out all submodule updates
                  recursiveSubmodules: true,
                  // Specify the reference repository path
                  reference: '',
                  // Whether to track the latest commits to the branch configured in the .gitmodules file
                  trackingSubmodules: false
                  ]],
                  submoduleCfg: [
                  ],
                  // Configure the remote parent project and submodule checkout information here
                  userRemoteConfigs: [
                  [
                  // Configure the remote parent project repository SSH credentials and URL here
                  credentialsId: '93207d20-****-****-****-410850900d86',
                  url: 'https://e.coding.net/StrayBirds/Parent/parent.git'
                  ],
                  // Configure the remote submodule repository SSH credentials and URL here
                  [
                  credentialsId: '560bdc1e-****-****-****-c8e3ccb3ccc6',
                  url: 'https://e.coding.net/StrayBirds/Submodule/sub.git'
                  ],
                  // If there are more submodules, add their configurations here
                  ]
                  ])
              }
          }
      }
  }
:::
</dx-codeblock>

After successful operation, the log will read as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/af71fb714644a655c775457881689cfc.png)

[](id:checkout)
### How do I check out code repositories from other projects?

During CI, you can use project tokens to check out code from CODING repositories in other projects.

In this example, we will use two different projects:

-   "Project A" is the project that contains the code repository that we will need to check out. 
-   "Project B" is the project that contains the CI checkout task. 

#### Step 1: Create project token in Project A

1. Open Project A, go to **Project Settings** > **Developer Options** > **Project Token**, and click **Create Project Token**.
![](https://qcloudimg.tencent-cloud.cn/raw/f2b5e9469fc2375658ab95e06a3cf1a9.png)
2.  Select the code repository for checkout and configure the necessary operation permissions.
![](https://qcloudimg.tencent-cloud.cn/raw/8fc94b33e1b91d172bd3c7409df6be4e.png)
3.  Click **OK** to create the token.

#### Step 2: Create credentials in Project B[](id:step2)

1. Open Project B, go to **Project Settings** > **Developer Options** > **Credential Management**, and click **Enter Credential**.
![](https://qcloudimg.tencent-cloud.cn/raw/f2b5e9469fc2375658ab95e06a3cf1a9.png)
2.  Go back to the page of the token created for Project A and click **View Password**.
![](https://qcloudimg.tencent-cloud.cn/raw/2e2a1ac3996d04931d7ae5728b7119b2.png)
3.  In the **Enter Credential** window for Project B, select **Username + Password** as the **Credential Type** and paste the corresponding project token information.
![](https://qcloudimg.tencent-cloud.cn/raw/2cabd65470900b5f6970092c06dc3ff8.png)
4.  Select the CI project to authorize and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/0733ac6d51d34859a0c54f8345a27692.png)

#### Step 3: Configure corresponding environment variables in CI task in Project B

1.  Go to CI Settings > **Process Configuration**, add a **Check out from code repository** step, and click **Environment Variable**.
![](https://qcloudimg.tencent-cloud.cn/raw/1c311af0420f7b522c4355a259b3f039.png)
After adding a checkout process, you can also go to CI Settings > **Variables and Caches** and click **Add Environment Variable**.
![](https://qcloudimg.tencent-cloud.cn/raw/d125416a8350370a5f042225dfda976e.png)

2.  Add the following two environment variables: 
<table>
<tr>
<th>Variable</th>
<th>Default Value</th>
</tr>
<tr>
<td>GIT_REPO_URL</td>
<td>Clone URL of the repository to be checked out (HTTPS)</td>
</tr>
<tr>
<td>CREDENTIALS_ID</td>
<td>The credential ID entered in <a href = "#step2">Step 2</a></td>
</tr>
</table>
<ul><li>GIT_REPO_URL</li>
<img src = "https://qcloudimg.tencent-cloud.cn/raw/81be69a1baf0f9fe404c87ad125fc10c.png" style="width: 100%">
<li>CREDENTIALS_ID</li>
<img src = "https://qcloudimg.tencent-cloud.cn/raw/8bf73f2b050dfddc4d67d9748ec5022d.png" style="width: 100%">
</ul>

The environment variables have been entered:
<img src = "https://qcloudimg.tencent-cloud.cn/raw/726d34013ec5cab13f4373ef6f9091e7.png" style="width: 100%">
</ul>

#### Step 4: Start build task and check out code
![](https://qcloudimg.tencent-cloud.cn/raw/a0b29d81fc914b2ac6a5115fda2e8031.png)

[](id:git-lfs)
### How do I check out from a repository using Git LFS?

During CI, you can use process configuration to check out code from a repository managed by the Git Large File Storage (LFS) plugin. This allows CI with Git repositories containing large files.

#### Introduction to Git LFS

The Git LFS plugin accelerates `git clone` and `git fetch` operations that involve frequently changed large files (such as images and videos).

Each time you add large files to the repository, the Git LFS plugin will store the files in the local Git LFS cache and replace large file content in the code repository with references to the cache address. When you commit code, all large files involved in the commit are committed to the remote Git LFS cache, which is associated with your remote repository. When you check out commits that reference large files, the plugin will replace the references with the actual file content from the cache.

Therefore, when using the Git LFS plugin, large files are only loaded for `git checkout`.

#### How do I check out code from a build plan?

Go to **Build Plan Settings** > **Process Configuration**, click **Check out from code repository** to add this step, and then add the Git-LFS-Pull plugin.
![](https://qcloudimg.tencent-cloud.cn/raw/7fa4d3d7d676fc99dded617c99bbb7a6.png)

#### Jenkinsfile
<dx-codeblock>
:::  groovy
pipeline {
  agent any
  stages {
    stage('check out') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: env.GIT_BUILD_REF]],
          extensions: [
            // Add GitLFSPull plugin
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
### Why can't I sync associated TGit repositories to the external repository list?

Currently, you must select **Current Account** as the authorization scope during TGit authorization in order to sync these repositories to the external repository list and check them out in a CI build task. Repositories with **Project Group** or **Project** authorization scopes cannot be synced.
![](https://qcloudimg.tencent-cloud.cn/raw/c3ccbb676cc103c8d7d8389a0038c9c1.png)
