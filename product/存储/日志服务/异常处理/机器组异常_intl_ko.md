## 문제 설명
로그 캡처에 이상이 발생했으며 연결된 서버 그룹의 상태가 이상인 것으로 발견되었습니다.

## 가능한 원인
서버 그룹과 CLS 시스템 간의 하트비트가 중단되어 로그를 캡처하고 보고하지 못합니다. 서버 그룹에 이상이 발생한 가능한 원인은 다음과 같습니다.
1. IP 주소 입력에 오류가 발생했습니다.
2. 네트워크 연결이 끊어졌습니다.
3. LogListener 프로세스가 실패하였습니다.
4. LogListener 구성에 오류가 발생했습니다.

## 해결책
위의 가능한 원인에 따라 문제를 점검하십시오.

## 처리 절차
1. 서버 그룹에 추가된 IP 주소가 올바른지 확인하십시오.
2. 다음 명령을 사용하여 네트워크 연결 여부를 확인하십시오.
```shell
telnet <region>.cls.myqcloud.com 80
```
그중, `<region>`은 CLS 소재 지역의 약어입니다. 구체적인 지역 정보는 [가용 영역](https://cloud.tencent.com/document/product/614/18940) 문서를 참조하십시오.
정상적으로 연결된 경우, 다음 코드가 제시됩니다. 그렇지 않으면 연결 실패가 제시됩니다. 이 경우, 네트워크가 정상적으로 연결되어 있는지 확인하십시오.
![](https://main.qcloudimg.com/raw/2660316a4496ac356b6e7ca5cdeb9daa.png)
3. 다음 명령을 사용하여 LogListener 프로세스가 정상적으로 실행되고 있는지 확인하십시오.
```shell
cd loglistener/tools && ./p.sh
```
일반적으로 세 가지 프로세스가 있습니다.
```shell
bin/loglistenerm -d                                #데몬 프로세스
bin/loglistener --conf=etc/loglistener.conf        #메인 프로세스    
bin/loglisteneru -u --conf=etc/loglistener.conf    #업데이트 프로세스
```
**실패한 프로세스가 있는 경우** 다시 시동하고 설치 디렉터리에서 다음 명령을 실행해야 합니다.
```shell
cd loglistener/tools && ./start.sh
```
4. LogListener의 키 및 IP 식별자 구성 정보가 올바른지 확인하십시오. 구성 파일 경로는 `/loglistener/etc/loglistener.conf`입니다.
![](https://main.qcloudimg.com/raw/cfa012cfb136cbbcf78667d4d1307d26.png)
 - 키는 Tencent Cloud 계정 또는 협력자를 위한 API 키입니다. 프로젝트 키를 지원하지 않습니다.
  - 구성 파일의 group_ip는 콘솔의 서버 그룹에 입력된 IP와 일치해야 합니다. LogListener는 서버 IP를 자동으로 가져오므로 서버가 여러 ENI로 바인딩될 때 일관성을 정기적으로 확인하십시오.

