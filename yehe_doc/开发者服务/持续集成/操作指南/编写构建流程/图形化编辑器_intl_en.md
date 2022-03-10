---
title: Graphical Editor - CODING Help Center
pageTitle: Graphical Editor
pagePrevTitle: Process Configuration Details
pagePrev: ci/process/detail.html
pageNextTitle: Trigger Rules
pageNext: ci/configuration/trigger.html
alias:
- devops/ci/visualeditor.html
- ci/visualeditor.html
- ci/visual-editor.html
---

### [Function Overview](#intro)

Editing a Jenkinsfile (a file that describes a build process) using a command-line editor is the most basic mode of human-computer interaction. Based on its core text editing function, CODING has been designed with an innovative graphical editor that is compatible with most custom command-line operations. Enjoy an intuitive WYSIWYG editing experience as you can view while building.

To access the function, go to "Build Plan Settings" > "Process Configuration".

![](https://qcloudimg.tencent-cloud.cn/raw/9aedee8c8b388db1be8a9c246c099de1.png)

### [Build Process Concepts](#ci-concept)

In essence, both graphical and text editors allow users to view and edit the core of the build process—the Jenkinsfile (a file that describes the process). Before we go into the details of editors, let's take a look at a few important concepts concerning the "file that describes the process".

> This document focuses on the syntax rules for declarative files.

#### [Pipeline](#pipeline)

A `pipeline` is a customizable working model that defines an entire process for delivering software. In general, it includes build, test, and deployment phases.

#### [Execution Environment](#agent)

The execution environment describes the execution environment of the entire process or a certain `stage` of executing a `pipeline`. It must appear in the top grid of a `descriptive file` or at every `stage`.

| Required?   | Yes                                         |
| ---------- | ------------------------------------------ |
| Parameter list   | See below                                     |
| Permitted location | Must appear in the top grid of a `descriptive file` or at every stage |

#### [Stage](#stage) 

A `stage` defines a series of closely related `steps`. Each `stage`, such as the "build stage", the "test stage", or the "deployment stage", undertakes an independent, clear responsibility in an entire pipeline. Generally, all actual build processes are provided in stages.

| Required?   | At least one                                         |
| ---------- | ------------------------------------------ |
| Parameter list   | A required string parameter that specifies the name of a stage |
| Permitted location | In the `stage` block                  |

#### [Stage List](#stages) 

The `stage list` includes a series of `stages`. A `stage list` will include at least one `stage`. A `pipeline` must have and only have one `stage list`.

| Required?   | Yes                                    |
| ---------- | ------------------------------------- |
| Parameter list   | None                                    |
| Permitted location | Can only appear once in the `pipeline` |

#### [Step List](#steps)

The `step list` describes what to do at a `stage` and what specific commands to run. For example, a `step` needs the system to print a "Building" message and run the command `echo 'building...'`.

| Required?   | Yes                           |
| ---------- | ---------------------------- |
| Parameter list   | None                           |
| Permitted location | In every `stage` block |

#### [Parallel](#parallel)

"Parallel" is used to declare some `stages` executed in parallel to accelerate the execution speed, especially when a `stage` and another `stage` are independent of each other. Take note that you cannot set the `execution environment` for any `stage` with a `parallel` block.

![](https://qcloudimg.tencent-cloud.cn/raw/f648557d4a333171959bd6158716b0bb.png)

#### [Sample File](#example)

```groovy
pipeline {
  agent any
  stages {
    stage('check out') {
      steps {
        sh 'ci-init'
        checkout([$class: 'GitSCM', branches: [[name: env.GIT_BUILD_REF]], 
                                    userRemoteConfigs: [[url: env.GIT_REPO_URL]]])
      }
    }
    stage('build') {
      steps {
        echo 'building...'
        sh 'make'
        echo 'build complete.'
      }
    }
    stage('Test') {
      steps {
        echo 'unit testing...'
        sh 'make check'
        junit 'reports/**/*.xml' 
        echo 'unit testing complete.'
      }
    }
    stage('deploy') {
      steps {
        echo 'deploying...'
        sh 'make publish'
        echo 'deployment complete'
      }
    }
  }
}
```

### Switching Between Editors

In essence, the graphical editor is preset code, allowing you to switch seamlessly to the text editor. However, you cannot switch from the text editor to the graphical editor. Code added or deleted in the text editor must pass a "rule check" before it can be converted into an editable view.

![](https://qcloudimg.tencent-cloud.cn/raw/f7d75ccd3885d18f4f3b1a125d189484.png)

The text editor supports a wider range of custom operations than the graphical editor. As the graphical editor is preset with numerous commonly used steps, you can use it for pattern-based and standardized work. The text editor has no limitations and only requires conformance to Jenkins syntax, lending itself to specific and special tasks.

==== 2020/09/07 ====
