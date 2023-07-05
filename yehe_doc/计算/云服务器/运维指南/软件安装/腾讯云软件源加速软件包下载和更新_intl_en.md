## Overview

To solve the problem of slow access to official sources when installing dependencies, Tencent Cloud has set up a cache service for some software. You can accelerate the installation of dependencies by using the Tencent Cloud software repository, which currently supports public network access and private network access.
- Public network access address: `http://mirrors.tencent.com`
- Private network access address: `http://mirrors.tencentyun.com/`

<dx-alert infotype="explain" title="">
- This document takes the public network access address of the Tencent Cloud software repository as an example to introduce how to use the software sources in the Tencent Cloud software repository in CVM. If you access the repository using a private network, please replace the public network access address **with the private network access address**.
- The source address used in this document is for reference only. Please obtain the latest address from the **Tencent Cloud software repository**.
</dx-alert>


## Notes

The Tencent Cloud software repository updates software sources from the official website of each software source once per day.

## Prerequisites

Log in to the CVM.

## Directions

### Accelerating pip using the Tencent Cloud image source


<dx-alert infotype="notice" title="">
Before using the Tencent Cloud image source, please confirm your CVM has Python installed.
</dx-alert>


#### Use the software source path temporarily
Execute the following command to install pip using Tencent Could PyPI.
```shell
pip install pip -i  the directory where PyPI is located in
```
For example, if you want to install the 17monip package, and the PyPI you need to use is in the `http://mirrors.tencent.com/pypi/simple` directory, run the following command:
```shell
pip install 17monip -i http://mirrors.tencent.com/pypi/simple --trusted-host mirrors.tencent.com 
```

#### Set the default software source path
Execute the following command to modify the `index-url` parameter in the `~/.pip/pip.conf` file to the source path of the Tencent Cloud software repository.

```shell
[global]
index-url = the directory where PyPI is located in
trusted-host = public network/private network access address
```
For example, if the PyPI you need to use is in the `http://mirrors.tencent.com/pypi/simple` directory, execute the following command:
```shell
[global]
index-url = http://mirrors.tencent.com/pypi/simple
trusted-host = mirrors.tencent.com
```

### Accelerating Maven using the Tencent Cloud image source


<dx-alert infotype="notice" title="">
Before using the Tencent Cloud image source, please confirm your CVM has JDK and Maven installed.
</dx-alert>


1. Open the `settings.xml` configuration file of Maven.
2. Find the `<mirrors> ... </ mirrors>` code block and configure the following content into it.
```xml
    <mirror>
        <id>nexus-tencentyun</id>
        <mirrorOf>*</mirrorOf>
        <name>Nexus tencentyun</name>
        <url>http://mirrors.tencent.com/nexus/repository/maven-public/</url>
    </mirror> 
```

### Accelerating NPM using the Tencent Cloud image source


<dx-alert infotype="notice" title="">
Before using the Tencent Cloud image source, please confirm your CVM has Node.js and NPM installed.
</dx-alert>


Execute the following command to install NPM using the Tencent Cloud NPM.
```shell
npm config set registry http://mirrors.tencent.com/npm/
```

### Accelerating Docker using the Tencent Cloud image source

#### Using Tencent Cloud Docker on the TKE cluster

No manual configuration is required. When the CVM in the Tencent Kubernetes Engine (TKE) cluster creates a node, Docker will be installed automatically and configured with the Tencent Cloud private network image.

#### Using Tencent Cloud Docker on CVM



<dx-alert infotype="notice" title="">
Before using the Tencent Cloud Docker, please confirm your CVM has Docker installed.
Only Docker 1.3.2 or later versions support the Docker Hub Mirror mechanism. If you have not installed Docker 1.3.2 or later versions, or if the installed version is too old, please install or upgrade it first.
</dx-alert>


Choose different operation steps based on the operating system of the CVM.
- The following steps are for Ubuntu 14.04, Debian, CentOS 6, Fedora, openSUSE, and other operating systems. The specific steps for other versions of operating systems may vary:
 1. Execute the following command to open the `/etc/default/docker` configuration file.
```shell
vim /etc/default/docker
```
 2. Press **i** to switch to the editing mode, enter the following content, and save.
```
DOCKER_OPTS="--registry-mirror=https://mirror.ccs.tencentyun.com"
```
- For Centos 7:
 1. Execute the following command to open the `/etc/docker/daemon.json` configuration file.
```shell
vim /etc/docker/daemon.json
```
 2. Press **i** to switch to the editing mode, enter the following content, and save.
```json
{
   "registry-mirrors": [
       "https://mirror.ccs.tencentyun.com"
  ]
}
```
- For Windows with Boot2Docker installed:
 1. Access the Boot2Docker Start Shell and execute the following command:
```shell
sudo su echo "EXTRA_ARGS=\"–registry-mirror=https://mirror.ccs.tencentyun.com\"" >> /var/lib/boot2docker/profile exit 
```
 2. Restart Boot2Docker.

### Accelerating MariaDB using the Tencent Cloud image


<dx-alert infotype="explain" title="">
The following steps take CentOS 7 as an example. Specific steps vary by operating system.
</dx-alert>


1. Execute the following command to create the `MariaDB.repo` file under `/etc/yum.repos.d/`.
```shell
vi /etc/yum.repos.d/MariaDB.repo
```
2. Press **i** to switch to the editing mode, enter the following content, and save.
```shell
# MariaDB 10.2 CentOS7-amd64
[mariadb]  
name = MariaDB  
baseurl = http://mirrors.tencent.com/mariadb/yum/10.2/centos7-amd64/
gpgkey = http://mirrors.tencent.com/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1  
```
3. Execute the following command to empty the YUM cache.
```shell
yum clean all
```
4. Execute the following command to install MariaDB.
```shell
yum install MariaDB-client MariaDB-server
```

### Accelerating MongoDB using the Tencent Cloud image


<dx-alert infotype="explain" title="">
The following steps take MongoDB 4.0 as an example. If you need to install another version, please change the version number in the mirror path.
</dx-alert>


#### Using Tencent Cloud MongoDB on CVMs with CentOS or Redhat systems

1. Execute the following command to create the `mongodb.repo` file under `/etc/yum.repos.d/`.
```shell
vi /etc/yum.repos.d/mongodb.repo
```
2. Press **i** to switch to the editing mode, enter the following content, and save.
```shell
[mongodb-org-4.0]
name=MongoDB Repository
baseurl=http://mirrors.tencent.com/mongodb/yum/el7-4.0
gpgcheck=0
enabled=1
```
3. Execute the following command to install MongoDB.
```shell
yum install -y mongodb-org
```

#### Using Tencent Cloud MongoDB on CVMs with the Debian system

1. Based on the different Debian versions, execute the following command to import the MongoDB GPG public key.
```shell
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. Execute the following command to configure the `mirror` path.
```
#Debian 8
echo "deb http://mirrors.tencent.com/mongodb/apt/debian jessie/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Debian 9
echo "deb http://mirrors.tencent.com/mongodb/apt/debian stretch/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. Run the following command to clear the cache.
```shell
sudo apt-get clean all
```
4. Run the following command to update the software package list.
```shell
sudo apt-get update
```
5. Execute the following command to install MongoDB.
```shell
sudo apt-get install -y mongodb-org
```

#### Using Tencent Cloud MongoDB on CVMs with the Ubuntu system

1. Execute the following command to import the MongoDB GPG public key.
```shell
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. Execute the following command to configure the `mirror` path.
```
#Ubuntu 14.04
echo "deb [ arch=amd64 ] http://mirrors.tencent.com/mongodb/apt/ubuntu trusty/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 16.04
echo "deb [ arch=amd64 ] http://mirrors.tencent.com/mongodb/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 18.04
echo "deb [ arch=amd64 ] http://mirrors.tencent.com/mongodb/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. Run the following command to clear the cache.
```shell
sudo apt-get clean all
```
4. Run the following command to update the software package list.
```shell
sudo apt-get update
```
5. Execute the following command to install MongoDB.
```shell
sudo apt-get install -y mongodb-org
```

### Accelerating Rubygems using the Tencent Cloud image source


<dx-alert infotype="notice" title="">
Before using the Tencent Cloud image source, please confirm your CVM has Ruby installed.
</dx-alert>


Execute the following command to modify the RubyGems source address.
```shell
gem source -r https://rubygems.org/
gem source -a http://mirrors.tencent.com/rubygems/
```
