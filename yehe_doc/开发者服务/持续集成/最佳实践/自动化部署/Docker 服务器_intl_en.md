This document describes how to use Continuous Integration to release a project to a Docker server.

## Prerequisites
Before configuring the CODING Continuous Integration (CODING-CI) build environment, you must activate the CODING DevOps service for your Tencent Cloud account.

## Open Project
1. Log in to the CODING Console and click the **team domain name** to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a **project icon** to open the project.
3. Select **Continuous Integration** from the menu on the left.

## Retrieve SSH Key Pair
Log in to the server console and create an SSH key pair. After you obtain the private key pair, enter it in CODING's project token. Then, copy the public key content in id_rsa.pub to`~/.ssh/authorized_keys` in the server.
![](https://qcloudimg.tencent-cloud.cn/raw/2b08584f812e649e7fd46f82c9e0d629.png)

## Retrieve Artifact Repository Information
1. Follow the instructions to retrieve the username and password for the Docker repository with one click and enter them in the environment variables of Continuous Integration.
![](https://qcloudimg.tencent-cloud.cn/raw/7cc22c8091a2b04265a1a6cf351a70ae.png)
2. Enter them in Variables and Caches in the build plan details.
![](https://qcloudimg.tencent-cloud.cn/raw/0e867ccd712f4589db29097fced5445c.png)

## Jenkinsfile
Go to "Build Plan Settings" > "Process Configuration". Refer to the following configuration for filling.
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
    stage('Deploy') {
      steps {
        echo 'deploying...'
        script {
          // Declare server information
          def remote = [:]
          remote.name = 'web-server'
          remote.allowAnyHosts = true
          remote.host = '106.54.86.239'
          remote.port = 22
          remote.user = 'ubuntu'

          // In "CODING Credential Management" > "Credential ID", enter credentialsId. You do not need to modify id_rsa.
          withCredentials([sshUserPrivateKey(credentialsId: "c4af855d-402a-4f38-9c83-f6226ae3441c", keyFileVariable: 'id_rsa')]) {
            remote.identityFile = id_rsa

            // Log in to the server via SSH and pull the Docker image
            // Configure DOCKER_USER and DOCKER_PASSWORD in the environment variables of Continuous Integration
            sshCommand remote: remote, sudo: true, command: "apt-get install -y gnupg2 pass"
            sshCommand remote: remote, command: "docker login -u ${env.DOCKER_USER} -p ${env.DOCKER_PASSWORD} $DOCKER_SERVER"
            sshCommand remote: remote, command: "docker pull ${imageName}"
            sshCommand remote: remote, command: "docker stop web | true"
            sshCommand remote: remote, command: "docker rm web | true"
            sshCommand remote: remote, command: "docker run --name web -d ${imageName}"
          }
        }
      }
    }
  }
}
```

## Docker Compose
The code for Docker Compose is slightly different:
```groovy
sshCommand remote: remote, sudo: true, command: "apt-get install -y gnupg2 pass"
sshCommand remote: remote, command: "docker login -u ${env.DOCKER_USER} -p ${env.DOCKER_PASSWORD} $DOCKER_SERVER"
sshCommand remote: remote, sudo: true, command: "mkdir -p /var/www/site/"
sshCommand remote: remote, sudo: true, command: "chmod 777 /var/www/site/"
sshPut remote: remote, from: 'docker-compose.yml', into: '/var/www/site/'
sshCommand remote: remote, command: "cd /var/www/site/ && echo IMAGE=${imageName} > .env && echo APP_KEY=${env.APP_KEY} >> .env && echo DB_CONNECTION=sqlite >> .env"
sshCommand remote: remote, command: "cd /var/www/site/ && docker-compose down --remove-orphans"
sshCommand remote: remote, command: "cd /var/www/site/ && docker-compose up -d --no-build"
```

`docker-compose.yml` code:
```yaml
version: '2.1'
services:
  web:
    env_file: .env
    build: .
    image: ${IMAGE:-laravel-demo:dev}
    ports:
     - "80:80"
    links:
    - redis
  redis:
    image: "redis:5"
```
