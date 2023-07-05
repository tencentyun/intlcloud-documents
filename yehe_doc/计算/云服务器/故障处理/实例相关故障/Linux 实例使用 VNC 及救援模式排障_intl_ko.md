일반적으로 VNC 및 복구 모드를 통해 대부분의 Linux 시스템 문제를 해결할 수 있습니다. 본 문서에서는 SSH 키를 통한 Linux 인스턴스 로그인 실패 및 시스템 오류와 같은 문제를 해결하는 방법을 설명합니다.


## 문제 해결 도구
- VNC를 통한 로그인은 Web 브라우저를 통해 CVM에 원격으로 연결하는 방법입니다. 이를 통해 CVM 상태를 직접 관찰하거나 시스템의 구성 파일을 수정할 수 있습니다. 일반적으로 SSH 키를 통해 인스턴스에 원격으로 로그인할 수 없는 경우 이 로그인 방법을 사용할 수 있습니다.
- 복구 모드는 일반적으로 Linux 시스템을 정상적으로 시작할 수 없거나 VNC를 통해 Linux 인스턴스에 로그인할 수 없는 경우에 사용됩니다. 일반적인 사용 사례: 비정상적인 fstab 구성, 주요 시스템 파일 누락, .lib 및 .dll 파일 손상/누락 등.

## 문제 진단 및 처리

<dx-accordion>
::: VNC를 사용하여 SSH 키 로그인 실패 문제 해결[](id:cantSSHlogin)
#### 오류 설명
SSH 키를 통해 Linux 인스턴스에 로그인하려고 하면 “ssh_exchange_identification: Connection closed by remote host” 오류 메시지가 표시됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/4cfe14beb79b3b7b1b617fce540a53a0.png)



#### 예상 원인
kex_exchange_identification 단계의 connection reset 오류는 일반적으로 ssh 관련 프로세스가 시작되었음을 의미하지만 sshd 구성 파일 권한이 수정되는 등 구성이 비정상적일 수 있습니다.


#### 해결 방식
sshd 프로세스를 확인하고 문제를 찾아 수정하려면 [처리 단계](#ProcessingSteps1)를 참고하십시오.


#### 처리 단계[](id:ProcessingSteps1)
1. [](id:ProcessingSteps1Step1) 다음 단계에 따라 VNC를 통해 Linux 인스턴스에 로그인합니다.
   1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인하여 대상 Linux CVM을 찾은 다음 작업 열에서 **로그인**을 클릭합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/93c135917fbe34913151bbefc5b48832.png)
 2. ‘표준 로그인 | Linux 인스턴스’ 창에서 **VNC를 통해 로그인**을 클릭합니다.
 3. ‘login’ 후 사용자 이름을 입력하고 **Enter**를 누르고, ‘Password’ 후에 비밀번호를 입력하고 **Enter**를 누릅니다. 다음 정보가 표시되면 로그인이 성공한 것입니다.
 ![](https://qcloudimg.tencent-cloud.cn/raw/0db1a72ceca22fbf56f8872f60baff4f.png)
2. 다음 명령어를 실행하여 sshd 프로세스가 정상적으로 실행되고 있는지 확인합니다.
```shellsession
ps -ef | grep sshd
```
아래와 같은 결과가 나오면 sshd 프로세스가 정상인 것입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c1024ca17237af64df91503164854983.png)
3. 다음 명령어를 실행하여 오류의 원인을 확인합니다.
```shellsession
sshd -t
```
아래에 표시된 ‘/var/empty/sshd must be owned by root and not group or world-writable.’과 유사한 메시지가 반환되는 경우,
이 오류는 `/var/empty/sshd/` 권한 문제로 인해 발생할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/19912fbd3406488556cf2e2937a6c2de.png)
문제 해결을 용이하게 하기 위해 `/var/log/secure` 로그에서 오류 메시지를 확인할 수도 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a696b1ce175631aebcfb92037680b506.png)
4. 다음 명령을 실행하여 `/var/empty/sshd` 디렉터리의 권한을 확인합니다.
```shellsession
ll -d /var/empty/sshd/
```
반환된 결과는 아래와 같습니다. 권한 구성은 777입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/952ac209bb81e882474f413b31bedfc1.png)
5. 다음 명령을 실행하여 `/var/empty/sshd/` 파일의 권한을 수정합니다.
```shellsession
chmod 711 /var/empty/sshd/
```
[SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)을 참고하여 테스트를 완료한 후, 원격으로 인스턴스에 로그인할 수 있습니다.


:::
::: VNC를 사용하여 Linux 시스템 시작 실패 문제 해결[](id:OSStartupFailed)

#### 오류 설명[](id:symptom)
SSH를 통해 원격으로 Linux CVM에 로그인할 수 없지만 VNC를 통해 CVM에 로그인한 후 시스템 시작 실패를 확인하고 “Welcome to emergency mode”라는 프롬프트 메시지를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/dea541a48d2a01503c1dbbc85b0d396f.png)


#### 예상 원인
`/etc/fstab`이 제대로 구성되지 않았습니다.
예를 들어 `/etc/fstab` 파일의 장치 이름을 기반으로 디스크 자동 연결을 구성했습니다. CVM이 다시 시작될 때 장치 이름이 변경되면 이 구성으로 인해 시스템이 정상적으로 시작되지 않습니다.


#### 해결 방식
`/etc/fstab` 구성 파일을 복구하려면 [처리 단계](#ProcessingSteps2)를 참고하십시오. 그 다음 CVM을 다시 시작하여 복구된 파일을 확인합니다.


#### 처리 단계[](id:ProcessingSteps2)
1. [처리 1단계](#ProcessingSteps1Step1)에 따라 VNC를 통해 Linux 인스턴스에 로그인합니다.
2. VNC 인터페이스에 진입하면 [오류 설명](#symptom)과 같은 인터페이스를 볼 수 있습니다. root 계정 암호(기본적으로 표시되지 않음)를 입력하고 **Enter**를 눌러 서버에 로그인합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7b9a8cdc6fe38ca6cb1e571790a54894.png)
3. 시스템 진입 후 다음 명령어를 실행하여 fstab 파일의 드라이브 문자 정보가 올바른지 확인합니다.
```shellsession
lsblk
```
아래 표시된 결과가 반환되면 파일의 드라이브 문자가 잘못된 것입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/be6158d53fcb6e261be719f523cacb93.png)
4. 다음 명령어를 실행하여 fstab 파일을 백업합니다.
```shellsession
cp /etc/fstab /home
```
5. 다음 명령어를 실행하여 VI 편집기를 사용하여 `/etc/fstab` 파일을 엽니다.
```shellsession
vi /etc/fstab
```
6. **i**를 눌러 편집 모드로 들어갑니다. 커서를 오류 줄의 시작 부분으로 이동하고 `#`을 입력하여 이 구성을 주석 처리합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a2d9e675d6586341e6b5e3a221ee7906.png)
7. **Esc**를 누르고 **:wq**를 입력한 다음 **Enter**를 눌러 구성을 저장하고 편집기를 종료합니다.
8. 콘솔을 통해 인스턴스를 다시 시작합니다. 자세한 내용은 [인스턴스 재시작](https://intl.cloud.tencent.com/document/product/213/4928)을 참고하십시오.
9. 정상적으로 실행 및 로그인할 수 있는지 확인합니다.


:::
::: 복구 모드를 사용하여 Linux 시스템 시작 실패 문제 해결[](id:rescueModeStartupFailed)
#### 오류 설명

Linux 시스템이 다시 시작된 후 인스턴스를 정상적으로 시작할 수 없습니다. 프롬프트 메시지에는 FAILED 시작 실패 항목이 많이 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ac026f0cbea1eab4761a8557d5078cde.png)



#### 예상 원인
다음과 같은 주요 시스템 파일. .bin 및 .lib 파일이 없습니다.


#### 해결 방식
문제 해결을 위해 콘솔을 통해 인스턴스 복구 모드로 들어가려면 [처리 단계](#ProcessingSteps3)를 참고하십시오.


#### 처리 단계[](id:ProcessingSteps3)

1. 복구 모드로 들어가기 전에 오작동의 영향을 피하기 위해 인스턴스를 백업하는 것이 좋습니다. [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755)을 통해 클라우드 디스크를 백업하고 [커스텀 미러 구축](https://intl.cloud.tencent.com/document/product/213/4942)을 통해 로컬 시스템 디스크를 백업합니다.
2. [CVM 콘솔](https://console.cloud.tencent.com/cvm/instance/index?rid=1)에 로그인합니다. ‘인스턴스’ 페이지에서 대상 인스턴스를 찾아 **더 보기** > **Ops 및 점검** > **복구 모드 진입**을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e695226792081b7cebe90507586a1d0f.png)
3. [](id:step3) ‘복구 모드 시작’ 팝업 창에서 복구 모드에서 인스턴스에 로그인하기 위한 비밀번호를 설정합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/fdceacda011b0b0678c76c6c1f2a3c56.png)
4. **복구 모드 진입**을 클릭하면 인스턴스 상태가 ‘복구 모드 진입’으로 변경되며 일반적으로 몇 분 안에 완료됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d6ed01e61aeb960da1209040c9383cc7.png)
복구 모드에 진입한 인스턴스의 상태가 빨간색 느낌표와 함께 ‘복구 모드’로 변경됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ca7c6bacd0f11471c23eb4980718f906.png)
5. [3단계](#step3)에서 설정한 'root' 계정과 비밀번호로 다음과 같이 인스턴스에 로그인합니다.
 - 인스턴스에 공용 IP가 있는 경우 [SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)을 참고하십시오.
 - 인스턴스에 공용 IP가 없는 경우 [VNC를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)을 참고하십시오.
2. 본 문서는 VNC를 통한 로그인을 예로 들어 설명합니다. 로그인에 성공하면 다음 명령을 순서대로 실행하여 시스템 디스크의 루트 파티션을 마운트합니다.
<dx-alert infotype="explain" title="">
복구 모드에서 인스턴스 시스템 디스크의 장치 이름은 vda이고 루트 파티션은 vda1이며 기본적으로 마운트 해제되어 있습니다.
</dx-alert>
```shellsession
mkdir -p /mnt/vm1
```
```shellsession
mount /dev/vda1 /mnt/vm1
```
실행 완료 후, 반환 결과는 아래와 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c48cd3e7b83abfc17cff3aedbf6dbfa2.png"/>
7. 성공적으로 마운트한 후 원본 시스템의 루트 파티션에 있는 데이터를 조작할 수 있습니다.
또한 `mount -o bind` 명령을 사용하여 원본 파일 시스템의 일부 서브 디렉터리를 마운트하고 `chroot` 명령을 사용하여 지정된 루트 디렉터리에서 명령을 실행할 수도 있습니다. 구체적인 명령은 다음과 같습니다.
```shellsession
mount -o bind /dev /mnt/vm1/dev
mount -o bind /dev/pts /mnt/vm1/dev/pts
mount -o bind /proc /mnt/vm1/proc
mount -o bind /run /mnt/vm1/run
mount -o bind /sys /mnt/vm1/sys
chroot /mnt/vm1 /bin/bash
```
`chroot` 명령을 실행할 때:
 - 오류 메시지가 없으면 `cd /` 명령을 계속 실행할 수 있습니다.
 - 아래와 같은 에러 메시지가 나타나면 루트 디렉터리를 정상적으로 전환할 수 없습니다. 이 경우 `cd /mnt/vm1`을 실행하여 루트 파티션 데이터를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/12e2bccf5c19edb4d248ac26d257c31e.png)
8. 명령을 통해 원래 시스템 루트 파티션의 `/usr/bin` 디렉터리에 있는 모든 파일이 삭제되었는지 확인할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0f2820f10b457378d26c9a6efaf14966.png)
9. 이 경우 동일한 운영체제를 사용하여 일반 인스턴스를 생성하고, 다음 명령어를 실행하여 정상 시스템의 `/usr/bin` 디렉터리에 있는 파일을 압축하여 비정상 인스턴스에 원격으로 복사할 수 있습니다.
 - 일반 인스턴스의 경우 다음 명령을 순서대로 실행합니다.
```shellsession
cd /usr/bin/ && tar -zcvf bin.tar.gz *
```
```shellsession
scp bin.tar.gz root@비정상 인스턴스ip:/mnt/vm1/usr/bin/
```
<dx-alert infotype="explain" title="">
인스턴스에 공인 IP가 있는 경우 공중망을 통해 복사를 수행할 수 있습니다. 그렇지 않으면 사설망을 통해 복사가 수행됩니다.
</dx-alert>
실행 결과는 다음 이미지와 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/937f1d97edda8a2b2786b856750dfb5e.png"/>
  - 비정상 인스턴스의 경우 복구 모드에서 다음 명령을 순서대로 실행하십시오.
```shellsession
cd /mnt/vm1/usr/bin/
```
```shellsession
tar -zxvf bin.tar.gz
```
```shellsession
chroot /mnt/vm1 /bin/bash
```
실행 결과는 다음 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/90e4c3d4c06806f07401ec01863dcdfa.png)
10. 인스턴스를 복구한 후 대상 인스턴스의 작업 열에서 **더 보기** > **Ops 및 점검** > **복구 모드 종료**를 선택합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d9f8f26b745a654cb145bbfc4bb1cd2a.png)
11. 복구 모드를 종료한 후 인스턴스는 종료 상태가 됩니다. 인스턴스를 시작하여 시스템을 확인하십시오. 아래와 같이 시스템이 복구됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/705c27323e74f424b775f88567d7252c.png)






:::
</dx-accordion>



