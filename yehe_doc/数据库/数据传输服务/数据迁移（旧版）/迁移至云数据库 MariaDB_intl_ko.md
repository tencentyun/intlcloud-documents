## 준비 작업
마이그레이션 사용자는 RELOAD, PROCESS, REPLICATION SLAVE, LOCK TABLES, REPLICATION CLIENT, SHOW DATABASE, EVENT, SELECT를 포함한 소스 데이터베이스의 권한이 있어야 합니다.

소스 데이터베이스의 뷰를 마이그레이션해야 하는 경우 SHOW VIEW 권한도 필요합니다.

## 작업 단계
### 1. 마이그레이션 작업 생성
1) [DTS 콘솔](https://console.cloud.tencent.com/dts)에 로그인해 데이터 마이그레이션 페이지에서 **마이그레이션 작업 생성**을 클릭합니다.
2) 마이그레이션 작업 생성 페이지에서 소스 및 타깃 데이터베이스의 유형 및 리전 정보를 선택한 후 **구매하기**를 클릭합니다.

>?마이그레이션 작업이 생성되면 변경할 수 없으므로 주의하여 리전을 선택하십시오.

### 2. 소스 인스턴스와 객체 인스턴스 설정
작업, 소스 데이터베이스, 타깃 데이터베이스를 설정하기 위한 관련 정보를 입력합니다.

#### 작업 설정
마이그레이션 작업 이름을 입력합니다. 작업을 즉시 실행하지 않으려면 마이그레이션 예약 실행을 설정할 수 있습니다.
![](https://main.qcloudimg.com/raw/286fd5ccef05146bea9dd758d6634db5.png)

#### 소스 데이터베이스 설정
소스 데이터베이스의 정보를 입력한 후 **연결성 테스트**를 클릭하여 소스 데이터베이스가 연결되어 있는지 확인합니다.
![](https://main.qcloudimg.com/raw/dcf2c22d49e2c1e2a290f8bf79ed369f.png)

#### 타깃 데이터베이스 설정
타깃 데이터베이스의 정보를 입력하고 **저장**을 클릭합니다.
![](https://main.qcloudimg.com/raw/58807df689398099800be9b2970ed03b.png)

### 3. 유형과 DB 테이블 선택
유형 및 테이블 목록을 선택하고 **다음 단계: 작업 확인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/96ed794fa406ee0004ee3682ef3b0d5e.png)

### 4. 인증 작업
원본 인스턴스가 정상적으로 실행되는지, 타깃 인스턴스로 마이그레이션할 집합이 충돌하는지 확인합니다.
![](https://main.qcloudimg.com/raw/204d55e7b3c700c4ed62419c879513c5.png)

### 5. 마이그레이션 완료
인증 통과 후 마이그레이션 작업 리스트로 돌아갑니다. 증분 동기화가 90% 완료된 후, 마이그레이션 작업 오른쪽의 **완료**를 클릭하면 마이그레이션 작업이 완료됩니다.
![](https://main.qcloudimg.com/raw/120798d5f56bf2db4f68d6203939c718.png)
마이그레이션 완료
![](https://main.qcloudimg.com/raw/030ccd93878ef42e924f6fe5cd2b510e.png)

