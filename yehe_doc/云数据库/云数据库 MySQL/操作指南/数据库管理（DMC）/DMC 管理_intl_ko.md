본 문서는 데이터베이스 관리 콘솔의 DB 테이블 생성, 데이터베이스 관리, 인스턴스 모니터링, 인스턴스 세션, 테이블 데이터 시각화 편집 등의 기능을 소개합니다.

## DB 테이블 생성
1. [데이터베이스 관리 콘솔](https://dms.cloud.tencent.com/#/login)에 로그인한 후, 메뉴에서 [생성]>[데이터베이스 생성]>[새 데이터베이스] 또는 [생성]>[테이블 생성]을 선택합니다.
![](https://main.qcloudimg.com/raw/4b1c803307c0c64d96ff6b8fdf43d3dd.png)
2. 팝업 대화 상자에서 생성할 DB 테이블에 대한 설정을 진행합니다.
>?문자 세트, 정렬 규칙은 [MySQL 공식 홈페이지 문서](https://dev.mysql.com/doc/)를 참조하십시오.
>
 - 데이터베이스 생성 대화 상자:
![](https://main.qcloudimg.com/raw/392a9c91adf523e57deb300f0be7e86d.png)
 - 테이블 생성 대화 상자:
![](https://main.qcloudimg.com/raw/0d4806266e021e7864c0aa605781929c.png)

## 데이터베이스 관리
[데이터베이스 관리 콘솔](https://dms.cloud.tencent.com/#/login)에 로그인한 후, 메뉴에서 [데이터베이스 관리]를 클릭해 데이터베이스 관리 페이지로 이동합니다. 데이터베이스를 생성, 편집, 삭제할 수 있습니다.
![](https://main.qcloudimg.com/raw/85b4d1def1c7eadaf415d9944ff3101c.png)

## 인스턴스 세션
[데이터베이스 관리 콘솔](https://dms.cloud.tencent.com/#/login)에 로그인한 후, 메뉴에서 [인스턴스 세션]을 클릭하여 인스턴스 세션 페이지로 이동합니다. 현재 데이터베이스의 모든 인스턴스 세션 세부 정보 및 세션 개요, 사용자, 액세스 출처, 데이터베이스 관점에서의 정보를 조회할 수 있습니다.
데이터베이스 관리 콘솔은 kill 세션 기능을 제공하여 세션을 편리하게 관리할 수 있습니다.
![](https://main.qcloudimg.com/raw/4218f038cb177548047f0042f4986351.png)

## SQL 창
[데이터베이스 관리 콘솔](https://dms.cloud.tencent.com/#/login)에 로그인한 후, 상단 메뉴에서 [SQL 창] 또는 왼쪽 테이블 '작업' 메뉴에서 [SQL 작업]을 클릭해 SQL 창 페이지로 이동합니다. SQL 창은 다음과 같은 기능을 지원합니다.
- SQL 명령어 실행 및 결과 조회
- SQL 포맷 최적화
- SQL 명령어 실행 계획 조회
- 자주 사용하는 SQL 저장
- SQL 템플릿
- SQL 결과 내보내기
![](https://main.qcloudimg.com/raw/cf0c070dc6ae01c6d9c8795ce0934fb6.png)

## 데이터 관리
[데이터베이스 관리 콘솔](https://dms.cloud.tencent.com/#/login)에 로그인한 후, 메뉴에서 [데이터 관리]>[데이터 가져오기] 또는 [데이터 내보내기]를 선택하면 데이터베이스에 데이터 가져오기 및 내보내기 작업을 할 수 있습니다.
![](https://main.qcloudimg.com/raw/5c58a3bbfe40ac943bd08a726427b7fa.png)

## 테이블 데이터 시각화 편집
데이터베이스 관리 콘솔 for MySQL에는 데이터 추가, 삭제, 변경 기능이 추가되었습니다. 왼쪽 메뉴에서 '데이터 테이블'을 클릭하여 테이블 데이터를 일괄 추가, 삭제, 수정할 수 있습니다. 수정 완료 후 '빠른 작업' 열에서 [확인]을 클릭하면 수정할 SQL 명령을 미리 볼 수 있으며, 2차 확인 후 일괄적으로 수정합니다.
