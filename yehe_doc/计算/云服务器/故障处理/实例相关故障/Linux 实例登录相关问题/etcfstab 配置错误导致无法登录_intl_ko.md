## 오류 설명[](id:symptom)
SSH를 통해 원격으로 Linux CVM에 로그인할 수 없지만 VNC를 통해 CVM에 로그인한 후 시스템 시작 실패를 확인하고 “Welcome to emergency mode”라는 프롬프트 메시지를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/dea541a48d2a01503c1dbbc85b0d396f.png)


## 가능한 원인
`/etc/fstab`이 제대로 구성되지 않았습니다.
예를 들어 `/etc/fstab` 파일의 장치 이름을 기반으로 디스크 자동 연결을 구성했습니다. CVM이 다시 시작될 때 장치 이름이 변경되면 이 구성으로 인해 시스템이 정상적으로 시작되지 않습니다.


## 해결 방법
[처리 단계](#ProcessingSteps)를 참고하여 `/etc/fstab` 구성 파일을 복구하고 CVM을 다시 시작합니다.


## 처리 단계[](id:ProcessingSteps)

다음 두 가지 방법으로 인스턴스에 액세스할 수 있습니다.

<dx-tabs>
::: 방법1: VNC를 통해 로그인(권장)[](id:useVNC)
1. [VNC를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32494)합니다.
2. VNC 페이지에서 [오류 설명](#symptom)과 같은 현상이 나타나면 root 계정과 비밀번호를 입력하고 **Enter**를 눌러 서버에 로그인하십시오.
 - 비밀번호는 기본적으로 보이지 않습니다.
 - root 계정과 비밀번호가 없다면 Rescue 모드를 시도해보십시오.
3. [](id:Step3)다음 명령어를 실행하여 `/etc/fstab` 파일을 백업합니다. 다음 예시에서 파일은 `/home` 디렉터리에 백업됩니다.
```shellsession
cp /etc/fstab /home
```
4. 다음 명령어를 실행하여 VI 편집기를 사용하여 `/etc/fstab` 파일을 엽니다.
```shellsession
vi /etc/fstab
```
5. **i**를 눌러 편집 모드로 들어갑니다. 커서를 오류 줄의 시작 부분으로 이동하고 `#`을 입력하여 이 구성을 주석 처리합니다.
<dx-alert infotype="explain" title="">
오류가 확실하지 않은 경우 시스템 디스크를 제외한 연결된 모든 디스크의 구성을 주석 처리하십시오. 문제를 해결한 후 [8단계](#Step7)에서 설명한 대로 이러한 구성을 복구할 수 있습니다.
</dx-alert>
<img src="https://qcloudimg.tencent-cloud.cn/raw/1c238789186d7f24c0244e0307bc3a22.png"/>
6. [](id:Step6) **Esc**를 누르고 **:wq**를 입력한 다음 **Enter**를 눌러 구성을 저장하고 편집기를 종료합니다.
7. 콘솔을 통해 인스턴스를 다시 시작하고 정상적으로 시작 및 로그인할 수 있는지 확인합니다.
<dx-alert infotype="explain" title="">
[인스턴스 재시작](https://intl.cloud.tencent.com/document/product/213/4928)을 참고하십시오.
</dx-alert>
8. [](id:Step8)로그인 성공 후 디스크 자동 연결 설정이 필요한 경우 [Cloud Disk Automount Failed upon Linux CVM Restart](https://intl.cloud.tencent.com/document/product/362/40001)를 참고하십시오.

:::
::: 방법2: 복구 모드[](id:useRescue)
1. 인스턴스 복구 모드로 들어갑니다. [복구 모드 사용](https://intl.cloud.tencent.com/document/product/213/46157)을 참고하십시오.
<dx-alert infotype="notice" title="">
[복구 모드를 사용한 시스템 복구](https://intl.cloud.tencent.com/document/product/213/46157#.E4.BD.BF.E7.94.A8.E6.95.91.E6.8F.B4.E6.A8.A1.E5.BC.8F.E8.BF.9B.E8.A1.8C.E7.B3.BB.E7.BB.9F.E4.BF.AE.E5.A4.8D)에 설명된 `mount` 및 `chroot` 명령을 실행하고 대상 시스템에 진입했는지 확인합니다.
</dx-alert>
2. 방법1의 [3단계](#Step3) - [6단계](#Step6)에 따라 `/etc/fstab` 파일을 복구합니다.
3. [복구 모드 종료](https://intl.cloud.tencent.com/document/product/213/46157#.E9.80.80.E5.87.BA.E6.95.91.E6.8F.B4.E6.A8.A1.E5.BC.8F)를 참고하여 인스턴스 복구 모드를 종료합니다.
4. 인스턴스가 복구 모드를 종료한 후에도 여전히 종료됩니다. [인스턴스 스타트업](https://intl.cloud.tencent.com/document/product/213/38168)의 설명에 따라 시작합니다. 그런 다음 시스템을 정상적으로 시작하고 로그인할 수 있는지 확인합니다.
5. 로그인 성공 후 디스크의 자동 연결을 구성하려면 [Configuring the /etc/fstab file](https://intl.cloud.tencent.com/document/product/362/40001)을 참고하십시오.

:::
</dx-tabs>







