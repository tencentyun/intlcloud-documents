---
title: Environment Variables - CODING Help Center
pageTitle: Environment Variables
pagePrevTitle: Trigger Rules
pagePrev: ci/configuration/trigger.html
pageNextTitle: Build Snapshots
pageNext: ci/configuration/snapshot.html
alias: 
- devops/ci/env.html
- ci/env.html
---

### [Function Overview](#intro)

In a continuous integration process, we may incorporate configurations (such as an account password or version number) into the build process as environment variables. CODING Continuous Integration (CODING-CI) supports environment variables in multiple formats. You can incorporate variables into a build process with the following methods (in order of highest priority to lowest):

- "withEnv" in a Jenkinsfile
- "environment" in a Jenkinsfile
- Startup parameters in a build plan (job)
- Environment variables in a build plan (job)
- Built-in system environment variables during a build process

This document describes these methods in detail.

### [withEnv and environment](#withenv-env)

You can use "environment" to define environment variables in a Jenkinsfile (as follows):

```groovy
pipeline {
    agent any
    environment {
        MY_PROJECT = 'project-1'
        MY_TEAM    = 'team-1'
    }
    stages {
        stage('Build') {
            steps {

                echo "MY_PROJECT is ${MY_PROJECT}"
                echo "MY_TEAM is ${MY_TEAM}"
                // The output is as follows:
                // MY_PROJECT is project-1
                // MY_TEAM is team-1
            }
        }
    }
}
```

In a build process, you may need to use environment variables of the same name at different stages. You can use "withEnv" to set the environment variables for some operations to avoid confusing the global environment variables. Steps executed with "withEnv" will prioritize the set environment variables. Refer to the following example:

```groovy
pipeline {
    agent any
    environment {
        MY_PROJECT = 'project-1'
        MY_TEAM    = 'team-1'
    }
    stages {
        stage('Build') {
            steps {

                echo "MY_PROJECT is ${MY_PROJECT}"
                echo "MY_TEAM is ${MY_TEAM}"
                // The output is as follows:
                // MY_PROJECT is project-1
                // MY_TEAM is team-1

                // Environment variables set with "withEnv" are only valid for steps within the scope and have a higher priority than those set with "environment". 
                withEnv(['MY_PROJECT=project-2']) {

                    echo "MY_PROJECT is ${MY_PROJECT}"
                    echo "MY_TEAM is ${MY_TEAM}"                    
                    // The output is as follows:
                    // MY_PROJECT is project-2
                    // MY_TEAM is team-1

                }
            }
        }
    }
}
```

> For more information, see the [official Jenkins documentation—Using environment variables](https://jenkins.io/zh/doc/pipeline/tour/environment/).

### [Startup parameters in build plans](#start-variable)

Startup parameters are the next most important environment variables. You can select or fill in their values when starting a build plan.

![](https://qcloudimg.tencent-cloud.cn/raw/f119bc47babb245b5d98e90496597683.png)

### [Add environment variable](#add-env)

Besides hardcoding environment variables into a Jenkinsfile, you can also set variables when configuring a build plan. CODING supports four types of environment variables: string, single-selection, multi-selection, and CODING credentials. You can also configure environment variables in a build plan as the default values of the startup parameters.

![](https://qcloudimg.tencent-cloud.cn/raw/eed418d4e132e0e48eb3b8815b670e3f.png)

### [Built-in system environment variables](#default-env)

In CODING-CI build processes, he corresponding environment variables are incorporated to every build task. You can view the list of default environment variables in "Build Snapshot":

![](https://qcloudimg.tencent-cloud.cn/raw/3ff925acee67e2239cd2a78edaa30b83.png)

The environment variables are summarized below by trigger rules (triggered upon code updates, scheduled trigger, or triggered upon merge requests):

| No. | Variable | Description | Triggered upon code updates | Scheduled trigger | Triggered upon merge requests |
| :---: | :----: | :-------: | :----: | :--------: | :------------: |
|1|CREDENTIALS_ID|Private deploy key CredentialsId, for pulling repositories |✅|✅|✅|
|2|DOCKER_REGISTRY_CREDENTIALS_ID|Docker private key CredentialsId (equivalent to CODING_ARTIFACTS_CREDENTIALS_ID)|✅|✅|✅|
|3|CREDENTIALS_ID|Repository private key CredentialsId, for pulling repositories in the project|✅|✅|✅|
|4| GIT_HTTP_URL| Code repository HTTPS URL|✅|✅|✅|
|5| GIT_BUILD_REF| The Git revision number for the build|✅|✅|✅|
|6| GIT_DEPLOY_KEY| Public deploy key of code repositories|✅|✅|✅|
|7| GIT_COMMIT| Revision number of the current version|✅|✅|✅|
|7| GIT_COMMIT_SHORT| First seven digits of the revision number|✅|✅|✅|
|8| GIT_PREVIOUS_COMMIT|Revision number of the last build run No.|✅|✅|✅|
|9| GIT_AUTHOR_EMAIL| Email address of the latest author of this version|✅|✅|✅|
|10| GIT_SSH_URL| SSH URL of the code repository|✅|✅|✅|
|11| GIT_COMMITTER_NAME| Name of the latest committer of this version|✅|✅|✅|
|12| GIT_AUTHOR_NAME| Name of the latest author of this version|✅|✅|✅|
|13| REF| Version to be built|✅|✅|✅|
|14| GIT_PREVIOUS_COMMIT|Revision number of the last successful build run|✅|✅|✅|
|15| GIT_COMMITTER_EMAIL| Email address of the latest committer of this version|✅|✅|✅|
|16| GIT_BRANCH| Branch triggering the build|✅|✅|✅|
|17| GIT_URL| SSH URL of the repository|✅|✅|✅|
|18| GIT_LOCAL_BRANCH/BRANCH_NAME | Local branch name|✅|✅|✅|
|19| FETCH_REF_SPECS| refs to be checked out by git|✅|✅|✅|
|20| GIT_REPO_URL| SSH URL of the repository|✅|✅|✅|
|21| JOB_ID| Build plan ID|✅|✅|✅|
|22| JOB_NAME| Build plan name|✅|✅|✅|
|23| CI_BUILD_NUMBER| Build No.|✅|✅|✅|
|24| PROJECT_ID| Project ID|✅|✅|✅|
|25| PROJECT_NAME| Project name|✅|✅|✅|
|26| PROJECT_WEB_URL| Project website URL|✅|✅|✅|
|27| PROJECT_API_URL| URL of project's backend API|✅|✅|✅|
|28| PROJECT_TOKEN| Project token password, for reading the project|✅|✅|✅|
|29| PROJECT_TOKEN_GK| Project token user|✅|✅|✅|
|30| GIT_TAG| Git tag triggering the build (only applicable when building with tags)|✅|||
|31| DEPOT_NAME| Current code repository name|✅|||
|32| CCI_CURRENT_PROJECT_COMMON_CREDENTIALS_ID (soon to be released)| Built-in project token's CredentialsId|✅|||
|33| CCI_CURRENT_TEAM (soon to be released)| Company name for the current build environment, such as "myteam" in myteam.coding.net|✅|||
|34| CCI_CURRENT_DOMAIN (soon to be released)| Domain name of the current build environment, such as "coding.net" in myteam.coding.net|✅|||
|35| MR_RESOURCE_ID| Merge request ID|||✅|
|36| MR_TARGET_BRANCH|Target branch of the merge request|||✅|
|37| MR_TARGET_SHA| Version number of the target branch of the merge request|||✅|
|38| MR_MERGED_SHA| Simulated merged version number|||✅|
|39| MR_SOURCE_BRANCH| Source branch of the merge request|||✅|
|40| MR_STATUS| Status of the merge request|||✅|
|41| MR_SOURCE_SHA| Version number of the source branch of the merge request|||✅|

==== 2020/10/14 ====
