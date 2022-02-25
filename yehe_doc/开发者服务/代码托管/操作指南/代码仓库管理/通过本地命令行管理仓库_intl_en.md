This document describes how to use the local command line to manage repositories.

## Open Project
1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, select **Code Repositories**.
4. If Code Repositories is not shown on the left, the project admin needs to go to **Project Settings** > **Projects and Members** > **Functions** to enable the relevant function.

## Get Data from Remote Repository[](id:obtain-data)
You can use the `git clone` command to clone a remote repository to your local device and automatically associate it.

```shell
git clone [remote-name]
```

## Push Data to Remote Repository[](id:push)
Use `git push [remote-name] [branch-name]` to push data from a local repository to a remote repository. For example, `git push learn-git master` will push data from the local repository to the "master" branch of the remote repository.

## Rename Remote Repository[](id:rename)
Use the `git remote rename [old-name] [new-name]` command to modify the local nickname of a remote repository. For example, to change the repository name from `learn-git` to `origin`, run the following code:

```shell
git remote rename learn-git origin
```

After you rename the remote repository, remember to use the new name when you need to specify the repository name in a Git command.

## Disassociate Remote Repository[](id:unlink)
To disassociate the remote repository "origin", run the following command:

```shell
git remote rm origin
```

>!This command disassociates the remote repository from the local repository, and does not delete the remote repository data. For more information about Git commands, see [Common Git Commands](https://intl.cloud.tencent.com/document/product/1132/44728).
