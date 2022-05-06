## 현상 설명
명령 실행 또는 시스템 시작 과정 중 명령 찾을 수 없음 또는 lib 라이브러리 찾을 수 없음 등의 오류 메시지가 표시됩니다.


## 예상 원인
CentOS 7, CentOS 8, Ubuntu 20 등 시스템의 bin, sbin, lib 및 lib64는 소프트 링크입니다:
```
lrwxrwxrwx   1 root root     7 Jun 19  2018 bin -> usr/bin
lrwxrwxrwx   1 root root     7 Jun 19  2018 lib -> usr/lib
lrwxrwxrwx   1 root root     9 Jun 19  2018 lib64 -> usr/lib64
lrwxrwxrwx   1 root root     8 Jun 19  2018 sbin -> usr/sbin
```
소프트 링크가 삭제되면 명령 실행 또는 시스템 실행 중에 오류가 보고됩니다.


## 해결 방법
[처리 단계](#ProcessingSteps)를 참고하여 필요한 소프트 링크 확인 및 생성합니다.


## 처리 단계[](id:ProcessingSteps)
1. 복구 모드를 시작합니다.
2. 'mount' 및 'chroot' 등의 명령을 실행합니다. 그 중 `chroot` 명령 실행 시:
 - 오류 발생 시, `cd /mnt/vm1`을 실행합니다.
 - 오류 미발생 시, `cd /`를 실행합니다.
3. 다음 명령을 실행하여 해당 소프트 링크가 존재하는지 확인합니다.
```
ls -al / | grep -E "lib|bin"
```
 - 존재하는 경우, [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)을 통해 고객센터에 도움을 요청하십시오.
 - 존재하지 않는 경우, 필요에 따라 다음 명령을 실행하여 해당 소프트 링크를 생성합니다.
```
ln -s usr/lib64 lib64
ln -s usr/sbin sbin
ln -s usr/bin bin
ln -s usr/lib lib
```
4. 다음 명령을 실행하여 소프트 링크를 확인합니다.
```
chroot /mnt/vm1 /bin/bash
```
오류 메시지가 보고되지 않으면 소프트 링크가 성공적으로 복구된 것입니다.
5. 복구 모드를 종료하고 시스템을 실행합니다.
