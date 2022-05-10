## 작업 시나리오

Discuz!는 전 세계에서 완성도 및 커버율이 가장 높은 포럼 웹 사이트 소프트웨어 시스템 중 하나로, 200여만 명의 웹 사이트 사용자를 보유하고 있으며, 귀하도 Discuz!를 통해 포럼을 구축할 수 있습니다. 본 문서는 Tencent Cloud CVM에서 Discuz! 포럼 구축 및 그에 필요한 LAMP(Linux + Apache + MariaDB + PHP)환경 구축에 대해 소개합니다.


Discuz! 포럼 수동 구축을 위해 자주 사용하는 커맨드인 [CentOS 환경에서 YUM을 통해 소프트웨어 설치](https://intl.cloud.tencent.com/document/product/213/2046) 등의 Linux 커맨드에 익숙해져야 하며, 설치된 소프트웨어의 사용 및 버전 호환성에 대한 이해도가 있어야 합니다.





## 소프트웨어
본 문서 중 구축한 Discuz! 포럼 소프트웨어의 구성 버전 및 설명은 다음과 같습니다.
- Linux: Linux 운영 체제의 경우, 본 문서는 CentOS 7.6을 예시로 사용합니다.
- Apache: Web 서버의 경우, 본 문서는 Apache 2.4.15를 예시로 사용합니다.
- MariaDB: 데이터베이스의 경우, 본 문서는 MariaDB 5.5.60를 예시로 사용합니다.
- PHP: 스크립트 언어의 경우, 본 문서는 PHP 5.4.16을 예시로 사용합니다.
- Discuz!: 포럼 웹 사이트 소프트웨어의 경우, 본 문서는 Discuz! X3.4를 예시로 사용합니다.


## 작업 순서
### 1단계: CVM(Cloud Virtual Machine) 로그인
[Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)합니다. 실제 작업 스타일에 따라 다른 로그인 방식을 선택할 수도 있습니다.
- [원격 로그인 소프트웨어를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)



### 2단계: LAMP 환경 구축 

CentOS 시스템에 대해 Tencent Cloud는 CentOS와 동기화된 소프트웨어 설치 소스를 제공하고 있어, 포함되어 있는 소프트웨어 모두 현재로써 가장 안정적인 버전으로, 직접 Yum을 통해 빠르게 설치할 수 있습니다.


#### 필요한 소프트웨어 설치 및 설정[](id:InstallNecessarySoftware)
1. 다음 명령어를 실행하여 필수 소프트웨어(Apache, MariaDB, PHP, Git)를 설치합니다.
```
yum install httpd php php-fpm php-mysql mariadb mariadb-server git -y
```
2. 다음 명령어를 차례대로 실행하여 서비스를 시작합니다.
```
systemctl start httpd
```
```
systemctl start mariadb
```
```
systemctl start php-fpm
```
3. [](id:step3)root 사용자가 데이터베이스에 액세스할 수 있도록 다음 명령어를 실행하여 root 계정 비밀번호 및 기본 환경을 설정합니다.
<dx-alert infotype="notice" title="">
- MariaDB 에 처음 로그인 하기 전, 다음 명령어를 실행하여 사용자 비밀번호 및 기본 설정으로 이동합니다.
- 처음으로 root 비밀번호를 입력하라는 메시지가 뜨면 **Enter**를 눌러 바로 root 비밀번호 설정 단계로 진입합니다. root 비밀번호 설정 시 인터페이스는 나타나지 않도록 기본 설정되어 있습니다. 인터페이스의 알림에 따라 순서대로 다른 기본 구성을 완료하십시오.
</dx-alert>
```
mysql_secure_installation
```
4. 다음 명령어를 실행하여 MariaDB에 로그인하고 [3단계](#step3)에서 설정한 비밀번호를 입력한 후 "**Enter**"를 누릅니다.
```
mysql -u root -p
```
방금 설정한 비밀번호를 입력하여 MariaDB 에 로그인 되면 제대로 설정되었음을 뜻합니다. 아래 그림 참고.
![](https://main.qcloudimg.com/raw/18c54971e141db38c3f483161fefe251.png)
5. 다음 명령어를 실행하여 MariaDB 데이터베이스를 종료합니다.
```
\q
```

#### 환경 설정 검증

환경 구축 성공 여부를 확인 및 보장하기 위해 아래의 작업을 통해 검증할 수 있습니다.
1. 다음 명령어를 실행하여 Apache의 기본 루트 디렉터리 `/var/www/html`에서 `test.php` 테스트 파일을 생성합니다.
```
vim /var/www/html/test.php
```
2. **i**를 눌러 편집 모드로 바꾸고 다음 내용을 입력합니다.
```
<?php
echo '<title>Test Page</title>';
phpinfo()
?>
```
3. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 뒤로 돌아갑니다.
4. 브라우저에서 해당 `test.php`파일에 액세스하고 환경 설정 성공 여부를 조회합니다.
```
http://CVM의 공인 IP/test.php 
```
다음 페이지가 나타나면 LAMP 환경 설정 성공을 의미합니다.
![](https://main.qcloudimg.com/raw/f511b15ac3016d710c2b1f833e69448d.png)




### 3단계: Discuz! 설치 및 설정  [](id:InstallDiscuz)

#### Discuz! 다운로드 
다음 명령어를 실행하여 설치 패키지를 다운로드 합니다.
```
git clone https://gitee.com/Discuz/DiscuzX.git
```

#### 설치 준비 작업
1. 다음 명령어를 실행하여 다운로드 완료한 설치 디렉터리로 이동합니다.
```
cd DiscuzX
```
2. 다음 명령어를 실행하여 "upload" 폴더 내의 모든 파일을 `/var/www/html/`로 복사합니다.
```
cp -r upload/* /var/www/html/
```
3. 다음 명령어를 실행하여 쓰기 권한을 기타 사용자에게 부여합니다.
```
chmod -R 777 /var/www/html
```

#### Discuz! 설치
1. Web 브라우저 주소창에 Discuz! 사이트의 IP 주소(즉, CVM 인스턴스의 공용 IP 주소) 또는 [관련 작업](#ConfigureDomain)을 통해 획득한 가용 도메인을 입력하면 바로 Discuz! 설치 인터페이스를 확인할 수 있습니다.
<dx-alert infotype="explain" title="">
본문은 설치 단계만 안내합니다. 버전이 너무 낮다는 보안 경고가 있을 경우 더 높은 버전의 이미지를 사용하는 것이 좋습니다.
</dx-alert>
2. **동의**를 클릭하여 설치 환경 확인 페이지로 이동합니다.
3. 현재 상태가 정상임을 확인한 후, **다음 단계**를 클릭하여 실행 환경 설정 페이지로 이동합니다.
4. 새로 설치를 선택하고 **다음 단계**를 클릭하여 데이터베이스 생성 페이지로 이동합니다.
5. 페이지 알림에 따라 정보를 작성하여 Discuz!를 위한 1개의 데이터베이스를 생성합니다.
<dx-alert infotype="notice" title="">
- [필수 소프트웨어 설치](#InstallNecessarySoftware)에서 설정한 root 계정과 비밀번호를 이용해 데이터베이스에 연결하고 시스템 메일함, 관리자 계정, 비밀번호와 Email을 설정하십시오.
- 자신의 관리자 아이디와 비밀번호를 기억하십시오.
</dx-alert>
6. **다음 단계**를 클릭하여 설치를 시작합니다.
6. 설치 완료 후 **포럼 설치가 완료되었습니다. 여기를 클릭해 액세스하세요**를 클릭하면 바로 포럼에 액세스할 수 있습니다.


## 관련 작업[](id:ConfigureDomain)
사용자의 Discuz! 포럼 웹 사이트에 별도의 도메인을 설정할 수 있습니다. 사용자는 복잡한 IP 주소를 사용할 필요 없이 기억하기 쉬운 도메인으로 웹 사이트에 액세스할 수 있습니다. 포럼을 구축하여 학습용으로만 사용하는 일부 사용자의 경우, IP를 사용해 직접 설치 및 임시 사용이 가능하지만 이를 권장하지는 않습니다.


## FAQ
CVM 사용 도중 문제가 생겼을 경우, 아래의 문서를 참고하여 실제 상황에 따라 문제를 분석 및 해결할 수 있습니다.
- CVM 로그인 문제는 [키 관련 문제](https://intl.cloud.tencent.com/document/product/213/18120), [로그인 및 원격 연결](https://intl.cloud.tencent.com/document/product/213/17278)을 참고하십시오.
- CVM 네트워크 문제는 [IP 주소 문제](https://intl.cloud.tencent.com/document/product/213/17285), [포트 관련 문제](https://intl.cloud.tencent.com/document/product/213/2502)를 참고하십시오.
- CVM 디스크 문제는 [시스템 디스크와 데이터 디스크](https://intl.cloud.tencent.com/zh/document/product/213/17351)를 참고하십시오.



