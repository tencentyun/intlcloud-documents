## 작업 시나리오
WordPress는 PHP 언어를 사용해 개발된 블로그 플랫폼으로, WordPress로 개인 블로그 플랫폼을 구축할 수 있습니다. 본 문서는 CentOS 7.6 운영 체제의 Tencent Cloud CVM을 예로, WordPress 개인 사이트를 수동 구축하는 방법을 소개합니다.

WordPress 개인 블로그 구축을 위해서는 [CentOS 환경에서 YUM을 통해 소프트웨어 설치](https://intl.cloud.tencent.com/document/product/213/2046) 등 Linux 상용 명령어를 숙지해야 하며, 설치된 소프트웨어의 사용 및 버전 호환성에 대한 이해도가 있어야 합니다.

## 소프트웨어 버전 예시
본 문서에서 구축한 WordPress 개인 사이트의 구성 버전 및 설명은 다음과 같습니다.
- Linux: Linux 운영 체제로, 본 문서는 CentOS 7.6 을 예로 듭니다.
- Nginx: Web 서버로, 본 문서는 Nginx 1.17.5 를 예로 듭니다.
- MariaDB: 데이터베이스로, 본 문서는 MariaDB 10.4.8 을 예로 듭니다.
- PHP: 스크립트 언어로, 본 문서는 PHP 7.2.22 를 예로 듭니다.
- WordPress: 블로그 플랫폼으로, 본 문서는 WordPress 5.0.4 를 예로 듭니다.

## 작업 순서 
### 1단계: CVM 로그인
- [표준 방식으로 Linux 인스턴스 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436). 실제 작업 스타일에 따라 다른 로그인 방식을 선택할 수도 있습니다:
- [원격 로그인 소프트웨어를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSH를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32501)



### 2단계: LNMP 환경 수동 구축
LNMP는 Linux, Nginx, MariaDB 및 PHP의 약칭으로, Web 서버에서 가장 흔한 운영 환경 조합 중 하나입니다. CVM 인스턴스 생성 및 로그인 후, [LNMP 환경 수동 구축](https://intl.cloud.tencent.com/document/product/213/32733)을 참조하여 기본 환경을 구축합니다.

<span id="database"></span>
### 3단계: WordPress 데이터베이스 설정
> MariaDB 버전에 따라 사용자 인증 방식 설정에 차이가 있습니다. 자세한 순서는 MariaDB 공식 웹 사이트를 참조 바랍니다.
>
1. 다음 명령어를 실행하여 MariaDB에 진입합니다.
```
mysql
```
2. 다음 명령어를 실행하여 MariaDB 데이터베이스를 생성합니다. 예: “wordpress”
```
CREATE DATABASE wordpress;
```
3. 다음 명령어를 실행하여 새로운 사용자를 생성합니다. 예: “user”, 로그인 비밀번호 ‘123456’
```
CREATE USER 'user'@'localhost' IDENTIFIED BY '123456';
```
4. 다음 명령어를 실행하여 사용자에게 “wordpress” 데이터베이스의 모든 권한을 부여합니다.
```
GRANT ALL PRIVILEGES ON wordpress.* TO 'user'@'localhost' IDENTIFIED BY '123456';
```
5. 다음 명령어를 실행하여 모든 설정을 적용합니다.
```
FLUSH PRIVILEGES;
```
6. 다음 명령어를 실행하여 MariaDB를 종료합니다.
```
\q
```

### 4단계: root 계정 설정
1. 다음 명령어를 실행하여 MariaDB에 진입합니다.
```
mysql
```
2. 다음 명령어를 실행하여 root 계정 비밀번호를 설정합니다.
> MariaDB 10.4 는 CentOS 시스템에 비밀번호 없이 root 계정 로그인 기능을 추가했습니다. 다음의 순서대로 root 계정 비밀번호를 설정 및 기억하세요.
>
```
ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD('비밀번호 입력');
```
3. 다음 명령어를 실행하여 MariaDB를 종료합니다.
```
\q
```


### 5단계: WordPress 설치 및 구성
#### WordPress 다운로드
> WordPress 공식 홈페이지에서 WordPress 최신 중국어 버전을 다운로드 및 설치할 수 있습니다. 본 튜토리얼에서는 WordPress 중국어 버전을 사용했습니다.
>
1. 다음 명령어를 실행하여 웹 사이트 디렉터리에서 PHP-Nginx 구성 테스트에 사용되는 ‘index.php’ 파일을 삭제합니다.
```
rm -rf /usr/share/nginx/html/index.php
```
2. 다음 명령어를 차례대로 실행하여 ‘/usr/share/nginx/html/’ 디렉터리에 들어간 뒤 WordPress를 다운로드 및 압축 해제합니다.
```
cd /usr/share/nginx/html
wget https://cn.wordpress.org/wordpress-5.0.4-zh_CN.tar.gz
tar zxvf wordpress-5.0.4-zh_CN.tar.gz
```


#### WordPress 구성 파일 수정
1. 다음 명령어를 차례대로 실행하여 WordPress 설치 디렉터리에 진입한 뒤 ‘wp-config-sample.php’ 파일을 ‘wp-config.php’ 파일로 복사하고, 기존의 예시 구성 파일은 백업해 보존합니다.
```
cd /usr/share/nginx/html/wordpress
cp wp-config-sample.php wp-config.php
```
2. 다음 명령어를 실행하여 새로 생성된 구성 파일을 열고 편집합니다.
```
vim wp-config.php
```
3. “**i**” 를 눌러 편집 모드로 전환한 뒤, 파일 중 MySQL 부분을 찾아 관련 구성 정보를 [WordPress 데이터베이스 구성](#database)의 콘텐츠로 수정합니다.
```
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
4. 수정 후, “**Esc**”를 누르고 “**:wq**”를 입력하여 파일을 저장하고 돌아갑니다.

### 6단계: WordPress 설치 인증
1. 다음 예시와 같이, 브라우저 주소란에 ‘http://도메인 또는 CVM 인스턴스의 공인 IP/wordpress 폴더’를 입력합니다.
```
http://192.xxx.xxx.xx/wordpress
```
WordPress 설치 페이지로 이동하여 WordPress 설정을 시작합니다.

2. WordPress 설치 마법사에 따라 아래의 설치 정보를 입력하고, [WordPress 설치]를 클릭해 설치를 완료합니다.
<table>
	<th style="width: 18%;">필요 정보</th>
	<th style="width: 25%;">설명</th>
					<tr>
					<td>
							사이트 제목
					</td>
					<td>
							WordPress 웹 사이트 명칭입니다.
					</td>
			</tr>
				<tr>
					<td>
							사용자 이름
					</td>
					<td>
							WordPress 관리자 명칭입니다. 기본 설정된 사용자 이름인 admin보다 크래킹이 어려우므로, 보안을 위해 admin 이름과 다르게 설정하시기 바랍니다.
					</td>
			</tr>
			<tr>
					<td>
							비밀번호
					</td>
					<td>
							기본 설정된 강력한 비밀번호 또는 사용자 정의 비밀번호를 사용할 수 있습니다. 기존 비밀번호와 중복 사용하지 마시고, 비밀번호를 안전한 위치에 저장하세요.
					</td>
			</tr>
				<tr>
					<td>
							사용자 이메일
					</td>
					<td>
							공지를 받을 이메일 주소입니다.
					</td>
			</tr>
	</table>
이제 WordPress 블로그에 로그인하여 블로그에 게시글을 업로드할 수 있습니다.

## 관련 작업
WordPress 블로그 웹 사이트에 단독 도메인을 설정할 수 있으므로, 복잡한 IP 주소를 사용할 필요 없이 기억하기 쉬운 도메인을 사용해 웹 사이트에 액세스할 수 있습니다. 학습용으로 웹 사이트 구축한 일부 사용자의 경우 IP로 바로 설치해 임시로 사용할 수 있지만 권장하지 않습니다.

## FAQ
CVM 사용 과정 중 문제가 발생할 경우, 아래의 문서를 참조하여 실제 상황에 맞게 문제를 분석 및 해결할 수 있습니다.
- CVM 로그인 문제는 [비밀번호 및 키](https://intl.cloud.tencent.com/document/product/213/18120), [로그인 및 원격 연결](https://intl.cloud.tencent.com/document/product/213/17278)을 참조 바랍니다.
- CVM 네트워크 문제는 [IP 주소](https://intl.cloud.tencent.com/document/product/213/17285), [포트 및 보안 그룹](https://intl.cloud.tencent.com/document/product/213/2502)을 참조 바랍니다.
- CVM 디스크 문제는 [시스템 디스크와 데이터 디스크](https://intl.cloud.tencent.com/document/product/213/17351)를 참조 바랍니다.

