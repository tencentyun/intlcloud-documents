## 작업 시나리오
Tencent Cloud에서는 CVM에서 사용자의 소프트웨어 설치 효율을 향상하고, 다운로드 및 설치 비용을 절감하기 위해 YUM 다운로드 소스를 제공하고 있습니다. CentOS 환경에서 사용자는 `yum` 명령어를 실행해 빠르게 소프트웨어를 설치할 수 있습니다. 또한 YUM 다운로드 소스 역시 소프트웨어 보관소를 추가할 필요 없이 바로 소프트웨어 패키지를 설치할 수 있습니다.

## 작업 순서

### 소프트웨어 설치

1. root 계정으로 CVM에 로그인합니다.
2. 다음 명령어를 실행하여 소프트웨어를 설치합니다.
> 참고: CentOS 7 시스템부터는 MariaDB가 yum 소스의 기본 데이터베이스 설치 패키지가 되었으므로, CentOS 7 이상의 운영 체제에서 yum 명령어를 사용해 MySQL 패키지를 설치하면 MySQL을 사용할 수 없습니다. 완전히 호환되는 MariaDB를 사용하거나 [이곳](https://www.linode.com/docs/databases/mysql/how-to-install-mysql-on-centos-7)을 참조하여 낮은 버전의 MySQL을 설치할 수 있습니다.
>
```
yum install 소프트웨어 이름
``` 
소프트웨어를 설치하는 과정에서, 시스템은 관련된 소프트웨어 패키지와 종속 관계를 자동으로 검색하고, 검색한 소프트웨어 패키지의 적합 여부를 인터페이스 알림을 통해 사용자에게 알려줍니다.
예시, `yum install PHP` 명령어를 실행하여 PHP를 설치하면 인터페이스에 아래와 같이 표시됩니다.
![](https://main.qcloudimg.com/raw/18c4a59a3e0e92b0dcafff662d1e3673.png)
4. 소프트웨어 패키지에 문제가 없는지 확인하고, `y`를 입력한 후 **Enter**를 누르면 소프트웨어 설치를 시작합니다.
아래 이미지와 같이, 인터페이스에 `Complete`라고 표시되면 설치 완료입니다.
![](https://main.qcloudimg.com/raw/fb2fbd8becd4576f67b47226a82ee033.png)

### 설치한 소프트웨어 정보 조회

소프트웨어 설치가 완료되면 다음 명령어를 실제 수요에 맞게 실행하여 정보를 확인합니다.
- 다음 명령어를 실행하여 소프트웨어 패키지의 실제 설치 디렉터리를 조회합니다.
```
rpm -ql 소프트웨어 이름
```
예시, 아래 이미지와 같이 `rpm -ql php` 명령어를 실행하여 PHP의 실제 설치 디렉터리를 확인합니다.
![](https://main.qcloudimg.com/raw/fda98060c9f6ba359d7e705de8d336bb.png)
- 다음 명령어를 실행하여 소프트웨어 패키지의 버전 정보를 조회합니다.
```
rpm -q
```
예시, 아래 이미지와 같이 `rpm -q php` 명령어를 실행하여 PHP의 버전 정보를 확인합니다.
![](https://main.qcloudimg.com/raw/35e1ecee46bc55a5d2510dce59360ecc.png)


