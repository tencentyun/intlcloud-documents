## 작업 시나리오
본 문서는 Windows Server 2012 운영 체제의 Windows 이미지 생성 방법을 예시로 소개합니다. 다른 버전의 Windows Server 운영 체제를 사용하셔도 본 문서를 참고하여 이미지를 생성할 수 있습니다.

## 작업 단계

### 준비 과정

시스템 디스크의 이미지를 제작 후 내보내기 할 경우 다음을 확인해야 합니다.
<dx-alert infotype="explain" title="">
데이터 디스크를 통해 이미지를 내보내는 경우에는 이 작업을 건너뛸 수 있습니다.
</dx-alert>



#### OS 파티션 및 실행 모드 확인

1. 운영 체제 인터페이스에서 <img src='https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png' style='margin: 0;'> 클릭 후, Windows PowerShell 창을 엽니다.
2. Windows PowerShell 창에서 **diskmgmt.msc**를 입력한 후, **Enter**를 눌러 '디스크 관리'를 엽니다.
3. 확인이 필요한 디스크 > **속성**을 우클릭하고, **볼륨** 탭을 선택하여 디스크 파티션 형식을 조회합니다.
2. 디스크 파티션 형식이 GPT 파티션인지 판단합니다.
 - GPT 파티션인 경우, 서비스 마이그레이션이 GPT 파티션을 지원하지 않으므로 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)을 통해 피드백을 보내주십시오.
 - GPT 파티션이 아닌 경우, 다음 단계를 실행하십시오.
3. 관리자 권한으로 CMD를 연 후, 다음 명령어를 실행하여 운영 체제가 EFI 방식으로 시작이 되는지 확인합니다.
```shellsession
bcdedit /enum {current}
```
다음은 반환 결과 예시입니다.
```shellsession
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
 - `path` 매개변수에 efi가 포함된 경우, 현재 운영 체제가 EFI 방식으로 실행됨을 의미합니다. [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)을 통해 피드백을 보내주십시오.
 - 만약 ‘path’ 매개변수에 efi가 포함되지 않은 경우, 다음 단계를 실행하십시오.

#### 소프트웨어 언마운트

충돌이 발생하는 드라이버와 소프트웨어를 언마운트 합니다(VMware tools, Xen tools, Virtualbox GuestAdditions 및 일부 기본 탑재된 드라이버 소프트웨어 포함).

#### cloud-base 설치

설치에 대한 자세한 내용은 [cloud-base 설치 문서](https://intl.cloud.tencent.com/document/product/213/32364)를 참고하십시오.

#### Virtio 드라이버 확인 또는 설치

**제어판** > **프로그램 및 기능**을 클릭하고 검색 상자에 Virtio를 입력합니다.
- 만약 반환 결과가 아래와 같으면 Virtio 드라이버가 설치된 것입니다.
![](https://main.qcloudimg.com/raw/ff1dffb01a7f77d515061bce184e033b.png)
- Virtio 드라이버가 설치되어 있지 않으면 수동으로 설치해야 합니다. 실제 상황에 따라 다운로드 버전을 선택하십시오.
<dx-alert infotype="explain" title="">
- Tencent Cloud는 Windows Server 2003 가져오기를 지원하지 않습니다.
- Windows Server 2008R2/2012R2/2016/2019/2022를 사용하는 경우 Tencent Cloud 커스텀 에디션 VirtIO 드라이버를 설치하십시오.
- 다른 버전의 Windows 운영 체제를 사용하는 경우 VirtIO 드라이버의 Tencent Cloud 커스텀 에디션을 설치하여 사용해 보시고 불안정한 경우 VirtIO 드라이버의 커뮤니티 에디션을 사용해 볼 수 있습니다.
</dx-alert>
<dx-tabs>
::: (권장) Tencent Cloud 커스텀 에디션 설치
Virtio의 Tencent Cloud 커스텀 에디션의 다운로드 주소는 다음과 같습니다. 실제 네트워크 환경에 따라 다운로드하십시오.
-  공용 네트워크 다운로드 주소: `http://mirrors.tencent.com/install/windows/virtio_64_1.0.9.exe`
-  내부 네트워크 다운로드 주소: `http://mirrors.tencentyun.com/install/windows/virtio_64_1.0.9.exe`
:::
::: 커뮤니티 에디션 설치
VirtIO 드라이버의 Tencent Cloud 커스텀 에디션을 설치하여 사용해 보십시오. 불안정한 경우 VirtIO 드라이버의 커뮤니티 에디션을 사용해 볼 수 있습니다.
[커뮤니티 에디션 virtio 다운로드](https://www.linux-kvm.org/page/WindowsGuestDrivers/Download_Drivers)
:::
</dx-tabs>


#### 기타 하드웨어 관련 구성 확인

클라우드 업로드 이후의 하드웨어는 다음의 변화가 포함되지만, 이에 국한되지는 않습니다.
 - 그래픽 카드가 Cirrus VGA로 교체됩니다.
 - 디스크가 Virtio Disk로 교체됩니다.
 - 네트워크 카드가 Virtio Nic로 교체되며, 기본값으로 로컬 연결이 됩니다.

### 이미지 내보내기
실제 필요에 맞는 이미지 내보내기 툴을 선택합니다.
<dx-tabs>
::: 플랫폼 툴로 이미지 내보내기[](id:Useplatform)
VMWare vCenter Convert 혹은 Citrix XenConvert 등과 같은 버츄얼 플랫폼의 이미지 내보내기 툴을 사용하십시오. 자세한 내용은 각 플랫폼의 내보내기 툴 문서를 참고하십시오.


<dx-alert infotype="explain" title="">
현재 Tencent Cloud 서비스에서 마이그레이션을 지원하는 이미지 형식에는 qcow2, vhd, raw, vmdk가 있습니다.
</dx-alert>


:::
::: \sdisk2vhd\s로 이미지 내보내기[](id:Usedisk2vhd)
머신의 시스템을 내보내야 하거나 플랫폼 툴을 사용하지 않고 내보내기를 하려는 경우, disk2vhd 툴을 사용해 내보낼 수 있습니다.
1. disk2vhd 툴을 [다운로드](https://download.sysinternals.com/files/Disk2vhd.zip)합니다.
2. disk2vhd 툴을 설치하고 실행합니다.
<dx-alert infotype="notice" title="">
 - 시스템 디스크가 아닌 디스크에 disk2vhd 툴을 설치하고 실행하십시오.
 - disk2vhd 실행을 위해 Windows의 VSS(볼륨 섀도 복사 서비스) 기능을 사전에 설치해야 합니다. VSS 기능에 대한 자세한 내용은 [Volume Shadow Copy Service](https://docs.microsoft.com/zh-cn/windows/win32/vss/volume-shadow-copy-service-portal?redirectedfrom=MSDN)를 참고하십시오.
</dx-alert>
3. 열려 있는 disk2vhd 툴에서 다음 정보에 따라 구성하고 **Create**를 클릭하여 이미지를 내보냅니다.
 - **Use Vhdx**: 선택하지 마십시오. 현재 시스템은 vhdx 형식의 이미지를 지원하지 않습니다.
 - **Use volume Shadow Copy**: 선택하지 마십시오. 볼륨 섀도 복사 기능을 사용하면 데이터의 완전성이 더 확보될 수 있습니다.
 - **VHD File name**: 생성된 .vhd 파일의 저장 위치입니다. 시스템 디스크가 아닌 디스크를 선택하십시오.
 - **Volume to include**: 이미지를 내보내기를 하려면 전체 시스템 디스크를 내보내야 합니다. **시스템 디스크의 모든 파티션을 선택하십시오**. 그렇지 않으면 Import Image 시 시스템에 들어갈 수 없다는 오류가 발생합니다.
시스템 디스크 파티션은 일반적으로 C:\ 파티션과 이전 부트 파티션 및 recovery 파티션으로, 숫자는 일반적으로 2 - 3개이며 모두 선택해야 합니다.
**구성 예시**
아래 그림과 같이 E 디스크에서 disk2vhd 툴을 실행한 후 시스템 디스크의 모든 파티션(부트 파티션 및 C:\ 파티션 실행), ‘Use volume Shadow Copy’를 선택하고 ‘Use Vhdx’ 선택을 취소합니다. 이미지를 내보낸 후 생성된 .vhd 파일은 E 디스크에 저장됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1e990f879e3920426abaa355f6d3adc1.png)


:::
</dx-tabs>


### 이미지 형식 변환(옵션)
[이미지 형식 변환](https://intl.cloud.tencent.com/document/product/213/46192)을 참고하여 'qemu-img'를 사용하여 이미지 파일을 지원되는 형식으로 변환합니다.

### 이미지 확인

<dx-alert infotype="explain" title="">
서비스를 중지하지 않고 바로 이미지를 생성했거나 다른 원인으로 인해 생성한 이미지 파일 시스템에 오류가 있을 수 있으므로 이미지를 생성한 후에 오류가 없는지 확인하십시오.
</dx-alert>


이미지 형식이 현재 플랫폼에서 지원하는 형식과 일치할 경우 이미지를 열어 파일 시스템을 직접 확인할 수 있습니다. 예를 들어, Windows 플랫폼은 vhd 형식의 이미지를 직접 첨부할 수 있습니다. Linux 플랫폼은 qemu-nbd를 사용해 qcow2 형식의 이미지를 열 수 있으며, Xen 플랫폼은 vhd 파일을 직접 사용할 수 있습니다.

본 문서는 Windows 플랫폼을 예시로, '디스크 관리'의 'VHD 추가'를 통해 vhd 포맷의 이미지를 확인합니다. 절차는 다음과 같습니다.
1. 운영 체제 인터페이스에서 <img src='https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png' style='margin:-4px 0px'>를 우클릭하여 팝업된 메뉴에서 **컴퓨터 관리**를 선택합니다.
2. **스토리지** > **디스크 관리**를 선택하여 디스크 관리 인터페이스로 이동합니다.
3. 창 상단에서 **작업** > **VHD 추가**를 아래 이미지와 같이 선택합니다.
![](https://main.qcloudimg.com/raw/90a6ce24b78ca128ade5018833011708.png)
다음 이미지와 같은 결과가 나오면 이미지가 생성되었다는 의미입니다.
![](https://main.qcloudimg.com/raw/41eac48fe77d3773dcf1ac9121b251ce.png)
