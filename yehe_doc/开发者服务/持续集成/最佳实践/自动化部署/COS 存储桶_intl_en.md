This document describes how to use Continuous Integration to release a project to a Cloud Object Storage (COS) bucket with one click.

## Prerequisites
Before configuring the CODING Continuous Integration (CODING-CI) build environment, you must activate the CODING DevOps service for your Tencent Cloud account.

## Open Project
1. Log in to the CODING Console and click the **team domain name** to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a **project icon** to open the project.
3. Select **Continuous Integration** from the menu on the left.

## Function Overview[](id:intro)
Tencent Cloud's auto-scaling storage allows you to release a project to COS with one click through Continuous Integration, which is applicable for scenarios such as building a static website or compiling files for download.

## Create Bucket[](id:new)
Create a **bucket** in cloud storage (such as [Tencent Cloud's COS](https://intl.cloud.tencent.com/zh/products/cos)) and retrieve the bucket name, region, and secret key.
![](https://qcloudimg.tencent-cloud.cn/raw/df35b52d91795d4b61e24ca9cc466896.png)

## Jenkinsfile
In Continuous Integration, refer to and write the following Jenkinsfile to trigger a build task and upload files.
```groovy
pipeline {
  agent any
  stages {
    stage('Check out') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: env.GIT_BUILD_REF]],
        userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]])
      }
    }
    stage('Compile') {
      steps {
        // Convert markdown to HTML
        // sh 'pip install mkdocs && mkdocs build'
        // React/VUE SPA generate HTML
        // sh 'npm run build'
        // Create Android package
        // sh './gradlew assembleDebug'
      }
    }
    stage('Upload to Tencent Cloud COS') {
      steps {
        sh "coscmd config -a ${env.COS_SECRET_ID} -s ${env.COS_SECRET_KEY}" +
           " -b ${env.COS_BUCKET_NAME} -r ${env.COS_BUCKET_REGION}"
        sh "rm -rf .git"
        sh 'coscmd upload -r ./ /'
        //sh 'coscmd upload -r ./dist /'
      }
    }
  }
}
```

## Environment Variables[](id:variable)
|Variable              | Description             | Example|
|-------------------|------------------|---------|
|COS_SECRET_ID  | Key ID for accessing Tencent Cloud | stringLength36stringLength36string36|
|COS_SECRET_KEY | Secret key for accessing Tencent Cloud | stringLength32stringLength323232|
|COS_BUCKET_NAME | Tencent Cloud COS bucket  | devops-host-1257110097|
|COS_BUCKET_REGION | Tencent Cloud COS region  | ap-nanjing|
