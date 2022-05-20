
## Overview
As agile development and DevOps get more popular, CI/CD has become an indispensable best practice by almost all developers. It aims to deliver practical software programs more quickly.

#### CI/CD 
![](https://qcloudimg.tencent-cloud.cn/raw/5189f5b66e1a9cfaa59718f7798dfbb6.jpg)

#### CI/CD strengths

- Reduced release cycle
- Reduced risks
- Improved code quality
- More efficient feedback loop
- Visual process

This document uses GitHub, Jenkins, and CODING as examples to describe how to use [Serverless Framework CLI](https://intl.cloud.tencent.com/document/product/583/36262) to quick build CI/CD for your SCF project.

## Automated Deployment Based on GitHub

[GitHub Actions](https://docs.github.com/cn/actions) is an automated software development workflow launched by GitHub. It uses actions to execute any tasks, including CI/CD.

![](https://qcloudimg.tencent-cloud.cn/raw/d1e50cd0ebe89323275c69c87dba6767.png)

### Prerequisites

- The SCF project has been hosted in GitHub.
- The project needs to contain the `serverless.yml` configuration file used for execution in Serverless Framework CLI.
- To use an HTTP-triggered function, place the [scf_bootstrap](https://intl.cloud.tencent.com/document/product/583/40690) file in the root directory of your project.

### Directions

>! SCF has released [Tencent Serverless Action](https://github.com/marketplace/actions/tencent-serverless-action) in GitHub.

1. Search for **Tencent Serveless Action** in GitHub.
![](https://qcloudimg.tencent-cloud.cn/raw/4adf8375e5a08bf5b4a7c64f04caf7af.png)
2. On the **Actions** tab, select **Set up a workflow yourself** as shown below.
![](https://qcloudimg.tencent-cloud.cn/raw/c890fa7a7b18936fc2857c5bca071f18.jpg)
3. How to use:
  - If you are familiar with the action usage, you can use the following command, which encapsulates the steps of installing Serverless Framework and running the deployment command.
```
    - name: serverless scf deploy
      uses: woodyyan/tencent-serverless-action@main
```
  - If you are new to actions, you can select one of the following YML code samples based on your programming language (Python, Java, or Node.js):
<dx-codeblock>
::: Python python
```yaml
# When the code is pushed to the `main` branch, the current workflow will be executed
# For more information on configuration, visit https://docs.github.com/cn/actions/getting-started-with-github-actions.
name: deploy serverless scf
on: # Configuration of the event and branch listened on
  push:
    branches:
      - main
jobs:
  deploy:
    name: deploy serverless scf
    runs-on: ubuntu-latest
    steps:
      - name: clone local repository
        uses: actions/checkout@v2
      - name: deploy serverless
        uses: woodyyan/tencent-serverless-action@main
        env: # Environment variable
          STAGE: dev # Your deployment environment
          SERVERLESS_PLATFORM_VENDOR: tencent # The serverless platform is `aws` by default outside the Chinese mainland. Here, it is set to `tencent`
          TENCENT_SECRET_ID: ${{ secrets.TENCENT_SECRET_ID }} # `secret ID` of your Tencent Cloud account, which needs to be configured in `Settings-Secrets`
          TENCENT_SECRET_KEY: ${{ secrets.TENCENT_SECRET_KEY }} # `secret key` of your Tencent Cloud account, which needs to be configured in `Settings-Secrets`

```
:::
::: Java java
```yaml
name: deploy serverless scf
on: # Configuration of the event and branch listened on
  push:
    branches:
      - main
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write
    steps:
      - uses: actions/checkout@v2
      - name: Set up JDK 11
        uses: actions/setup-java@v2
        with:
          java-version: '11'
          distribution: 'temurin'
          server-id: github # Value of the distributionManagement/repository/id field of the pom.xml
          settings-path: ${{ github.workspace }} # location for the settings.xml file
      - name: Build with Gradle # Use this for a Gradle project
        uses: gradle/gradle-build-action@937999e9cc2425eddc7fd62d1053baf041147db7
        with:
          arguments: build
      - name: Build with Maven # Use this for a Maven project
        run: mvn -B package --file pom.xml
      - name: Create zip folder # This step is used to store JAR and `scf_bootstrap` files for HTTP-triggered Java functions. You only need to specify the `Jar` directory in `Serverless.yml` for event-triggered Java functions.
        run: mkdir zip
      - name: move jar and scf_bootstrap to zip folder # This step is used to move JAR and `scf_bootstrap` files for HTTP-triggered Java functions. You only need to specify the `Jar` directory in `Serverless.yml` for event-triggered Java functions. Note that if you use Maven for compilation, you need to change the JAR path below to `/target`
        run: cp ./build/libs/XXX.jar ./scf_bootstrap ./zip
      - name: deploy serverless
        uses: woodyyan/tencent-serverless-action@main
        env: # Environment variable
          STAGE: dev # Your deployment environment
          SERVERLESS_PLATFORM_VENDOR: tencent # The serverless platform is `aws` by default outside the Chinese mainland. Here, it is set to `tencent`
          TENCENT_SECRET_ID: ${{ secrets.TENCENT_SECRET_ID }} # `secret ID` of your Tencent Cloud account
          TENCENT_SECRET_KEY: ${{ secrets.TENCENT_SECRET_KEY }} # `secret key` of your Tencent Cloud account
```
:::
::: NodeJS nodejs
```yaml
# When the code is pushed to the `main` branch, the current workflow will be executed
# For more information on configuration, visit https://docs.github.com/cn/actions/getting-started-with-github-actions.
name: deploy serverless scf
on: # Configuration of the event and branch listened on
  push:
    branches:
      - main
jobs:
  deploy:
    name: deploy serverless scf
    runs-on: ubuntu-latest
    steps:
      - name: clone local repository
        uses: actions/checkout@v2
      - name: install dependency
        run: npm install
      - name: build
        run: npm build
      - name: deploy serverless
        uses: woodyyan/tencent-serverless-action@main
        env: # Environment variable
          STAGE: dev # Your deployment environment
          SERVERLESS_PLATFORM_VENDOR: tencent # The serverless platform is `aws` by default outside the Chinese mainland. Here, it is set to `tencent`
          TENCENT_SECRET_ID: ${{ secrets.TENCENT_SECRET_ID }} # `secret ID` of your Tencent Cloud account, which needs to be configured in `Settings-Secrets`
          TENCENT_SECRET_KEY: ${{ secrets.TENCENT_SECRET_KEY }} # `secret key` of your Tencent Cloud account, which needs to be configured in `Settings-Secrets`
```
:::
</dx-codeblock>

     `TENCENT_SECRET_ID` and `TENCENT_SECRET_KEY` are required during the deployment. You need to configure such variables in `Secrets` in the GitHub code repository settings as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/32ccf627154de6cfb657e026384e7555.jpg)
You can get the Tencent Cloud secret ID and key from [CAM](https://console.cloud.tencent.com/cam/capi).
4. After the configuration, every time the code is pushed, the deployment process will be automatically triggered, and you can view the execution result and error logs on the **Actions** tab in real time as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/286c92e3001b96ed67dcbc2139ff976a.png) 
In addition, you can add testing to the process for steps such as security check and release based on your project needs.



## Automated Deployment Based on Jenkinsfile

Jenkinsfile is commonly used on Jenkins and CODING platforms. After configuring the Jenkinsfile, you can complete automated deployment on such platforms.

### Prerequisites

- You have hosted your SCF project onto platforms such as CODING, GitHub, GitLab, and Gitee.
- The project needs to contain the `serverless.yml` configuration file used for execution in Serverless Framework CLI.
- To use an HTTP-triggered function, place the [`scf_bootstrap`](https://intl.cloud.tencent.com/document/product/583/40690) file in the root directory of your project.

### Directions

This document provides Jenkinsfile code in three programming languages: Python, Java, and Node.js. Carefully read the comments.

```python
pipeline {
  agent any
  stages {
    stage('check out') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: env.GIT_BUILD_REF]],
            userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]])
      }
    }
		stage('Package'){ // This stage is only used for a Java project
       steps{
        container("maven") {
          echo 'Package start'
          sh "mvn package" // This line is used for a Java Maven project
					sh "./gradlew build" // This line is used for a Java Gradle project
					sh "mkdir zip" // This line is used to store JAR and `scf_bootstrap` files for HTTP-triggered Java functions. You only need to specify the `Jar` directory in `Serverless.yml` for event-triggered Java functions.
          sh "cp ./build/libs/XXX.jar ./scf_bootstrap ./zip" // This line is used to move JAR and `scf_bootstrap` files for HTTP-triggered Java functions. You only need to specify the `Jar` directory in `Serverless.yml` for event-triggered Java functions. Note that if you use Maven for compilation, you need to change the JAR path below to `/target`.
        }           
		   }
    }
    stage('Install dependency') {
      steps {
        echo 'Installing dependency...'
        sh 'npm i -g serverless'
        sh 'npm install' // This line is used for a Node.js project
        echo 'Dependency installed.'
      }
    }
    stage('deploy') {
      steps {
        echo 'deploying...'
        withCredentials([
          cloudApi(
            credentialsId: "${env.TENCENT_CLOUD_API_CRED}",
            secretIdVariable: 'TENCENT_SECRET_ID',
            secretKeyVariable: 'TENCENT_SECRET_KEY'
          ),
        ]) {
             // Generate the credential file
             sh 'echo "TENCENT_SECRET_ID=${TENCENT_SECRET_ID}\nTENCENT_SECRET_KEY=${TENCENT_SECRET_KEY}" > .env'
             // Deploy
             sh 'sls deploy --debug'   
             // Remove the credential
             sh 'rm .env' 
        }
        echo 'deployment complete'
      }
    }
  }
}
```

You can use the above Jenkinsfile to quickly configure CI/CD on platforms such as Jenkins and CODING.



>! You can get Tencent Cloud `TENCENT_SECRET_ID` and `TENCENT_SECRET_KEY` required during the deployment from [CAM](https://console.cloud.tencent.com/cam/capi).
