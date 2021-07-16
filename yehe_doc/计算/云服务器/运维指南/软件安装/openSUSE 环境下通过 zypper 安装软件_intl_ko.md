## 작업 시나리오
클라우드 서버에서 소프트웨어 설치의 효율성을 향상하고 소프트웨어 다운로드 및 설치 비용을 줄이기 위해 Tencent Cloud는 zypper 다운로드 소스를 제공합니다. openSUSE 운영 체제 및 일부 SLES 클라우드 서버 사용자는 zypper를 통해 소프트웨어를 빠르게 설치할 수 있습니다. 본 문서는 openSUSE 운영 체제를 예로 사용해 zypper를 통한 소프트웨어의 빠른 설치를 안내합니다.

## 작업 순서
### 소프트웨어 소스 조회

1. root 계정을 사용해 openSUSE 운영 체제의 클라우드 서버에 로그인하십시오.
2. `zypper service-list` 또는 `zypper sl` 커맨드를 실행하여 소프트웨어 소스를 나열하십시오.
예를 들어,  `zypper sl` 커맨드를 실행할 경우 다음과 같은 정보를 리턴합니다.
![](https://main.qcloudimg.com/raw/ee336605784eca333f10777ccb7cf5ed.png)
 - 소프트웨어 소스에 가용 소스가 추가된 경우 [패키지 설치](#SearchPackage)를 참조하십시오.
 - 소프트웨어 소스가 가용 소스를 추가하지 않으면 [소프트웨어 소스 추가](#AddSoftwareSource)를 참조하십시오.

<spam id="AddSoftwareSource"></span>
### 소프트웨어 소스 추가

`zypper service-add` 또는 `zypper sa` 커맨드를 실행하여 수동으로 소프트웨어 소스를 추가하십시오.
예를 들어, `zypper sa` 커맨드를 실행할 경우 다음 예시를 참조합니다.
```
zypper sa -t YaST http://mirrors.cloud.tencent.com/opensuse opensuse
zypper sa -t YaST http://mirrors.cloud.tencent.com/opensuse/update update
```

<span id="SearchPackage"></span>
### 패키지 설치

1. `zypper search` 또는 `zypper se` 커맨드를 실행하여 패키지를 검색하십시오.
예를 들어, Nginx 패키지를 검색할 경우 다음 커맨드를 실행할 수 있습니다.
```
zypper se nginx
```
다음과 같은 결과를 리턴합니다.
![](https://main.qcloudimg.com/raw/292106a01b048171007247cb9cdf00c0.png)
2. 검색된 패키지 이름을 기준으로 `zypper install` 또는 `zypper in` 커맨드를 실행하여 소프트웨어를 설치하십시오.
> 여러 소프트웨어를 설치해야 하는 경우 패키지 이름은 공백으로 구분됩니다.
> 소프트웨어를 설치할 때, 소프트웨어에 종속성 패키지가 필요한 경우 종속성 패키지를 직접 설치할 필요 없이 소프트웨어가 자동으로 다운로드되어 설치됩니다.
> 
예를 들어, Nginx를 설치할 경우 다음 커맨드를 실행할 수 있습니다.
```
zypper install nginx
```
예를 들어, PHP 및 PHP-FPM과 같은 소프트웨어를 설치할 경우 다음 커맨드를 실행할 수 있습니다.
```
zypper install MySQL-server-community php5-mysql php5 php5-fpm
```


### 설치된 소프트웨어의 정보 조회

1. 소프트웨어 설치가 완료되면 다음 커맨드를 실행하여 소프트웨어 패키지의 구체적인 설치 디렉터리를 조회하십시오.
```
rpm -ql
```
예를 들어, Nginx 패키지의 특정 설치 디렉터리를 조회할 경우 다음 커맨드를 실행하십시오.
```
rpm -ql nginx
```
다음과 같은 정보를 리턴합니다.
![](https://main.qcloudimg.com/raw/b4ad19a8735041bf78942f5ea351dc2e.png)
2. 다음 커맨드를 실행하여 소프트웨어 패키지의 버전 정보를 조회하십시오.
```
rpm -q
```
예를 들어, Nginx 패키지의 버전 정보를 조회할 경우 다음 커맨드를 실행하십시오.
```
rpm -q nginx
```
다음과 같은 정보를 리턴합니다.
![](https://main.qcloudimg.com/raw/9950192d2cf51c7ab30c2109b3e52d14.png)
