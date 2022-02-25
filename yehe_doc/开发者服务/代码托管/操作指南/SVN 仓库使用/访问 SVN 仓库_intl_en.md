The SVN repository service currently supports most mainstream SVN clients. We recommend you use the latest stable version of the client.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, select **Code Repositories**.
4. If Code Repositories is not shown on the left, the project admin needs to go to **Project Settings** > **Projects and Members** > **Functions** to enable the relevant function.

## Mac Environment
In a Mac environment, you can use Homebrew to install the SVN client.

1.  Run the following command to install Homebrew:
<dx-codeblock>
:::  curl
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
:::
</dx-codeblock>
2. After you install Homebrew, input the following command in your terminal to install SVN:
<dx-codeblock>
:::  curl
brew install subversion
:::
</dx-codeblock>
3. Run the `svn --version` command to verify that SVN has been correctly installed:
<dx-codeblock>
:::  shell
svn, version 1.9.7 (r1800392)
compiled Feb 28 2018, 15:54:50 on x86_64-apple-darwin17.3.0
Copyright (C) 2017 The Apache Software Foundation.
This software consists of contributions made by many people;
see the NOTICE file for more information.
Subversion is open source software, see http://subversion.apache.org/
The following repository access (RA) modules are available:

* ra_svn : Module for accessing a repository using the svn network protocol.
- with Cyrus SASL authentication
- handles 'svn' scheme
* ra_local : Module for accessing a repository on local disk.
- handles 'file' scheme
* ra_serf : Module for accessing a repository via WebDAV protocol using serf.
- using serf 1.3.9 (compiled with 1.3.9)
- handles 'http' scheme
- handles 'https' scheme
The following authentication credential caches are available:
* Plaintext cache in /Users/Liwenqiu/.subversion
* Mac OS X Keychain
:::
</dx-codeblock>
4. Run the command `svn checkout svn://subversion.e.coding.net/example/example-project` (replacing the URL with your SVN repository URL) to check out the SVN repository:
![](https://qcloudimg.tencent-cloud.cn/raw/1274622a4cdac2a0420bb584b2046641.png)
5. Then, you can use the `add` and `commit` commands to add content to the repository:
![](https://qcloudimg.tencent-cloud.cn/raw/8236fc8708588e94be3587d7adfff834.png)
6. In addition to using SVN protocol, you can use `svn+ssh` protocol to access the repository, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/72787c591d71f0d22756c4b82c652394.png)

## Cornerstone Tool
You can use SVN repositories through Cornerstone.
1. Open Cornerstone and click Add Repository to add an SVN repository reference (replacing the URL with your SVN repository URL):
![](https://qcloudimg.tencent-cloud.cn/raw/a981abfaca7eac488508cce5f29f3835.png)
Then, you can view the repository content.
![](https://qcloudimg.tencent-cloud.cn/raw/9f97ad882b1eb2d93ec79258b3202a7c.png)
2. Use `Check Out` to check out the repository, edit the files, and use `Commit` to commit the changes, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/1d8e741305eb3f20e4489dbf95627f6d.png)

## Windows Environment
In Windows, we recommend you use TortoiseSVN.
1. After [downloading](https://tortoisesvn.net/downloads.html) and installing the tool, right-click on any file directory.
![](https://qcloudimg.tencent-cloud.cn/raw/51048cbbfe7c3a7a7ccaff2251678ddd.png)
Select `Checkout` to check out the SVN repository (replace the URL with your SVN repository URL).
![](https://qcloudimg.tencent-cloud.cn/raw/082024fc1daffb9695b6096c5c0f1de9.png)
2. The first time you use `Checkout`, you must enter your username and password. Select `Save authentication` to save the authentication information so you will not have to enter your password next time.
![](https://qcloudimg.tencent-cloud.cn/raw/8f8bde285ecc5a46bbe31ccb723a2484.png)
3. Open the checked-out folder and create a `README.md` file.
![](https://qcloudimg.tencent-cloud.cn/raw/6bdd2488cce1c0dfb4f7a88e66afcc2e.png)
Right-click on a blank space and select `SVN commit...` to save the new file to the version repository:
![](https://qcloudimg.tencent-cloud.cn/raw/d494de1ddd16038b3f3544859e52e78e.png)

## Linux Environment
On a Linux system, you can use the system's package management tool to install SVN.

### Install with yum in Fedora
<dx-codeblock>
:::  shell
$ sudo yum install subversion
:::
</dx-codeblock>

### Install with apt-get in Ubuntu or Debian
<dx-codeblock>
:::  shell
$ sudo apt-get install subversion
:::
</dx-codeblock>

After installation, use `svn checkout / commit` to access the SVN repository.
>?This method is similar to the command line used in Mac systems.

#### "Negotiate authentication mechanism" error when using the SVN command line in Ubuntu
You may see the following error when using the SVN command-line client in Ubuntu:
<dx-codeblock>
:::  svn
svn: E210007: Cannot negotiate authentication mechanism
:::
</dx-codeblock>
This occurs because the SVN authentication process uses the SASL library, so you need to run the following command to install the dependent library required to use SASL authentication:
<dx-codeblock>
:::  shell
$ sudo apt-get install cyrus-sasl2-dbg
:::
</dx-codeblock>