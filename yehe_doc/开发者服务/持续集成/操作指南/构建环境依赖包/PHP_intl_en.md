---
title: PHP - CODING Help Center
pageTitle: PHP
pagePrevTitle: Install Maven Dependency
pagePrev: ci/depend/maven.html
pageNextTitle: Incremental Code Convention Check
pageNext: ci/lint/jenkins-git-diff.html
alias: ci/depend/php.html
---

There are two common extended PHP dependencies:

- C extension: Install with pecl
- PHP extension: Install with composer

### pecl

You can install PHP extensions using the `docker-php-ext-install` or `pecl` command:

```groovy
pipeline {
  agent {
    docker {
      reuseNode 'true'
      registryUrl 'https://coding-public-docker.pkg.coding.net'
      image 'public/docker/php:8.0'
      // image 'public/docker/php:7.4' and 7.3, 7.2, 7.1, and 5.6
      args '-v /var/run/docker.sock:/var/run/docker.sock -v /usr/bin/docker:/usr/bin/docker'
    }
  }
  stages {
    stage('Install dependency') {
      steps {
        // Method 1: Internal PHP extension
        // Possible values for ext-name:
        // bcmath bz2 calendar ctype curl dba dom enchant exif fileinfo filter ftp gd gettext gmp
        // hash iconv imap interbase intl json ldap mbstring mysqli oci8 odbc opcache pcntl pdo
        // pdo_dblib pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite pgsql phar posix pspell
        // readline recode reflection session shmop simplexml snmp soap sockets sodium spl standard
        // sysvmsg sysvsem sysvshm tidy tokenizer wddx xml xmlreader xmlrpc xmlwriter xsl zend_test zip
        sh 'apt-get update && apt-get install -y libbz2-dev'
        sh 'docker-php-ext-install bz2'
        sh 'php -i | grep bz2'
        // Method 2: Third-party pecl extension
        sh "pecl install imagick"
        sh 'docker-php-ext-enable imagick'
        sh 'php -i | grep imagick'
      }
    }
  }
}
```

### [Public composer repository](#composer-public)

As the public composer repository [Packagist](https://packagist.org/) is located outside of China, users in mainland China should switch to the Tencent Cloud Mirror for fast access:

```shell
composer config -g repos.packagist composer https://mirrors.cloud.tencent.com/composer/

composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

# Restore default official source (outside China)
# composer config -g --unset repos.packagist
```

### [Private composer repository](#composer-private)

To use a private repository, you need to first retrieve the username and password. See [Building a Team Repository](/docs/artifacts/practices/team-share.html).

#### composer.json

Go to the PHP project directory and set the repository URL:

```shell
composer config repos.private-composer composer https://codes-farm-composer.pkg.coding.net/composer-demo/private-composer
```

You can see the change in `composer.json`. Commit it to the code repository.

![](https://help-assets.codehub.cn/enterprise/20210208175109.png)

#### auth.json

Go to the PHP project directory and set the username and password for the repository:

```shell
composer config http-basic.codes-farm-composer.pkg.coding.net pt03xe33nvww 0ad2d123456
```

Ignore the `auth.json` generated and do not commit it to the code repository.

![](https://help-assets.codehub.cn/enterprise/20210208175623.png)

#### [Local installation](#composer-require)

Install the private package locally:

```shell
composer require codes-farm/socialite-providers:0.3.0
```

Then, commit `composer.lock` to the code repository.

#### [Continuous integration build](#jenkins)

Enter the username and password in the environment variables:

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
    stage('Check out') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: env.GIT_BUILD_REF]], 
            userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]])
      }
    }
    stage('Install dependency') {
      steps {
        sh "composer config http-basic.codes-farm-composer.pkg.coding.net ${CODING_ARTIFACTS_USERNAME} ${CODING_ARTIFACTS_PASSWORD}"
        sh "composer install"
      }
    }
  }
}
```

==== 2021/06/18 ====
