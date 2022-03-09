---
title: PHP - CODING 帮助中心
pageTitle: PHP
pagePrevTitle: 安装 Maven 依赖包
pagePrev: ci/depend/maven.html
pageNextTitle: 增量检查代码规范
pageNext: ci/lint/jenkins-git-diff.html
alias: ci/depend/php.html
---

PHP 有两种常用扩展依赖包：

-   C 扩展：使用 pecl 安装；
-   PHP 扩展：使用 composer 安装；

### pecl

PHP 可使用 `docker-php-ext-install` 或 `pecl` 命令安装扩展：

```groovy
pipeline {
  agent {
    docker {
      reuseNode 'true'
      registryUrl 'https://coding-public-docker.pkg.coding.net'
      image 'public/docker/php:8.0'
      // image 'public/docker/php:7.4' 以及 7.3、7.2、7.1、5.6
      args '-v /var/run/docker.sock:/var/run/docker.sock -v /usr/bin/docker:/usr/bin/docker'
    }
  }
  stages {
    stage('安装依赖') {
      steps {
        // 第 1 种方式：PHP 内置扩展
        // Possible values for ext-name:
        // bcmath bz2 calendar ctype curl dba dom enchant exif fileinfo filter ftp gd gettext gmp
        // hash iconv imap interbase intl json ldap mbstring mysqli oci8 odbc opcache pcntl pdo
        // pdo_dblib pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite pgsql phar posix pspell
        // readline recode reflection session shmop simplexml snmp soap sockets sodium spl standard
        // sysvmsg sysvsem sysvshm tidy tokenizer wddx xml xmlreader xmlrpc xmlwriter xsl zend_test zip
        sh 'apt-get update && apt-get install -y libbz2-dev'
        sh 'docker-php-ext-install bz2'
        sh 'php -i | grep bz2'
        // 第 2 种方式：第三方 pecl 扩展
        sh "pecl install imagick"
        sh 'docker-php-ext-enable imagick'
        sh 'php -i | grep imagick'
      }
    }
  }
}
```

### [公共 composer 制品库](#composer-public)

composer 公共制品库 [Packagist](https://packagist.org/) 在海外，内地用户访问可能很慢，建议切换为腾讯云镜像：

```shell
composer config -g repos.packagist composer https://mirrors.cloud.tencent.com/composer/

composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

# 恢复默认官方源（海外）
# composer config -g --unset repos.packagist
```

### [私有 composer 制品库](#composer-private)

使用私有制品库需先获得用户名/密码，参考文档：[《搭建团队级制品库》](/docs/artifacts/practices/team-share.html)。

#### composer.json

进入 PHP 项目目录，设置制品库地址：

```shell
composer config repos.private-composer composer https://codes-farm-composer.pkg.coding.net/composer-demo/private-composer
```

可以看到 `composer.json` 发生了变化，将它提交到代码库。

![](https://help-assets.codehub.cn/enterprise/20210208175109.png)

#### auth.json

进入 PHP 项目目录，设置制品库用户名/密码：

```shell
composer config http-basic.codes-farm-composer.pkg.coding.net pt03xe33nvww 0ad2d123456
```

可以看到生成了 `auth.json`，将它忽略掉，不要提交到代码库。

![](https://help-assets.codehub.cn/enterprise/20210208175623.png)

#### [本地安装](#composer-require)

本地安装私有包：

```shell
composer require codes-farm/socialite-providers:0.3.0
```

然后将 `composer.lock` 提交到代码库。

#### [持续集成构建](#jenkins)

把用户名/密码填入环境变量：

![](https://qcloudimg.tencent-cloud.cn/raw/fb8e4e76463e6dae2f8393834ddb1b1d.png)

```groovy
pipeline {
  agent {
    docker {
      reuseNode 'true'
      registryUrl 'https://coding-public-docker.pkg.coding.net'
      image 'public/docker/php:8.0'
      args '-v /var/run/docker.sock:/var/run/docker.sock -v /usr/bin/docker:/usr/bin/docker'
    }
  }
  stages {
    stage('检出') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: env.GIT_BUILD_REF]], 
            userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]])
      }
    }
    stage('安装依赖') {
      steps {
        sh "composer config http-basic.codes-farm-composer.pkg.coding.net ${CODING_ARTIFACTS_USERNAME} ${CODING_ARTIFACTS_PASSWORD}"
        sh "composer install"
      }
    }
  }
}
```

==== 2021/06/18 ====
