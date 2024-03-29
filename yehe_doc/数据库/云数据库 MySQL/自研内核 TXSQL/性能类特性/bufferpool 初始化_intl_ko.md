## 기능 소개
buffer pool 초기화 속도를 높이고 데이터베이스 인스턴스 실행 소요시간을 줄입니다.

### 지원 버전
- 커널 버전 MySQL 5.6 20200915 이상
- 커널 버전 MySQL 5.7 20200630 이상

## 적용 시나리오
데이터베이스 실행 속도 향상에 사용됩니다.

## 성능 테스트 데이터
8개의 instance가 주어진 경우, 성능 테스트 데이터는 다음과 같습니다:

| buffer_pool_size | buffer pool 초기화 시간(최적화 전) | buffer pool 초기화 시간(최적화 후) | 속도 향상률 |
| :--------------: | :----------------------------- | :----------------------------- | :------: |
|       50GB        | 2.55s                          | 0.13s                          |  1962%   |
|       200GB       | 10.28s                         | 0.52s                          |  1977%   |
|       500GB       | 25.72s                         | 1.32s                          |  1948%   |

## 사용 설명
커널은 기본적으로 구현됩니다.
