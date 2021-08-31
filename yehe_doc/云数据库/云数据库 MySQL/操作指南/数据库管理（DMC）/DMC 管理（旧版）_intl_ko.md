본 문서에서는 DMC 구버전 콘솔의 DB 테이블 생성, 인스턴스 세션 관리, 데이터베이스 Realtime Monitoring, InnoDB Current-Lock 대기 관리 등의 기능을 소개합니다.
>?
>- SQL 창, 테이블 데이터 시각화 Edit 등의 기능을 사용하려면 데이터 관리 콘솔 상단 메뉴에서 [신버전으로 돌아가기]를 클릭합니다. 신버전 DMC 콘솔로 이동할 수 있습니다.
>- TencentDB for MySQL 8.0은 현재 InnoDB Current-Lock 대기 관리와 phpMyAdmin 기능을 지원하지 않습니다.

## DB 테이블 생성
1. [DMC 콘솔](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)에 로그인 후, 상단 메뉴에서 [생성]>[데이터베이스 생성]>[신규 데이터베이스] 혹은 [생성]>[테이블 생성]을 선택합니다.
![](https://main.qcloudimg.com/raw/899520a477489601623a73558b9d5718.png)
2. 팝업 대화 상자에서 새로 생성한 DB 테이블을 설정할 수 있습니다. 설정 완료 후 [제출]을 클릭합니다.
>?문자 세트, 정렬 규칙은 [MySQL 공식 홈페이지 문서](https://dev.mysql.com/doc/)를 참조 바랍니다.
>
 - 데이터베이스 생성 대화 상자:
![](https://main.qcloudimg.com/raw/3d894dd9ca840274ce66321a84089d00.png)
 - 테이블 생성 대화 상자:
![](https://main.qcloudimg.com/raw/4423064c24df9f0b083fec5281b428c7.png)

## 인스턴스 세션 관리
[DMC 콘솔](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)에 로그인 후, 메뉴에서 [인스턴스 세션]을 클릭하여 인스턴스 세션 관리 페이지로 이동합니다. 현재 데이터베이스에서 모든 인스턴스 세션 세부 정보를 조회할 수 있습니다. 세션 개요, 사용자, 액세스 출처와 데이터베이스의 네 가지 범주 관련 정보가 표시됩니다.
데이터 관리 콘솔은 kill 세션 기능을 제공하며, 사용자의 세션 관리를 지원합니다.
![](https://main.qcloudimg.com/raw/0c16ea83442b6c61f2d237f95b60e768.png)

## 데이터베이스 Realtime Monitoring
[DMC 콘솔](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)에 로그인 후, 메뉴에서 [Realtime Monitoring]을 클릭하여 데이터베이스 Realtime Monitoring 페이지로 이동합니다. Realtime Monitoring 기능은 4초에 1번 새로 고쳐지며, 다음과 같이 모니터링 정보를 제공합니다.

MySQL Status Information|  InnoDB Row Operation |   Threads   |Network
---|---|---|---
[qps] 초당 응답 조회수 표시 | [read] InnoDB 스토리지 엔진 테이블의 불러오기 기록 행수 | [running] 액티브의 연결수, 즉 현재 sql 실행 중인 연결 표시 |[in(KB)] 인스턴스에 진입한 네트워크 트래픽 표시
[tps] 초당 처리하는 트랜잭션 개수 표시 | [insert] InnoDB 스토리지 엔진의 입력 기록 행수| [connected] 인스턴스에 연결된 유휴 연결, 즉 sql 미실행 연결 표시| [out(KB)] 아웃바운드 인스턴스의 네트워크 트래픽 표시
[ins] insert 명령 초당 실행 횟수 표시 | [update] InnoDB 스토리지 엔진의 업데이트 기록 행수 표시 |-  |- |
[upd] update 명령 초당 실행 횟수 표시 | [delete] InnoDB 스토리지 엔진의 삭제 기록 행수 표시|- |- |
[del] delete 명령 초당 실행 횟수 표시 |- |- |- |
[sel] select 명령 초당 실행 횟수 표시 |- |- |- |
[hit%] 캐시 히트율 표시, 주로 innodb_buffer_pool 히트율을 가리킴 | - | - |- |

## InnoDB Current-Lock 대기 관리
>- TencentDB for MySQL 8.0은 InnoDB Current-Lock 대기 관리 기능을 지원하지 않습니다.
>
[DMC 콘솔](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)에 로그인 후, 메뉴에서 [InnoDB current-lock 대기]를 클릭하여 InnoDB Current-Lock 대기 관리 페이지로 이동합니다. 사용자는 HOLDLOCK 및 Current-Lock 대기 상세 정보를 시각적으로 조회할 수 있습니다. 또한, 세션 삭제 작업도 진행할 수 있습니다. 다음 이미지와 같습니다:


## 내장 phpMyAdmin
>?TencentDB for MySQL 8.0은 phpMyAdmin 기능을 지원하지 않습니다.
>
[DMC 콘솔](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)에 로그인 후, 메뉴에서 [phpMyAdmin 이동]을 클릭하여 Tencent 데이터 관리 콘솔에 내장된 phpMyAdmin에 들어가 데이터베이스 관련 작업을 진행합니다. phpMyAdmin은 다음과 같이 대부분의 MySQL 기능을 지원합니다.
- 데이터베이스, 테이블, 뷰, 필드 및 인덱스를 조회하고 삭제
- 데이터베이스, 테이블, 필드, 인덱스를 생성, 복사, 삭제, 이름 변경 및 변경
 - 데이터베이스 생성과 테이블 상세 작업
 - 데이터베이스 삭제와 테이블 상세 작업
- 서버, 데이터베이스와 테이블 및 관련 서버 설정 점검
- SQL 명령 실행, 편집
- 스토리지 과정과 트리거 관리

## DBbrain 스마트 최적화
[DMC 콘솔](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)에 로그인 후, 메뉴에서 [DBbrain 스마트한 최적화]를 클릭해 DBbrain 콘솔로 이동합니다.

