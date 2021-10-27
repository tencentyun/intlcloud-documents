## 현상 설명
로그에 다음 이미지와 같이 “fork: Cannot allocate memory”. 오류 보고가 나타납니다.
![](https://main.qcloudimg.com/raw/db85a43e7495f1655a2b59063ffc33e3.png)

## 예상 원인
가능한 원인은 프로세스 수 초과입니다. 시스템 내부의 총 프로세스 수가 `pid_max` 에 도달하면 신규 프로세스 생성 시 “fork: Cannot allocate memory” 오류가 보고됩니다.

## 해결 방법
1. [처리 순서](#ProcessingSteps)를 참고하여 인스턴스 메모리 사용률이 지나치게 높지는 않은지 확인합니다.
2. 총 프로세스 수가 제한을 초과하는지 확인하고 총 프로세스 수 'pid_max'의 구성을 수정합니다. 



## 처리 순서[](id:ProcessingSteps)
1. [지나치게 높은 인스턴스 메모리 사용률](https://intl.cloud.tencent.com/document/product/213/40501)을 참고하여 인스턴스 메모리 사용률을 확인합니다. 인스턴스 메모리 사용률이 정상이라면 다음 단계를 실행합니다.
2. 다음 명령어를 실행하여 시스템의 `pid_max` 값을 조회합니다.
```
sysctl  -a | grep pid_max
```
`pid_max`의 기본값은 32768입니다. 반환 결과는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/816a0bd183244aadf14e04c6ed200d68.png)
3. 다음 명령어를 실행하여 시스템 내부의 총 프로세스 수를 조회합니다.
```
pstree -p | wc -l
```
총 프로세스 수가 `pid_max`에 도달하면 신규 프로세스 생성 시 시스템에서 'fork: Cannot allocate memory' 오류가 보고됩니다.
>?`ps -efL` 명령어를 실행하여 프로세스 수가 비교적 많은 프로그램을 파악합니다.
>
4. 프로세스 수를 늘리기 위해 `/etc/sysctl.conf` 구성 파일의 `kernel.pid_max` 값을 65535로 수정합니다. 수정이 완료되면 다음과 같은 화면이 나타납니다.
![](https://main.qcloudimg.com/raw/a4bbf49b3236b9f50988e914298adb31.png)
5. 아래의 명령어를 실행하여 설정을 즉시 활성화합니다.
```
sysctl -p
```
