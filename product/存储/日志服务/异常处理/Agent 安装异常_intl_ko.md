> CLS Loglistener 설치와 사용에 대한 세부 정보는 [LogListener 설치 가이드](https://cloud.tencent.com/document/product/614/17414) 문서를 참조하고 [Loglistener 메커니즘](https://cloud.tencent.com/document/product/614/17415)을 파악하십시오.

## 가능한 원인

다음과 같은 이유로 Loglistener가 올바르게 설치되지 않을 수 있습니다.
1. 커널 버전은 64비트만 지원합니다.
2. 설치 방법이 잘못되었습니다.
3. 최신 기능은 높은 버전의 Loglistener에 의존합니다.


## 처리 절차

1. 커널 버전을 확인하십시오.
Loglistener 설치 디렉터리의 bin 디렉터리에 있는 실행 가능한 파일은 Linux 64비트 커널만 지원합니다. **uname -a** 명령을 실행하여 커널 버전이 x86_64인지를 확인하십시오.
2. 실행 명령 설치를 확인하십시오.
Tools 디렉터리의 스크립트 파일은 bash 스크립트이며 `sh install.sh` 실행 방식을 지원하지 않습니다. `./install.sh` 또는 `bash install.sh` 방식을 권장합니다. [LogListener 설치 가이드](https://cloud.tencent.com/document/product/614/17414) 문서에 따라 조작하십시오.
3. Loglistener 버전을 확인하십시오.
CLS의 최신 기능은 새로운 버전의 Loglistener에 따라 달라질 수 있습니다. 새로운 기능 사용 이상인 경우 [Loglistener 최신 버전](https://main.qcloudimg.com/raw/8656fcadd12ab9689674df09b510b52b/loglistener.2.2.2.tar.gz)을 다운로드하십시오.
4. Loglistener가 성공적으로 설치되었는지 확인하십시오.
다음 명령을 사용하여 설치 디렉터리에서 LogListener 프로세스가 정상적으로 실행되고 있는지 확인하십시오.
```shell
cd loglistener/tools && ./p.sh
```
정상적인 상황에서 출력은 다음과 같습니다.
 ![](https://main.qcloudimg.com/raw/e256cf61689ead123251a8f9f3a753c9.png)
다음 명령을 실행하여 설치 디렉터리에서 구성 항목이 올바르게 구성되어 있고 네트워크 상태가 정상인지 확인하십시오.
```shell
cd loglistener/bin && ./check
```
정상적인 상황에서 출력은 다음과 같습니다.
 ![](https://main.qcloudimg.com/raw/e7e85f139feb14b1aaa3353b2bafd5e1.png)
 위의 명령을 올바르게 실행하면 Loglistener를 성공적으로 설치할 수 있습니다.

