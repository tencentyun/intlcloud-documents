## 작업 시나리오
워드프레스는 PHP로 개발된 블로그 플랫폼입니다. 이 문서에서는 CentOS 7.6이 설치된 Tencent Cloud CVM에서 비공개 WordPress 사이트를 수동으로 구축하는 방법을 설명합니다.

WordPress 사이트를 구축하려면 [CentOS 환경에서 YUM을 통해 소프트웨어 설치](https://intl.cloud.tencent.com/document/product/213/2046) 등 일반적인 Linux 명령에 익숙해야 합니다. 또한 관련 소프트웨어 프로그램의 사용법과 버전 호환성 정보를 알아야 합니다.

<dx-alert infotype="notice" title="">
Tencent Cloud는 클라우드 마켓의 이미지 환경을 통해 WordPress 사이트를 배포할 것을 권장하며, 수동 구축 과정이 오래 걸릴 수 있습니다.
</dx-alert>



## 소프트웨어
다음 소프트웨어 프로그램은 WordPress 사이트를 구축하는 데 사용됩니다.
- Linux: Linux 운영 체제, 본 문서는 CentOS 7.6을 예시로 사용합니다.
- Nginx: Web 서버, 본 문서는 Nginx 1.17.5을 예시로 사용합니다.
- MariaDB: 데이터베이스, 본 문서는 MariaDB 10.4.8을 예시로 사용합니다.
- PHP: 스크립트 언어, 본 문서는 PHP 7.2.22를 예시로 사용합니다.
- WordPress: 블로그 플랫폼, 본 문서는 WordPress 5.0.4를 예시로 사용합니다.

## 작업 단계 
### 1단계: CVM(Cloud Virtual Machine) 로그인
[Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)합니다. 실제 작업 스타일에 따라 다른 로그인 방식을 선택할 수도 있습니다.
- [원격 로그인 소프트웨어를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)



### 2단계: LNMP 환경 수동 구축
LNMP는 Linux, Nginx, MariaDB 및 PHP의 약칭입니다. 웹 서버를 위한 가장 일반적인 실행 환경 중 하나입니다. CVM 인스턴스를 생성하고 로그인한 후 [LNMP 환경 수동 구축](https://intl.cloud.tencent.com/document/product/213/32733)을 참고하여 LNMP 환경을 구축할 수 있습니다.


### 3단계: WordPress 데이터베이스 구성[](id:database)


<dx-alert infotype="notice" title="">
사용자 인증 방법은 MariaDB 버전에 따라 다릅니다. 자세한 내용은 MariaDB 공식 웹 사이트를 참고하십시오.
</dx-alert>


1. 아래의 명령어를 실행하여 MariaDB에 진입하십시오.
```shellsession
mysql
```
2. 아래의 명령어를 실행하여 “wordpress”와 같은 MariaDB 데이터베이스를 생성하십시오.
```shellsession
CREATE DATABASE wordpress;
```
3. 아래의 명령어를 실행하여 “user”와 같은 새로운 사용자를 추가하십시오. 로그인 비밀번호는 ‘123456’입니다.
```shellsession
CREATE USER 'user'@'localhost' IDENTIFIED BY '123456';
```
4. 아래의 명령어를 실행하여 사용자에게 “wordpress” 데이터베이스의 모든 권한을 부여하십시오.
```shellsession
GRANT ALL PRIVILEGES ON wordpress.* TO 'user'@'localhost' IDENTIFIED BY '123456';
```
5. 아래의 명령어를 실행하여 root 계정 비밀번호를 설정하십시오.
<dx-alert infotype="explain" title="">
CentOS 시스템의 MariaDB 10.4에 root 계정 ‘비밀번호 없이 로그인’ 기능이 추가되었습니다. 아래의 순서대로 root 계정 비밀번호를 설정하고 기억하십시오.
</dx-alert>
```shellsession
ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD('비밀번호를 입력하십시오.');
```
6. 아래의 명령어를 실행하여 모든 구성을 활성화하십시오.
```shellsession
FLUSH PRIVILEGES;
```
7. 아래의 명령어를 실행하여 MariaDB를 종료하십시오.
```shellsession
\q
```


### 4단계: WordPress 설치 및 설정
#### WordPress 다운로드


<dx-alert infotype="explain" title="">
WordPress는 WordPress 공식 홈페이지에서 최신 중국어 버전의 WordPress를 다운로드하여 설치할 수 있으며, 이 튜토리얼에서는 WordPress 중국어 버전을 사용합니다.
</dx-alert>


1. 아래의 명령어를 실행하여 웹 사이트 디렉터리에서 PHP-Nginx 구성 테스트에 사용하는 ‘index.php’ 파일을 삭제하십시오.
```shellsession
rm -rf /usr/share/nginx/html/index.php
```
2. 아래의 명령어를 차례대로 실행하여 ‘/usr/share/nginx/html/’ 디렉터리에 진입한 뒤 WordPress를 다운로드 및 압축 해제 하십시오.
```shellsession
cd /usr/share/nginx/html
```
```shellsession
wget https://cn.wordpress.org/wordpress-5.0.4-zh_CN.tar.gz
```
```shellsession
tar zxvf wordpress-5.0.4-zh_CN.tar.gz
```


#### WordPress 구성 파일 수정
1. 아래의 명령어를 차례대로 실행하여 WordPress 설치 디렉터리에 진입한 뒤 ‘wp-config-sample.php’ 파일을 ‘wp-config.php’ 파일로 복제하십시오. 본래의 예시 구성 파일은 백업되어 보존됩니다.
```shellsession
cd /usr/share/nginx/html/wordpress
```
```shellsession
cp wp-config-sample.php wp-config.php
```
2. 아래의 명령어를 실행하여 새로 생성된 구성 파일을 연 뒤 편집하십시오.
```shellsession
vim wp-config.php
```
3. **i**를 눌러 편집 모드로 들어갑니다. 파일에서 MySQL 섹션을 찾아 [WordPress 데이터베이스 구성](#database)에 설명된 대로 설정을 수정합니다.
```shellsession
	// ** MySQL settings - You can get this info from your web host ** //
	/** The name of the database for WordPress */
	define('DB_NAME', 'wordpress');
	
	/** MySQL database username */
	define('DB_USER', 'user');
	
	/** MySQL database password */
	define('DB_PASSWORD', '123456');
	
	/** MySQL hostname */
	define('DB_HOST', 'localhost');
```
4. 수정 완료 후, **Esc**키를 누르고 **:wq**를 입력합니다. 그런 다음 변경 사항을 저장하고 파일을 닫습니다.

### 5단계: WordPress 설치 확인
1. 브라우저 주소란에 `http://도메인 이름 또는 CVM 인스턴스 공용 IP/wordpress 폴더`를 예시처럼 입력하십시오.
```shellsession
http://192.xxx.xxx.xx/wordpress
```
WordPress 설치 페이지로 이동하여 WordPress 구성을 시작하십시오.
2. WordPress 설치 마법사에 따라 아래의 설치 정보를 입력하고 **WordPress 설치**를 클릭해 설치를 완료합니다.
<table>
	<th style="width: 18%;">필요 정보</th>
	<th style="width: 25%;">설명</th>
					<tr>
					<td>
							웹 사이트 제목
					</td>
					<td>
							WordPress 웹 사이트 명칭
					</td>
			</tr>
				<tr>
					<td>
							사용자 이름
					</td>
					<td>
							WordPress 관리자 이름. 보안을 위해 크랙되기 쉬운 admin이 아닌 다른 이름을 사용하십시오.
					</td>
			</tr>
			<tr>
					<td>
							비밀번호
					</td>
					<td>
							기본 강력한 암호 또는 사용자 정의 암호를 사용합니다. 이전 비밀번호를 사용하지 마시고 비밀번호를 안전한 곳에 보관하십시오.
					</td>
			</tr>
				<tr>
					<td>
							이메일 주소
					</td>
					<td>
							알림을 수신할 이메일 주소입니다.
					</td>
			</tr>
	</table>
이제 WordPress 사이트에 로그인하여 블로그를 게시할 수 있습니다.

## 관련 작업
WordPress 사이트의 도메인 이름을 설정할 수 있습니다. 이러한 방식으로 사용자는 복잡한 IP 주소 대신 도메인 이름을 사용하여 사이트를 방문할 수 있습니다. 학습 목적으로 사이트를 구축하는 경우 사이트에 대한 IP 주소를 설정할 수 있습니다. 그러나 이 방법은 다른 경우에는 권장되지 않습니다.


## FAQ
CVM 사용 도중 문제가 생겼을 경우, 아래의 문서를 참고하여 실제 상황에 따라 문제를 분석 및 해결할 수 있습니다.
- CVM 로그인 문제는 [키 관련 문제](https://intl.cloud.tencent.com/document/product/213/18120), [로그인 및 원격 연결](https://intl.cloud.tencent.com/document/product/213/17278)을 참고하십시오.
- CVM 네트워크 문제는 [IP 주소 문제](https://intl.cloud.tencent.com/document/product/213/17285), [포트 관련 문제](https://intl.cloud.tencent.com/document/product/213/2502)를 참고하십시오.
- CVM 디스크 문제는 [시스템 디스크와 데이터 디스크](https://intl.cloud.tencent.com/document/product/213/17351)를 참고하십시오.



