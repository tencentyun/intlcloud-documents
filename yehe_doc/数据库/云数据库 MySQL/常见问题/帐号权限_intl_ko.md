### 어느 한 호스트 주소의 클라이언트에서 TencentDB for MySQL에 액세스할 수 있도록 권한을 주는 방법은 무엇인가요?
[MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 데이터베이스 계정을 수정하여 호스트 주소에 권한을 설정하면 데이터베이스에 액세스할 수 있습니다. 
  
### 데이터베이스 관리 콘솔(DMC)에 로그인할 수 없는 이유는 무엇인가요?
1) 사용 중인 서비스 계정으로 인한 것일 수 있습니다. [데이터베이스 계정 관리](https://console.cloud.tencent.com/cdb)로 이동하여 로그인 계정에서 액세스할 데이터베이스의 호스트 주소 클라이언트에 권한을 부여했는지 확인하고, 호스트 주소를 '%' 혹은 액세스할 클라이언트 호스트 주소로 설정해야 합니다.
![](https://main.qcloudimg.com/raw/2e0f60d3237e8e244b51dd7e164de315.png)  

또한, root 계정을 통해 DMC에 직접 로그인하는 방법도 있습니다.

2) 위의 문제로 인한 것이 아니라면, 계정 비밀번호 오류일 수 있습니다. 비밀번호를 다시 입력하거나 [비밀번호를 재설정](https://intl.cloud.tencent.com/document/product/236/31901)하시길 바랍니다.


### 데이터베이스/테이블을 생성할 수 없는 이유는 무엇인가요?
로그인한 계정이 서비스 계정일 경우 데이터베이스/테이블을 생성할 권한이 없는 것일 수 있습니다. 아래 이미지와 같이 [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 해당 계정에 권한을 부여하시기 바랍니다.  
![](https://main.qcloudimg.com/raw/b33188cf3aba103b415c0ecc38fb0168.png)

### sql_mode와 같은 데이터베이스 매개변수를 수정할 권한이 없는 이유는 무엇인가요?
사용자의 서브 계정에 인스턴스 매개변수를 수정할 권한이 없는 것일 수 있습니다. 루트 계정으로 작업하거나 [CAM 액세스 관리](https://intl.cloud.tencent.com/document/product/236/14469)로 이동하여 서브 계정에 관련 작업 권한을 부여해야 합니다.

### 서브 계정에서 MySQL 권한을 수정하도록 설정하는 방법은 무엇인가요?
사용자에게 CDB 인스턴스를 생성하고 관리할 수 있는 권한을 주고자 한다면, 해당 사용자의 이름을 QcloudCDBFullAccess 정책으로 설정할 수 있습니다. 자세한 내용은 [CBD의 전체 읽기/쓰기 정책](https://intl.cloud.tencent.com/document/product/236/14468)을 참조하십시오.


