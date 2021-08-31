### What should I do if there is no bash in the container?

If there is no bash in the container, enter the command you want to run in the command line. The result of the command is then displayed on the screen. You can consider the command line as a simplified bash without certain features such as autocomplete. We recommend that you run the bash installation command before proceeding.

### Why is software installation using `apt-get` so slow?
When software installation using `apt-get` takes up too much time, this may be due to slow server access to software sources outside China. We provide acceleration solutions for containers with different operating systems. You can select a solution when required.

#### Precautions
Before selecting the acceleration solution, check the operating system of the container as instructed below: 
 - Ubuntu: run `cat /etc/lsb-release` to check if the `/etc/lsb-release` file exists.
 - CentOS: run `cat /etc/redhat-release` to check if the `/etc/redhat-release` file exists.
 - Debian: run `cat /etc/debian_version` to check if the `/etc/debian_version` file exists.

#### Solutions<span id="solve"></span>

#### Ubuntu 16.04
For containers running Ubuntu 16.04, run the following commands on your terminal to set the apt source to a Tencent Cloud source server:
```shell
cat << ENDOF > /etc/apt/sources.list
deb http://mirrors.tencentyun.com/ubuntu/ xenial main restricted universe multiverse
deb http://mirrors.tencentyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://mirrors.tencentyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-updates main restricted universe multiverse
ENDOF
```

#### CentOS 7

For containers running CentOS 7, directly change the source address as instructed below to speed up the installation:
1. Copy and run the following code in the container:
```shell
cat << ENDOF > /etc/yum.repos.d/CentOS-Base.repo
[os]
name=Qcloud centos os - \$basearch
baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/os/\$basearch/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
[updates]
name=Qcloud centos updates - \$basearch
baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/updates/\$basearch/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
#[centosplus]
#name=Qcloud centosplus - \$basearch
#baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/centosplus/\$basearch/
#enabled=1
#gpgcheck=1
#gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
#[cloud]
#name=Qcloud centos contrib - \$basearch
#baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/cloud/$basearch/openstack-kilo/
#enabled=1
#gpgcheck=1
#gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
#[cr]
#name=Qcloud centos cr - \$basearch
#baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/cr/\$basearch/
#enabled=1
#gpgcheck=1
#gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
[extras]
name=Qcloud centos extras - \$basearch
baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/extras/\$basearch/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
#[fasttrack]
#name=Qcloud centos fasttrack - \basearch
#baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/fasttrack/\$basearch/
#enabled=1
#gpgcheck=1
#gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
ENDOF
```
2. Run the following command to clear and rebuild the YUM cache.
```
yum clean all && yum clean metadata && yum clean dbcache && yum makecache
```

##### Debian

For containers running Debian, run the following commands on your terminal to set the apt source to a Tencent Cloud source server:
```shell
cat << ENDOF > /etc/apt/sources.list
deb http://mirrors.tencentyun.com/debian stretch main contrib non-free
deb http://mirrors.tencentyun.com/debian stretch-updates main contrib non-free
deb http://mirrors.tencentyun.com/debian-security stretch/updates main

deb-src http://mirrors.tencentyun.com/debian stretch main contrib non-free
deb-src http://mirrors.tencentyun.com/debian stretch-updates main contrib non-free
deb-src http://mirrors.tencentyun.com/debian-security stretch/updates main
ENDOF
```

#### Conclusion

Changing the source address in the container directly is an interim solution. When the container is rescheduled, your change becomes invalid. Therefore, we recommend that you solve this problem with the following method when creating the image:

Add the source address provided in [Solutions](#solve) for corresponding operating systems to the `RUN` field of the Dockerfile file for creating the container image. For example, append the following code to the Dockerfile file for an image running the Ubuntu operating system:
```shell
RUN cat << ENDOF > /etc/apt/sources.list
deb http://mirrors.tencentyun.com/ubuntu/ xenial main restricted universe multiverse
deb http://mirrors.tencentyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://mirrors.tencentyun.com/ubuntu/ xenial-updates main restricted universe multiverse
#deb http://mirrors.tencentyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
#deb http://mirrors.tencentyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-updates main restricted universe multiverse
#deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
#deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-backports main restricted universe multiverse
ENDOF
```



### What should I do if I cannot find tools such as vim and netstat after logging in to a container?

Download the required tools by running commands such as `apt-get install vim` and `apt-get install net-tools` (run `yum install vim` on CentOS.)

### What should I do if a tool cannot be found when I run the `apt-get install` command?

Install the software program as follows:
1. Run the following command to update the software list.
```
apt-get update
```
2. Run the following command to install the software program (run `yum updateinfo` on CentOS.)
```
apt-get install
```

### How do I use an in-house tool in a container?

Go to the remote terminal page, click "File Assistant" in the lower-right corner, and upload your tool.

### How do I upload a live file such as dump or log for local analysis?

Go to the remote terminal page, click "File Assistant" in the lower-right corner, and upload your file.

### Why can’t I upload a file to a container or download a file to the local system?

This issue occurs if the tar program is not included in your container image. To correct it, you can install the tar program by running `apt-get install vim` or `apt-get install net-tools` (run `yum install vim` on CentOS) and try again.

### Why can’t I find the tools that I installed previously?

When Kubernetes re-schedules your container, it pulls an image to create a new container, and tools that are not in the image will not be installed in the new container. Therefore, we recommend that you install some common troubleshooting tools when creating the image.

### How do I copy text in the console?

You can copy text by highlighting and copying it.

### How do I paste the copied text?

Press Shift+Insert to paste the copied text.

### Why is the connection lost?

This happens when you perform some operations on the container or CVM on another page that modify the container status, or when the current page remains idle for more than 3 minutes. In both cases, the server disconnects the connection.

### What should I do if the "TERM environment variable not set" error occurs when I run commands such as `top`?

Run `export TERM linux`.

### Why does the bash prompt display only "<" and part of the path when I enter a directory with a long absolute path?

The bash prompt is set to display "<Username>@<Host name> <Current directory>" by default. If the current path is too long, bash displays only "<" and the last part of the path by default.

