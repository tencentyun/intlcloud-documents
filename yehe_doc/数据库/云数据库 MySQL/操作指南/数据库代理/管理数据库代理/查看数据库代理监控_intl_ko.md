본문에서는 TencentDB for MySQL 콘솔에서 데이터베이스 프록시 노드 모니터링 데이터를 보는 방법을 설명합니다.

## 전제 조건
[데이터베이스 프록시 활성화](https://www.tencentcloud.com/document/product/236/42052)가 완료되어 있어야 합니다.

## 지원되는 모니터링 메트릭

| 메트릭 이름 | 단위 | 설명 |
|---------|---------|---------|
| 현재 연결 | 개 | 현재 노드 연결 개수 |
| 요청 | 회/초 | 노드 액세스 요청 건수|
| 읽기 요청 | 회/초 | 읽기 작업 요청 건수 |
| 쓰기 요청 | 회/초 | 쓰기 작업 요청 건수 |
| CPU 사용률 | % | CPU 사용 상황 |
| 메모리 활용률 | % | 메모리 사용 비율 |
| 메모리 사용량 | MB | 메모리 사용량 |

## 작업 단계
**방법1:**
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, 인스턴스 리스트에서 프록시가 활성화된 프라이머리 인스턴스를 선택하고, 인스턴스 ID를 클릭하거나 **작업** 열에서 **관리**를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 **데이터베이스 프록시** > **성능 모니터링** 페이지를 선택하고 모니터링 데이터를 볼 프록시 노드 이름을 클릭합니다. 이름을 클릭하여 서로 다른 노드 간에 전환할 수 있습니다.
>?4시간 이내 모니터링의 기본 세분성은 5초입니다.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/pMhC112_7.png)

**방법2:**

1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, 인스턴스 리스트에서 프록시가 활성화된 소스 인스턴스의 **작업**열에서 ID 또는 **관리**를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 **데이터베이스 프록시** > **개요**를 선택하고 **프록시 노드** 열의 대상 노드 ID 뒤에 있는 아이콘 ![](https://qcloudimg.tencent-cloud.cn/raw/f3f75f219f501d9b6836b3f542e49ed4.png)을 클릭하면 노드의 성능 모니터링 데이터를 볼 수 있습니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QtfL186_9.png)
리디렉션 후 표시되는 페이지는 다음과 같습니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/2HR2348_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_1673407877191.png)
