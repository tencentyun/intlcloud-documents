---
title: Upload Generic Artifacts - CODING Help Center
pageTitle: Upload Generic Artifacts
pagePrevTitle: Team Template
pagePrev: ci/manage/team-template.html
pageNextTitle: Retrieve Entered Credentials
pageNext: ci/plugins/credentials.html
alias: devops/ci/plugins/generic.html
---

### Feature Overview

In an actual production environment, many tasks are repetitive. CODING Continuous Integration (CODING-CI) features plugins that can help you handle tedious and repetitive tasks efficiently. You can also use custom parameters to address unique needs. More built-in plugins are coming soon. At the moment, you can use the following convenient plugin types in CODING-CI:

+ Upload generic artifacts
+ Retrieve uploaded credentials
+ Automatically add reviewers in merge requests
+ Manual confirmation

### Use plugin to upload generic artifacts

In the process of building a CI task, you can choose to upload an artifact to the CODING Artifact Repository (CODING-AR). Generic artifacts upload plugin allows you to conveniently upload generic artifacts of up to 5 GB in Continuous Integration. Before using this function, ensure that you have a basic understanding of generic repositories. For more information, see [Using Generic Repositories](/docs/artifacts/quick-start/generic.html).

### Getting Started

You can use a fixed template or a Jenkinsfile configuration to upload generic artifacts.

#### Fixed Template

1. Before using the plugin, make sure that you have created a generic repository. Take a test repository as an example below.

![](https://qcloudimg.tencent-cloud.cn/raw/54ec7032d56af41a26e48e553a3d3bbd.png)

2. Click "New Build Plan" and select "Artifact Repository" > CODING Generic Artifact Upload.

![](https://qcloudimg.tencent-cloud.cn/raw/0020b661a390fda99745a659e3fa760d.png)

3. Set the default value to "test" repository you have just created. You can also fill in your artifact repository URL in the code.

![](https://qcloudimg.tencent-cloud.cn/raw/43b2652696c852a4fa82827f9d5d633b.png)

4. Select "Trigger build after creation" and click "OK" to run the build.

5. After the build is complete, the file uploaded beforer will appear in the artifact repository.

![](https://qcloudimg.tencent-cloud.cn/raw/d375f383c3c9871b22bbe99b8d4f279b.png)

#### Jenkinsfile Configuration

1. When selecting a code repository, make sure the code repository contains a Jenkinsfile with the configuration below.

```groovy
pipeline {
    agent any
    stages {
        stage('Upload to generic repository') {
            steps {
                // Use the fallocate command to create a file of 10 MB in size. (The default working directory in Continuous Integration is /root/workspace.)
                sh 'fallocate -l 10m my-generic-file'

                codingArtifactsGeneric(
                    files: 'my-generic-file',
                    repoName: 'myrepo', // Fill in your repository parameters here, for example, ${env.GENERIC_REPO_NAME}
                )
            }
        }
    }
}

```

2. In "Process Configuration", you can modify the Jenkinsfile configuration.

![](https://qcloudimg.tencent-cloud.cn/raw/21e69231d0c9f1d87b087e2959573ee3.png)

### More examples of parameters

```groovy
pipeline {
    agent any
    stages {
        stage('Upload to generic repository') {
            steps {
                // Use the fallocate command to create a file of 10 MB in size. (The default working directory in Continuous Integration is /root/workspace.)
                sh 'fallocate -l 10m my-generic-file'

                codingArtifactsGeneric(
                    files: 'my-generic-file',
                    repoName: 'myrepo',
                )
            }
        }
    }
}

```

### Parameter Descriptions

| Parameter | Required? | Parameter type | Graphical parameter type | Default value | Description |
|---------|------|-----------|--------------|------|------|
| files | Yes | \-  | List of files to be uploaded, wildcards are supported `build/libs/**/xx` | | |
| repoName | Yes (Not required if repoURL is set separately) | string  | Repository name | \- | This parameter determines the repository to which an artifact is uploaded. Simply enter the repoName to upload the artifact to the repository under the current project by default. If the repository is not in the current project, use the repoURL |
| version | No | string | string | latest | Version of the artifact, default: "latest" |
| zip | No | \- | string | string | Packages the artifacts in the selected directory into a zip file, and then uploads the individual artifacts. For example, demo\.zip. (Do not set the parameter. Multiple files will be uploaded as individual artifacts.)|
| credentialsId | No | string  | Credentials (username\+password) | env\.CODING\_ARTIFACTS\_CREDENTIALS\_ID | Credentials used to upload repository (Only the username \+   password project token is supported). By default, the environment variable `CODING_ARTIFACTS_CREDENTIALS_ID` will be used. |
| repoURL | No | string  | string | https://`<`env.CCI_CURRENT_TEAM>-generic.`<`env.CCI_CURRENT_DOMAIN>/`<`env.PROJECT_NAME>/`<`params.repoName>| By default, the CI built-in environment variables `CCI_CURRENT_TEAM`, `CCI_CURRENT_DOMAIN`, and `PROJECT_NAME` and `repoName` set in the parameters will be used. For example, `https://myteam-generic.coding.net/myproject/myrepo/`.  You can manually set the parameter to upload the artifact to a repository outside of the current project.  After you set the parameter, the repoName will be invalid. |
| withBuildProps | No | boolean | boolean | true | Set to `true`. By default, the current CI build environment will be associated with the built-in artifact fields. |
| workspace | No | string | No | 


==== 2020/08/24 ====
