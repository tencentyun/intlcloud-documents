CBS(Cloud Block Storage)에 더 좋은 모니터링 환경을 제공하는 것은 높은 데이터 안정성을 유지하는데 중요한 부분입니다. 사용자는 [클라우드 모니터링](https://intl.cloud.tencent.com/document/product/248)을 사용하여 서비스 모니터링 **이미 [마운트](https://intl.cloud.tencent.com/document/product/362/5745)된 CVM 인스턴스 중** CBS에서 CBS의 메트릭 데이터를 조회하고 관련 CBS의 알람을 분석하거나 설정하십시오. [클라우드 모니터링](https://intl.cloud.tencent.com/document/product/248) 실행 중인 상태의 CVM 인스턴스는 디스크의 원시 데이터를 수집하고 데이터를 읽기 쉬운 차트 형식으로 표시합니다. 통계 데이터는 일반적으로 한 달 동안 저장됩니다. 사용자는 한 달 동안 시간대 별로 디스크의 관련 상태를 모니터링하여 사용량과 읽기/쓰기 등 방면의 정보를 더 잘 이해할 수 있습니다.
사용자는 [클라우드 모니터링 콘솔](https://console.cloud.tencent.com/monitor/cvm) 또는 [클라우드 모니터링 API](https://intl.cloud.tencent.com/document/api/248/4667)를 통해 데이터를 획득할 수 있습니다. 자세한 내용은 [특정 메트릭의 모니터링 데이터 가져오기](https://intl.cloud.tencent.com/document/product/248/6141)와 [모니터링 이미지와 보기 및 리포트 가져 오기](https://intl.cloud.tencent.com/document/product/248/6142)를 참조하십시오.
현재 클라우드 모니터링은 CBS를 위해 다음 모니터링 메트릭을 제공합니다.

| 메트리 명칭               | 메트릭 중문 명칭  | 계산 방식                                     | 메트릭 의미                        | 단위   | 데이터 분할 정도 통계(period) |
| ------------------ | ------- | ---------------------------------------- | --------------------------- | ---- | ------------ |
| disk_read_iops          | 디스크 읽기 IOPS  | 통계 기간 내 IOPS의 읽기 평균치 블록 메모리 | 블록 메모리에서 메모리 중 I/O까지 초당 읽는 횟수           | 횟수    | 5s, 10s, 60s, 300s |
| disk_read_traffic       | 디스크 읽기 트래픽 | 통계 기간 내 처리량 읽기 평균치 디스크 블록| 데이터가 디스크 블록에서 메모리까지 읽는 속도     | KB/s  | 5s, 10s, 60s, 300s |
| disk_write_iops           | 디스크 쓰기 IOPS   | 통계 기간 내 IOPS의 쓰기 평균치 디스크 블록 | 메모리에서 디스크 블록 중의 I/O까지 초당 쓰는 횟수 | 횟수   | 5s, 10s, 60s, 300s |
| disk_write_traffic  | 디스크와 트래픽  | 통계 기간 내 쓰기 처리량의 평균치 디스크 블록 |데이터가 메모리에서 디스크 블록까지 쓰는 속도  | KB/s  | 5s, 10s, 60s, 300s |
| disk_await | 디스크 I/O 대기 시간   | 통계 기간 내 ioawait의 평균치 디스크 블록 | 샘플링 기간 내 몇 퍼센트의 시간 동안 CPU가 유휴상태고 미해결 I/O 요청이 있는지 여부              | ms | 5s, 10s, 60s, 300s |
| disk_svctm | 디스크 I/O 서비스 시간   | 통계 기간 내 svctm의 평균치 디스크 블록 | I/O 서비스 시간 | ms | 5s, 10s, 60s, 300s |
| disk_util      | 디스크 I/O 혼잡 비율 | 통계 기간 내 io_util의 평균치 디스크 블록 | 디스크에 I/O 작동 시간(즉, 비유휴 시간)의 비율 | % | 5s, 10s, 60s, 300s |

모니터링 메트릭에 대한 자세한 설명은 [제품 파일 클라우드 모니터링](https://intl.cloud.tencent.com/document/product/248)을 참조하십시오.
