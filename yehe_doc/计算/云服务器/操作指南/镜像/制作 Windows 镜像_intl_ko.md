## 작업 시나리오
본 문서는 Windows Server 2012 운영 체제의 Windows 이미지 생성 방법을 예시로 소개합니다. 다른 버전의 Windows Server 운영 체제를 사용하셔도 본 문서를 참고하여 이미지를 생성할 수 있습니다.

## 작업 순서

### 준비 작업

생성한 시스템 디스크의 이미지를 내보낼 때 다음과 같은 검사를 진행해야 합니다.
>? 데이터 디스크를 통해 이미지를 내보내는 경우 이 작업을 건너뛸 수 있습니다.
>

#### OS 파티션 및 실행 모드 검사

1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;">를 클릭하여, Windows PowerShell 창을 여십시오.
2. Windows PowerShell 창에서 **diskmgmt.msc**를 입력한 후, **Enter**를 눌러 "디스크 관리"를 여십시오.
3. 검사가 필요한 디스크 > [속성]을 마우스 우클릭하고, [볼륨] 탭을 선택하여 디스크 파티션 형식을 확인하십시오.
2. 디스크 파티션 형식이 GPT 파티션인지 확인합니다.
 - GPT 파티션인 경우 현재 서비스 마이그레이션을 지원하지 않습니다. [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1)을 통해 피드백해주십시오.
 - GPT 파티션이 아닌 경우 다음 단계를 실행합니다.
3. 관리자 권한으로 CMD를 연 후, 다음 명령어를 실행하여 운영 체제가 EFI 모드로 실행되는지 확인합니다.
```
bcdedit /enum {current}
```
다음은 반환 결과 예시입니다.
```
Windows 실행 로더
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
 - `path` 매개변수에 efi가 포함되어 있다면 운영 체제가 EFI 모드로 실행된 것을 의미합니다. [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1)을 통해 피드백해주십시오.
 - `path`매개변수에 efi가 포함되어 있지 않다면 다음 단계를 실행하십시오.

#### 소프트웨어 언마운트

충돌이 발생하는 드라이버와 소프트웨어를 언마운트하십시오(VMware tools, Xen tools, Virtualbox GuestAdditions 및 일부 LLD의 소프트웨어 포함).

#### cloud-base 설치

설치에 대한 자세한 내용은 [cloud-base 설치 문서](https://intl.cloud.tencent.com/document/product/213/32364)를 참조하십시오.

#### Virtio 드라이버 검사 또는 설치

1. [제어판] > [프로그램 및 기능]을 연 다음, 검색창에 Virtio를 검색하십시오.
 - 반환 결과가 다음 이미지와 같다면 Virtio 드라이버가 설치되었음을 의미합니다.
![](https://main.qcloudimg.com/raw/ff1dffb01a7f77d515061bce184e033b.png)
 - Virtio 드라이버가 미설치 상태라면 수동으로 설치해야 합니다.
    - Microsoft Windows Server 2008 R2(스탠다드 버전, 데이터센터 버전, 엔터프라이즈 버전), Microsoft Windows Server 2012 R2(스탠다드 버전), Microsoft Windows Server 2016(데이터센터 버전), Microsoft Windows Server 2019(데이터센터 버전)에서는 Tencent Cloud 사용자 정의 버전 Virtio를 다운로드하십시오. 다운로드 주소는 다음과 같습니다. 실제 네트워크 환경에 맞춰 다운로드하십시오.
      - 공용 네트워크 다운로드 주소: `http://mirrors.tencent.com/install/windows/virtio_64_1.0.9.exe`
      - 내부 네트워크 다운로드 주소: `http://mirrors.tencentyun.com/install/windows/virtio_64_1.0.9.exe`
    - 기타 시스템 버전은 [커뮤니티 버전 virtio](https://www.linux-kvm.org/page/WindowsGuestDrivers/Download_Drivers)를 다운로드하십시오.

#### 기타 하드웨어 관련 설정 검사

클라우드 업로드 이후 하드웨어는 다음과 같이 변하지만, 이에 국한되지는 않습니다.
 - 그래픽 카드가 Cirrus VGA로 교체됩니다.
 - 디스크가 Virtio Disk로 교체됩니다.
 - ENI가 Virtio Nic로 교체되며, 기본적으로 로컬 연결됩니다.

### 이미지 내보내기
실제 필요에 맞는 이미지 내보내기 툴을 선택합니다.
<dx-tabs>
::: 플랫폼 툴로 이미지 내보내기[](id:Useplatform)
VMWare vCenter Convert 혹은 Citrix XenConvert 등과 같은 가상화 플랫폼의 이미지 내보내기 툴을 사용합니다. 자세한 내용은 각 플랫폼의 내보내기 툴 문서를 참조하십시오.
>? 현재 Tencent Cloud의 서비스 마이그레이션이 지원하는 이미지 포맷은 qcow2, vhd, raw, vmdk입니다.
>
:::
::: \sdisk2vhd\s로 이미지 내보내기[](id:Usedisk2vhd)
물리 머신의 시스템을 내보내거나 플랫폼 툴을 사용하지 않을 경우, disk2vhd 툴을 사용하여 내보낼 수 있습니다.
1. disk2vhd 툴을 설치하고 여십시오.
[disk2vhd 툴 다운로드 클릭하기>>](https://download.sysinternals.com/files/Disk2vhd.zip)
3. 다음 이미지와 같이 내보낼 이미지의 저장 경로를 선택하고, 복사할 볼륨을 선택한 다음 [Create]를 클릭합니다.
>! 
> - disk2vhd 실행을 위해 Windows의 VSS(볼륨 섀도 복사 서비스) 기능을 사전에 설치해야 합니다. VSS 기능에 대한 자세한 정보는 [Volume Shadow Copy Service](https://docs.microsoft.com/zh-cn/windows/win32/vss/volume-shadow-copy-service-portal?redirectedfrom=MSDN)를 참조하십시오.
> - 현재 시스템은 vhdx 포맷의 이미지를 지원하지 않으므로 "Use Vhdx"를 선택하지 마십시오.
> - 데이터의 완전성을 보장하기 위해 "Use volume Shadow Copy"를 선택하여 볼륨 섀도 복사 기능을 사용하는 것이 좋습니다.
> 
![image](https://main.qcloudimg.com/raw/68d9c4e5e7db49c4cefdd3785ce9b68d.jpg)
:::
</dx-tabs>


### 이미지 검사

>? 서비스를 중지하지 않은 채로 이미지를 생성했거나 혹은 다른 원인으로 인해 생성한 이미지 파일 시스템에 오류가 있을 수 있습니다. 따라서 이미지를 생성한 후 오류를 검사하는 것이 좋습니다.
>
이미지 포맷과 플랫폼이 지원하는 형식이 일치할 경우 이미지를 직접 열어 파일 시스템을 검사할 수 있습니다. 예를 들어 Windows 플랫폼은 vhd 포맷의 이미지를 직접 추가할 수 있고, Linux 플랫폼은 qemu-nbd로 qcow2 포맷의 이미지를 열 수 있습니다. Xen 플랫폼은 vhd 파일을 직접 활성화할 수 있습니다.

본 문서는 Windows 플랫폼을 예시로 들고 있어, '디스크 관리'의 'VHD 추가'를 통해 vhd 포맷의 이미지를 확인합니다. 절차는 다음과 같습니다.
1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-4px 0px">를 마우스 우클릭하여 팝업된 메뉴에서 [컴퓨터 관리]를 선택합니다.
2. [스토리지]> [디스크 관리]를 선택해 [디스크 관리] 인터페이스로 이동합니다.
3. 다음 이미지와 같이 실행창 상단의 [작업]>[VHD 추가]를 선택합니다.
![](https://main.qcloudimg.com/raw/90a6ce24b78ca128ade5018833011708.png)
다음 이미지와 같은 결과가 나오면 이미지가 생성되었다는 의미입니다.
![](https://main.qcloudimg.com/raw/41eac48fe77d3773dcf1ac9121b251ce.png)
