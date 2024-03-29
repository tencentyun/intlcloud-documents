읽기 전용 인스턴스를 생성한 후 데이터베이스 프록시 서비스를 구매하고 연결 주소 정책을 구성할 수 있습니다. 그 다음 자동으로 쓰기 요청을 소스 인스턴스로 전달하고 읽기 요청을 읽기 전용 인스턴스로 전달하도록 애플리케이션에서 데이터베이스 프록시 주소를 구성할 수 있습니다. 본문은 콘솔에서 읽기/쓰기 분리를 활성화하는 방법을 설명합니다.

## 전제 조건
[데이터베이스 프록시 활성화](https://intl.cloud.tencent.com/document/product/236/42052)가 완료되어 있어야 합니다.

## 작업 단계
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, 페이지 상단의 리전을 선택하고 대상 인스턴스 ID를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 **데이터베이스 프록시** > **개요**를 선택하고 연결 주소에서 대상 액세스 주소를 찾은 다음 **작업** 열에서 **구성 조정**을 클릭합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XFJj414_14.png)
3. 팝업 창에서 읽기-쓰기 속성을 설정하고 읽기 가중치를 지정한 후 **확인**을 클릭합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4e4x371_15.png)
