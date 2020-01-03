## 작업 시나리오

본 문서는 Windows Server 2012 운영 체제를 예로 들어, Windows 미러 이미지 제작 방법을 안내합니다.

## 작업 순서

### 준비 과정

시스템 디스크의 미러 이미지를 제작 후 내보내기 할 경우 아래의 검사를 진행해야 합니다.
> 만약 데이터 디스크를 통해 미러 이미지를 내보내기 하는 경우 이 작업을 건너뛸 수 있습니다.
>
#### OS 파티션 및 시작 모드 검사

1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> 클릭 후, Windows PowerShell 창을 여십시오.
2. Windows PowerShell 창에서 **diskmgmt.msc**를 입력한 후, **Enter**를 눌러 "디스크 관리"를 여십시오.
3. 검사가 필요한 디스크 > [속성] 마우스 우클릭, [볼륨] 탭을 선택하여 디스크 파티션 형식을 검사하십시오.
2. 디스크 파티션 형식이 GPT 파티션 여부를 판단하십시오.
 - GPT 파티션인 경우, 서비스 마이그레이션은 GPT 파티션을 지원하지 않으므로 티켓을 제출하여 피드백을 요청하십시오.
 - GPT 파티션이 아닌 경우, 다음 단계를 실행하십시오.
3. 관리자 권한으로 CMD를 연 후, 다음 커맨드를 실행하여 운영 체제가 EFI 방식으로 시작이 되는지 확인합니다.
```
bcdedit /enum {current}
```
아래의 리턴 결과를 예로 합니다.
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
 - 만약 'path' 파라미터에 efi가 포함된 경우, 현재 운영 체제가 EFI 방식에서 시작된 것입니다. [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6andlevel2_id=7andsource=0anddata_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVMandstep=1)로 피드백을 요청하십시오.
 - 만약 ‘path’ 파라미터에 efi가 포함되지 않은 경우, 다음 단계를 실행하십시오.

#### 소프트웨어 언마운트

충돌이 발생하는 드라이버와 소프트웨어를 언마운트 하십시오(VMware tools, Xen tools, Virtualbox GuestAdditions 및 기본 탑재된 드라이버의 소프트웨어 일부 포함).

#### cloud-base 설치

설치에 대한 자세한 내용은 [cloud-base 설치 문서](https://intl.cloud.tencent.com/document/product/213/32364)를 참조하십시오.

#### Virtio 드라이버 검사 또는 설치

1. [제어판] > [프로그램 및 기능]을 연 다음, 검색창에 Virtio를 검색하십시오.
 - 만약 리턴 결과가 아래와 같으면 Virtio 드라이버가 설치된 것입니다.
 - 만약 Virtio 드라이버가 미설치 상태라면 수동으로 설치해야 합니다.
    - Microsoft Windows Server 2008 R2(스탠다드 에디션, 데이터센터 에디션, 엔터프라이즈 에디션), Microsoft Windows Server 2012 R2(스탠다드 에디션)의 경우, [Tencent Cloud 사용자 정의 에디션 Virtio](http://windowsvirtio-10016717.file.myqcloud.com/InstallQCloud.exe?_ga=1.44298212.1367540472.1504757536)를 다운로드하십시오
    - 기타 시스템 에디션의 경우, [커뮤니티 에디션 virtio](https://www.linux-kvm.org/page/WindowsGuestDrivers/Download_Drivers)를 다운로드하십시오.

#### 기타 하드웨어 관련 구성 검사

클라우드 업로드 이후의 하드웨어는 다음의 변화가 포함되지만, 이에 국한되지는 않습니다.
 - 그래픽 카드가 Cirrus VGA로 교체됩니다.
 - 디스크가 Virtio Disk로 교체됩니다.
 - 네트워크 카드가 Virtio Nic로 교체되며, 기본값으로 로컬 연결이 됩니다.

### 미러 이미지 내보내기

실제 수요에 따라 각각의 미러 이미지 내보내기 툴을 선택합니다.
- [플랫폼 툴을 사용해 미러 이미지 내보내기](#Useplatform)
- [disk2vhd를 사용해 미러 이미지 내보내기](#Usedisk2vhd)

<span id="Useplatform"></span>
#### 플랫폼 툴을 사용해 미러 이미지 내보내기

VMWare vCenter Convert 혹은 Citrix XenConvert 등과 같은 버츄얼 플랫폼의 미러 이미지 내보내기 툴을 사용하십시오. 자세한 내용은 각 플랫폼의 내보내기 툴 문서를 참조하십시오.
> 현재 Tencent Cloud 마이그레이션에서 지원하는 미러 이미지 형식은 qcow2, vhd, raw, vmdk입니다.
>

<span id="Usedisk2vhd"></span>
#### disk2vhd를 사용해 미러 이미지 내보내기

머신의 시스템을 내보내야 하거나 플랫폼 툴을 사용하지 않고 내보내기를 하려는 경우, disk2vhd 툴을 사용해 내보낼 수 있습니다.
1. disk2vhd 툴을 설치하고 여십시오.
[disk2vhd 툴 다운로드 클릭하기>>](https://download.sysinternals.com/files/Disk2vhd.zip)
3. 내보내기할 미러 이미지의 저장 경로를 선택한 후, 복사할 볼륨을 선택한 다음 아래와 같이 [Create]를 클릭하십시오.
> 
>- disk2vhd 실행을 위해 Windows의 VSS(볼륨 섀도 복사 서비스) 기능을 사전에 설치해야 합니다.
>- 현재 시스템은 vhdx 형식의 미러 이미지를 지원하지 않으므로 "Use Vhdx"를 선택하지 마십시오.
>- "Use volume Shadow Copy"를 선택해 볼륨 섀도 복사 기능을 사용할 경우, 데이터의 완전성이 더 확보될 수 있습니다.
> 
![image](https://main.qcloudimg.com/raw/68d9c4e5e7db49c4cefdd3785ce9b68d.jpg)

### 미러 이미지 검사

> 서비스를 정지하지 않고 직접 미러 이미지를 제작하거나 또는 다른 이유로 인해 제작된 미러 이미지의 파일 시스템에 잘못될 수 있으므로 미러 이미지 제작 후 오류 여부를 검사할 것을 권장합니다.
>
미러 이미지 형식이 현재 플랫폼에서 지원하는 형식과 일치할 경우 미러 이미지를 열어 파일 시스템을 직접 검사할 수 있습니다. 예를 들어, Windows 플랫폼은 vhd 형식의 미러 이미지를 직접 첨부할 수 있습니다. Linux 플랫폼은 qemu-nbd를 사용해 qcow2 형식의 미러 이미지를 열 수 있으며, Xen 플랫폼은 vhd 파일을 직접 사용할 수 있습니다.
Linux 플랫폼을 예로 합니다.
```
modprobe nbd
qemu-nbd -c /dev/nbd0 xxxx.qcow2
mount /dev/nbd0p1 /mnt
```
만약 qcow2 미러 이미지의 첫 번째 파티션을 내보내기 할 경우, 파일 시스템이 손상되며 mount 시 오류가 보고됩니다.
또한, 미러 이미지를 업로드하기 전에 먼저 클라우드 서버를 시작해 미러 이미지 파일의 사용 가능 여부를 테스트할 수 있습니다.
