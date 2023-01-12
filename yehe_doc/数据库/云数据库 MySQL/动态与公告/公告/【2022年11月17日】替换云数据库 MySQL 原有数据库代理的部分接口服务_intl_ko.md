TencentDB for MySQL은 새로운 데이터베이스 프록시 버전을 출시했습니다. 새 버전의 모든 기능을 지원하기 위해 아래 설명된 대로 데이터베이스 프록시를 교체, 업그레이드 및 구성하기 위한 새 API가 제공됩니다.

## 변경 일자
2022년 11월 17일 목요일부터 변경됩니다.

## 교체된 API

| 이전 API | 새로운 API | 설명 |
|---------|---------|---------|
| UpgradeCDBProxy | [AdjustCdbProxy](https://intl.cloud.tencent.com/document/product/236/45187) | 데이터베이스 프록시 구성 업그레이드 |
| ModifyCDBProxy | [AdjustCdbProxyAddress](https://intl.cloud.tencent.com/document/product/236/45194) | 데이터베이스 프록시의 읽기/쓰기 분리 구성 |
