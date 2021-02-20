### MySQL의 인스턴스 스토리지 용량 사용 현황을 어떻게 조회할까요?
[DBbrain 콘솔](https://console.cloud.tencent.com/dbbrain)에 로그인하십시오. 왼쪽 메뉴에서 [Performance Optimization]을 선택한 뒤 상단에서 원하는 데이터베이스를 선택하고 [Space Analysis] 페이지를 여십시오. 
용량 분석 페이지에서 최근 한 주의 일일 증가량 비교, 잔여 디스크 용량, 예상 가용 일수 및 최근 한 주의 디스크 용량 추이를 확인할 수 있습니다. 또한 인스턴스의 데이터베이스 테이블이 차지하는 용량의 상세 내용과 조각화 상태를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/612e0641f7c2c09c6d5f820d56d8f1e4.png)

### MySQL의 모든 SQL 실행 내역을 어떻게 분석할까요?
[DBbrain 콘솔](https://console.cloud.tencent.com/dbbrain)에 로그인하십시오. 왼쪽 메뉴에서 [Performance Optimization]을 선택한 뒤 상단에서 원하는 데이터베이스를 선택하고 [Audit Log Analysis] 페이지를 여십시오.
1. 뷰 오른쪽 상단의 [Create Analysis Task]을 클릭한 뒤 시간대를 설정하고 [OK]를 클릭합니다.
2. Task List에서 [SQL 분석 조회]를 클릭하여 SQL 분석 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/60c636949f6bcbafe726256d2a08db5f.png)
3. SQL 분석 페이지에서 SQL Type, Host, User, SQL Code 뷰를 선택할 수 있으며, 시간대 별로 뷰를 확대해 세부 시간을 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/e20326e6719f18a5dac27bec64fa1182.png)
4. SQL 템플릿을 클릭하면 오른쪽에 SQL 명령 세부사항 팝업창이 뜹니다.
 - 분석 페이지에서 세부 SQL 명령을 조회 및 복사할 수 있으며, 제시된 최적화 권장 사항 또는 설명을 참고하여 SQL 명령을 최적화하십시오.
 - 통계 페이지에서 해당 SQL의 Host, User, SQL Code 관련 통계 분석 및 실행 시간을 조회할 수 있습니다.

### MySQL의 인스턴스 장애 또는 오류 시, 어떻게 자가 진단을 최적화할 수 있을까요?
1. [DBbrain 콘솔](https://console.cloud.tencent.com/dbbrain)에 로그인합니다. 왼쪽 메뉴에서 [Performance Optimization]를 선택한 뒤 상단에서 원하는 데이터베이스를 선택하고 [Exception Diagnosis] 페이지를 엽니다.
2. ‘진단 알림’ 열에 클래스, 시작 시간, 진단 항목, 소요 시간 등 이벤트 기록 진단에 관한 대략적인 정보가 표시됩니다. DBbrain은 인스턴스 상태를 정기 점검합니다.
![](https://main.qcloudimg.com/raw/fe0dd650bb834eb093e7964917da758e.png)
3. [View details] 또는 ‘진단 알림’ 열의 진단 페이지를 클릭하면 진단 상세 페이지가 열립니다. 뷰에서 진단 이벤트를 클릭하면 하단에 이벤트 개요, 현상 설명, 스마트 분석, 전문가 제안 등 이벤트 상세 내용이 표시됩니다. 전문가 제안에 따른 최적화로 데이터베이스 오류 해결과 인스턴스 성능 향상이 가능합니다.
 ![](https://main.qcloudimg.com/raw/576a445b12b249f278d50cbe89ab238e.png)

### MySQL의 상태 보고를 어떻게 정기적으로 받을 수 있을까요?
[DBbrain 콘솔](https://console.cloud.tencent.com/dbbrain)에 로그인하십시오. 왼쪽 메뉴에서 [Performance Optimization]을 선택한 뒤 상단에서 원하는 데이터베이스를 선택하고 [Health Report] 페이지를 열면 선택한 시간대의 상태 점수 추이 및 이슈 개요를 조회할 수 있습니다. 
- 보고 시간 범위를 설정한 뒤 [Create Health Report]을 클릭하십시오. 작업이 완료되면 설정한 시간의 상태 보고를 조회 또는 다운로드할 수 있습니다.  
- [정기 생성 설정]을 클릭하면 상태 보고의 자동 생성 주기를 설정할 수 있습니다. 
 ![](https://main.qcloudimg.com/raw/0cf1ac4dd76a106cde20f854086c38f7.png)

### MySQL의 슬로우 로그는 어떻게 조회하고 최적화할까요?
1. [DBbrain 콘솔](https://console.cloud.tencent.com/dbbrain)에 로그인합니다. 왼쪽 메뉴에서 [Performance Optimization]를 선택한 뒤 상단에서 원하는 데이터베이스를 선택하고 [Slow SQL Analysis] 페이지를 열면 ‘SQL 통계’ 열에 인스턴스의 슬로우 쿼리 개수와 CPU 사용률이 표시됩니다.
2. SQL 통계 도표에 있는 슬로우 쿼리를 클릭하거나 스크롤 선택하면 하단에 SQL 템플릿 취합 및 실행 정보가 표시됩니다. 데이터는 오름차순 정렬과 내림차순 정렬이 가능합니다. 오른쪽의 소모 시간 분포에는 선택한 시간대의 SQL 총 소모 시간 분포 현황이 표시됩니다.
 ![](https://main.qcloudimg.com/raw/c937f9639acc557e9cb58eb885f36805.png)
3. 취합된 SQL 템플릿 행을 클릭하면 오른쪽에 SQL 관련 최적화 제안 및 통계 정보 팝업창이 뜹니다. 팝업창에서 최적화 제안 사항에 따라 SQL을 작성하거나 인덱스를 추가할 수 있어 SQL 실행 효율 및 데이터베이스 기능을 향상시킬 수 있습니다.
 


### TencentDB for MySQL로 작업할 때 왜 lag 현상이 발생할까요?
동시 작업으로 인한 lock wait가 원인으로, 정상적인 현상입니다.

### TencentDB for MySQL에서 중국어 데이터 조회 시 왜 글자가 깨질까요?
데이터베이스에 데이터 저장 시 [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인하여 인스턴스 상세 페이지로 들어가 해당 인스턴스의 문자 세트 기본 값을 조회하십시오. `character_set_client`, `character_set_results`, `character_set_connection`를 CDB 인스턴스와 동일한 문자 세트로 설정하십시오. 그렇지 않으면 저장된 데이터에 포함된 중국어가 깨져서 표시될 수 있습니다.
예를 들어, CDB 인스턴스의 문자 세트 기본 값이 utf8인 경우, 데이터베이스 연결 코딩 시, 다음 명령을 실행하여 중국어 데이터를 CDB에 저장해야 합니다.

```
SET NAMES 'utf8';
```

### TencentDB for MySQL의 연결 개수가 초과하는 주요 원인과 해결 방법은 무엇일까요?
- sleep 스레드 수가 너무 많을 경우에는 콘솔에서 wait_timeout 및 interactive_timeout 매개변수 값을 낮추는 것이 좋습니다.
- 슬로우 쿼리가 많이 쌓여 있을 경우에는 10s로 기본 설정되어 있는 long_query_time의 매개변수 값을 1s ~ 2s로 설정한 뒤 슬로우 쿼리 로그를 모니터링하십시오.
- sleep 스레드 수도 적고 쌓인 슬로우 쿼리도 없다면 콘솔에서 max_connections의 매개변수 값을 높이는 것이 좋습니다.

### TencentDB for MySQL의 CPU 점유율이 과도한 주요 원인과 해결 방법은 무엇일까요?
- 슬로우 쿼리 힙이 있는 경우, 인스턴스 모니터링의 슬로우 쿼리 및 테이블 일괄 스캔 상태를 조회한 뒤 슬로우 쿼리 로그(콘솔에서 다운로드 가능)를 참고해 분석 및 최적화할 수 있습니다. 모니터링에 슬로우 쿼리는 없으며, 테이블 일괄 스캔만 표시된 경우, 콘솔에서 long_query_time를 1s ~ 2s로 조정합니다. 이후 일정 시간 사용한 뒤 슬로우 쿼리를 다시 분석하십시오.
- 슬로우 쿼리 힙이 없는 경우, 인스턴스 모니터링에 표시된 메모리 점유율을 확인하십시오. 인스턴스 사양을 과도하게 초과했고, 디스크의 읽기 및 쓰기 용량이 현저히 증가했다면 메모리 용량이 부족할 수 있으니 메모리를 업그레이드하는 게 좋습니다.

### 인스턴스의 어떤 모니터링 지표를 평소에 확인하면 좋을까요?
CPU 사용률, 메모리 사용률, 디스크 용량 사용률을 점검하십시오. 실제 사용 상황에 따라 [알람 설정](https://intl.cloud.tencent.com/document/product/236/8457)을 하면 알람이 발송되고, 알람 해제를 위한 적절한 조치를 취할 수 있습니다.
