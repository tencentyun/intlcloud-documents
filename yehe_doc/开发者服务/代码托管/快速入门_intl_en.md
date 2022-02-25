## Operational Scenarios
CODING Code Repository (CODING-CR) is based on the Git open-source version control system. With Git, your local computer and CODING each have a complete code repository, so both can engage in distributed version management. To manage code on your local computer, you must first download, install, and set up Git. If you don't need to manage code on your local computer, CODING allows you to perform most code repository operations in your browser. This document explains how to get started with CODING-CR.


## Prerequisites
Before using CODING_CR, you must activate the CODING DevOps service for your Tencent Cloud account. Follow the pop-up prompts to go to **Personal Settings** and enter your email, password, and mobile number. You will use this information when performing subsequent operations, such as code cloning or push.

## Local Environment Initialization

### Install Git

#### Windows

1. Download Git from the [Git website](https://git-scm.com/downloads) and follow the prompts to install it. We recommend using the default options.
2. After installation, right-click to open Git Bash and get started with Git.

#### Linux

On a Linux system, you can use the system's package management tool to directly install the pre-compiled Git binary installation package.


- On a Fedora/Centos system, use yum to install Git: `yum install git-core`.
- On a Ubuntu/Debian system, use apt-get to install Git: `apt-get install git`.

#### macOS

1. Run the following command to install the package management tool [Homebrew](https://raw.githubusercontent.com/Homebrew/install/master/install).
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

>? If an error occurs, see [Open Source Repositories](https://gitee.com/cunkai/HomebrewCN/blob/master/README.md) and download from a domestic source.

2. After Homebrew is installed, enter `brew install git` to install Git.
3. After Git is installed, run `git --version` to check your current Git version.

### Local environment initialization[](id:git-init)

After Git is installed, create a folder, open the folder, and enter `git init` to initialize the local environment.
![](https://main.qcloudimg.com/raw/02780e09b68633ea13bae8fa7eb75c02.png)

### Set user information[](id:user-config)

After Git is installed, you should immediately set a committer name and email address, which will be used to create a record for each commit. Use the following command to set user information.

```shell
$ git config --global user.name "Your name"
$ git config --global user.email "Your email"
```

For example, if your CODING account is named **Dahei** and your Git user information is: **name – Dabai** and **Email – dabai@coding.net**, when your code is pushed to your CODING repository, the status is displayed as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/a63e9f0cb83bf866463f8d7ed67f8220.png)

>? You can configure custom user information in Git. We recommend you directly use the username and email address of your CODING account for efficient collaboration.

## Create a CODING Code Repository[](id:remote-repo)

1. Open any project and click **Code Repositories** on the left navigation bar to open the Code Repository Management page, where you can create or open a code repository.
![](https://qcloudimg.tencent-cloud.cn/raw/fe9ae36021ee13c152a030c2b28c2fc9.png)
2. If the code repository entry is not displayed, a project admin must open the project, click **Project Settings** in the lower-left corner, and go to **Project and Members** > **Functions** to enable the code repository function.
![](https://qcloudimg.tencent-cloud.cn/raw/33eef2d664098f563993e6b3e151807e.png)

## Push and Pull Code[](id:push-pull)

This section will demonstrate how to pull code from and push code to remote repositories to facilitate cloud-based coding.

### Pull code from remote repository[](id:pull)

After initializing a local code repository, you can open the terminal in a folder and run the `git clone + repository address` command to pull code.
![](https://qcloudimg.tencent-cloud.cn/raw/858828b7bf6446de0664996871f454c9.png)

When pulling for the first time, you must enter your credentials. Enter the email and password you used to register a CODING account. You can also open the dropdown menu in the upper-right corner and go to **Personal Account Settings** to modify your credential information.
![](https://qcloudimg.tencent-cloud.cn/raw/a4148dc6c01695af8cbcb37bac9179b2.png)

When the operation is successful, you can modify the code in your local code repository.
![](https://qcloudimg.tencent-cloud.cn/raw/869eb179777442c425e33673b9186fae.png)

### Edit files[](id:edit)

In a folder, create the `readme.txt` and `learn-git.txt` files. In one of the files, write `I'm learning git.` (or customize as needed) and save it.

### Flowchart[](id:map)

Before committing code, you can refer to this flowchart to understand the status lifecycle Git uses when tracking files.
![](https://qcloudimg.tencent-cloud.cn/raw/8a64c6421d8c4fc2f9fc6705d07d30e5.png)


### Track files (git add)[](id:git-add)

After creating or editing a file, run the `git add` command to add the file to the staging area (Index Stage) of the local Git repository.

Command to **track a specific file**:

```shell
git add readme.txt
```

Command to **add multiple files**:

```shell
git add readme.txt learn_git.txt
```

To track **all files** at once, you can directly enter `git add` in the terminal. 

### Commit files (git commit)[](id:git-commit)

After files to commit are added to the staging area, run `git commit` to commit the files to the local repository. This command commits all files in the staging area:

```shell
git commit -m "wrote a readme and a learn_git file"
```

![](https://main.qcloudimg.com/raw/a798f400fa32cde0352c8593071bebdd.png)

The content enclosed in quotes following `-m` is your commit description. The following lines are the result returned. Make sure that you add a change description to each commit to provide a clear description of what changes were committed.

In addition to the `git commit` command, you can also use the standard plugin to standardize commit messages in the repository for easy backtracking.

```bash

// Step 1: Install yarn

brew install yarn

// Step 2: Install plugin

yarn add -D standard-version

// Step 3: Commit code with the plugin

git cz
```

**Associate issues automatically**

When you commit code, `# Issue ID` is included in the commit message. You can also directly associate issues in the project.

If the [Development Convention](https://help.coding.net/docs/repo/config/spec.html) function is enabled for this repository and a commit convention (such as check associated issues) is specified in the [Branch Convention](https://help.coding.net/docs/repo/config/spec.html#branch-spec), make sure issues of the corresponding type are associated in the commit message. Otherwise, this branch will violate the convention.


For example, for an issue (requirement) with the ID 630, add `#630` in the commit message to automatically associate the requirement. Add `project-1#630` to associate issue 630 in `project-1`.


### View file status (git status)[](id:git-status)

If you are not sure that Git is precisely tracking file changes and want to confirm the file status, use the `git status` command to see the file status.

- **If no files are tracked in the current repository**, the result returned is as follows:
<dx-codeblock>
:::  bash
$ git status
On branch master
Your branch is up-to-date with 'origin/master'
nothing to commit, working directory clean
:::
</dx-codeblock>
- **If a file has changed but the changes were not tracked**, the result returned is as follows:
![](https://main.qcloudimg.com/raw/736337385dc67fea3189bd51a590a813.png)
Run `git add` to track the file. After successful tracking, the font color will change from red to green.
- **When a file has been tracked and already committed to the repository**, the result returned is as follows:
![](https://main.qcloudimg.com/raw/ed38b46b8758663a41a2f3ba26b2b4cf.png)

### Push files to remote repository (git push)[](id:git-push)

On the terminal, run the command:

```shell
git push
```

To automatically create a merge request and associate issues upon commit, use the following command:

```bash
git push origin local-branch:mr/target-branch/local-branch
```

The `git push` is the push command. It pushes the local branch to the remote repository, which is equivalent to creating a remote backup. Go to the CODING code repository to view pushed files. If multiple people collaborate in maintaining the remote repository, you need to run the `git pull` command to synchronize your local repository with the remote repository to get any code committed by other users.

## View and Edit Remote Repositories[](id:view-modify)

After a file is pushed to the CODING code repository, you can edit, save, and commit code on the webpage. Let's take the `README.md` file as an example. After editing and committing the changes, you can add a simple description of the modified content. If you do not add a description, the default commit description is "File xxx updated".

![](https://qcloudimg.tencent-cloud.cn/raw/9f0065c189843a0036e500afea6ff4d8.png)
