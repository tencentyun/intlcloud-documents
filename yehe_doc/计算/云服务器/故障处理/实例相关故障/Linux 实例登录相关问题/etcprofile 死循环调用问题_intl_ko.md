## 현상 설명
SSH를 사용하여 Linux 인스턴스에 로그인할 때 ‘Last login:’ 이라는 관련 정보가 출력되고 SSH 명령이 중지됩니다.


## 예상 원인
`/etc/profile` 파일이 수정되었기 때문에 `/etc/profile`에서 `/etc/profile` 호출 현상이 발생하여 무한 루프 호출에 빠져 로그인 실패가 발생하였을 수 있습니다.



## 해결 방법
[처리 단계](#ProcessingSteps)를 참고하여, `/etc/profile` 파일을 확인 및 복구합니다.


## 처리 순서[](id:ProcessingSteps)
1. [VNC 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)합니다.
2. 다음 명령을 실행하여 `/etc/profile` 파일을 확인합니다.
```
vim  /etc/profile
```
3. `/etc/profile` 파일에 `/etc/profile` 관련 명령어가 포함되어 있는지 확인합니다.
 - 포함된 경우 다음 단계를 실행합니다.
 - 포함되지 않은 경우 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)을 통해 고객센터에 도움을 요청하십시오.
4. **i**를 눌러 편집 모드로 들어가고 `/etc/profile`에서 해당 명령 앞에 `#`을 추가하여 명령을 주석 처리합니다.
5. **Esc**를 눌러 편집 모드를 종료하고 **:wq**를 입력하여 변경 사항을 저장합니다.
6. 다시 [SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)합니다.
