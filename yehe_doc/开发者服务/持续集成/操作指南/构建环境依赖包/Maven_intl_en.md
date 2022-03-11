---
title: Maven - CODING Help Center
pageTitle: Maven
pagePrevTitle: Install Go Dependency
pagePrev: ci/depend/go.html
pageNextTitle: Install PHP Dependency
pageNext: ci/depend/php.html
alias: ci/depend/maven.html
---

Dependencies are stored in "Maven Repository" by Java. Use Maven, Gradle, or other build tools to manage and install dependencies. This document takes Gradle as an example. Previous Maven projects can be upgraded to Gradle with one click using the command:

```shell
gradle init --type pom
```

### Gradle bin

Bin is downloaded first for building with Gradle . As the official download link connects to a location outside of China, users in mainland China should switch to the Tencent Cloud Image for fast access by modifying `gradle/wrapper/gradle-wrapper.properties` in the project:

```shell
# Tencent Cloud Mirror
distributionUrl=https\://mirrors.cloud.tencent.com/gradle/gradle-6.8.1-bin.zip

# Default outside China
# distributionUrl=https\://services.gradle.org/distributions/gradle-6.8.1-bin.zip
```

### [Public artifact repository](#public)

Although the Maven public repository is overseas, CODING-CI has built-in mainland China mirrors for acceleration, so no configuration is needed. To accelerate the connection for a local development, modify `~/.gradle/init.gradle` as follows:

```groovy
def repoConfig = {
    all { ArtifactRepository repo ->
        if (repo instanceof MavenArtifactRepository) {
            def url = repo.url.toString()
            if (url.contains('repo1.maven.org/maven2')
                || url.contains('jcenter.bintray.com')
                || url.contains('maven.google.com')
                || url.contains('plugins.gradle.org/m2')
                || url.contains('repo.spring.io/libs-milestone')
                || url.contains('repo.spring.io/plugins-release')
                || url.contains('repo.grails.org/grails/core')
                || url.contains('repository.apache.org/snapshots')
            ) {
                println "gradle init: [buildscript.repositories] (${repo.name}: ${repo.url}) removed"
                remove repo
            }
        }
    }

    // Tencent Cloud aggregate maven mirror: central, jcenter, google, and gradle-plugin
    maven { url 'https://mirrors.cloud.tencent.com/nexus/repository/maven-public/' }
    maven { url 'https://maven.aliyun.com/repository/central' }
    maven { url 'https://maven.aliyun.com/repository/jcenter' }
    maven { url 'https://maven.aliyun.com/repository/google' }
    maven { url 'https://maven.aliyun.com/repository/gradle-plugin' }
    maven { url 'https://maven.aliyun.com/repository/spring' }
    maven { url 'https://maven.aliyun.com/repository/spring-plugin' }
    maven { url 'https://maven.aliyun.com/repository/grails-core' }
    maven { url 'https://maven.aliyun.com/repository/apache-snapshots' }
}

allprojects {
    buildscript {
        repositories repoConfig
    }

    repositories repoConfig
}
```

### [Private artifact repository](#private)

To use a private Maven repository, you need to first retrieve the username and password. 

#### gradle.properties

Add the repository URL and username and password to the `gradle.properties` file in the same directory as `build.gradle`:

```ini
codingArtifactsMavenUrl=https://codes-farm-maven.pkg.coding.net/repository/share/build/
codingArtifactsUsername=Not required
codingArtifactsPassword=Not required
```

#### build.gradle

```groovy
repositories {
    maven {
        url codingArtifactsMavenUrl
        credentials {
            username = codingArtifactsUsername
            password = codingArtifactsPassword
        }
    }
}

dependencies {
    implementation 'com.tencent:cloudpay:1.6'
    implementation '[GROUP_ID]:[ARTIFACT_ID]:[VERSION]'
}
```

#### [Local build](#local-build)

Input the username and password as parameters in the build command:

```shell
./gradlew build -Dorg.gradle.project.codingArtifactsUsername=foo -Dorg.gradle.project.codingArtifactsPassword=bar
```

#### [Continuous integration build](#Jenkins)

Enter the username and password in the environment variables:

![](https://qcloudimg.tencent-cloud.cn/raw/d816b901437777ba681d82b03455e910.png)

```shell
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
        sh "./gradlew build -Dorg.gradle.project.codingArtifactsUsername=$CODING_ARTIFACTS_USERNAME -Dorg.gradle.project.codingArtifactsPassword=$CODING_ARTIFACTS_PASSWORD"
      }
    }
  }
}
```

==== 2020/08/21 ====
