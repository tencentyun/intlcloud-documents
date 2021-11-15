본 문서에서는 DMC 신버전 콘솔의 DB 테이블 생성, 데이터베이스 관리, 인스턴스 모니터링, 인스턴스 세션, 테이블 데이터 시각화 편집 등의 기능을 소개합니다.
>- 데이터베이스 Realtime Monitoring, InnoDB Current-Lock 대기 등의 기능을 사용하려면 데이터 관리 콘솔 메뉴 오른쪽 상단에서 [구버전으로 돌아가기]를 클릭합니다. 구버전 DMC 콘솔로 이동할 수 있습니다.

## DB 테이블 생성
1. [DMC 콘솔](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)에 로그인 후, 상단 메뉴에서 [생성]>[데이터베이스 생성]>[신규 데이터베이스] 혹은 [생성]>[테이블 생성]을 선택합니다.
![](https://main.qcloudimg.com/raw/4b1c803307c0c64d96ff6b8fdf43d3dd.png)
2. 팝업 대화 상자에서 새로 생성한 DB 테이블을 설정할 수 있습니다. 설정 완료 후 [제출]을 클릭합니다.
>?문자 세트, 정렬 규칙은 [MySQL 공식 홈페이지 문서](https://dev.mysql.com/doc/)를 참조 바랍니다.
>
 - 데이터베이스 생성 대화 상자:
![](https://main.qcloudimg.com/raw/392a9c91adf523e57deb300f0be7e86d.png)
 - 테이블 생성 대화 상자:
![](https://main.qcloudimg.com/raw/0d4806266e021e7864c0aa605781929c.png)

## 데이터베이스 관리
[DMC 콘솔](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)에 로그인 후, 메뉴에서 [Database Management]를 클릭해 데이터베이스 관리 페이지로 이동합니다. 데이터베이스를 생성, 편집, 삭제할 수 있습니다.
![](https://main.qcloudimg.com/raw/85b4d1def1c7eadaf415d9944ff3101c.png)

## 인스턴스 세션
[DMC 콘솔](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)에 로그인 후, 메뉴에서 [인스턴스 세션]을 클릭하여 인스턴스 세션 페이지로 이동합니다. 현재 데이터베이스에서 모든 인스턴스 세션 세부 정보를 조회할 수 있습니다. 세션 개요, 사용자, 액세스 출처와 데이터베이스의 네 가지 범주 관련 정보가 표시됩니다.
데이터 관리 콘솔은 kill 세션 기능을 제공하며, 사용자의 세션 관리를 지원합니다.
![](https://main.qcloudimg.com/raw/4218f038cb177548047f0042f4986351.png)

## SQL 창
[DMC 콘솔](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)에 로그인 후, 상단 메뉴에서 [SQL 창] 또는 왼쪽 테이블 '작업' 메뉴에서 [SQL 작업]을 클릭해 SQL 창 페이지로 이동합니다. SQL 창은 다음과 같은 기능을 지원합니다.
- SQL 명령어 실행 및 결과 조회
- SQL 형식 최적화
- SQL 명령어 실행 계획 조회
- 자주 사용하는 SQL 저장
- 템플릿 SQL
- SQL 결과 내보내기
![](https://main.qcloudimg.com/raw/cf0c070dc6ae01c6d9c8795ce0934fb6.png)

## 데이터 관리
[DMC 콘솔](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)에 로그인 후, 메뉴에서 [데이터 관리]>[데이터 가져오기] 또는 [데이터 내보내기]를 선택하면 데이터베이스 데이터 가져오기와 내보내기를 진행할 수 있습니다.
![](https://main.qcloudimg.com/raw/5c58a3bbfe40ac943bd08a726427b7fa.png)

## 테이블 데이터 시각화 편집
새로운 버전의 DMC for MySQL은 데이터 추가, 삭제, 변경을 지원합니다. 사용자는 왼쪽 메뉴에서 '데이터 테이블'을 클릭하여 테이블 데이터를 대량으로 추가, 삭제, 수정할 수 있습니다. 수정 완료 후, '단축 작업' 메뉴에서 [확인]을 클릭하여 수정할 SQL 명령을 확인합니다. 2차 확인 후 일괄적으로 수정됩니다.

