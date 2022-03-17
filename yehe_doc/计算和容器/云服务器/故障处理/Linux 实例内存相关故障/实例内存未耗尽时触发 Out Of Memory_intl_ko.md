## 현상 설명
다음과 같이 Linux CVM에 메모리 사용량이 남은 상황에서 OOM(Out Of Memory)이 트리거됩니다.
![](https://main.qcloudimg.com/raw/72cbd63ac445a1caa8d82fa1e55ba5a5.png)

## 예상 원인
가능한 원인은 시스템 내 사용 가능한 메모리가 `min_free_kbytes` 값보다 적은 것입니다. `min_free_kbytes` 값은 Linux 시스템에 강제로 남겨지는 최소 유휴 메모리(Kbytes)입니다. 시스템 내 사용 가능한 메모리가 `min_free_kbytes` 설정 값보다 적은 경우, 시스템은 oom-killer을 실행하거나 강제 재시작되도록 기본 설정되어 있습니다. 구체적인 실행은 커널 매개변수 `vm.panic_on_oom` 값에 의해 결정됩니다.
 - `vm.panic_on_oom=0`인 경우 시스템에 OOM 메시지가 나타나고 oom-killer가 실행되어 메모리 점유율이 가장 높은 프로세스를 종료합니다.
 - `vm.panic_on_oom =1`인 경우 시스템이 자동으로 재시작됩니다.

## 해결 방법
1. [처리 순서](#ProcessingSteps)를 참고하여 인스턴스 메모리 사용률이 지나치게 높지는 않은지, 프로세스 수에 제한이 있는지 확인합니다.
2. `min_free_kbytes` 값 설정을 확인하고 올바르게 수정합니다.


## 처리 순서[](id:ProcessingSteps)
1. [지나치게 높은 인스턴스 메모리 사용률](https://intl.cloud.tencent.com/document/product/213/40501)을 참고하여 인스턴스 메모리 사용률을 확인합니다. 인스턴스 메모리 사용률이 정상이라면 다음 단계를 실행합니다.
2. [로그 오류 보고 fork: Cannot allocate memory](https://intl.cloud.tencent.com/document/product/213/40502)를 참고하여 프로세스 수가 제한을 초과하는지 확인합니다. 초과하지 않는다면 다음 단계를 실행합니다.
3. CVM에 로그인한 후 다음 명령어를 실행해 `min_free_kbytes` 값을 조회합니다.
```
sysctl -a | grep min_free
```
`min_free_kbytes` 값의 단위는 kbytes입니다. 다음과 같이 `min_free_kbytes = 1024000`으로 1GB입니다.
![](https://main.qcloudimg.com/raw/18ac6c04962abfbf67132eab1a604167.png)
4. 다음 명령어를 실행하여 VIM 편집기로 `/etc/sysctl.conf` 구성 파일을 엽니다.
```
vim /etc/sysctl.conf
```
5. **i**를 눌러 편집 모드로 전환한 다음 `vm.min_free_kbytes` 설정 항목을 수정합니다. 해당 설정 항목이 존재하지 않는 경우 구성 파일에 직접 추가할 수 있습니다.
<dx-alert infotype="explain" title="">
`vm.min_free_kbytes` 값을 전체 메모리의 1% 이하로 수정할 것을 권장합니다.
</dx-alert>
6. **Esc**를 누르고 **:wq**를 입력한 다음, **Enter**를 눌러 저장하고 VIM 편집기를 종료합니다.
7. 아래의 명령어를 실행하여 설정을 활성화합니다.
```
sysctl -p
```
