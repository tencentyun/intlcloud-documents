This document describes how to use the Git Large File Storage (LFS) extension.

## Feature Overview

CODING supports the Git LFS extension. You can use Git LFS to commit large files of any size without occupying Git repository storage space.

## Install

>!The Git LFS plugin requires Git 1.8.5 or later.

**Linux** 

1.  Download the `git-lfs` installation package.
<dx-codeblock>
:::  shell
   curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
:::
</dx-codeblock>
2.  Install `git-lfs`.
<dx-codeblock>
:::  shell
sudo apt-get install git-lfs
:::
</dx-codeblock>
3. Deploy the LFS tool to Git.
<dx-codeblock>
:::  shell
git lfs install
:::
</dx-codeblock>

**Mac**

1.  Install [Homebrew](https://brew.sh).
<dx-codeblock>
:::  shell
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
:::
</dx-codeblock>
2.  Install `git-lfs`.
<dx-codeblock>
:::  shell
brew install git-lfs
:::
</dx-codeblock>
3.  Deploy the LFS tool to Git.
<dx-codeblock>
:::  shell
git lfs install
:::
</dx-codeblock>

**Windows**

1.  Download and install the [Windows installer](https://github.com/github/git-lfs/releases).
2.  Run the Windows installer.
3.  Run `git lfs install` in the command line.

## How to Use

For Git commands, see [Common Git Commands](https://intl.cloud.tencent.com/document/product/1132/44728).

### Track files

Git LFS does not process large files by default. Use the `git lfs track` command to track large files.

**Track a single file**

Use the command `git lfs track "coding.png"` to track the file "coding.png".

**Track files with a specific extension**

Use the command `git lfs track "*.png"` to track files with the ".png" extension. This tracks both existing and future files with the ".png" extension.

**View tracked file patterns**

Run the `git lfs track` command:

```shell
Listing tracked patterns
  *.png (.gitattributes)
```

### Commit large files

You need to commit the ".gitattributes" file to the repository when committing code. After the commit is complete, run the `git lfs ls-files` command to view the tracked LFS file list.

```shell
f05131d24d * cat.png
7db207c488 * dog.png
```

After the code is pushed to the remote repository, tracked LFS files will be shown after "Git LFS":

```shell
$ git push origin master
Git LFS: (2 of 2 files) 12.58 MB / 12.58 MB
Counting objects: 2, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 548 bytes | 0 bytes/s, done.
Total 5 (delta 1), reused 0 (delta 0)
To https://e.coding.net/coding/coding-manual.git
67fcf6a..47b2002  master -> master
```

### Clone a remote repository containing Git LFS files

Use the `git lfs clone` command to clone a remote repository containing "Git LFS" files to a local machine.

```shell
$ git lfs clone https://e.coding.net/coding/coding-manual.git
Cloning into 'coding-manual'
remote: Counting objects: 16, done.
remote: Compressing objects: 100% (12/12), done.
remote: Total 16 (delta 3), reused 9 (delta 1)
Receiving objects: 100% (16/16), done.
Resolving deltas: 100% (3/3), done.
Checking connectivity...done.
Git LFS: (4 of 4 files) 0 B / 100 B
```

>? 
>-To learn more about how to use Git LFS, run the `git lfs help` command.
>-If you need to store files from the original repository in LFS, see the [tutorial](https://github.com/bozaro/git-lfs-migrate).
