## 작업 시나리오

본 문서는 Windows Server 2012 운영 체제를 예로, Windows 이미지를 만드는 방법을 안내합니다.

## 작업 순서

### 준비 과정

시스템 디스크의 이미지를 만든 후 내보낼 때 아래의 검사를 진행해야 합니다.
> 데이터 디스크를 통해 이미지를 내보내는 경우에는 이 작업을 건너뛸 수 있습니다.
>
#### OS 파티션 및 시작 모드 검사

1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> 클릭 후, Windows PowerShell 창을 엽니다.
2. Windows PowerShell 창에서 **diskmgmt.msc**를 입력하고, **Enter**를 눌러 "디스크 관리"를 엽니다.
3. 확인이 필요한 디스크 > [속성]을 마우스 우클릭하고, [볼륨] 탭을 선택하여 디스크 파티션 형식을 확인합니다.
2. 디스크 파티션 형식이 GPT 파티션인지 확인합니다.
 - GPT 파티션이라면, 서비스 마이그레이션이 아직 GPT 파티션을 지원하지 않기 때문에 [Submit Ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1)을 통해 피드백 바랍니다.
 - GPT 파티션이 아니라면, 다음 단계를 실행합니다.
3. 관리자 권한으로 CMD를 열고, 다음 명령어를 실행하여 운영 체제가 EFI 모드로 시작되는지 확인합니다.
```
bcdedit /enum {current}
```
아래의 출력 결과를 예로 듭니다.
```
Windows 시작 로더
식별자                  {current}
device                  partition=C:
path                    \WINDOWS\system32\winload.exe
description             Windows 10
locale                  zh-CN
inherit                 {bootloadersettings}
recoverysequence        {f9dbeba1-1935-11e8-88dd-ff37cca2625c}
displaymessageoverride  Recovery
recoveryenabled         Yes
flightsigning           Yes
allowedinmemorysettings 0x15000075
osdevice                partition=C:
systemroot              \WINDOWS
resumeobject            {1bcd0c6f-1935-11e8-8d3e-3464a915af28}
nx                      OptIn
bootmenupolicy          Standard
```
 - 'path' 매개변수에 efi가 포함되었다면, 현재 운영 체제가 EFI 모드에서 시작된 것이므로 [Submit Ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1)을 통해 피드백 바랍니다.
 - ‘path’ 매개변수에 efi가 포함되지 않았다면, 다음 단계를 실행합니다.

#### 소프트웨어 삭제

충돌이 발생하는 드라이버와 소프트웨어를 삭제합니다(VMware tools, Xen tools, Virtualbox GuestAdditions 및 하위 드라이버가 기본 포함된 일부 소프트웨어 포함).

#### cloud-base 설치

설치에 대한 자세한 내용은 [cloud-base 설치 문서](https://intl.cloud.tencent.com/document/product/213/32364)를 참조 바랍니다.

#### Virtio 드라이버 검사 또는 설치

1. [제어판] > [프로그램 및 기능]을 연 다음, 검색창에 Virtio를 검색합니다.
 - 출력 결과가 아래 이미지와 같으면 Virtio 드라이버가 설치되었음을 의미합니다.
![image](https://main.qcloudimg.com/raw/87808940ddd5317dd8c67a699e3dc5c0.png)
 - Virtio 드라이버가 미설치 상태라면 수동으로 설치해야 합니다.
    - Microsoft Windows Server 2012 R2(표준 버전)의 경우, [Tencent Cloud 사용자 정의 에디션 Virtio](http://windowsvirtio-10016717.file.myqcloud.com/InstallQCloud.exe?_ga=1.44298212.1367540472.1504757536)를 다운로드합니다.
    - 기타 시스템 버전은 [커뮤니티 에디션 virtio](https://www.linux-kvm.org/page/WindowsGuestDrivers/Download_Drivers)를 다운로드합니다.

#### 기타 하드웨어 관련 구성 확인

클라우드 업로드 이후의 하드웨어는 다음의 변화가 포함되지만, 이에 국한되지는 않습니다.
 - 그래픽 카드가 Cirrus VGA로 교체됩니다.
 - 디스크가 Virtio Disk로 교체됩니다.
 - ENI가 Virtio Nic로 교체되며, 로컬 연결되도록 기본 설정되어 있습니다.

### 이미지 내보내기

실제 수요에 따라 각각의 이미지 내보내기 툴을 선택합니다.
- [플랫폼 툴을 사용해 이미지 내보내기](#Useplatform)
- [disk2vhd를 사용해 이미지 내보내기](#Usedisk2vhd)

<span id="Useplatform"></span>
#### 플랫폼 툴을 사용해 이미지 내보내기

VMWare vCenter Convert 혹은 Citrix XenConvert 등과 같은 가상화 플랫폼의 이미지 내보내기 툴을 사용합니다. 자세한 내용은 각 플랫폼의 내보내기 툴 문서를 참조 바랍니다.
> 현재 Tencent Cloud 마이그레이션에서 지원하는 이미지 형식은 qcow2, vhd, raw, vmdk입니다.
>

<span id="Usedisk2vhd"></span>
#### disk2vhd를 사용해 이미지 내보내기

물리적 기기의 시스템을 내보내야 하거나 플랫폼 툴을 사용하지 않고 내보내려면, disk2vhd 툴을 사용해 내보낼 수 있습니다.
1. disk2vhd 툴을 설치하고 엽니다.
[disk2vhd 툴 다운로드 클릭하기>>](https://download.sysinternals.com/files/Disk2vhd.zip)
3. 아래 이미지와 같이 내보낼 이미지의 저장 경로를 선택하고, 복사할 볼륨을 선택한 다음 [Create]를 클릭합니다.
> 
> - Disk2vhd는 Windows 시스템에 VSS(Volume Shadow Copy Service)가 설치된 후에 시작할 수 있습니다.  VSS 기능에 대한 자세한 내용은 [Volume Shadow Copy Service] (https://docs.microsoft.com/en-us/windows/win32/vss/volume-shadow-copy-service-portal?redirectedfrom=MSDN)를 참고하
>- 현재 시스템은 vhdx 형식의 이미지를 지원하지 않으므로 "Use Vhdx"를 선택하지 마시기를 바랍니다.
>- "Use volume Shadow Copy"를 선택해 볼륨 섀도 복사 기능을 사용할 경우, 데이터의 완전성을 더 확보할 수 있습니다.
> 
![image](https://main.qcloudimg.com/raw/68d9c4e5e7db49c4cefdd3785ce9b68d.jpg)

### 이미지 확인

> 서비스를 중지하지 않고 바로 이미지를 만들거나 다른 원인으로, 만든 이미지의 파일 시스템에 오류가 있을 수 있으므로 이미지를 만든 후에 오류가 없는지 확인하시기 바랍니다.
>
이미지 형식이 현재 플랫폼에서 지원하는 형식과 일치할 경우 이미지를 열어 파일 시스템을 바로 확인할 수 있습니다. 예시, Windows 플랫폼은 vhd 형식의 이미지를 직접 첨부할 수 있습니다. Linux 플랫폼은 qemu-nbd를 사용해 qcow2 형식의 이미지를 열 수 있습니다. Xen 플랫폼은 vhd 파일을 직접 사용할 수 있습니다.
Linux 플랫폼을 예로 듭니다.
```
modprobe nbd
qemu-nbd -c /dev/nbd0 xxxx.qcow2
mount /dev/nbd0p1 /mnt
```
qcow2 이미지의 첫 번째 파티션을 내보내면 파일 시스템이 손상되며, mount 시 오류가 발생합니다.
또한, 이미지를 업로드하기 전에 먼저 CVM을 시작하여 이미지 파일의 사용 가능 여부를 테스트할 수 있습니다.
