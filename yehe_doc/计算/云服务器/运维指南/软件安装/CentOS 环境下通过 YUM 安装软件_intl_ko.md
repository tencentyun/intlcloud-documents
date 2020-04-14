## 작업 시나리오
Cloud Virtual Machine(CVM)의 소프트웨어 설치 효율을 높이고, 소프트웨어 다운로드 및 설치 비용을 절감하기 위해 Tencent Cloud는 YUM 다운로드 소스를 제공하고 있습니다. CentOS 환경에서 `yum` 명령어를 통해 소프트웨어를 빠르게 설치할 수 있습니다. YUM 다운로드 소스의 경우, 소프트웨어 보관소를 추가할 필요 없이 바로 패키지를 설치할 수 있습니다.

## 작업 순서

### 소프트웨어 설치

1. root 계정으로 CVM에 로그인합니다.
2. 다음 명령어를 실행하여 소프트웨어를 설치합니다.
> CentOS 7 시스템부터 YUM 소스의 기본 데이터베이스 설치 패키지로 MariaDB를 사용하고 있습니다. CentOS 7 및 이상 버전의 운영 체제에서 `yum` 명령어를 사용해 MySQL 패키지를 설치하면 MySQL을 사용할 수 없게 됩니다. 완전히 호환되는 MariaDB를 선택하거나 [참조](https://www.linode.com/docs/databases/mysql/how-to-install-mysql-on-centos-7)하여 MySQL 하위 버전을 설치할 수 있습니다.
>
```
yum install 소프트웨어 명칭
``` 
소프트웨어 설치 과정에서 시스템이 자동으로 관련 패키지 및 종속 관계를 검색하고, 검색한 패키지가 적합한지 확인할 수 있도록 인터페이스에 알림을 표시합니다.
예시, `yum install PHP` 명령어를 실행하여 PHP를 설치한 후의 인터페이스는 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/18c4a59a3e0e92b0dcafff662d1e3673.png)
4. 패키지가 적합한지 확인한 후 `y`를 입력하고 **Enter**를 눌러 소프트웨어 설치를 시작합니다.
인터페이스에 `Complete`가 표시되면 설치 완료입니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/fb2fbd8becd4576f67b47226a82ee033.png)

### 설치된 소프트웨어의 정보 조회

소프트웨어를 설치한 후 실제 수요에 맞게 명령어를 실행하여 정보를 조회합니다.
- 다음 명령어를 실행하여 패키지의 자세한 설치 디렉터리를 조회합니다.
```
rpm -ql 소프트웨어 이름
```
예시, `rpm -ql php` 명령어를 실행하여 PHP의 상세 설치 디렉터리를 조회합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/fda98060c9f6ba359d7e705de8d336bb.png)
- 다음 명령어를 실행하여 패키지의 버전 정보를 조회합니다.
```
rpm -q
```
예시, `rpm -q php` 명령어를 실행하여 PHP의 버전 정보를 조회합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/35e1ecee46bc55a5d2510dce59360ecc.png)


