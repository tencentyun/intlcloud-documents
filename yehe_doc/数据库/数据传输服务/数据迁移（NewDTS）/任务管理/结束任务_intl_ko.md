
## 작업 시나리오
전체 + 증분 데이터 마이그레이션 중에 전체 마이그레이션이 완료되면 작업이 자동으로 증분 마이그레이션을 시작합니다. 이 작업은 자체적으로 중지되지 않으며 수동으로 종료해야 합니다. 

## 전제 조건
데이터 마이그레이션 유형이 ‘전체 + 증분 마이그레이션’이어야 합니다. 

## 작업 단계
[DTS 콘솔](https://console.cloud.tencent.com/dts/migration)에 로그인하고 왼쪽 사이드바에서 **데이터 마이그레이션**을 선택하고 대상 마이그레이션 작업을 선택한 후 **완료**를 클릭하여 중지합니다. 다음 조건을 충족하는 경우에만 작업을 완료할 수 있습니다.
 - 마이그레이션 단계가 **증분 동기화**로 표시됩니다.
 - 원본/대상 데이터베이스 데이터 간격은 0MB이고 원본/대상 데이터베이스 시간 지연은 0초입니다.

![](https://qcloudimg.tencent-cloud.cn/raw/19f54868ca6574ac523daa12889d7042.png)

