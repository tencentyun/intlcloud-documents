## 현상 설명
슬로우 쿼리 현상이 나타날 시, 일반적으로 CPU 사용률, 슬로우 쿼리 수량 등 여러 모니터링 지표가 동시에 급증합니다. 

## 예상 원인
일반적인 상황에서 SQL 명령의 실행 효율이 충분히 높지 않으면 이로 인해 대량의 요청이 TencentDB for MySQL에 축적이 됩니다. 주요 원인은 2가지 입니다.
- [] (id:yy1)원인1: SQL명령에 인덱스를 사용하지 않았거나 바람직한 인덱스를 사용하지 않음.
- [] (id:yy2)원인2: QPS 압력이 현재 인스턴스의 최댓값보다 높음. 

## 해결 방법
2가지 예상되는 원인에 대하여 각각 다른 해결 방식이 있습니다.
- 해결 방법1: SQL명령을 최적화하여 SQL명령의 실행 효율 향상. 세부 사항은 [조치1]를 참고 하십시오. (#cs1)
- 해결 방식2: TencentDB for MySQL의 설정 향상. 세부 사항은 [조치2]를 참고 하십시오. (#cs2)

## 처리 순서
### [조치1: SQL 명령 최적화] (id:csl)
데이터베이스 스마트 관리자 DBbrain을 통해 바로 슬로우 쿼리 최적화를 진행할 수 있습니다. DBbrain이 SQL명령을 분석하여 권장하는 추가 인덱스를 제공합니다. 
1. [DBbrain 콘솔](https://console.cloud.tencent.com/dbbrain/performance/analysis)에 로그인한 후, 왼쪽 메뉴에서 [Performance Optimization]을 선택한 다음 상단에서 해당하는 데이터베이스를 선택하고 [Slow SQL Analysis] 페이지를 선택합니다.
2. ‘SQL 통계’ 도표의 슬로우 쿼리(막대 그래프)에서 클릭(하나의 시간대 선택) 혹은 드래그(다수의 시간대 선택) 하면, 아래에 SQL 템플릿 취합 및 실행 정보가 표시됩니다. (실행 횟수, 총 소요된 실행 시간, 스캔 행 수, 반환 행 수 등 포함)
![](https://main.qcloudimg.com/raw/0659dcb5dfb47bf00c4df2646946f0ce.png)
3. 취합된 SQL 템플릿의 행을 클릭하면 우측에 SQL의 구체적인 분석과 통계 데이터가 팝업 되어 해당하는 권장 인덱스를 확인 할 수 있습니다. 
![](https://main.qcloudimg.com/raw/f72dcf38d05fc7381007502e930f3014.png)

### [조치2: TencentDB for MySQL의 설정 향상] (id:cs2)
각 규격에 해당하는 [QBS 공식 홈페이지 부하 테스트 데이터](https://intl.cloud.tencent.com/document/product/236/8842)를 확인하고 현재 인스턴스의 QPS 데이터와 비교 하여 해당하는 [MySQL CPU와 메모리 규격](https://intl.cloud.tencent.com/document/product/236/19707)을 변경하십시오. 
