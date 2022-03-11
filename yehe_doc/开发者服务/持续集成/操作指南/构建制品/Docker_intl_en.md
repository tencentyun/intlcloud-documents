---
title: Docker - CODING Help Center
pageTitle: Docker
pagePrevTitle: Build Composer Artifacts
pagePrev: ci/artifacts/composer.html
pageNextTitle: Build File Type Artifact
pageNext: ci/artifacts/generic.html
alias: 
-   devops/ci/artifacts/docker.html
-   ci/artifacts/docker.html
---

### Feature Overview

This document provides an example of a Jenkinsfile for building a Docker image with a continuous integration task. After you build the Docker image, you can use a preset plugin to upload it to the CODING Artifact Repository (CODING-AR). Before using this function, ensure that you have a [basic understanding](https://intl.cloud.tencent.com/document/product/1135/45430) of Docker artifact repositories.

### Jenkinsfile

```groovy
pipeline {
  agent any
  stages {
    stage('Check out') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: env.GIT_BUILD_REF]],
          userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]
        ])
      }
    }
    stage('Build Docker image') {
      steps {
        script {
          ARTIFACT_VERSION = "1.2.0"
          // Note: When creating a project, use hyphens in the link ID instead of underscores. For example, the ID of "My Project" should be my-project.
          // Modify build/my-api to your artifact repository name and image name
          CODING_DOCKER_IMAGE_NAME = "${env.PROJECT_NAME.toLowerCase()}/build/my-api"
          // The environment variable CODING_ARTIFACTS_CREDENTIALS_ID has been built into the artifact repository in this project. No need to set again.
          docker.withRegistry("https://${env.CCI_CURRENT_TEAM}-docker.pkg.coding.net", "${env.CODING_ARTIFACTS_CREDENTIALS_ID}") {
            docker.build("${CODING_DOCKER_IMAGE_NAME}:${ARTIFACT_VERSION}").push()
          }
        }
      }
    }
  }
}
```


