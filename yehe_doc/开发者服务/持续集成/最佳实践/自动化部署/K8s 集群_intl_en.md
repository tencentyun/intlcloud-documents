This document describes how to use Continuous Integration to release a project to a K8s cluster.

## Prerequisites
Before configuring the CODING Continuous Integration (CODING-CI) build environment, you must activate the CODING DevOps service for your Tencent Cloud account.

## Open Project
1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the **team domain name** to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a **project icon** to open the project.
3. Select **Continuous Integration** from the menu on the left.

Follow the steps below to easily deploy a project to a K8s cluster through Continuous Integration:
1. Retrieve the username and password for the Docker repository (You can obtain them by creating an access token with one click in CODING Artifact Repository). Then, enter them in the environment variables of Continuous Integration.
2. Build a Docker image and upload it to the repository.
3. Using a cloud computing service provider (such as Tencent Cloud), create a K8s cluster and deployment. Retrieve kubeconfig and enter it in CODING Credential Management.
4. Use the following Jenkinsfile in Continuous Integration: Run kubectl and deploy.

## Jenkinsfile
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
    stage('Build') {
      steps {
        echo 'building...'
        script {
          // Modify dockerServer, dockerPath, and imageName
          dockerServer = 'codes-farm-docker.pkg.coding.net'
          dockerPath = '/laravel-demo/laravel-docker'
          imageName = "${dockerServer}${dockerPath}/laravel-demo:1.0.0"
          def customImage = docker.build(imageName)

          // Push Docker image to repository
          docker.withRegistry("https://${dockerServer}", CODING_ARTIFACTS_CREDENTIALS_ID) {
            customImage.push()
          }
        }
      }
    }
    stage('Deploy to K8s') {
      steps {
        echo 'deploying...'
        script {
          // Modify credentialsId: Fill in the K8s credential ID
          withKubeConfig([credentialsId: 'f23cc59c-dfd1-40b9-a12f-2c9b6909e908']) {
            // Use kubectl to create a K8s secret key: originates from the environment variables DOCKER_USER and DOCKER_PASSWORD
            sh(script: "kubectl create secret docker-registry coding --docker-server=${dockerServer} --docker-username=${env.DOCKER_USER} --docker-password=${env.DOCKER_PASSWORD} --docker-email=support@coding.net", returnStatus: true)

            // Use kubectl to modify the K8s deployment: Specify the Docker image link and secret key
            // Modify laravel-demo and web to the values in your deployment
            sh "kubectl patch deployment laravel-demo --patch '{\"spec\": {\"template\": {\"spec\": {\"containers\": [{\"name\": \"web\", \"image\": \"${imageName}\"}], \"imagePullSecrets\": [{\"name\": \"coding\"}]}}}}'"
          }
        }
      }
    }
  }
}
```



## Notice[](id:notice)
As a **K8s deployment** includes at least five steps, we recommend you to use [Continuous Deployment](https://intl.cloud.tencent.com/document/product/1137/44819) instead of writing all of them in **Continuous Integration** to facilitate future maintenance.
