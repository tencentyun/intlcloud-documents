본 문서는 [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 스마트 매개변수 튜닝을 구현하는 방법을 설명합니다.

## 배경
‘딥 러닝’이라는 개념은 일반 사용자들 사이에서 인기를 얻고 있습니다. 관련 기술이 점점 성숙해짐에 따라 TencentDB 팀은 딥 러닝을 사용하여 데이터베이스의 운영 효율성을 향상시키는 방법을 구상하고 있습니다. 가장 먼저 떠오르는 것은 데이터베이스 매개변수 튜닝입니다. 비즈니스 시스템의 큰 차이로 인해 SQL 최적화와 같이 세분화된 방식으로 타깃형 튜닝을 수행하는 것이 불가능하며 이는 DBA의 과제입니다. 더 나은 성능의 매개변수 템플릿 세트를 구축하기 위해서는 종종 경험을 활용해야 합니다. 데이터베이스 매개변수 튜닝 기능은 전문 DBA의 독점 기술에 가깝습니다.

2019년과 2021년 사이에 TencentDB 팀은 <Automatic Database Tuning using Deep Reinforcement Learning> 및 <An Oline Cloud Database Hybrid Tuning System for Personalized Requirements> 이라는 제목의 두 논문을 각각 발표했으며 이론에 대한 국제 특허를 출원했습니다. 이제 이 이론은 논문을 기반으로 실제 사용 사례에서 매개변수를 튜닝하여 데이터베이스 성능을 향상시키는 사용 가능한 시스템으로 개발되었습니다.

**데이터베이스 매개변수 튜닝이 필요한 이유:**
- **많은 수의 매개변수**: 예를 들어 MySQL에는 수백 개의 구성 항목이 있으므로 튜닝이 어렵습니다.
- **높은 인건비**: 전임 DBA가 필요하고 전문적인 경험이 필요하므로 인건비가 많이 듭니다.
- **빈약한 도구 보편성**: 기존 도구는 기능이 제한되고 작업 시간이 많이 소요되어 효과가 좋지 않습니다.
- **클라우드의 새로운 니즈**: 일부 사용자는 전임 운영팀이 없어 매개변수 튜닝을 구현하는 것이 불가능합니다.

## 전제 조건
실행 중인 TencentDB for MySQL 인스턴스가 있습니다.

## 사용 제한
- 시나리오 기반 스마트 튜닝은 인스턴스당 월 3회만 수행할 수 있습니다. 이 한도는 매월 1일에 재설정됩니다.
- AI 기반 스마트 분석(출시 예정)은 인스턴스당 월 1회만 수행할 수 있습니다. 이 한도는 매월 1일에 재설정됩니다.
- 스마트 매개변수 튜닝은 CPU 코어가 4개 이상인 인스턴스에 대해서만 수행할 수 있습니다.
- 스마트 매개변수 튜닝 작업 목록은 최근 15개의 튜닝 결과만 유지합니다.
- 인스턴스가 종료/반환되거나 만료되면 해당 인스턴스에서 진행 중인 스마트 매개변수 조정 작업이 자동으로 중단되고 삭제됩니다.
- 인스턴스당 한 번에 하나의 튜닝 작업만 실행할 수 있습니다.
- 스마트 매개변수 튜닝 기능은 현재 베이징, 상하이 및 광저우 리전에서만 지원되며 향후 더 많은 리전에서 사용할 수 있습니다.

## 작업 단계
### 이전에 구매한 MySQL 인스턴스
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인하여 상단의 리전을 선택합니다. 인스턴스 목록에서 인스턴스 ID 또는 **작업** 열의 **관리**를 클릭하여 인스턴스 관리 페이지로 들어갑니다.
2. 인스턴스 관리 페이지에서 **데이터베이스 관리** > **매개변수 설정** > **스마트 매개변수 튜닝**을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a1231071d9542857295c3875d25038a3.png)
3. 스마트 매개변수 튜닝 팝업 창에서 **시나리오 기반 스마트 튜닝** 또는 **AI 기반 스마트 분석**을 튜닝 방법으로 선택하고 **분석**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/88a18f17f80772ea67a0c7127fd74218.png)
 - **시나리오 기반 스마트 튜닝**을 선택한 경우 다음 단계를 진행합니다.
**시나리오 기반 스마트 튜닝**: 선택한 시나리오를 기반으로 하는 효율적이고 표적화된 스마트 분석입니다.
 **시나리오** 드롭다운 목록에서 비즈니스 시나리오(주문 트랜잭션, OLTP 성능 테스트 또는 압력 테스트)를 선택합니다.
 시나리오 선택 후 보다 정확한 시스템 분석을 위해 시나리오 내 비즈니스 비율을 사용자 정의 할 수 있습니다. 구성 완료 후 **분석**을 클릭합니다.
    - 주문 트랜잭션(TPCC)
      - 사용자 정의 항목: 주문 처리(높음), 결제(높음), 주문 조회(낮음), 물류(낮음), 창고(낮음)
      - 데이터 읽기 모드: 캐시(기본값), 디스크 + 캐시
      - 동시성: 낮음, 중간, 높음(기본값)
    - OLTP 성능 테스트(Sysbench)
      - 사용자 정의 항목: 데이터 읽기(높음), 데이터 쓰기(기본값 없음)
      - 데이터 읽기 모드: 캐시(기본값), 디스크 + 캐시
      - 동시성: 낮음, 중간, 높음(기본값)
    - 압력 테스트(myslap)
      - 동시성: 낮음, 중간, 높음(기본값)
![](https://qcloudimg.tencent-cloud.cn/raw/6e8dac90a50b17e84199b3f6776a2d90.png)
 - **AI 기반 스마트 분석**(출시 예정)을 선택한 경우 다음 단계를 따릅니다.
**AI 기반 스마트 분석**: 데이터베이스 운영 메트릭에 대한 심층 분석을 통해 데이터베이스 비즈니스 유형을 결정하고 특정 시나리오에서 다양한 매개변수의 성능을 딥 러닝 알고리즘으로 분석한 후 매개변수 권장 사항을 제시합니다.
AI 기반 스마트 분석을 선택한 후 **분석**을 클릭합니다.
>!
>- AI 기반 스마트 분석은 개선 중이며 곧 제공될 예정입니다.
>- 딥 러닝 알고리즘과 빅 데이터 분석을 기반으로 스마트 분석으로, 시간이 많이 소요됩니다. 사용량이 적은 시간에 수행하는 것이 좋습니다.
4. 분석이 시작되면 매개변수 튜닝 작업이 시작됩니다. 매개변수 설정 페이지에서 **스마트 매개변수 튜닝** > **작업 보기**를 선택하여 작업 세부정보를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1c66551fd214b1775bf33bdd4a98a935.png)
5. 매개변수 튜닝 작업이 완료된 후 **스마트 매개변수 튜닝** > **작업 보기**의 **작업** 열에서 **결과 보기**를 클릭할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/895d52add70eb601b4e5c994f634cbfc.png)
6. 매개변수 튜닝 권장 사항을 확인한 후 **인스턴스에 적용**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/39a40c1a3cc2a26bef76ccdbee0f129e.png)
7. 팝업 창에서 매개변수 변경을 확인하고 실행 모드를 선택하고 재시작 규칙을 읽고 동의 체크한 후 **확인**을 클릭합니다.
실행 모드:
  - 즉시 실행 : 확인 후 즉시 인스턴스에 변경 사항이 적용됩니다.
  - 점검 시간 중: 점검 시간 동안 인스턴스에 변경 사항이 적용되며, 인스턴스 세부 정보 페이지에서 수정할 수 있습니다.

### 새로 구매한 MySQL 인스턴스
TencentDB for MySQL 인스턴스를 구매할 때 매개변수 템플릿을 선택한 후 **매개변수 적응** 활성화 여부를 선택할 수 있습니다. 이 기능이 활성화되면 시스템은 주문 트랜잭션, OLTP 성능 테스트 또는 압력 테스트가 될 수 있는 선택된 비즈니스 시나리오에 따라 2차 조정을 수행합니다.
**매개변수 설정** > **스마트 매개변수 튜닝** > **작업 보기**에서 변경 결과를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bf0e00d4ba24814e1bad20f17cd50575.png)

