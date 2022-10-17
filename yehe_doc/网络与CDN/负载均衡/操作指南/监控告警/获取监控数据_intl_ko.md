Tencent Cloud Cloud Monitor는 CLB 인스턴스 및 실제 서버에 대한 데이터를 수집 및 표시하여 CLB 통계를 얻고 시스템이 정상적으로 실행되고 있는지 검증하고 알람을 생성하는 데 도움이 됩니다. Tencent Cloud 모니터에 대한 자세한 내용은 [Cloud Monitor](https://intl.cloud.tencent.com/doc/product/248) 문서를 참고하십시오.

Tencent Cloud는 기본적으로 모든 사용자에게 클라우드 모니터링 기능을 제공하며 수동 활성화가 필요하지 않습니다. Cloud Monitor를 사용하여 CLB 인스턴스의 모니터링 데이터를 수집하고 다음 방법을 사용하여 데이터를 볼 수 있습니다.

## CLB 콘솔
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인하고 CLB 인스턴스 ID 옆에 모니터링 아이콘을 클릭 한 다음 플로팅 창에서 인스턴스의 성능 데이터를 찾아보십시오.
![](https://main.qcloudimg.com/raw/6580c81d6fd1eee2234fcb5262a976bb.png)
2. CLB 인스턴스의 ID/이름을 클릭하여 세부 정보 페이지에 액세스하십시오. [모니터링]을 클릭하면 모니터링 데이터를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/3eb231b336c9325ae16bfe2937e41b39.png)

## Cloud Monitor 콘솔
CLB 모니터링 데이터를 보려면 [Cloud Monitor 콘솔](https://console.cloud.tencent.com/monitor/overview)에 로그인합니다. 왼쪽 사이드 바에서 [[CLB]](https://console.cloud.tencent.com/monitor/clb)를 클릭 한 다음 CLB 인스턴스의 ID/이름을 클릭하여 모니터링 세부 정보 페이지로 이동하면 CLB 인스턴스의 모니터링 데이터를 보고 드롭다운 목록을 펼쳐 리스너 및 실제 서버 모니터링 정보를 볼 수 있습니다.

## API 방식
GetMonitorData API를 사용하여 모든 제품의 모니터링 데이터를 가져올 수 있습니다. 자세한 내용은 [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/33881), [Public Network CLB Monitoring Metrics](https://intl.cloud.tencent.com/zh/document/product/248/10997), [Private Network CLB Layer-4 Protocol Monitoring Metrics](https://intl.cloud.tencent.com/document/product/248/39529) 및 [Layer-7 Protocol](https://intl.cloud.tencent.com/document/product/248/39530)을 참고하십시오.
