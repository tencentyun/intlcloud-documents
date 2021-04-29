## 정책 생성
프로젝트별 권한 작업을 세분화할 수 있습니다. 예, 데이터 조회, 퍼지와 프리패치, 도메인 관리 권한을 각각 다른 서브 계정에 부여하려면 다음과 같은 절차를 통해 정책을 생성할 수 있습니다.
1. [액세스 관리 콘솔](https://console.cloud.tencent.com/cam/overview)에 로그인하고 왼쪽 메뉴에서 [Policies]을 클릭합니다.
2. [Create Custom Policy]을 클릭한 후 [제품 기능 또는 프로젝트에 따른 권한 생성]을 선택하세요.
![](https://main.qcloudimg.com/raw/59c8c89263412208344bd071430db23d.png)
3. 수요에 따라 정책 이름을 입력하고 아래의 서비스 유형에서 [CDN]을 선택하세요.
![](https://main.qcloudimg.com/raw/e057955abd823f0b92ff6cc13a016c4c.png)
4. 수요에 따라 권한이 필요한 작업 그룹을 활성화하고, 프로젝트에 연결(프로젝트에 권한을 부여하지 않도록 디폴트 설정되어 있음)한 후 서브 계정과 연결합니다.
![](https://main.qcloudimg.com/raw/961dfce5817ba690b554f12dfa22d7c9.png)

## 리소스별&프로젝트별
현재 작업 그룹 분류 및 해당하는 OPEN API 2.0 및 OPEN API 3.0 인터페이스는 다음과 같습니다. 작업 그룹의 권한을 가진 서브 계정 사용자가 권한이 있는 프로젝트의 도메인에 대하여 2.0포트 및 3.0포트를 호출할 수 있습니다.

| 권한 그룹              | API2.0                                                       | API3.0                                                       | 권한 필요 여부 |
| :-------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------- |
| 소모 데이터 및 통계량 조회  | DescribeCdnHostInfo DescribeCdnHostDetailedInfo GetCdnStatusCode<br/>GetCdnStatTop<br/>GetCdnProvIspDetailStat | DescribeCdnData DescribeOriginData<br/>ListTopData<br/>DescribeIpVisit | 예           |
| 도메인 정보 조회          | GetHostInfoById<br/>GetHostInfoByHost                        | DescribeDomains<br/>DescribeDomainsConfig                    | 예           |
| CDN 로그 다운로드 링크 조회 | GenerateLogList<br/>GetCdnLogList                            | DescribeCdnDomainLogs                                        | 예           |
| 도메인 추가              | AddCdnHost                                                   | AddCdnDomain                                                 | 예           |
| 도메인 활성화 / 비활성화       | OnlineHost OfflineHost                                       | StartCdnDomain<br/>StopCdnDomain                             | 예           |
| 도메인 삭제              | DeleteCdnHost                                                | DeleteCdnDomain                                              | 예           |
| 도메인 설정 수정          | UpdateCdnConfig                                              | UpdateDomainConfig                                           | 예           |
| 퍼지와 프리패치              | RefreshCdnDir<br/>RefreshCdnUrl<br/>GetCdnRefreshLog<br/>CdnPusherV2<br/>GetPushLogs<br/>CdnOverseaPushser | PurgeUrlsCache<br/>PurgePathCache<br/>DescribePurgeTasks<br/>PushUrlsCache<br/>DescribePushTasks | 예           |
| 서비스 조회              | QueryCdnIp(인증 필요 없음)                                       | DescribeCdnIp                                                | 예           |

## 콘솔 권한
- 소모 데이터 및 통계량 조회: 정책에서 [소모 데이터 및 통계량 보기]를 활성화하고 프로젝트를 연결하면, 콘솔에서 다음 모듈 정보를 조회할 수 있습니다.
  - 개요: 데이터 디스플레이 모듈
  - 통계 분석: 실시간 모니터링
  - 통계 분석: 데이터 분석
  - 전체 네트워크 데이터 모니터링
- 도메인 정보 조회: 정책에서 [도메인 이름 정보 조회]를 활성화하고 프로젝트를 연결하면, 콘솔의 [도메인 이름 관리] 페이지에서 권한을 가진 프로젝트의 도메인 목록 및 세부 설정 정보를 확인할 수 있습니다.
- CDN 로그 다운로드 링크 조회: 정책에서 [CDN 로그 다운로드 링크 조회]를 활성화하고 프로젝트를 연결하면, 콘솔 [로그 관리] 페이지에서 액세스 로그 다운로드 링크를 조회할 수 있습니다.
- 도메인 추가: 정책에서 [도메인 이름 추가]를 활성화하고 프로젝트를 연결하면, 지정된 프로젝트에 도메인을 추가할 수 있습니다.
- 도메인 활성화/비활성화: 정책에서 [도메인 활성화/비활성화]를 활성화하고 프로젝트를 연결하면 특정 프로젝트의 가속 도메인을 활성화/비활성화할 수 있습니다.
- 도메인 삭제: 정책에서 [도메인 삭제]를 활성화하고 프로젝트를 연결하면, 특정 프로젝트의 가속 도메인을 삭제할 수 있습니다. 도메인을 삭제하려면 비활성화 상태여야 하므로 활성화 상태인 도메인을 삭제하려면 [도메인 활성화/비활성화] 권한을 갖고 있어야 합니다.
- 도메인 설정 수정: 정책에서 [도메인 설정 수정]을 활성화하고 프로젝트를 연결하면, 특정 프로젝트의 가속 도메인 설정을 수정할 수 있습니다.
- 퍼지와 프리패치: 정책에서 [퍼지와 프리패치]를 활성화하고 프로젝트를 연결하면, [캐시와 퍼지] 페이지에서 해당하는 퍼지, 프리패치(화이트리스트) 작업을 제출할 수 있고 퍼지와 프리패치 작업의 실행 상태를 조회할 수 있습니다.
