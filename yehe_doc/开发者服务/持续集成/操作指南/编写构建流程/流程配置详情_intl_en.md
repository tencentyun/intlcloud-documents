---
title: Process Configuration Details - CODING Help Center
pageTitle: Process Configuration Details
pagePrevTitle: Text Editor
pagePrev: ci/process/text.html
pageNextTitle: Graphical Editor
pageNext: ci/process/visual-editor.html
alias: process/detail.html
---

This document provides you a guidance on compiling a build process and describes parameters in each step.

### Code repositories

#### Git

Checks out source code from a Git repository in the current project. This command is a simpler version of the checkout command.

Parameter list:

- Git URL `url`: string
- Branch `branch`: string
- Change log `changelog`: string
- Identity authentication ID `credentialsId`: string
- Poll `poll`: boolean

#### Check out from version control

Universally checks out SCM code (Git or SVN).

This step returns content in a map format. If you are using Git, you could use the following:

```groovy
def scmVars = checkout scm
def commitHash = scmVars.GIT_COMMIT
// or
def commitHash = checkout(scm).GIT_COMMIT
```

The parameter scm is an object that allows the SCM type to be configured, such as the following:

- GitSCM example:

  ```groovy
  checkout([$class: 'GitSCM', branches: [[name: env.GIT_BUILD_REF]],
                userRemoteConfigs: [[url: env.GIT_REPO_URL]]])
  ```

  userRemoteConfigs parameter list:

- `url`: string
- `name`: string, name of a remote repository such as "origin"
- `refspec`: string, for more information, see [Git Internals - The Refspec](https://git-scm.com/book/zh/v2/Git-内部原理-引用规格).
- `branches`: array of objects (optional)
- `changelog`: boolean (optional)
- `credentialsId`: string (optional)
- `doGenerateSubmoduleConfigurations`: boolean (optional)
- `submoduleCfg`: array (optional)

- SubversionSCM: Checks out code from an SVN server. Example:

  ```groovy
  checkout([$class: 'SubversionSCM', remote: 'http://sv-server/repository/trunk']]])
  ```

  Parameter list:

- `locations`: array of objects
- `remote`: string
- `credentialsId`: string
- `local`: string, specifies a local directory (relative to the workspace) as the location of code to be checked out
- `depthOption`: string. Corresponds to --depth. The default value is unlimited. [Learn More](http://svnbook.red-bean.com/en/1.7/svn.advanced.sparsedirs.html).
- `ignoreExternalsOption`: boolean

### Build process

#### Subnodes

Parameter list:

- `label`: string, environment label name such as java-8

#### Collect artifacts

Collects build results (such as jar, war, or apk). Note that the artifacts collected are saved and deleted along with the build history. This is just a temporary storage space. We recommend using "Artifact Management" for version management of build results.

Parameter list:

- `artifacts`: string, you can use the wildcard * to specify the path pattern of files in the workspace to be collected while keeping to the [Apache Ant Path Rules](http://ant.apache.org/manual/Types/fileset.html)
- `allowEmptyArchive`: boolean (optional). Generally, this command results in "Building Failed" if no file appropriate to the collection pattern is found. If this parameter is set to "true", a build process returns a warning if there are no artifacts, instead of a failure result.
- `caseSensitive`: boolean (optional). By default, file path rules are case-sensitive. If this parameter is set to "false", the rules are non-case-sensitive.
- `defaultExcludes`: boolean (optional)
- `excludes`: boolean (optional), you can exclude certain files when setting the path pattern while keeping to the [Apache Ant Path Rules](http://ant.apache.org/manual/Types/fileset.html)
- `fingerprint`: boolean (optional), file hashes are also calculated during collection
- `onlyIfSuccessful`: boolean (optional), only collected when "Build successful" is returned

#### Execute shell script

Executes a shell script.

Example:

```groovy
pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                echo 'Hello World'
                sh 'ls -al'
            }
        }
    }
}
```

#### Collect JUnit test reports

Collects JUnit and TestNG test reports (in XML). You can specify the XML files to be collected using `**/build/test-reports/*.xml`, for example. Do not include XML files that are not reports. You can use commas to separate multiple rules.

Parameter list:

- `testResults`: string
- `allowEmptyResults`: boolean (optional), "file does not exist" or "file is empty" is allowed
- `keepLongStdio`: boolean (optional), all test logs, including those of passed test cases, are kept

### Others

#### Change directory substep

Changes directory substeps. You can fill in some substeps in the "dir" block, which will be run in the specified directory path.

Parameter list:

- `path`: string

#### Sleep

Pauses for a period of time until the set due time. Similar to `sleep xxx` in Unix.

Parameter list:

- `time`: int
- `unit`: Select one from `NANOSECONDS, MICROSECONDS, MILLISECONDS, SECONDS, MINUTES, HOURS, and DAYS`.

#### Error

Sends an error signal. Used when you need to partially terminate an execution process. You can also use throw new Exception(), but the exception stack printed is shorter if you use "error".

Parameter list:

- `message`: string

#### Current directory

Returns the current directory path as a string.

Parameter list:

- `tmp`: boolean (optional). This parameter returns a temporary directory associated with the workspace. Generally, it is used when you need to store some temporary files without confusing the workspace directory.

#### Write file

Writes the specified content into a file.

Parameter list:

- `file`: string
- `text`: string
- `encoding`: string. File encoding. If left empty, the default encoding in the current run environment is used. In the case of a binary file, a base-64-encoded result is returned.

#### Read file

Reads a file from a relative path and returns the file content as a string.

Parameter list:

- `file`: string, path address relative to the workspace directory
- *encoding*: string. File encoding. If left empty, the default encoding in the current run environment is used. In the case of a binary file, a base-64-encoded result is returned.

#### Retry substep

Retries the specified block until the set maximum number of retries is reached. Stops retrying if the execution process ends normally. Keeps retrying until the set maximum number of retries is reached if an exception occurs in the execution process. The build process terminates if an exception occurs during the last try.

Parameter list:

- `count`: int

#### Time-limited substep

Executes the process in a block within a limited time. When the time is up, the exception `org.jenkinsci.plugins.workflow.steps.FlowInterruptedException` is returned. The optional unit parameter is minutes by default.

Parameter list:

- `time`: int
- `activity`: boolean. Time is calculated when there is no new content in the log rather than based on an absolute execution time.
- `unit`: Select one from `NANOSECONDS, MICROSECONDS, MILLISECONDS, SECONDS, MINUTES, HOURS, and DAYS`.

#### Catch error in substep

Catches errors in the specified substep.

#### Timed substep

Records the execution time of the specified substep in the form of a Unix timestamp.

#### Loop substep

Loops the execution of the specified substep for the designated number of times.

#### Conditional loop substep

Loops the execution of the specified substep until the substep returns "true".

#### Print information

Prints information in the log.

Parameter list:

- `message`: string

#### Run arbitrary pipeline script

Runs an arbitrary pipeline script.

#### Run Groovy source file

Runs a Groovy source file in this location during the build process.

Example:

```groovy
pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                echo 'Hello World'
                load 'test.groovy'
            }
        }
    }
}
```

#### Run yarn audit

Runs a yarn audit in the specified directory. In Continuous Integration, you can see the vulnerabilities found during the yarn dependency audit on the results page.

Parameter list:

- `directory`: string (optional). Fill in the directory location of yarn.lock. Runs in the root directory of the project by default.
- `collectResult`: boolean (optional). Collects yarn audit reports.

#### Run npm audit

Runs an npm audit in the specified directory. In Continuous Integration, you can see the vulnerabilities found during the npm dependency audit on the results page.

Parameter list:

- `directory`: string (optional). Fill in the directory location of package.json. Runs in the root directory of the project by default.
- `collectResult`: boolean (optional). Collects npm audit reports.

#### Merge merge request

Merges code. You can merge the specified merge request.

Parameter list:

- `token`: string, project token
- `depot`: string, repository name
- `mrResourceId`: string, specified resource ID
- `commitMessage`: string, merged commit message template
- `deleteSourceBranch`: boolean (optional), deletes source branch
- `fastForward`: boolean (optional), tries fast-forward merge

#### Merge request comment

Comments on a merge request. You can comment on a specified merge request.

Parameter list:

- `token`: string, project token
- `depot`: string, repository name
- `mrResourceId`: string, specified resource ID
- `commentContent`: string, comment template


==== 2020/08/13 ====
