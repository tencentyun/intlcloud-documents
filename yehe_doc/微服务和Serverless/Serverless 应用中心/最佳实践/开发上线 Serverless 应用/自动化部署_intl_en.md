## Overview
During serverless application development, we need to manually run deployment commands to deploy development projects to the cloud and automate the serverless application deployment by introducing some CI capabilities.

## Automated Deployment Based on GitHub

### Prerequisites

- You have created a serverless application project. For how to create a serverless application project and create environments and branches, see [Project Development](https://intl.cloud.tencent.com/document/product/1040/38253).
- You have hosted your serverless application project in GitHub.

### Directions

During the development and testing phase, if you want your code to be deployed automatically after each commit for ease of development, testing, and debugging, perform the following operations:
1. Select a branch for which you want to perform automated deployment (the `dev` branch is selected in this example).
2. Create your actions under the branch.  
![](https://main.qcloudimg.com/raw/6863deb3acfb9a8de75d8a0447ec4d20.png)
>!GitHub specifies that if an event occurs on a particular repository branch, the workflow file must be placed in that branch's repository.
3. Configure Tencent Cloud secrets (keys).
![](https://main.qcloudimg.com/raw/e67ecc4fd932124db5d6bfa54b3ebb73.png)
4. Configure action deployment.
```
# When the code is pushed to the `dev` branch, the current workflow will be executed
# For more information on configuration, visit https://docs.github.com/cn/actions/getting-started-with-github-actions.
name: deploy serverless
on: # Configuration of the event and branch listened on
      push:
        branches:
          - dev 
jobs:
      test: # Configure unit testing
        name: test
        runs-on: ubuntu-latest
        steps:
          - name: unit test
            run: '' 
      deploy:
        name: deploy serverless
        runs-on: ubuntu-latest
        needs: [test]
        steps:
          - name: clone local repository
            uses: actions/checkout@v2
          - name: install serverless
            run: npm install -g serverless
          - name: install dependency
            run: npm install
          - name: build
            run: npm build
          - name: deploy serverless
            run: sls deploy --debug
            env: # Environment variable
              STAGE: dev # Your deployment environment
              SERVERLESS_PLATFORM_VENDOR: tencent # The serverless platform is `aws` by default outside the Chinese mainland. Here, it is set to `tencent`.
              TENCENT_SECRET_ID: ${{ secrets.TENCENT_SECRET_ID }} # `secret ID` of your Tencent Cloud account
              TENCENT_SECRET_KEY: ${{ secrets.TENCENT_SECRET_KEY }} # `secret key` of your Tencent Cloud account 
```

After the above configuration, the code that you commit to the `dev` branch every time will be automatically deployed.

## Automated Deployment Based on CODING

### Prerequisites

- You have signed up for a CODING account. If you are a Tencent Cloud user, you can use [CODING DevOps](https://console.cloud.tencent.com/coding) to quickly register a CODING account.
- You have created a serverless application project. For how to create a serverless application project and create environments and branches, see [Project Development](https://intl.cloud.tencent.com/document/product/1040/38253).
- You have hosted your serverless application project on platforms such as CODING, GitHub, GitLab, and Gitee.

### Overview
During the development and testing phase, if you want your code to be deployed automatically after each commit for ease of development, testing, and debugging, perform the following operations:

1. Create your CODING DevOps project.
2. Create a build plan and choose to customize a build process.
3. Configure the build plan.
   1. Configure basic information. This example shows how to configure the GitHub repository `June1991/express-demo`.
   2. Configure trigger rules. This example shows how to configure a rule to trigger build when code is pushed to the `dev` branch.
   3. Configure environment variables. This example shows how to set the `STAGE` variable to the deployment environment `dev` and set `TENCENT_CLOUD_API_CRED` to the Tencent Cloud account key (key configuration path: **Project Settings** > **Developer Options** > **Credential Management** > **Enter Credential** > **Tencent Cloud API key**).
   4. Configure the pipeline (process).
```
pipeline {
         agent any
         stages {
           stage('Check out') {
             steps {
               checkout([$class: 'GitSCM', branches: [[name: env.GIT_BUILD_REF]],
                   userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]])
             }
           }
           stage('Install dependencies') {
             steps {
               echo 'Installing dependencies...'
               sh 'npm i -g serverless'
               sh 'npm install'
               echo 'Dependencies installed.'
             }
           }
           stage('Deploy') {
             steps {
               echo 'Deploying...'
      
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
After the above configuration, the code that you commit to the `dev` branch every time will be automatically deployed.
