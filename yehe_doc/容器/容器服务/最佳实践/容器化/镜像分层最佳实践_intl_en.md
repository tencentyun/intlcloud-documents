## Overview
This document describes how to build and manage business images in layers and provides best practices for managing container images of all types using TCR.  

### Advantages of container image layering

- Resources are shared to improve the utilization.  
- Image management is standardized to facilitate DevOps implementation.  
- TCR's Ops-free image acceleration easily makes large-scale image distribution faster by 5-10 times.  
- TCR Enterprise has been accessed to Tencent CloudAudit. You can check the logs of read and write operations of instances, namespaces, and image repositories in "Event History".  

## Prerequisites
Before using a private image managed in [TCR](https://console.cloud.tencent.com/tcr) for application deployment, you need to complete the following preparations:

- You have created a TCR Enterprise instance in the [TCR console](https://console.cloud.tencent.com/tcr). If you haven't done so, create one first. For more information, see [Creating an Enterprise Edition Instance](https://intl.cloud.tencent.com/document/product/1051/35486).  
- If you are using a sub-account, you must have granted the sub-account operation permissions for the corresponding instance. For more information, see [Example of Authorization Solution of TCR Enterprise](https://intl.cloud.tencent.com/document/product/1051/37248).  

```
 Note: This also applies to the existing TCR instances. You only need to modify the image repository address.  
```
## 1. F3S Docker Files Overview


The project consists of the following parts:

```shell
$ tree -L 3 ./f3s-docker-files
./f3s-docker-files
├── README.md                                       ------  README file
├── DockerBuildImages.sh                            ------  Image build script
├── 0.base                                          ------  0. Build various types of system images at the base layer
│   ├── alpine                                      ------    Build the alpine system image at the base layer
│   │   └── Dockerfile
│   └── centos-7.8                                  ------    Build the CentOS 7.8 system image at the base layer
│       ├── Dockerfile
│       └── centos-7.8.2003-x86_64-docker.tar.xz
├─  1.ops                                           ------  1. Build various types of images at the Ops layer
│   └── Dockerfile-alpine                           ------    Build the alpine image at the Ops layer
├── 2.lang                                          ------  2. Build various types of images at the language layer
│   └── Dockerfile-alpine-kona                      ------    alpine-kona image at the language layer 
└── 3.app                                           ------  3. Build various types of images at the application layer
    ├── jmeter
    │   ├── Dockerfile-jmeter-base                  ------    Build the jmeter-base image
    │   ├── Dockerfile-jmeter-grafana-reporter      ------    Build the jmeter-grafana-reporter image
    │   ├── Dockerfile-jmeter-master                ------    Build the jmeter-master image
    │   └── Dockerfile-jmeter-slave                 ------    Build the jmeter-slave image
    ├── nginx
    │   ├── Dockerfile-alpine-nginx                 ------    Build the alpine-nginx image
    │   ├── default.conf
    │   └── nginx.conf
    └── skywalking
        └── Dockerfile-alpine-kona-skywalking       ------    Build the alpine-kona-skywalking image

```

- **alpine/Dockerfile**: Build with the official [Alpine 3.13 Docker image](https://hub.docker.com/_/alpine) to support common Ops tools.  
- **centos-7.8/Dockerfile**: Build with the official [CentOS 7.8 Docker image](https://github.com/CentOS/sig-cloud-instance-images/blob/CentOS-7.8.2003-x86_64/docker/Dockerfile) to support common Ops tools.  
- **Dockerfile-alpine-kona**: Build with the [Dockerfile-alpine](#20-dockerfile-alpine) and TencentKona [8.0.5 binary package](https://github.com/Tencent/TencentKona-8/releases). The Kona is partially trimmed to control the image size.  
- **Dockerfile-jmeter-base**: Build based on the official [JMeter 5.4.1 binary package](https://jmeter.apache.org/).  
- **Dockerfile-jmeter-grafana-reporter**: Build based on [Grafana-Reporter](https://github.com/IzakMarais/reporter) to generate JMeter PDF reports from Grafana dashboards.  
- **Dockerfile-jmeter-master**: Build based on [Jmeter-base](#23-dockerfile-jmeter-base) to implement distributed master stress test with JMeter.  
- **Dockerfile-jmeter-slave**: Build based on [Jmeter-base](#23-dockerfile-jmeter-base) to implement distributed slave stress test with JMeter.  
- **Dockerfile-alpine-nginx**: Build with [Dockerfile-alpine](#20-dockerfile-alpine) to add NGINX configuration initialization and logging specifications.  
- **Dockerfile-alpine-kona-skywalking**: Build with the official [Dockerfile-alpine-kona](#21-dockerfile-alpine-kona) and [SkyWalking 8.5 binary package](https://skywalking.apache.org/).  


## 2. Project Resource Description


### **2.0 Dockerfile-alpine**

============ALPINE DOCKER FILE============

~~~sh
# build
FROM alpine:3.13

ENV FROM alpine:3.13

# The Alpine image does not contain `tzdata`, so you cannot set the time zone directly via the environment variable `TZ`. To this end, you need to install `tzdata`:
ENV TZ=Asia/Shanghai

RUN echo 'http://mirrors.tencent.com/alpine/v3.13/main/' > /etc/apk/repositories \
    && echo 'http://mirrors.tencent.com/alpine/v3.13/community/' >> /etc/apk/repositories \
    && apk --no-cache add apache2-utils \
                          bind-tools \
                          bridge-utils \
                          busybox-extras \
                          curl \
                          ebtables \
                          ethtool \
                          fio \
                          fping \
                          iperf3 \
                          iproute2 \
                          iptables \
                          iputils \
                          ipvsadm \
                          jq \
                          lftp \
                          lsof \
                          mtr \
                          netcat-openbsd \
                          net-tools \
                          nmap \
                          procps \
                          psmisc \
                          rsync \
                          smartmontools \
                          strace \
                          sysstat \
                          tcpdump \
                          tree \
                          tzdata \
                          unzip \
                          util-linux \
                          wget \
                          zip  \
    && echo "${TZ}" > /etc/timezone \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && rm -rf /var/cache/apk/*

ENV BUILD f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine:v3.13


# docker build -t f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine:v3.13 .

~~~

============Build, tag and push the base image============

~~~bash
cd $pwd/0.base/alpine
docker build -t f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine:v3.13   -f Dockerfile .
docker push f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine:v3.13 
~~~

### **2.1 Dcokerfile-CentOS-7.8**

============Centos-7.8 DOCKER FILE============
~~~sh
# build
# CentOS 7.8 official Dockerfile: https://github.com/CentOS/sig-cloud-instance-images/blob/CentOS-7.8.2003-x86_64/docker/Dockerfile
# CentOS 7.8 official package: wget https://raw.githubusercontent.com/CentOS/sig-cloud-instance-images/CentOS-7.8.2003-x86_64/docker/centos-7.8.2003-x86_64-docker.tar.xz

FROM scratch

ADD centos-7.8.2003-x86_64-docker.tar.xz /

LABEL name="CentOS Base Image" \
      vendor="CentOS" \
      license="GPLv2" \
      build-date="20200504"


# Add some widgets and change the time zone
RUN set -ex \
    && yum install -y wget \
    && rm -rf /etc/yum.repos.d/CentOS-* \
# Add the `Tencent yum` source
    && wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.cloud.tencent.com/repo/centos7_base.repo \
    && yum fs filter documentation \
    && yum install -y atop \
                      bind-utils \
                      curl \
                      dstat \
                      ebtables \
                      ethtool \
                      fping \
                      htop \
                      iftop \
                      iproute \
                      jq \
                      less \
                      lsof \
                      mtr \
                      nc \
                      net-tools \
                      nmap-ncat \
                      perf \
                      psmisc \
                      strace \
                      sysstat \
                      tcpdump \
                      telnet \
                      tree \
                      unzip \
                      wget \
                      which \
                      zip \
                      ca-certificates \
    && rm -rf /etc/localtime \
    && ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
# Install dumb-init
    && wget -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.5/dumb-init_1.2.5_x86_64 \
    && chmod +x /usr/local/bin/dumb-init \
# Install gosu grab gosu for easy step-down from root
# https://github.com/tianon/gosu/releases
    && wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/1.13/gosu-amd64" \
    && chmod +x /usr/local/bin/gosu \
    && gosu nobody true \
# Install the Chinese language package to solve the VI garbled text issue
    && yum -y install kde-l10n-Chinese glibc-common \
    && localedef -c -f UTF-8 -i zh_CN zh_CN.utf8 \
    && export LC_ALL=zh_CN.utf8 \
    && yum clean all  \
    && rm -rf /tmp/* \
    && rm -rf /var/lib/yum/* \
    && rm -rf /var/cache/yum

# Solve the LESS garbled text issue
ENV LESSCHARSET utf-8

# Set language environment variables
ENV LANG=en_US.UTF-8

# If this line is not added, `stdin: true` and `tty: true` in Kubernetes will not take effect
CMD ["/bin/bash"]


ENV BUILD f3s-docker-file.tencentcloudcr.com/f3s-tcr/centos:v7.8

# docker build -t f3s-docker-file.tencentcloudcr.com/f3s-tcr/centos:v7.8 .
~~~

============Build, tag and push the base image============
~~~sh
cd $pwd/0.base/centos-7.8
docker build --no-cache -t f3s-docker-file.tencentcloudcr.com/f3s-tcr/centos:v7.8  -f Dockerfile .
docker push f3s-docker-file.tencentcloudcr.com/f3s-tcr/centos:v7.8
# To test run:  docker run --name test -it --rm f3s-docker-file.tencentcloudcr.com/f3s-tcr/centos:v7.8 uname -a
# docker export <container-id> | docker import f3s-docker-file.tencentcloudcr.com/f3s-tcr/centos:v7.8
# quick interative termnal: docker run -it --entrypoint=sh f3s-docker-file.tencentcloudcr.com/f3s-tcr/centos:v7.8 sh
~~~

### **2.2 Dcokerfile-Ops**

============Ops DOCKER FILE============
~~~sh
# build
FROM f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine:v3.13
MAINTAINER westzhao

ENV LANG=C.UTF-8

# Download the Ops tool
RUN apk --no-progress --purge --no-cache add --upgrade wget \
    curl \
    mysql-client \
    busybox \
    busybox-extras \
    bash \
    bash-doc \
    bash-completion \
    tzdata \
    vim \
    unzip && \
# Download the glibc to support JDK and solve the Chinese character issue && \
wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.33-r0/glibc-2.33-r0.apk && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.33-r0/glibc-bin-2.33-r0.apk && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.33-r0/glibc-i18n-2.33-r0.apk && \
    apk add glibc-2.33-r0.apk glibc-bin-2.33-r0.apk glibc-i18n-2.33-r0.apk && \
    rm glibc-2.33-r0.apk glibc-bin-2.33-r0.apk glibc-i18n-2.33-r0.apk && \
    /usr/glibc-compat/bin/localedef -i en_US -f UTF-8 C.UTF-8  && \
    echo "export LANG=$LANG" > /etc/profile.d/locale.sh && \
# Change the time zone
    mkdir -p /share/zoneinfo/Asia/ && \
    mkdir -p /etc/zoneinfo/Asia/ && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime  && \
    cp /usr/share/zoneinfo/Asia/Shanghai /share/zoneinfo/Asia/Shanghai && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/zoneinfo/Asia/Shanghai && \
    echo "Asia/Shanghai" > /etc/timezone  && \
    apk del tzdata && \
# Delete the APK cache && \
    rm -rf /var/cache/apk/*

~~~

============Build, tag and push the base image============
~~~sh
docker build --no-cache -t f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine:latest  -f ./1.ops/Dockerfile-alpine .
docker push f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine:latest
# To test run:  docker run --name test -it --rm f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine:latest sh $(java -version)
# docker export <container-id> | docker import f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine:latest
# quick interative termnal: docker run -it --entrypoint=sh f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine:latest sh
~~~


### **2.3 Dockerfile-alpine-kona**

============Alpine Kona DOCKER FILE============
~~~sh
# build
# build
FROM f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine:latest
MAINTAINER westzhao

ENV LANG=C.UTF-8


# Download the Kona installation package via wget && \
RUN cd  /opt && \
wget https://github.com/Tencent/TencentKona-8/releases/download/8.0.5-GA/TencentKona8.0.5.b12_jdk_linux-x86_64_8u282.tar.gz && \
    tar -xvf TencentKona8.0.5.b12_jdk_linux-x86_64_8u282.tar.gz && \
    rm TencentKona8.0.5.b12_jdk_linux-x86_64_8u282.tar.gz && \
    ln -nfs /opt/TencentKona-8.0.5-282 /opt/jdk && \
# Trim the unused resources of the JDK && \
rm /opt/jdk/release && \
    rm /opt/jdk/THIRD_PARTY_README && \
    rm /opt/jdk/LICENSE && \
    rm /opt/jdk/ASSEMBLY_EXCEPTION && \
    rm -rf /opt/jdk/sample/ && \
    rm -rf /opt/jdk/demo/ && \
    rm -rf /opt/jdk/src.zip && \
    rm -rf /opt/jdk/man/ && \
    rm -rf /opt/jdk/lib/missioncontrol  && \
    rm -rf /opt/jdk/lib/visualvm  && \
    rm -rf /opt/jdk/lib/ant-javafx.jar  && \
    rm -rf /opt/jdk/lib/javafx-mx.jar  && \
    rm -rf /opt/jdk/lib/jconsole.jar  && \
    rm -rf /opt/jdk/jre/lib/amd64/libawt_xawt.so  && \
    rm -rf /opt/jdk/jre/lib/amd64/libjavafx_font_freetype.so  && \
    rm -rf /opt/jdk/jre/lib/amd64/libjavafx_font_pango.so  && \
    rm -rf /opt/jdk/jre/lib/amd64/libjavafx_font.so  && \
    rm -rf /opt/jdk/jre/lib/amd64/libjavafx_font_t2k.so  && \
    rm -rf /opt/jdk/jre/lib/amd64/libjavafx_iio.so  && \
    rm -rf /opt/jdk/jre/lib/amd64/libjfxwebkit.so  && \
    rm -rf /opt/jdk/jre/lib/desktop  && \
    rm -rf /opt/jdk/jre/lib/ext/jfxrt.jar  && \
    rm -rf /opt/jdk/jre/lib/fonts  && \
    rm -rf /opt/jdk/jre/lib/locale/de  && \
    rm -rf /opt/jdk/jre/lib/locale/fr  && \
    rm -rf /opt/jdk/jre/lib/locale/it  && \
    rm -rf /opt/jdk/jre/lib/locale/ja  && \
    rm -rf /opt/jdk/jre/lib/locale/ko  && \
    rm -rf /opt/jdk/jre/lib/locale/ko.UTF-8  && \
    rm -rf /opt/jdk/jre/lib/locale/pt_BR  && \
    rm -rf /opt/jdk/jre/lib/locale/sv  && \
    rm -rf /opt/jdk/jre/lib/locale/zh_HK.BIG5HK  && \
    rm -rf /opt/jdk/jre/lib/locale/zh_TW  && \
    rm -rf /opt/jdk/jre/lib/locale/zh_TW.BIG5  && \
    rm -rf /opt/jdk/jre/lib/oblique-fonts  && \
    rm -rf /opt/jdk/jre/lib/deploy.jar  && \
    rm -rf /opt/jdk/jre/lib/locale/

# JAVA_HOME
ENV JAVA_HOME=/opt/jdk
ENV CLASSPATH=.:$JAVA_HOME/lib/
ENV PATH=$JAVA_HOME/bin:$PATH
~~~

============Build, tag and push the base image============
~~~sh
docker build --no-cache -t f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-kona:latest  -f ./2.lang/Dockerfile-alpine-kona .
docker push f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-kona:latest
# To test run:  docker run --name test -it --rm f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-kona:latest sh $(java -version)
# docker export <container-id> | docker import f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-kona:latest
# quick interative termnal: docker run -it --entrypoint=sh f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-kona:latest sh
~~~

### **2.4 Dockerfile-alpine-kona-skywalking**

============Alpine Kona SkyWalking DOCKER FILE============
~~~sh
# build
FROM f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-kona:latest
MAINTAINER westzhao

ENV LANG=C.UTF-8

# Download the Ops tool
RUN mkdir /3.app && \
    wget -q -O /3.app/apache-skywalking-apm-8.5.0.tar.gz https://archive.apache.org/dist/skywalking/8.5.0/apache-skywalking-apm-8.5.0.tar.gz && \
    tar zxf /3.app/apache-skywalking-apm-8.5.0.tar.gz -C /3.app && \
    mv /3.app/apache-skywalking-apm-bin/agent /3.app/skywalking && \
    rm -rf /3.app/apache-skywalking-apm-8.5.0.tar.gz && \
    rm -rf /3.app/apache-skywalking-apm-bin/

# JAVA_HOME
ENV JAVA_HOME=/opt/jdk
ENV CLASSPATH=.:$JAVA_HOME/lib/
ENV PATH=$JAVA_HOME/bin:$PATH
~~~

============Build, tag and push the base image============
~~~sh
docker build --no-cache -t f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-kona-skywalking:latest  -f ./3.app/skywalking/Dockerfile-alpine-kona-skywalking .
docker push f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-kona-skywalking:latest
# To test run:  docker run --name test -it --rm f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-kona-skywalking:latest sh $(java -version)
# docker export <container-id> | docker import f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-kona-skywalking:latest
# quick interative termnal: docker run -it --entrypoint=sh f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-kona-skywalking:latest sh
~~~

### **2.5 Dockerfile-jmeter-base**

============JMETER BASE DOCKER FILE============
~~~sh
# build
FROM f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-kona:latest
MAINTAINER westzhao

ARG JMETER_VERSION=5.4.1

# Download JMeter
RUN mkdir /jmeter && \
cd /jmeter && \
wget https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-$JMETER_VERSION.tgz && \
    tar -xzf apache-jmeter-$JMETER_VERSION.tgz && \
    rm apache-jmeter-$JMETER_VERSION.tgz && \
# Download JMeterPlugins-Standard && \
cd /jmeter/apache-jmeter-$JMETER_VERSION/ && \
    wget -q -O /tmp/JMeterPlugins-Standard-1.4.0.zip https://jmeter-plugins.org/downloads/file/JMeterPlugins-Standard-1.4.0.zip && \
    unzip -n /tmp/JMeterPlugins-Standard-1.4.0.zip && \
    rm /tmp/JMeterPlugins-Standard-1.4.0.zip && \
# Download pepper-box && \
    wget -q -O /jmeter/apache-jmeter-$JMETER_VERSION/lib/ext/pepper-box-1.0.jar https://github.com/raladev/load/blob/master/JARs/pepper-box-1.0.jar?raw=true && \
# Download bzm-parallel && \
cd /jmeter/apache-jmeter-$JMETER_VERSION/ && \
    wget -q -O /tmp/bzm-parallel-0.7.zip https://jmeter-plugins.org/files/packages/bzm-parallel-0.7.zip && \
    unzip -n /tmp/bzm-parallel-0.7.zip && \
    rm /tmp/bzm-parallel-0.7.zip

ENV JMETER_HOME /jmeter/apache-jmeter-$JMETER_VERSION/

ENV PATH $JMETER_HOME/bin:$PATH
~~~

============Build, tag and push the base image============
~~~sh
docker build --no-cache -t f3s-docker-file.tencentcloudcr.com/f3s-tcr/jmeter-base:latest -f ./3.app/jmeter/Dockerfile-jmeter-base .
docker push f3s-docker-file.tencentcloudcr.com/f3s-tcr/jmeter-base:latest
~~~

### **2.6 Dockerfile-jmeter-master**

============JMETER-MASTER DOCKER FILE============
~~~sh
# build
FROM f3s-docker-file.tencentcloudcr.com/f3s-tcr/jmeter-base:latest
MAINTAINER westzhao

EXPOSE 60000
~~~

============Build, tag and push the base image============
~~~sh
docker build --no-cache -t f3s-docker-file.tencentcloudcr.com/f3s-tcr/jmeter-master:latest -f ./3.app/jmeter/Dockerfile-jmeter-master .
docker push f3s-docker-file.tencentcloudcr.com/f3s-tcr/jmeter-master:latest
~~~

### **2.7 Dockerfile-jmeter-slave**

================JMETER-SLAVES DOCKER FILE=====================
~~~sh
# build
FROM f3s-docker-file.tencentcloudcr.com/f3s-tcr/jmeter-base:latest
MAINTAINER westzhao

EXPOSE 1099 50000

ENTRYPOINT $JMETER_HOME/bin/jmeter-server \
-Dserver.rmi.localport=50000 \
-Dserver_port=1099 \
-Jserver.rmi.ssl.disable=true
~~~

============Build, tag and push the base image============
~~~sh
docker build --no-cache -t f3s-docker-file.tencentcloudcr.com/f3s-tcr/jmeter-slave:latest -f ./3.app/jmeter/Dockerfile-jmeter-slave .
docker push f3s-docker-file.tencentcloudcr.com/f3s-tcr/jmeter-slave:latest
~~~

### **2.8 Dockerfile-jmeter-grafana-reporter**


================JMETER-GRAFANA-REPORTER DOCKER FILE=====================

~~~sh
# build
# Multi-stage builds
FROM golang:1.14.7-alpine3.12 AS build
MAINTAINER westzhao
# Download the Ops and compilation tools
WORKDIR /go/src/${owner:-github.com/8710925}/reporter
# ADD . .
# RUN go install -v github.com/8710925/reporter/cmd/grafana-reporter

RUN apk --no-progress --purge --no-cache add --upgrade git && \
# Compile grafana-reporter
    git clone https://${owner:-github.com/8710925}/reporter . \
    && go install -v github.com/8710925/reporter/cmd/grafana-reporter


# create grafana reporter image
FROM alpine:3.12
COPY --from=build /go/src/${owner:-github.com/8710925}/reporter/util/texlive.profile /
COPY --from=build /go/src/${owner:-github.com/8710925}/reporter/util/SIMKAI.ttf /usr/share/fonts/west/

RUN apk --no-progress --purge --no-cache add --upgrade  wget \
    curl \
    fontconfig \
    unzip \
    tzdata \
    perl-switch && \
    wget -qO- \
    "https://github.com/yihui/tinytex/raw/master/tools/install-unx.sh" | \
    sh -s - --admin --no-path \
    && mv ~/.TinyTeX /opt/TinyTeX \
    && /opt/TinyTeX/bin/*/tlmgr path add \
    && tlmgr path add \
    && chown -R root:adm /opt/TinyTeX \
    && chmod -R g+w /opt/TinyTeX \
    && chmod -R g+wx /opt/TinyTeX/bin \
    && tlmgr update --self --repository http://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet \
    && tlmgr install epstopdf-pkg ctex  everyshi everysel euenc \
# Change the time zone
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime  \
    && echo "Asia/Shanghai" > /etc/timezone  \
    && apk del tzdata \
    # Cleanup
    && fmtutil-sys  --all \
    && texhash \
    && mktexlsr \
    && apk del --purge -qq \
    && rm -rf /var/lib/apt/lists/*

COPY --from=build /go/bin/grafana-reporter /usr/local/bin


ENTRYPOINT [ "/usr/local/bin/grafana-reporter","-ip","jmeter-grafana:3000" ]
~~~
============Build, tag and push the base image============
~~~sh
docker build --no-cache -t f3s-docker-file.tencentcloudcr.com/f3s-tcr/jmeter-grafana-reporter:latest -f ./3.app/jmeter/Dockerfile-jmeter-grafana-reporter .
docker push f3s-docker-file.tencentcloudcr.com/f3s-tcr/jmeter-grafana-reporter:latest
~~~


### **2.9 Dockerfile-alpine-nginx**

================Alpine Nginx DOCKER FILE=====================
~~~sh
# build
FROM f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-kona:latest
MAINTAINER westzhao

ENV LANG=C.UTF-8

# Download the Ops tool
RUN apk --no-progress --purge --no-cache add --upgrade nginx && \
# Delete the APK cache && \
    rm -rf /var/cache/apk/*

COPY ./3.app/nginx/default.conf /etc/nginx/http.d/default.conf
COPY ./3.app/nginx/nginx.conf /etc/nginx/nginx.conf

EXPOSE 80 443

CMD ["/usr/sbin/nginx", "-g", "daemon off;", "-c", "/etc/nginx/nginx.conf"]
~~~

============Build, tag and push the base image============
~~~sh
docker build --no-cache -t f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-nginx:latest -f ./3.app/nginx/Dockerfile-alpine-nginx .
docker push f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-nginx:latest
# To test run:  docker run --name test -it --rm -p 8888:80 f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-nginx:latest nginx -v
# docker export <container-id> | docker import f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-nginx:latest
# quick interative termnal: docker run -it --entrypoint=sh f3s-docker-file.tencentcloudcr.com/f3s-tcr/alpine-nginx:latest sh
~~~
