## 현상 설명
CentOS 6.x 운영 체제의 CVM를 재시작하거나 `service network restart` 명령어를 실행한 후, CVM에서 도메인 이름이 확인되지 않는 상황이 나타날 수 있습니다. 동시에 `/etc/resolv.conf` 구성 파일을 조회할 경우, DNS 정보가 비어 있는 걸 발견할 수 있습니다.

## 예상 원인
CentOS 6.x 운영 체제에서 grep 버전이 다를 경우, initscripts의 버전이 9.03.49-1보다 낮아 결함이 존재할 수 있습니다.

## 해결 방식
initscripts의 최신 버전으로 업데이트하고 DNS 정보를 다시 생성하십시오.

## 처리 순서
1. CVM에 로그인하십시오.
2. 아래의 명령어를 실행하여 initscripts 의 버전을 확인하고, 9.03.49-1 보다 낮은 버전으로 인해 initscripts에 결함이 있는지 확인하십시오.
```
rpm -q initscripts
```
아래와 유사한 정보 리턴
```
initscripts-9.03.40-2.e16.centos.x86_64
```
initscripts의 버전이 initscripts-9.03.40-2보다 낮은 버전이라서(initscripts-9.03.49-1) DNS 삭제 위험이 있다는 것을 알 수 있습니다.
3. 아래의 명령어를 순서에 따라 실행하여 initscripts를 최신 버전으로 업데이트하고 DNS 정보를 다시 생성하십시오.
```
yum makecache
yum -y update initscripts
service network restart
```
3. 업데이트 완료 후, 아래의 명령어를 실행해 initscripts의 버전 정보를 조회하여 업데이트 성공 여부를 확인하십시오.
```
rpm -q initscripts
```
아래와 유사한 정보 리턴
```
initscripts-9.03.58-1.el6.centos.2.x86_64
```
표시되는 버전이 이전의 버전과 다르며, initscripts-9.03.49-1보다 높아 업데이트 작업이 성공했다는 것을 알 수 있습니다.
