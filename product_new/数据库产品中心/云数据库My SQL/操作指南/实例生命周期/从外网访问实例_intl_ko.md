## 작업 시나리오
혹 귀하의 Cloud Virtual Machine(CVM)과 TencentDB for MySQL는 같은 지역에 배포되어있다면, 공용 네트워크 주소를 신청할 필요가 없습니다. 혹 다른 지역이나 Tencent Cloud외 시스템에 배포되면 공용 네트워크 주소로 TencentDB for MySQL(중국 홍콩과 외국 지역의 MySQL 인스턴스는 당분간 공용 네트워크를 오픈하지 않습니다)를 연결해야 합니다. 이 파일은 공용 네트워크 액세스 주소와 로그인 인스턴스에 대해 소개드립니다.

## 조작 프로세스

### 공용 네트워크 액세스 주소 오픈
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb/ )에 로그인합니다.
2. 인스턴스 리스트에서 수정하려는 인스턴스를 선택하고, 낱개 인스턴스 도메인 네임 혹은 조작 칼럼의 [관리]를 클릭하여 인스턴스 상세 페이지에 접속합니다.
![](https://main.qcloudimg.com/raw/cd32da2cfe0e7bc51bfe9d41563c4dc8.png)
3. 인스턴스 상세 페이지의 기본정보에서 [공용 네트워크 주소]를 찾아 [오픈]을 클릭합니다.
![](https://main.qcloudimg.com/raw/1ca02f08affa0a9756f041781827d864.png)
4. [확인]을 클릭하면 공용 네트워크 오픈은 처리 상태가 됩니다.
![](https://main.qcloudimg.com/raw/a1f1412c229b66b75b4ea2834cb55589.png)
5. 오픈 시에 기본정보에서 공용 네트워크 주소를 조회할 수 있습니다.
6. on/off를 통해 공용 네트워크 액세스 권한을 종료할 수 있습니다. 공용 네트워크를 재오픈 시, 도메인 네임에 대응하는 공용 네트워크 IP는 그대로 유지됩니다.

#### 로그인 인스턴스
1. 네트워크에 연결하여 MySQL 클라이언트를 설치한 서버에서 표준 MySQL 문법을 사용하여 클라우드 데이터베이스에 로그인합니다. 클라우드 데이터베이스 계정은 [계정관리]의 임의 계정을 적용할 수 있습니다.
```
mysql -h hostname -P port -u username -p
```
>
>-hostname을 목표 MySQL 데이터베이스 인스턴스의 공용 네트워크 IP 주소로 변경해주시기 바랍니다. port는 공용 네트워크의 포트 번호로 변경하고, username을 공용 네트워크에서 액세스하는 유저명으로 변경해주세요. 예를 들면 cdb_outerroot. Enter password가 팝업하면 cdb_outerroot 계정에 대응하는 비밀번호를 입력해주세요.
>- 공용 네트워크를 액세스 시에 공용 네트워크는 유저명을 액세스합니다. 원활한 액세스 제어 관리를 위해 별도로 구축하시기를 권장드립니다.
>
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
2. 클라우드 데이터베이스에 로그인 시, MySQL 문법을 실행하여 클라우드 데이터베이스를 관리할 수 있습니다. MySQL 문법은 [MySQL 공식 파일](http://dev.mysql.com/doc/)을 참조해주세요.
3. 예시는 다음과 같습니다.
  ![](https://mc.qcloudimg.com/static/img/76b4346a84f7388ae263dc6c09220fc0/image.png)
