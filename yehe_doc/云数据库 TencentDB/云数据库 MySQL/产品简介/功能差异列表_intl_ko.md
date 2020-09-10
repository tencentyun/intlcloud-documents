본 문서는 TencentDB for MySQL의 각 아키텍처 유형별로 지원하는 기능과 차이 비교에 대해 소개함으로써 각 아키텍처의 특징을 이해하고 자신에게 맞는 인스턴스를 구매할 수 있도록 도와줍니다.
아래의 테이블에서 '-' 표시는 지원하지 않는다는 의미입니다.

| 기능       | 고가용성 버전         |파이낸스 버전             |단일 노드 고IO 버전        |기본 버전                 | 
| :------------ | :----------------- | :----------------- |:----------------------- | :-------------------- |
| 버전          | <li>MySQL 5.5<li>MySQL 5.6<li>MySQL 5.7<li>MySQL 8.0 |<li>MySQL 5.6<li>MySQL 5.7<li>MySQL 8.0 |<li>MySQL 5.6<li>MySQL 5.7<li>MySQL 8.0 |MySQL 5.7 | 
| 노드 수       |  2                        | 3                       |1                         |1                         |
| 사양 설정    |최대 488GB/6TB    | 최대 488GB/6TB  |최대488GB/6TB    | 최대8GB/1T        | 
| [엔진 버전 업그레이드](https://intl.cloud.tencent.com/document/product/236/8126) | 지원(MySQL 5.5, 5.6만)       | 지원       | 지원      | 지원     |
| [파이낸스 버전 업그레이드](https://intl.cloud.tencent.com/document/product/236/35986)  | 지원           | -         | -            | -       |
| [읽기 전용 인스턴스](https://intl.cloud.tencent.com/document/product/236/7270)    | 지원(MySQL 5.6, 5.7, 8.0만)| 지원| 지원   |- | 
| [재해 복구 인스턴스](https://intl.cloud.tencent.com/document/product/236/7272)    | 지원(MySQL 5.6, 5.7, 8.0만)| 지원|-      |-  | 
| [계정 관리](https://intl.cloud.tencent.com/document/product/236/31900)  | 지원      | 지원         | -             | 지원       |
| [매개변수 설정](https://intl.cloud.tencent.com/document/product/236/35793)  | 지원           | 지원         |-           | 지원     |
| [백업](https://intl.cloud.tencent.com/document/product/236/32340)        | 지원          | 지원           |-         |-          | 
| [롤백](https://intl.cloud.tencent.com/document/product/236/7276)          | 지원          | 지원         |-           |-          | 
| [데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/236/8463)    |  지원         | 지원         |지원        |-       |
| [SQL 파일 가져오기](https://intl.cloud.tencent.com/document/product/236/8466)    |  지원      | 지원         |-           |-       |
| [보안 그룹](https://intl.cloud.tencent.com/document/product/236/14470)       | 지원         | 지원        |지원       | -            |
| [모니터링 및 알람](https://intl.cloud.tencent.com/document/product/236/8455) | 지원                    | 지원                   | 지원                    |지원                    |
| [작업 로그](https://intl.cloud.tencent.com/document/product/236/34588) | 지원                    | 지원                   | 지원                    |지원                    |


