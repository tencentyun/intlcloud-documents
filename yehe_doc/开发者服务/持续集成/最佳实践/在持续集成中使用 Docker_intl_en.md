This document describes how to use Docker in Continuous Integration.

## Prerequisites
Before configuring the CODING Continuous Integration (CODING-CI) build environment, you must activate the CODING DevOps service for your Tencent Cloud account.

## Open Project
1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the **team domain name** to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a **project icon** to open the project.
3. Select **Continuous Integration** from the menu on the left.

## Overview[](id:intro)
Besides using Docker as a build environment for Continuous Integration, you may need to run additional services in Docker as test dependencies, or build a Docker image in a CI process and push it to the relevant repository.

## Run Specific Docker Image and Execute Commands[](id:commands)
In a build process, you may need to use a public Docker image repository. Refer to the following Jenkinsfile for the command to pull a specific Docker image.
```groovy
pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                  script {
                    docker.image("ubuntu").inside('-e MY_ENV=123') {
                          sh 'echo ${MY_ENV}'
                    }     
                  }
            }
        }
    }
}
```

## Run Docker Image of Specific Registry[](id:registry)
In a build process, you may need to use a private Docker image repository. For example, you might need to use a Docker image repository that has been uploaded to the CODING Artifact Repository (CODING-AR). Refer to the following Jenkinsfile.
```groovy
pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                  script {
                    docker.withRegistry('https://registry.example.com') {

                        // Pulls my-custom-image from the hostname registry.example.com
                        docker.image('my-custom-image').inside {
                            sh 'make test'
                        }
                    }
                  }
            }
        }
    }
}
```

Refer to the following Jenkinsfile in the case that a configured registry requires authentication to pull the image and needs a valid credential ID.
```groovy
pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                  script {
                    docker.withRegistry('https://registry.example.com', 'my-credentials-id') {

                    }
                  }
            }
        }
    }
}
```

## Build Docker Image in CI Process[](id:docker)
```groovy
pipeline {
    agent any
    stages {
        // You need to check out the code before using the Dockerfile in the code repository
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: env.GIT_BUILD_REF]], 
                    userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]])
            }
        }
        stage('Build') {
            steps {
                script {
                    // Uses the root path Dockerfile to build by default
                    docker.build('my-docker-image:1.0.0')
                }
            }
        }
    }
}
```

If you need to specify additional parameters for a build, such as using a Dockerfile in a specific directory, refer to the following Jenkinsfile.
```groovy
pipeline {
    agent any
    stages {
        // You need to check out the code before using the Dockerfile in the code repository
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: env.GIT_BUILD_REF]], 
                    userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]])
            }
        }
        stage('Build') {
            steps {
                script {
                    // Uses /dockerfiles/Dockerfile.build to build
                    docker.build('my-docker-image:1.0.0', '-f Dockerfile.build ./dockerfiles')
                }
            }
        }
    }
}
```

## Push docker image to Specific Registry[](id:registry)
Refer to the following Jenkinsfile.
```groovy
pipeline {
    agent any
    stages {
        // You need to check out the code before using the Dockerfile in the code repository
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: env.GIT_BUILD_REF]], 
                    userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]
                ])
            }
        } 

        stage('Build') {
            steps {
                  script {
                      docker.build('my-docker-image:1.0.0')

                    docker.withRegistry('https://registry.example.com', 'my-credentials-id') {
                        docker.image('my-docker-image:1.0.0').push()                    
                    }
                  }
            }
        }
    }
}
```


## Use Docker to Run Additional Services as Test Dependencies[](id:testing-depand)
In the test process, you can use Docker to run MySQL and other services that can be used as test dependencies. Two containers are used in the following example: one as a MySQL service and the other as an execution environment. (Use a Docker link to link the two containers.)
```groovy
pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                  script {
                    docker.image('mysql:5').withRun('-e "MYSQL_ROOT_PASSWORD=my-secret-pw"') { c ->
                        // Note: The callback run environment is not the MySQL:5 environment run above, but the host environment running Docker. 

                        // Runs the second MySQL as the execution environment

                        docker.image('mysql:5').inside("--link ${c.id}:db") {
                          // The commands run here are all in the second MySQL Docker container run
                          // Waits for the MySQL service
                          sh 'while ! mysqladmin ping -hdb --silent; do sleep 1; done'
                        }

                        // After the callback content finishes running, the MySQL Docker container will automatically stop and is removed
                    }       
                  }
            }
        }
    }
}
```

## Run Multiple Containers at the Same Time as Test Dependencies[](id:nested)
If you need more than one additional service as test dependencies, you can run multiple services in a nested way.
```groovy
pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                  script {
                    docker.image('mysql:5').withRun('-e "MYSQL_ROOT_PASSWORD=my-secret-pw"') { c1 ->
                        // Note: The callback run environment is not the MySQL:5 environment run above, but the host environment running Docker.

                        docker.image('redis').withRun('') { c2 ->
                            // Note: The callback run environment is not the Redis environment run above, but the host environment running Docker.
                            sh 'docker ps'
                        } 
                    }       
                  }
            }
        }
    }
}
```

## References[](id:reference)
For more information about Docker-based configuration in Jenkins, see the official Jenkins documentation:
- [Using Docker with Pipeline](https://jenkins.io/zh/doc/book/pipeline/docker/)
- [Pipeline Syntax: agent](https://www.jenkins.io/zh/doc/book/pipeline/syntax/#%E4%BB%A3%E7%90%86)
