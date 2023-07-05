## 작업 시나리오
본문은 CentOS 8.2 및 CentOS 7.9 운영 체제의 Tencent Cloud Virtual Machine(CVM)을 예시로, CentOS 시각화 인터페이스를 구축하는 방법을 소개합니다.

## 관련 설명
- 성능 및 범용성을 고려하여 Tencent Cloud에서 제공하는 Linux 공용 이미지는 기본적으로 그래픽 모듈을 설치하지 않습니다.
- 설치 오류로 인해 인스턴스가 정상적으로 실행되지 않을 수 있으므로, [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942), [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755)을 통해 데이터를 백업할 것을 권장합니다.

## 작업 순서
실제로 사용하는 CVM 운영 체제에 따라 다음 단계를 참고하십시오.
<dx-tabs>
::: CentOS\s8.2
1. 인스턴스에 로그인합니다. 자세한 내용은 [Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참고하십시오.
2. 다음 명령을 실행하여 그래픽 인터페이스 모듈을 설치합니다.
```
yum groupinstall "Server with GUI" -y
```
3. 다음 명령을 실행하여 그래픽 인터페이스 기본 실행을 설정합니다.
```
systemctl set-default graphical
```
4. 아래의 명령을 실행하여 인스턴스를 재시작합니다.
```
reboot
```
5. VNC 방식으로 인스턴스에 로그인합니다. 자세한 내용은 [VNC를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)을 참고하십시오.
인스턴스에 로그인한 후 시각화 인터페이스가 나타나면 구축이 완료된 것입니다. 인터페이스 안내에 따라 구성을 진행하고, 바탕 화면으로 이동하여 필요에 따라 관련 작업을 수행할 수 있습니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/58e12a33b38e0114f5b3116b31f7b026.png)
:::
::: CentOS\s7.9
1. 인스턴스에 로그인합니다. 자세한 내용은 [Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참고하십시오.
2. 다음 명령을 실행하여 그래픽 인터페이스 모듈을 설치합니다.
```
yum groupinstall "GNOME Desktop" "Graphical Administration Tools" -y
```
3. 다음 명령을 실행하여 그래픽 인터페이스 기본 실행을 설정합니다.
```
ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target
```
4. 아래의 명령을 실행하여 인스턴스를 재시작합니다.
```
reboot
```
5. VNC 방식으로 인스턴스에 로그인합니다. 자세한 내용은 [VNC를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)을 참고하십시오.
인스턴스에 로그인한 후 시각화 인터페이스가 나타나면 구축이 완료된 것입니다. 인터페이스 안내에 따라 구성을 진행하고, 바탕 화면으로 이동하여 필요에 따라 관련 작업을 수행할 수 있습니다. 아래 이미지를 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/246952ae60c02724727029b6a3c0ef1a.png)
:::
</dx-tabs>
