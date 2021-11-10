본 문서는 Tencent Cloud 데이터 마이그레이션 제품 DTS를 사용하여 Alibaba Cloud ApsaraDB for RDS(RDS)의 데이터를 TencentDB for MySQL로 마이그레이션하는 과정을 안내합니다.

## 원본 데이터베이스 요구 사항
ApsaraDB RDS for MySQL 5.6 또는 5.7.
>!데이터 전송 중 TencentDB 데이터는 반드시 비동기화 복사를 해야 합니다. 데이터 복사 방식 수정이 필요한 경우에는 데이터 전송이 완료된 후 업데이트하십시오.

## 원본 데이터베이스 기본 정보와 AccessKey 획득 
1. [RDS 관리 콘솔](https://account.aliyun.com/login/login.htm?oauth_callback=https%3A%2F%2Frdsnew.console.aliyun.com%2F%3Fspm%3Da2c4g.11186623.2.5.cdjgiR)에 로그인해 객체 인스턴스를 선택합니다.
2. 객체 인스턴스의 기본 정보 페이지에서 필요한 정보를 획득할 수 있습니다. 구체적인 사항은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/d20077e3364fc3fa692c4e67b6760f5b.png)
>!Alibaba Cloud에서 제공하는 외부 네트워크 주소는 IP 형식으로 변환해야 합니다. 예시는 [IP/서버 주소 조회](http://ip.chinaz.com) 링크에서 확인할 수 있습니다.
>
3. 커서를 우측 상단의 프로필 사진에 두면 나타나는 드롭다운 메뉴에서 [액세스 키]를 선택합니다. 페이지에 들어가면 필요한 Accesskey를 획득할 수 있습니다.
![](https://main.qcloudimg.com/raw/916987de380ebce2919fae56eb19936b.png)
## TencentDB의 DTS 작업 생성
### 1. 마이그레이션 작업 생성
1) [DTS 콘솔](https://console.cloud.tencent.com/dts)에 로그인해 데이터 마이그레이션 페이지에서 [마이그레이션 작업 생성]을 클릭합니다.
2) '링크 리전'에서 상응하는 리전을 선택하고 [0달러 구매]를 클릭합니다.

### 2. 마이그레이션 작업 설정
작업, 소스 라이브러리와 객체 라이브러리를 설정하고 네트워크 연결성 테스트에 성공한 후 [생성]을 클릭합니다.

#### a. 작업 설정
- 작업 이름: 작업 이름을 지정합니다.
- 예약 실행: 마이그레이션 작업 시작 시간을 지정합니다.

<span id="ykxx" ></span>
#### b. 소스 라이브러리 정보
선택할 액세스 유형에 따라 순서대로 상응하는 소스 라이브러리 연결 정보를 입력한 후 [테스트 연결성]을 클릭합니다.
>!
>- Alibaba Cloud에서 TencentDB의 외부 매핑한 IP의 화이트리스트를 활성화해야 합니다. 그렇지 않으면 연결성 테스트를 통과할 수 없습니다. 예를 들어,
>  - 공인 IP가 있는 MySQL Tencent Cloud 매핑 시, 상응하는 리전의 공인 IP를 Alibaba Cloud의 화이트리스트에 추가해야 합니다.
>  -  DTS 설정 시 소스 라이브러리 유형은 '전용선' 혹은 'VPN'이며, 작업 생성 후 외부 매핑 IP가 나타납니다. 해당 IP를 Alibaba Cloud 화이트리스트에 추가해야 합니다.
> 
>- [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 해당 리전의 DTS IP 화이트리스트 정보를 문의할 수 있습니다. 또는 [테스트 연결성]을 클릭하면 연결성 테스트 실패 후 연결성 테스트 결과에 DTS IP 화이트리스트 정보가 제공됩니다.
>
![](https://main.qcloudimg.com/raw/643d71c704dfd69a3b4a6f1cb80c2858.png)

#### d. 객체 라이브러리 정보
객체 인스턴스 유형을 TencentDB 인스턴스로 선택하고 상응하는 객체 라이브러리 링크 정보를 입력합니다.
![](https://main.qcloudimg.com/raw/883eb101608f68fa886d020c2b55b81d.png)

### 3. 마이그레이션이 필요한 데이터베이스 선택
마이그레이션이 필요한 데이터베이스를 선택하고 마이그레이션 작업 정보를 생성 및 확인합니다.
![](https://main.qcloudimg.com/raw/5a384d22e7ee47744814a83a99c8f8a4.png)

### 4. 데이터 일관성 점검
데이터 점검 유형을 선택합니다(모두 점검 혹은 점검하지 않음 선택 가능).
>!모두 점검 선택 시 점검 비율을 입력해야 합니다.
>
![](https://main.qcloudimg.com/raw/a9e2b8ed5c722602104a0ace1fb9b0ef.png)

### 5. 마이그레이션 작업 정보 인증
마이그레이션 생성을 완료한 후에는 마이그레이션 작업 정보를 인증해야 합니다. [다음 단계: 작업 인증]을 클릭, 인증을 진행하여 모든 항목의 인증을 통과해야 마이그레이션 작업을 실행할 수 있습니다. 인증 완료 후 [실행]을 클릭하시면 됩니다.
 작업 인증에는 3가지 상태가 있습니다.

 - 통과: 인증 통과를 의미합니다.
 - 경고: 인증 미통과를 의미하며, 마이그레이션 과정 혹은 마이그레이션 후 데이터베이스의 정상적인 실행에 영향을 줄 수 있습니다. 하지만 마이그레이션 작업의 실행에는 영향을 주지 않습니다.
 - 실패: 인증에 통과하지 못해 마이그레이션을 진행할 수 없다고 표시됩니다. 인증 실패 시 오류가 발생한 인증 페이지에 따라 마이그레이션 작업 정보를 체크 및 수정한 후 다시 인증하십시오.
![](https://main.qcloudimg.com/raw/0b8c1c1cf54b071205acb9b36578773f.png)

### 6. 마이그레이션 실행
>!시스템 설계의 한계로 인해 1회성 제출 혹은 다수의 마이그레이션 작업을 정렬하는 경우에는 정렬 순서에 따라 순차적으로 실행됩니다.
>
인증 통과 후 [마이그레이션 실행]을 클릭해 즉시 데이터 마이그레이션을 시작할 수 있습니다. 마이그레이션 작업을 예약한 경우, 마이그레이션 작업이 설정된 시간에 정렬되고 시작되니 주의하시기 바랍니다. 작업 시간을 설정하지 않은 경우에는 즉시 마이그레이션 작업이 시작됩니다.
마이그레이션 실행 후에는 마이그레이션 작업에서 해당 작업의 진행 정보를 볼 수 있습니다. 커서를 절차 뒤의 느낌표 프롬프트에 대면 마이그레이션의 필요 과정 및 현재 단계가 표시됩니다.
>?오류 발생: 'errMsg': '백업 작업 시작 실패 SDK.ServerUnreachable Unable to connect server:HTTP Error 403: Forbidden'
>다음 방법으로 문제를 진단할 수 있습니다.
>- Alibaba Cloud의 키에 원본 RDS 인스턴스를 콜드 스탠바이 시킬 권한이 있는지 확인합니다. Alibaba Cloud 루트 계정을 사용할 경우에는 모든 권한을 가지기 때문에 원인을 해결할 수 있습니다.
>- Alibaba Cloud 콘솔에 로그인해 해당 RDS 인스턴스에 콜드 스탠바이 혹은 업그레이드 등의 충돌 작업이 있는지 확인합니다. 자동 백업을 설정한 경우에는 자동 백업 옵션을 해제해야 합니다.
>- 이전 단계를 거쳐도 계속 문제가 있을 경우 Alibaba Cloud의 [클라우드 API](https://help.aliyun.com/document_detail/26272.html?spm=a2c4g.11186623.6.916.voEDSM)에서 콜드 스탠바이 작업 실패의 원인을 문의하십시오.  

### 7. 마이그레이션 취소(선택 사항)
마이그레이션 과정 중 마이그레이션을 취소해야 할 경우에는 [취소]를 클릭하십시오.
![](https://main.qcloudimg.com/raw/9d9cf9edda859dfd44007be0d4313986.png)

### 8. 마이그레이션 작업 접속
- 서비스측이 Alibaba Cloud RDS에 입력을 하지 않도록 서비스 접속 계정과 비밀번호를 수정하거나 권한을 조정할 수 있습니다. 하지만 DTS 동기화에 사용하는 계정은 정상적으로 읽고 쓸 수 있어야 합니다.
- Alibaba Cloud RDS의 서비스 연결을 끊고 `show processlist` 명령어를 통해 연결된 서비스가 없음을 인증합니다.
- `show master status`로 Alibaba Cloud RDS의 최신 gtid를 획득해 TencentDB와 동기화된 gtid(`show slave status`로 획득)와 비교함으로써 TencentDB Alibaba Cloud RDS와의 동기화에 딜레이가 없도록 합니다.
-  원본 Alibaba Cloud RDS 계정으로 TencentDB에 로그인할 수 있는지 인증합니다. 로그인할 수 없을 경우 Alibaba Cloud RDS 계정 권한을 최고로 높일 수 있습니다. 조작 방법은 다음과 같습니다.
   DTS 작업 동기화를 유지한 채로 Alibaba Cloud RDS에 높은 권한을 가진 계정을 추가합니다(계정 비밀번호의 암호화 방식을 범용 암호화 방식으로 수정 가능). 그 후 DTS를 TencentDB에 동기화합니다.
- 사용자는 DTS 콘솔(다음 그림)을 통하거나 직접 코어 테이블 콘텐츠를 추출해 데이터 일관성을 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/19123fc859e7ddca13cd465a0cc30077.png)
- `show slave status`를 통해 TencentDB의 동기화 위치를 기록합니다.


### 9. 마이그레이션 완료
마이그레이션 진행도의 100% 도달 시 오른쪽 [완료] 버튼을 클릭해 작업을 완료합니다. 또는 DTS 클라우드 [API](https://intl.cloud.tencent.com/document/product/571/18122)를 호출하여 동기화를 끊고 작업을 완료합니다.
![](https://main.qcloudimg.com/raw/6485672d5cf6feb6a4faeecb4e072c00.png)

>!현재 마이그레이션이 [미완료] 상태일 경우에는 마이그레이션 작업이 계속 진행되어 데이터베이스 데이터가 동기화됩니다.

### 10. 서비스 재시작
TencentDB의 읽기 전용 기능을 끄고 애플리케이션을 실행한 후 TencentDB의 상태를 계속 모니터링함으로써 애플리케이션이 정상적으로 실행될 수 있도록 합니다. 
