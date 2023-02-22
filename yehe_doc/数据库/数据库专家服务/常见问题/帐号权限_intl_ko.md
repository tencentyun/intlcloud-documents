### 서버에 설치된 MySQL 클라이언트에 TencentDB for MySQL 인스턴스 액세스 권한을 어떻게 부여합니까?
[MySQL 콘솔](https://console.cloud.tencent.com/cdb)로 이동하여 MySQL 클라이언트가 설치된 서버의 주소를 수정하여 액세스를 제어할 수 있습니다. 

자세한 내용은 [버킷 개요](https://intl.cloud.tencent.com/document/product/436/38493)를 참고하십시오.  

### 데이터 관리 콘솔(DMC)에 로그인할 수 없으면 어떻게 해야 합니까?
1) 잘못된 데이터베이스 계정을 사용하고 있을 수 있습니다. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)로 이동하여 로그인 계정에서 액세스할 데이터베이스의 호스트 주소 클라이언트에 권한을 부여했는지 확인하고, 새 호스트를 ‘%’ 또는 MySQL 클라이언트가 설치된 서버의 주소로 설정하여 계정 액세스 권한을 부여합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/6iPR545_2.png)
자세한 내용은 [버킷 개요](https://intl.cloud.tencent.com/document/product/436/38493)를 참고하십시오.  

root 계정을 사용하여 DMC에 로그인할 수도 있습니다.

2) 올바른 계정을 사용하고 있다면 비밀번호가 올바르지 않을 수 있습니다. 올바른 비밀번호를 입력하거나 [비밀번호 재설정](https://intl.cloud.tencent.com/document/product/236/31901)하십시오.


### 데이터베이스/테이블을 생성할 수 없으면 어떻게 해야 합니까?
데이터베이스 또는 테이블을 생성할 권한이 없는 데이터베이스 계정을 사용하고 있을 수 있습니다. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인하여 인스턴스 이름을 클릭한 후 데이터베이스 관리에서 계정 관리로 이동하여 계정을 찾은 후 작업 열에서 권한 수정을 클릭하여 아래와 같이 권한을 부여하십시오.  
![](https://staticintl.cloudcachetci.com/yehe/backend-news/tQ3Q678_3.png)

### sql_mode와 같은 데이터베이스 매개변수 수정 권한이 없으면 어떻게 해야 합니까?
매개변수 수정 권한이 없는 서브 계정을 사용 중일 수 있습니다. 루트 계정을 사용하거나 [CAM](https://intl.cloud.tencent.com/document/product/236/14469)으로 서브 계정에 권한을 부여할 수 있습니다.

### 서브 계정에 TencentDB for MySQL 인스턴스 수정 권한을 어떻게 부여합니까?
사용자에게 TencentDB 인스턴스를 생성하고 관리할 수 있는 권한을 부여하려면 [CDB의 전체 읽기/쓰기 정책](https://intl.cloud.tencent.com/document/product/236/14468)에 설명된 대로 사용자에 대한 QcloudCDBFullAccess 정책을 구현할 수 있습니다.

