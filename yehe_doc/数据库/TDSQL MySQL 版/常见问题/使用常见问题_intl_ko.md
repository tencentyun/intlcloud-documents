### 인스턴스 사양은 어떻게 선택합니까?
- 특별한 성능 요구 사항이 없는 TDSQL for MySQL의 기능 테스트: 각각 2GB의 메모리와 25GB의 디스크 용량이 있는 2개의 샤드.
- 데이터의 전체 크기는 작지만 빠르게 증가하는 초기 비즈니스 단계: 각각 16GB 메모리와 200GB 디스크 용량을 가진 2개의 샤드.
- 샤딩이 실제 비즈니스 수요를 기반으로 하는 안정적인 개발 단계: 4개의 샤드, 각각의 사양은 현재 비즈니스 피크 * 성장률 / 4와 같습니다.
인스턴스 사양에 대한 자세한 내용은 [TDSQL for MySQL 인스턴스 및 샤드 설정](https://intl.cloud.tencent.com/document/product/1042/33354)을 참고하십시오.

### TDSQL for MySQL 구문과 기존 MySQL 구문의 차이점은 무엇입니까?
현재 명령 라인으로 사용자 권한을 구성할 수 없습니다. 구성하려면 TDSQL for MySQL [콘솔](https://console.cloud.tencent.com/dcdb)에 로그인해야 합니다.
현재 TDSQL for MySQL은 사용자 정의 함수, 뷰, 트리거, 외래 키 등을 지원하지 않습니다.
MySQL 구문과의 호환성에 대한 자세한 내용은 [사용 제한](https://intl.cloud.tencent.com/document/product/1042/33356)을 참고하십시오.

### 샤드키는 무엇을 합니까?
- 분할된 테이블을 쿼리할 때 select 구문에 shardkey 필드를 지정하는 것이 좋습니다. proxy는 shardkey 필드의 hash 값을 기반으로 SQL 요청을 해당 샤드로 라우팅할 수 있습니다. 그렇지 않으면 실행을 위해 요청을 클러스터의 모든 샤드에 보내야 하며 proxy는 샤드에서 반환된 모든 결과 집합을 집계하므로 실행 효율성이 떨어집니다.
- 분할된 테이블을 쿼리할 때 insert/replace 구문에서 shardkey 필드를 지정해야 합니다. 그렇지 않으면 proxy가 이 SQL 문이 라우팅되어야 하는 샤드를 모르기 때문에 SQL 문을 실행할 수 없습니다.
- 분할된 테이블을 쿼리할 때 delete/update 문의 where 조건에 shardkey 필드를 지정해야 합니다. 그렇지 않으면 보안상의 이유로 이 SQL 문을 실행할 수 없습니다.

### 샤드키는 어떻게 선택합니까?
shardkey는 수평 샤딩 동안 샤딩 규칙을 생성하기 위해 사용되는 데이터 테이블 필드로, 테이블 생성 시 지정해야 합니다. TDSQL for MySQL에서 샤드키는 대부분의(또는 주요) 데이터베이스 작업이 수행되는 데이터 필드인 것이 좋습니다. 이러한 테이블 샤딩 솔루션을 아래와 같이 Group-Shard라고 합니다.
![](https://main.qcloudimg.com/raw/f0a5b31d7c69eb34b84dbc9d57b5201a.png)
그룹 샤드 솔루션을 사용하면 연결된 데이터 중 일부와 여러 샤딩된 테이블의 복잡한 비즈니스 논리적 작업을 하나의 물리적 샤드로 집계할 수 있습니다. 예를 들어 이커머스 플랫폼의 주문 테이블과 사용자 테이블이 모두 UserID를 기반으로 샤딩된 경우 join 쿼리를 통해 사용자가 최근에 주문한 주문 수를 빠르게 계산할 수 있습니다(교차 노드 join 또는 분산 트랜잭션 제외).

샤드키 선택의 몇 가지 일반적인 경우는 다음과 같습니다.
 - 사용자 기반 인터넷 애플리케이션의 경우 대부분의(또는 핵심) 데이터베이스 작업이 사용자를 기반으로 하므로 사용자 데이터에 해당하는 필드를 샤드키로 사용할 수 있습니다.
 - 이커머스 애플리케이션이나 O2O 애플리케이션의 경우 대부분의(또는 핵심) 데이터베이스 운영이 판매자와 구매자를 기반으로 하므로 판매자 또는 구매자 데이터에 해당하는 필드를 샤드키로 사용할 수 있습니다. 초대형 셀러가 거래의 대부분을 차지하는 경우 일부 샤드에 대한 부하와 압력이 크게 증가합니다.
 - 게임 애플리케이션의 경우 대부분(또는 코어) 데이터베이스 작업이 플레이어를 기반으로 하므로 플레이어 데이터에 해당하는 필드를 샤드키로 사용할 수 있습니다.
 - IoT(Internet of Things) 애플리케이션의 경우 대부분(또는 코어) 데이터베이스 작업이 IoT 정보를 기반으로 하므로 센서, 독립 장치 또는 SIM 카드의 IMEI 데이터에 해당하는 필드를 샤드키로 사용할 수 있습니다.
 - 세무/산업 및 상업/사회 보험 애플리케이션의 경우 프론트엔드 비즈니스의 대부분(또는 핵심) 데이터베이스 운영은 납세자, 법정 대리인, 거주자의 정보를 기반으로 하므로 납세자 또는 법정 대리인의 데이터에 해당하는 필드를 샤드키로 사용할 수 있습니다.
대부분의 다른 유형의 경우 대부분의(또는 핵심) 데이터베이스 작업의 기반이 되는 데이터 필드를 동일한 방식으로 찾을 수 있지만 샤드 키 선택에 특정 제한이 있습니다. 자세한 내용은 [샤드키 선택 제한](https://intl.cloud.tencent.com/document/product/1042/38506)을 참고하십시오.

### 샤드키를 변경할 수 있습니까?
한 번 선택한 shardkey는 변경할 수 없습니다. 테이블의 shardkey를 수정하려면 새 테이블을 생성해야 합니다.
샤딩된 테이블의 행에서 shardkey 값을 수정하려면 새 값을 insert하고 이전 값을 delete해야 합니다. update할 수 없습니다.
