Tencent Cloud는 [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942) 기능 외에 가져오기 기능도 지원합니다. 로컬 또는 기타 플랫폼의 서버 시스템 디스크에 있는 이미지 파일을 CVM(Cloud Virtual Machine)의 사용자 정의 이미지로 가져올 수 있으며, 가져온 이미지를 사용해 CVM을 생성하거나 기존 CVM의 시스템을 재설치할 수 있습니다.

<span id="가져오기 준비"></span>
## 가져오기 준비

가져오기 조건에 부합하는 이미지 파일을 미리 준비해야 합니다.
- **Linux 시스템 유형의 이미지 제한:**
<table>
<tr><th>이미지 속성</th><th>조건</th></tr>
<tr><td>운영 체제</td><td><ul><li>CentOS, Ubuntu, Debian, CoreOS, openSUSE, SUSE 릴리스 버전 기반의 이미지</li><li>32비트와 64비트 지원</li></ul></td></tr>
<tr><td>이미지 형식</td><td><ul><li>RAW, VHD, QCOW2, VMDK 이미지 형식 지원</li><li><code>qemu-img info imageName &#124; grep 'file format'</code>을 통해 이미지 형식 조회</li></ul></td></tr>
<tr><td>이미지 크기</td><td><ul><li>이미지의 실제 크기가 50G 미만인 경우 <code>qemu-img info imageName &#124; grep 'disk size'</code>를 사용해 실제 크기 조회</li><li>이미지의 vsize가 500G 미만인 경우 <code>qemu-img info imageName &#124; grep 'virtual size'</code>를 사용해 이미지 vsize 조회</li></ul><b>주의사항: </b>이미지 가져오기 시 QCOW2 형식으로 전환한 후의 이미지 정보를 기준으로 심사합니다.</td></tr>
<tr><td>네트워크</td><td><ul><li>Tencent Cloud는 인스턴스에 <code>eth0</code> 네트워크 인터페이스를 기본으로 제공합니다.</li><li>사용자는 인스턴스 내의 metadata 서비스를 통해 인스턴스의 네트워크 설정을 조회할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/4934">인스턴스 메타데이터</a>를 참조 바랍니다.</li></ul></td></tr>
<tr><td>드라이버</td><td><ul><li>이미지에 가상화 플랫폼 KVM의 Virtio 드라이버가 반드시 설치되어 있어야 합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux 시스템 Virtio 드라이버 검사</a>를 참조 바랍니다.</li><li>이미지에 cloudinit를 설치하시기를 권장합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/12587">Linux 시스템에서 cloudinit 설치</a>를 참조 바랍니다.</li><li>다른 원인으로 cloudinit가 설치되지 않으면 <a href="https://intl.cloud.tencent.com/document/product/213/12849">이미지 강제 가져오기</a>를 참조하여 자체적으로 인스턴스를 구성하시기 바랍니다.</li></ul></td></tr>
<tr><td>커널 제한</td><td>네이티브 커널이 가장 적합하며, 수정 시 CVM으로 가져오지 못할 수 있습니다.</td></tr>
</table>
- **Windows 시스템 유형의 이미지 제한:**
<table>
<tr><th>이미지 속성</th><th>조건</th></tr>
<tr><td>운영 체제</td><td><ul><li>Windows Server 2008 관련 버전, Windows Server 2012 관련 버전, Windows Server 2016 관련 버전</li><li>32비트와 64비트 지원</li></ul></td></tr>
<tr><td>이미지 형식</td><td><ul><li>RAW, VHD, QCOW2, VMDK 이미지 형식 지원</li><li><code>qemu-img info imageName &#124; grep 'file format'</code>을 통해 이미지 형식 조회</li></ul></td></tr>
<tr><td>파일 시스템 유형</td><td><ul><li>MBR 파티션을 사용한 NTFS 파일 시스템만 지원합니다.</li><li>GPT 파티션을 지원하지 않습니다.</li><li>논리 볼륨 관리(LVM)를 지원하지 않습니다. </li></ul></td></tr>
<tr><td>이미지 크기</td><td><ul><li>이미지의 실제 크기가 50G 미만인 경우 <code>qemu-img info imageName &#124; grep 'disk size'</code>를 사용해 실제 크기 조회</li><li>이미지의 vsize가 500G 미만인 경우 <code>qemu-img info imageName &#124; grep 'virtual size'</code>를 사용해 이미지 vsize 조회</li></ul><b>주의사항: </b>이미지 가져오기 시 qcow2 형식으로 전환한 후의 이미지 정보를 기준으로 심사합니다.</td></tr>
<tr><td>네트워크</td><td><ul><li>Tencent Cloud는 인스턴스에 <code>로컬 연결</code> 네트워크 인터페이스를 기본으로 제공합니다.</li><li>사용자는 인스턴스 내의 metadata 서비스를 통해 인스턴스의 네트워크 설정을 조회할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/4934">인스턴스 메타데이터</a>를 참조 바랍니다.</li></ul></td></tr>
<tr><td>드라이버</td><td>이미지에 가상화 플랫폼 KVM의 Virtio 드라이버가 반드시 설치되어 있어야 합니다. Windows 시스템은 Virtio 드라이버가 기본적으로 설치되어 있지 않습니다. 사용자는 <a href="http://windowsvirtio-10016717.file.myqcloud.com/InstallQCloud.exe">Windows Virtio 드라이버</a>를 설치한 뒤 로컬 이미지를 내보낼 수 있습니다.</td></tr>
<tr><td>기타</td><td>가져온 Windows 시스템 이미지는 <a href="https://intl.cloud.tencent.com/document/product/213/2757">Windows 활성화</a> 서비스를 <b> 제공하지 않습니다</b>.</td></tr>
</table>

## 가져오기 순서

 1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
 2. 왼쪽 메뉴의 [[Image](https://console.cloud.tencent.com/cvm/image)]를 클릭합니다.
 3. [Custom Image]를 선택하고 [Import Image]를 클릭합니다.
 4. 작업 인터페이스에 따라 먼저 [COS를 활성화](https://console.cloud.tencent.com/cos4/index)하고 [bucket 버킷을 생성](/doc/product/436/6232)한 다음, 이미지 파일을 bucket에 업로드하여 [이미지 파일 URL을 획득](/doc/product/436/6260)합니다.
 5. [Next]를 클릭합니다.
 6. 실제 상황에 따라 테이블 서식을 입력하고 [Import]를 클릭합니다.
 > 입력한 COS 파일의 URL이 정확한지 확인합니다.
 >
가져오기 성공, 실패 여부에 대한 알림은 [내부 메시지](https://console.cloud.tencent.com/message)를 통해 발송됩니다.

## 가져오기 실패

여러가지 이유로 콘솔에서 이미지 가져오기 작업에 실패할 수 있습니다. 작업 실패 시 아래의 내용에 따라 진단 및 해결하시기 바랍니다.

### 주의 사항

본문에 따라 실패 원인을 진단하기 전에 [내부 메시지 관리 페이지](https://console.cloud.tencent.com/messageCenter/messageConfig)의 소식 구독란에서 구독 제품 서비스와 관련된 알림을 확인하며, 실패 원인이 포함된 내부 메시지, SMS와 이메일을 수신하도록 설정해야 합니다.
> 메시지 센터에서 제품 서비스 관련 정보를 구독하지 않은 경우에는 가져오기 성공/실패에 대한 내부 메시지를 받지 못할 수 있습니다.

### 실패 원인 진단

자세한 오류 알림 및 오류 설명은 [에러 코드](#errorcode)를 참조 바랍니다.

#### InvalidUrl: COS 링크 무효

InvalidUrl 오류 알림이 뜬다면 이미지 가져오기 페이지에 잘못된 COS 링크를 입력했다는 뜻으로, 예상되는 원인은 아래와 같습니다.
* 입력한 내용이 [Tencent Cloud COS](https://console.cloud.tencent.com/cos4/index)의 이미지 링크가 아닐 경우.
* COS 파일의 액세스 권한은 개인 읽기지만, 서명이 유효하지 않을 경우.
> 서명이 포함된 COS 파일 링크는 한 번만 액세스할 수 있습니다.
>
* 다른 리전의 COS 링크를 입력했을 경우.
> 이미지 가져오기 서비스는 내부 네트워크를 통해 로컬 리전의 COS 서버로 액세스됩니다.
>
* 사용자의 이미지 파일이 삭제된 경우.
COS 링크가 유효하지 않다는 오류 보고를 받았다면, 상기 원인을 기준으로 해결할 수 있습니다.

#### InvalidFormatSize: 형식 또는 크기가 조건에 부합하지 않음

InvalidFormatSize 오류 알림이 뜨는 경우 가져온 이미지의 형식 또는 크기가 Tencent Cloud의 이미지 가져오기 기능 제한에 부합하지 않다는 뜻으로, 해당되는 제한은 아래와 같습니다.
* 이미지 가져오기 기능은 ‘qcow2’, ‘vhd’, ‘vmdk’, ‘raw’ 네 종류의 이미지 파일 형식을 지원합니다.
* 가져온 이미지의 실제 파일 크기는 50GB를 초과할 수 없습니다(qcow2 형식으로 전환한 이미지 파일을 기준으로 함).
* 가져온 이미지의 시스템 디스크 크기는 500GB를 초과할 수 없습니다.

형식 또는 크기가 조건에 부합하지 않는다는 오류 보고를 받았을 경우,
- [Linux 이미지 생성](https://intl.cloud.tencent.com/document/product/213/17814)의 이미지 형식 변환 방법을 참조하여 이미지 파일을 적합한 파일 형식으로 변환하고, 크기 제한에 부합하도록 이미지 콘텐츠를 간략화하여 다시 이미지 가져오기 할 수 있습니다.
- [오프라인 인스턴스 마이그레이션](https://console.cloud.tencent.com/csm/importOfflineCvm) 기능을 사용해 인스턴스를 마이그레이션할 수 있습니다. 최대 500GB의 이미지 파일 마이그레이션을 지원합니다.

#### VirtioNotInstall: Virtio 드라이버가 설치되지 않음

VirtioNotInstall 오류 알림이 뜨는 경우 가져온 이미지에 Virtio 드라이버가 설치되어 있지 않다는 뜻입니다. Tencent Cloud의 KVM 가상화 기술을 사용하려면 사용자가 가져온 이미지 내에 virtio 드라이버가 설치되어 있어야 합니다. 일부 사용자 정의 Linux 운영 체제 외에, 대부분의 Linux 운영 체제에는 Virtio 드라이버가 이미 설치되어 있습니다. Windows 운영 체제는 사용자가 수동으로 Virtio 드라이버를 설치해야 합니다.
* Linux 이미지 가져오기는 [Linux 시스템 Virtio 드라이버 검사](https://intl.cloud.tencent.com/document/product/213/9929) 문서를 참조 바랍니다.
* Windows 이미지 가져오기는 [Windows 이미지 생성](https://intl.cloud.tencent.com/document/product/213/17815) 문서를 참조하여 Virtio 드라이버를 설치할 수 있습니다.

#### CloudInitNotInstalled: cloud-init 프로그램이 설치되지 않음

CloudInitNotInstalled 오류 알림이 뜨는 경우 가져온 이미지에 cloud-init 프로그램이 설치되어 있지 않다는 뜻입니다. Tencent Cloud는 오픈 소스 프로그램 cloud-init을 사용해 CVM을 초기화하므로, cloud-init 프로그램 미설치 시 사용자의 CVM 초기화에 실패하게 됩니다.
* Linux 이미지 가져오기는 [Linux 시스템에서 cloud-init 설치](https://intl.cloud.tencent.com/document/product/213/12587) 문서를 참조 바랍니다.
* Windows 이미지 가져오기는 [Windows 운영 체제에서 cloudbase-init 설치](https://intl.cloud.tencent.com/document/product/213/32364) 문서를 참조 바랍니다.
* cloud-init/cloudbase-init 설치 후, CVM을 실행할 때 정확한 데이터 소스부터 가져오도록 문서를 따라 구성 파일을 교체합니다.

#### PartitionNotPresent: 파티션 정보가 손실됨

PartitionNotPresent 오류 알림이 뜨는 경우 가져온 이미지가 불완전하다는 뜻으로, 이미지 생성 시 부트 파티션이 포함되어 있는지 확인해야 합니다.

#### RootPartitionNotFound: 루트 파티션이 손실됨

RootPartitionNotFound 오류 알림이 뜨는 경우 가져온 이미지의 루트 파티션을 찾을 수 없다는 뜻이므로, 이미지 파일을 점검하시기 바랍니다. 자주 발생하는 원인은 다음과 같습니다.
* 설치 패키지 파일을 업로드한 경우.
* 데이터 디스크 이미지를 업로드한 경우.
* 부트 파티션 이미지를 업로드한 경우.
* 잘못된 파일을 업로드한 경우.

#### InternalError: 알 수 없는 오류

InternalError 오류 알림이 뜰 경우 가져온 이미지 서비스에 해당 오류 원인에 대한 기록이 없다는 뜻으로, 이러한 문제는 고객센터로 문의하여 기술팀을 통해 문제를 해결하시기 바랍니다.

<a id="errorcode"></a>
## 에러 코드
 
|에러 코드|오류 원인|권장 처리 방법|
|-----|-----|-----|
|InvalidUrl|COS 링크 무효|COS 링크와 가져온 이미지 링크가 같은지 검사 |
|InvalidFormatSize|형식 또는 크기가 조건에 부적합|이미지가 [가져오기 준비](#가져오기 준비)에서 ‘이미지 형식’과 ‘이미지 크기’ 제한에 부합해야 합니다.|
|VirtioNotInstall|virtio 드라이버 미설치|이미지에 virtio 드라이버를 설치해야 합니다. [가져오기 준비](#가져오기 준비)의 ‘드라이버’ 부분을 참조 바랍니다.|
|PartitionNotPresent|파티션 정보를 찾지 못했거나| 이미지 손상, 잘못된 생성 방식으로 인한 이미지 손상일 수 있습니다.|
|CloudInitNotInstalled|cloud-init 미설치|Linux 이미지에는 cloud-init를 설치해야 합니다. [가져오기 준비](#가져오기 준비)의 ‘드라이버’ 부분을 참조 바랍니다.|
|RootPartitionNotFound|루트 파티션 미점검|잘못된 생성 방식으로 인한 이미지 손상일 수 있습니다.|
|InternalError|기타 오류|고객센터로 문의 바랍니다.|

