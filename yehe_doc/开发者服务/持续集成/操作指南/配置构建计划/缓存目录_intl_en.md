---
title: Cache Directory - CODING Help Center
pageTitle: Cache Directory
pagePrevTitle: Build Snapshots
pagePrev: ci/configuration/snapshot.html
pageNextTitle: Build Node Types
pageNext: ci/node/type.html
alias: 
- devops/ci/cache.html
- ci/cache.html
- practice/jenkins-dockerfile.html
---

### [Function Overview](#intro)

When installing dependencies for a local project, the downloaded files are cached for the next installation. After you run the `npm install` command, `./node_modules` is generated in the project and is cached in the `~/.npm` directory, which is more compact and universal.

- Default build nodes

    CODING distributes computing resources for each build plan, which are destroyed once a build is finished. As a new build node is assigned for each build, the "cache directory" needs to be specified to accelerate the next build.

- Custom build nodes

    If you would like to access computing resources and execute the task in the build plan using a custom build node, the server will not be destroyed once the build is finished, so you do not need to specify the "cache directory".

When using Docker in Continuous Integration, you will need to enable the "cache directory" in Docker.

### [Default build nodes](#default)

CODING provides the basic task computing resources for build plans. A CVM is assigned for each task in a Linux build environment with root user permissions, the cache directory is as follows:

Package management tool | Cache directory
---------|--------------
Maven    | /root/.m2/
Gradle   | /root/.gradle/
npm      | /root/.npm/
composer | /root/.cache/composer/
pip3     | /root/.cache/pip/
yarn     | /usr/local/share/.cache/yarn/

In "Build Plan Settings" > "Variables and Caches", select or enter the cache directory.

![](https://qcloudimg.tencent-cloud.cn/raw/121994da6136d1bfd9887902947e5081.png)

### [Docker build environment](#build-in-docker)

If you are using Docker in a build plan, go to "Variables and Caches", select the cache directory, and then enable it in Docker.

#### Jenkinsfile

```groovy
pipeline {
  agent any
  stages {
    stage('check out') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: env.GIT_BUILD_REF]], 
          userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]
        ])
      }
    }
    stage('Java cache') {
      agent {
        docker {
          image 'adoptopenjdk:11-jdk-hotspot'
          args '-v /root/.gradle/:/root/.gradle/ -v /root/.m2/:/root/.m2/'
          reuseNode true
        }
      }
      steps {
        sh './gradlew test'
      }
    }
    stage('npm cache') {
      steps {
        script {
          docker.image('node:14').inside('-v /root/.npm/:/root/.npm/') {
            sh 'npm install'
          }
        }
      }
    }
  }
}
```

#### [Custom build nodes](#customize)

When using a Docker environment in a custom build node, find the cache directory corresponding to the server username. For example, if the default username for Ubuntu servers is ubuntu, the cache directory is `/home/ubuntu/.npm/`, and the codes are as follows:

```groovy
docker.image('node:14').inside('-v /home/ubuntu/.npm/:/root/.npm/') {
  sh 'npm install'
}
```

### [Cache basic docker images](#docker-image)

As the basic Docker images, such as the basic `Dockerfile` image and CI agent image, need to be pulled for every build, the process can be accelerated by caching the images.

You can use the `Jenkinsfile` below by modifying the image name:

```groovy
pipeline {
  agent any
  environment{
    DOCKER_CACHE_EXISTS = fileExists '/root/.cache/docker/php-8.0-cli.tar'
  }
  stages {
    stage('Load cache') {
      when { expression { DOCKER_CACHE_EXISTS == 'true' } }
      steps {
        sh 'docker load -i /root/.cache/docker/php-8.0-cli.tar'
      }
    }
    stage('Use images (modify this section)') {
      agent {
        docker {
          image 'php:8.0-cli'
          args '-v /root/.cache/:/root/.cache/'
          reuseNode 'true'
        }
      }
      steps {
        sh "php -v"
      }
    }
    stage('Generate cache (run once only)') {
      when { expression { DOCKER_CACHE_EXISTS == 'false' } }
      steps {
        sh 'mkdir -p /root/.cache/docker/'
        sh 'docker save -o /root/.cache/docker/php-8.0-cli.tar php:8.0-cli'
      }
    }
  }
}
```

Add the path `/root/.cache/` in "Cache Directory". The duration of the second build is significantly shorten due to the cache:

![](https://qcloudimg.tencent-cloud.cn/raw/0651bc9b9a2af57a843acb3913315d67.png)

> ⚠️Keep cached images up to date with official updates.

### [Save Dockerfiles](#dockerfile)

If you are using a `Dockerfile` as the build environment in Continuous Integration, instead of running the `docker build` command at initialization, save the built Docker images to a repository to pull and reuse them again.

#### Jenkinsfile

```groovy
// Creates a CODING Docker repository and obtains the username, password, and repository URL
sh "docker login -u $DOCKER_USER -p $DOCKER_PASSWORD my-team-docker.pkg.coding.net"

// Use MD5 of Dockerfile as tag
md5 = sh(script: "md5sum Dockerfile | awk '{print \$1}'", returnStdout: true).trim()
imageFullName = "my-team-docker.pkg.coding.net/my-project/my-repo/my-app:dev-${md5}"

// Check if images exist in remote repository
dockerNotExists = sh(script: "docker manifest inspect $imageFullName > /dev/null", returnStatus: true)
def testImage = null
if (dockerNotExists) {
    testImage = docker.build("$imageFullName", "--build-arg APP_ENV=testing ./")
    sh "docker push $imageFullName"
} else {
    testImage = docker.image(imageFullName)
}

// Use images for automated testing
testImage.inside("-e 'APP_ENV=testing'") {
    stage('Test') {
        echo 'testing...'
        sh 'ls'
        echo 'test done.'
    }
}
```

Explanation: By running the following command in the shell, you can determine "if the images exist" based on the returned value.

```shell
docker manifest inspect ecoding/foo:bar
no such manifest
$ echo $?
1
```

==== 2021/09/17 ====
