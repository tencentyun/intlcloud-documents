### I don't have bash in my container.

In this case, you can enter the command you want to run in the command line, and the result of the command will be displayed on the screen. You can regard the command line as a lite edition of bash without functions such as autocomplete. We recommend running the bash installation command before proceeding.

### Why is the software installation so slow when I run "apt-get"?

This might be due to network issues. Please try the following to speed up.

#### Ubuntu 16.04

For containers on Ubuntu 16.04, you can copy and run the following command to configure the apt source as a Tencent Cloud source server.
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

For containers on CentOS 7, you can modify the source address directly to speed up the installation by following the steps below:
1. Copy and run the following code:
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
2. Run the following command to empty and rebuild the YUM cache.
```
yum clean all && yum clean metadata && yum clean dbcache && yum makecache
```

Directly modifying the source address is a temporary solution. When the container is rescheduled, your changes will become invalid. Therefore, we recommend solving this issue when creating the image as instructed below:
Modify the Dockerfile used to create the container image.
Modify the source address in the RUN field of the Dockerfile according to the system. For example, if the image is on Ubuntu, add the following:
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

You can do it in a similar way for images on CentOS.

### I didn’t find tools such as vim or netstat after I logged in to a container.

You can download the required tools by running commands such as `apt-get install vim` and `net-tools` (`yum install vim` on CentOS).

### The system prompted that no tool was found when I run the apt-get install command.

You can install the software as follows:
1. Run the following command to update the software list.
```
apt-get update
```
2. Run the following command to install the software (run `yum updateinfo` on CentOS).
```
apt-get install
```

### How do I use an in-house tool in a container?

Enter the remote terminal page, click “File Assistant” at the bottom right and upload your tool. 

### How do I copy a live file such as dump or log for local analysis?

Enter the remote terminal page, click “File Assistant” and download files. 

### Why can't I upload a file to a container or download a file to the local system?

That is probably because the tar program is not installed in your container image. You can install it by running `apt-get install vim` or `net-tools` (`yum install vim` on CentOS) and try again.

### Why can’t I find tools that I installed previously?

When Kubernetes re-schedules your container, it will pull an image to create a new container. Tools that do not exist in the image will not be in the new container. We recommend installing some common troubleshooting tools when making images.

### How do I copy text in the console?

Simply select and copy the text.

### How do I paste the copied text?

Press Shift + Insert to paste the copied text.

### Why is the connection broken?

This might have happened if you modified the container status by performing actions on the container/CVM in other related products or services. This might also have happened if the page has been idle for 3 minutes or longer. In both cases the server will terminate the connection.

### What if I receive the error "TERM environment variable not set" when I run commands such as "top"?

Run "export TERM linux".

### Why does the bash prompt only display "<" and a part of the path when I enter a directory with a long absolute path?

That is because the bash prompt is set to display "username@hostnamecurrentdirectory" by default. If the current path is too long, bash will only display "<" and the last part of the path by default.
