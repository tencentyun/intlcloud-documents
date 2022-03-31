본 문에서는 TencentDB for MySQL 성능 테스트 툴인 SysBench와 CVM 인스턴스에 SysBench를 설치하는 방법을 소개합니다.

## SysBench 툴 소개
SysBench는 고부하 데이터베이스를 실행할 때 시스템의 관련 핵심 매개변수의 성능을 평가하는 데 사용되는 크로스 플랫폼 및 멀티 스레드 모듈식 벤치마크 테스트 툴 입니다. 복잡한 데이터베이스 벤치마크 설정을 무시하고 데이터베이스가 설치되지 않은 경우에도 데이터베이스 시스템 성능을 빠르게 알 수 있습니다.

## SysBench 테스트 모델
 - SysBench 표준 OLTP 읽기/쓰기 혼합 시나리오에서 트랜잭션에는 18개의 읽기/쓰기 SQL이 포함됩니다.
 - SysBench 표준 OLTP 읽기 전용 시나리오에서 트랜잭션에는 14개의 읽기 SQL(10개의 기본 키 포인트 쿼리, 4개의 범위 쿼리)이 포함됩니다.
 - SysBench 표준 OLTP 쓰기 전용 시나리오에서 트랜잭션에는 4개의 쓰기 SQL(2개의 UPDATE, 1개의 DETELE 및 1개의 INSERT)이 포함됩니다.

## SysBench 매개변수 설명
| 매개변수     | 설명 | 
|---------|---------|
| db-driver | 데이터베이스 엔진  | 
| mysql-host | MySQL 인스턴스 연결 주소  |
| mysql-port | MySQL 인스턴스 연결 포트  |
| mysql-user | MySQL 인스턴스 계정  |
| mysql-password | MySQL 인스턴스 계정에 해당하는 비밀번호  |
| mysql-db | MySQL 인스턴스 데이터베이스 이름 |
| table_size| 테스트 테이블 크기  |
|tables | 테스트 테이블 수 |
| events | 테스트 요청 수 |
| time | 테스트 시간 |
| threads | 테스트 스레드 수 |
| percentile | 통계할 백분율, 기본값은 95%, 즉 95%의 경우에서 실행 시간 요청 |
| report-interval | 테스트 진행 보고서가 N초에 한 번 출력됨을 나타내며, 0은 테스트 진행 보고서 출력이 비활성화되고 최종 보고서 결과만 출력됨을 의미 |
| skip-trx | 트랜잭션 건너뛰기 여부. <br>1: 건너뛰기<br>0: 건너뛰지 않음 |

## 설치 방법
이 부하 테스트는 SysBench 버전 1.0.20을 사용합니다. 자세한 내용은 [Sysbench 공식 문서](https://github.com/akopytov/sysbench?spm=a2c4g.11186623.2.12.36061072oZL2qS)를 참고하십시오.
1. CVM 인스턴스에서 다음 명령어를 실행하여 SysBench를 설치합니다.
```
yum install gcc gcc-c++ autoconf automake make libtool bzr mysql-devel git mysql
git clone https://github.com/akopytov/sysbench.git
##Git에서 SysBench 다운로드
cd sysbench
##SysBench 디렉터리 열기
git checkout 1.0.20
##SysBench 1.0.20 버전 으로 전환
./autogen.sh
##autogen.sh 실행
./configure --prefix=/usr --mandir=/usr/share/man
make
##컴파일
make install
```
2. 다음 명령을 실행하여 커널이 모든 CPU를 사용하여 데이터 패킷을 처리하는 동시에 CPU 간의 컨텍스트 전환을 줄일 수 있도록 클라이언트를 설정합니다.
```
sudo sh -c 'for x in /sys/class/net/eth0/queues/rx-*; do echo ffffffff>$x/rps_cpus; done'
sudo sh -c "echo 32768 > /proc/sys/net/core/rps_sock_flow_entries"
sudo sh -c "echo 4096 > /sys/class/net/eth0/queues/rx-0/rps_flow_cnt"
sudo sh -c "echo 4096 > /sys/class/net/eth0/queues/rx-1/rps_flow_cnt"
```
>?ffffffff는 32개의 CPU 사용을 의미합니다(1개 f는 4개의 CPU를 의미).

