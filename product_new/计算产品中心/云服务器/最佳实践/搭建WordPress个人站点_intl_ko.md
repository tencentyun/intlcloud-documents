## 작업 시나리오
WordPress는 PHP 언어를 사용해 개발한 블로그 플랫폼입니다. WordPress를 통해 개인의 블로그 플랫폼을 구축해 사용할 수 있습니다. 본 문서는 CentOS 7.6 운영 체제의 Tencent Cloud 서버를 예시로 하며, WordPress 개인 웹 사이트를 수동으로 구축합니다.



## 기능 요구 사항
WordPress 개인 블로그 구축을 위해 [CentOS 환경에서 YUM을 통해 소프트웨어 설치](https://intl.cloud.tencent.com/document/product/213/2046) 등 상용 커맨드인 Linux 커맨드에 능숙해야 합니다. 설치된 소프트웨어의 사용 및 버전 호환성에 대해 이해해야 합니다.
> Tencent Cloud는 클라우드 마켓의 미러 이미지 환경을 통해 사용자의 WordPress 개인 블로그를 배포하길 권장합니다. 수동 구축 과정은 시간이 오래 걸릴 수 있습니다. 구체적인 절차는 [미러 이미지를 사용해 WordPress 개인 웹 사이트 구축](https://cloud.tencent.com/document/product/213/9740)을 참조하십시오.






## 작업 순서 
### 1단계: CVM 로그인
Linux CVM에 로그인하십시오. 아직 로그인하지 않았을 경우, CVM의 로그인 비밀번호 및 공용 네트워크 IP를 준비하십시오. [표준 방식을 사용해 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참조하여 로그인을 완료하십시오.

### 2단계: LNMP 환경 수동 구축
LNMP는 Linux, Nginx, MariaDB 및 PHP의 약어입니다. 이 조합은 가장 흔한 Web 서버 운영 환경 중 하나입니다. CVM 인스턴스 생성 및 로그인 후, [LNMP 환경 수동 구축](https://cloud.tencent.com/document/product/213/38056)을 참조하여 기본 환경 구축을 완료하십시오.



### 3단계: WordPress 데이터베이스 구성<span id="database"></span>
> MariaDB 버전에 따라, 사용자 신원 인증 방식 설정에는 차이가 있습니다. 자세한 절차는 MariaDB 공식 웹 사이트를 참조하십시오.
>
1. 아래의 명령어를 실행하여 MariaDB에 진입하십시오.
```
mysql
```
2. 아래의 명령어를 실행하여 “wordpress”와 같은 MariaDB 데이터베이스를 생성하십시오.
```
CREATE DATABASE wordpress;
```
3. 아래의 명령어를 실행하여 “user”와 같은 새로운 사용자를 추가하십시오. 로그인 비밀번호는 ‘123456’입니다.
```
CREATE USER 'user'@'localhost' IDENTIFIED BY '123456';
```
4. 아래의 명령어를 실행하여 사용자에게 “wordpress” 데이터베이스의 모든 권한을 부여하십시오.
```
GRANT ALL PRIVILEGES ON wordpress.* TO 'user'@'localhost' IDENTIFIED BY '123456';
```
5. 아래의 명령어를 실행하여 모든 구성을 활성화하십시오.
```
FLUSH PRIVILEGES;
```
6. 아래의 명령어를 실행하여 MariaDB를 종료하십시오.
```
\q
```

### 4단계: root 계정 구성
1. 아래의 명령어를 실행하여 MariaDB에 진입하십시오.
```
mysql
```
2. 아래의 명령어를 실행하여 root 계정 비밀번호를 설정하십시오.
> CentOS 시스템의 MariaDB 10.4에 root 계정 비밀번호 없이 로그인 기능을 추가했습니다. 아래의 순서를 진행해 root 계정 비밀번호를 설정하고 기억하십시오.
>
```
ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD('비밀번호를 입력하십시오.');
```
3. 아래의 명령어를 실행하여 MariaDB를 종료하십시오.
```
\q
```


### 5단계: WordPress 설치 및 구성
#### WordPress 다운로드
> WordPress는 [WordPress 공식 웹 사이트](https://wordpress.org/download/releases/)에서 WordPress 최신 중문 버전을 설치할 수 있습니다. 본 튜토리얼은 WordPress 중문 버전을 사용합니다.
>
1. 아래의 명령어를 실행하여 웹 사이트 디렉터리에서 PHP-Nginx 구성 테스트에 사용하는 ‘index.php’ 파일을 삭제하십시오.
```
rm -rf /usr/share/nginx/html/index.php
```
2. 아래의 명령어를 차례대로 실행하여 ‘/usr/share/nginx/html/’ 디렉터리에 진입한 뒤 WordPress를 다운로드 및 압축 해제 하십시오.
```
cd /usr/share/nginx/html
wget https://cn.wordpress.org/wordpress-5.0.4-zh_CN.tar.gz
tar zxvf wordpress-5.0.4-zh_CN.tar.gz
```



#### WordPress 구성 파일 수정
1. 아래의 명령어를 차례대로 실행하여 WordPress 설치 디렉터리에 진입한 뒤 ‘wp-config-sample.php’ 파일을 ‘wp-config.php’ 파일로 복제하십시오. 본래의 예시 구성 파일은 백업되어 보존됩니다.
```
cd /usr/share/nginx/html/wordpress
cp wp-config-sample.php wp-config.php
```
2. 아래의 명령어를 실행하여 새로 생성된 구성 파일을 연 뒤 편집하십시오.
```
vim wp-config.php
```
3. “**i**” 또는 “**Insert**”를 눌러 편집 모드로 전환한 뒤, 파일 중 MySQL 부분을 찾아 관련 구성 정보를 [WordPress 데이터베이스 구성](#database)의 내용을 수정하십시오.
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
4. 수정 완료 후, “**Esc**”를 누르고 “**:wq**”를 입력하여 파일을 저장하고 돌아가십시오.

### 6단계: WordPress 설치 인증
1. 브라우저 주소란에 wordpress 폴더가 추가된 CVM 인스턴스 공용 네트워크 IP를 예시처럼 입력하십시오.
```
http://192.xxx.xxx.xx /wordpress
```
WordPress 설치 페이지로 이동하여 WordPress 구성을 시작하십시오.
2. WordPress 설치 마법사에 따라 아래의 설치 정보를 입력하고 [WordPress 설치]를 클릭해 설치를 완료하십시오.
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
							WordPress 관리자 명칭. 보안상의 이유로 admin 명칭과 다르게 설정하길 권장합니다. 기본 사용자 이름이 admin과 비교하여 크래킹이 더 어렵기 때문입니다.
					</td>
			</tr>
			<tr>
					<td>
							비밀번호
					</td>
					<td>
							기본값의 비밀번호 또는 사용자 정의 비밀번호를 사용할 수 있습니다. 현재 비밀번호의 중복 사용을 금하여 비밀번호를 안전한 위치에 저장합니다.
					</td>
			</tr>
				<tr>
					<td>
							사용자 이메일
					</td>
					<td>
							알림을 수신하는 데 사용하는 이메일 주소입니다.
					</td>
			</tr>
	</table>
이제 WordPress 블로그에 로그인할 수 있으며, 블로그에 게시글을 업로드할 수 있습니다.

## 후속 작업
1. 자신의 WordPress 블로그 웹 사이트에 단독 도메인 이름을 설정할 수 있습니다. 사용자가 기억하기 쉬운 도메인 이름을 이용해 웹 사이트에 액세스할 수 있으며, 복잡한 IP 주소를 사용하지 않아도 됩니다.
[Tencent Cloud 도메인 이름 구매](https://dnspod.cloud.tencent.com/?from=qcloud)를 통해 가능합니다. 
2. 도메인 이름은 중국 서버의 웹 사이트를 가리키며, 반드시 웹 사이트 ICP비안을 진행해야 합니다. 도메인 이름이 ICP비안을 얻기 전까지 웹 사이트는 활성화되지 않습니다. Tencent Cloud를 통해 [웹 사이트 ICP비안](https://cloud.tencent.com/product/ba?from=qcloudHpHeaderBa&fromSource=qcloudHpHeaderBa)을 진행할 수 있습니다. ICP비안은 무료이며, 심사 기간은 약 20일 정도입니다.
3. Tencent Cloud의 [Tencent Cloud DNS](https://console.cloud.tencent.com/cns/domains)에 도메인 이름 확인을 구성한 후에만 사용자가 도메인 이름을 통해 웹 사이트에 액세스할 수 있습니다. 자세한 내용은 [도메인 이름 확인](https://cloud.tencent.com/document/product/302/3446)을 참조하십시오.



## FAQ
CVM 사용 과정 중 문제가 생겼을 경우, 아래의 문서를 참조하여 실제 상황과 결합하여 문제 분석 및 해결할 수 있습니다.
- CVM의 로그인 문제는 [비밀번호 및 키](https://intl.cloud.tencent.com/document/product/213/18120), [로그인 및 원격 연결](https://intl.cloud.tencent.com/document/product/213/17278)을 참조하십시오.
- CVM의 네트워크 문제는 [IP 주소](https://intl.cloud.tencent.com/document/product/213/17285), [포트 및 보안 그룹](https://intl.cloud.tencent.com/document/product/213/2502)을 참조하십시오.

