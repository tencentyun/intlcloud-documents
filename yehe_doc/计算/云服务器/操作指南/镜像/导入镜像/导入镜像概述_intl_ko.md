[사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942) 기능 외에도, Tencent Cloud는 가져오기 기능을 지원합니다. 로컬 또는 기타 플랫폼 서버 시스템 디스크의 이미지 파일을 Cloud Virtual Machine(CVM)의 사용자 정의 이미지로 가져올 수 있습니다. 가져온 후 해당 이미지를 사용하여 CVM를 생성하거나 기존 CVM의 시스템을 재설치할 수 있습니다.

<span id="가져오기 준비"></span>
## 가져오기 준비

가져오기 조건에 맞는 이미지 파일을 미리 준비해야 합니다.
- **Linux 시스템 유형의 이미지 조건:**
<table>
<tr><th>이미지 속성</th><th>조건</th></tr>
<tr><td>운영 체제</td><td><ul><li>CentOS, Ubuntu, Debian, CoreOS, openSUSE, SUSE 릴리스 버전 기반의 이미지</li><li>32비트와 64비트 지원</li></ul></td></tr>
<tr><td>이미지 형식<td><td><ul><li>RAW, VHD, QCOW2, VMDK 이미지 형식을 지원합니다</li><li><code>qemu-img info imageName &#124; grep 'file format'</code> 을 사용하여 조회할 수 있습니다</li></ul></td></tr>
<tr><td>이미지 크기</td><td><ul><li>이미지 실제 크기가 50G 미만인 경우 <code>qemu-img info imageName &#124; grep 'disk size'</code>를 사용하여 이미지의 실제 크기를 조회할 수 있습니다</li><li>이미지 vsize가 500G 미만인 경우 <code>qemu-img info imageName &#124; grep 'virtual size'</code>를 사용하여 이미지 vsize를 조회할 수 있습니다</li></ul><b>주의 사항: </b>이미지 가져오기 시 QCOW2 형식으로 전환한 후의 이미지 정보를 기준으로 크기를 확인합니다.</td></tr>
<tr><td>네트워크</td><td><ul><li>Tencent Cloud는 인스턴스에 <code>eth0</code> 네트워크 인터페이스를 기본으로 제공합니다</li><li>사용자는 인스턴스 내의 metadata 서비스를 통해 인스턴스의 네트워크 구성을 조회할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/4934">인스턴스 메타데이터</a>를 참조 바랍니다.</li></ul></td></tr>
<tr><td>드라이버</td><td><ul><li>이미지에는 반드시 가상화 플랫폼인 KVM의 Virtio 드라이버를 설치해야 합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux 이미지 가져오기로 Virtio 드라이버 확인</a>을 참조 바랍니다.</li><li>이미지는 cloudinit 설치를 권장합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/12587">Linux 이미지 가져오기로 cloudinit 설치</a>를 참조 바랍니다.</li><li>다른 원인으로 이미지에 cloudinit를 설치할 수 없다면 <a href="https://intl.cloud.tencent.com/document/product/213/12849">이미지 강제 가져오기</a>를 참고하여 자체로 인스턴스를 구성하시기 바랍니다.</li></ul></td></tr>
<tr><td>커널 조건</td><td>이미지는 네이티브 커널이도록 권장하며, 수정한 후에는 CVM으로 가져오지 못할 수 있습니다.</td></tr>
</table>
- **Windows 시스템 유형의 이미지 조건:**
<table>
<tr><th>이미지 속성</th><th>조건</th></tr>
<tr><td>운영 체제</td><td><ul><li>Windows Server 2012 관련 버전, Windows Server 2016 관련 버전</li><li>32비트와 64비트 지원</li></ul></td></tr>
<tr><td>이미지 형식<td><td><ul><li>RAW, VHD, QCOW2, VMDK 이미지 형식을 지원합니다</li><li><code>qemu-img info imageName &#124; grep 'file format'</code> 을 사용하여 조회할 수 있습니다</li></ul></td></tr>
<tr><td>파일 시스템 유형</td><td><ul><li>MBR 파티션을 사용한 NTFS 파일 시스템만 지원합니다.</li><li>GPT 파티션을 지원하지 않습니다.</li><li>논리 볼륨 관리(LVM)를 지원하지 않습니다. </li></ul></td></tr>
<tr><td>이미지 크기</td><td><ul><li>이미지 실제 크기가 50G 미만인 경우 <code>qemu-img info imageName &#124; grep 'disk size'</code>를 사용하여 이미지의 실제 크기를 조회할 수 있습니다</li><li>이미지 vsize가 500G 미만인 경우 <code>qemu-img info imageName &#124; grep 'virtual size'</code>를 사용하여 이미지 vsize를 조회할 수 있습니다</li></ul><b>주의 사항: </b>이미지 가져오기 시 qcow2 형식으로 전환한 후의 이미지 정보를 기준으로 크기를 확인합니다.</td></tr>
<tr><td>네트워크</td><td><ul><li>Tencent Cloud는 인스턴스에 <code>로컬 연결</code> 네트워크 인터페이스를 기본으로 제공합니다</li><li>사용자는 인스턴스 내의 metadata 서비스를 통해 인스턴스의 네트워크 구성을 조회할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/4934">인스턴스 메타데이터</a>를 참조 바랍니다.</li></ul></td></tr>
<tr><td>드라이버</td><td>이미지에는 반드시 가상화 플랫폼인 KVM의 Virtio 드라이버를 설치해야 합니다. Windows 시스템은 Virtio 드라이버를 기본적으로 설치하지 않으므로, 사용자는 <a href="http://windowsvirtio-10016717.file.myqcloud.com/InstallQCloud.exe">Windows Virtio 드라이버</a>를 설치한 뒤 로컬 이미지를 내보낼 수 있습니다.</td></tr>
<tr><td>기타</td><td>가져온 Windows 시스템 이미지에는 <a href="https://intl.cloud.tencent.com/document/product/213/2757">Windows 활성화</a> 서비스를 <b>제공하지 않습니다</b></td></tr>
</table>

## 가져오기 순서

 1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
 2. 왼쪽 메뉴의[[Image](https://console.cloud.tencent.com/cvm/image)]를 클릭합니다.
 3. [Custom Image]를 선택하고 [Import Image]를 클릭합니다.
 4. 작업 인터페이스에 따라 먼저 [Enable Cloud Object Storage](https://console.cloud.tencent.com/cos4/index)한 다음 [Createbucket ](/doc/product/436/6232)하여 이미지 파일을 bucket에 업로드하고, [Get Image file URL](/doc/product/436/6260)합니다.
 5. [Next]를 클릭합니다.
 6. 실제 상황에 따라 폼을 입력하고 [Import]를 클릭합니다.
 > 입력한 COS 파일 URL이 정확한지 확인하세요.
 >
가져오기 성공 또는 실패 여부가 [내부 메시지](https://console.cloud.tencent.com/message) 형식으로 공지됩니다.

## 가져오기 실패

콘솔에서 이미지 가져오기 작업 진행 후, 여러 이유로 작업에 실패할 수 있습니다. 작업에 실패한 상태라면 아래의 내용에 따라 진단할 수 있습니다.

### 주의 사항

본 문서대로 실패 원인을 진단하기 전에 [내부 메시지 관리 페이지](https://console.cloud.tencent.com/messageCenter/messageConfig)의 소식 구독란에서 제품 서비스 관련 공지를 확인하여 실패 원인이 포함된 내부 메시지, SMS와 메일을 수신할 수 있도록 합니다.
> 메시지 센터에서 제품 서비스 관련 정보를 구독하지 않았다면, 가져오기 성공/실패에 대한 내부 메시지를 받을 수 없습니다.

### 실패 원인 진단

자세한 오류 알림 및 오류 설명은 [에러 코드](#errorcode)를 참조 바랍니다.

#### InvalidUrl: COS 링크 무효

InvalidUrl 오류 발생 시 이미지 가져오기 페이지에 잘못된 COS 링크를 입력했다는 알림이 뜨며, 예상 원인은 아래와 같습니다.
* [Tencent Cloud COS](https://console.cloud.tencent.com/cos4/index)의 이미지 링크가 아닌 것을 입력함
* COS 파일의 액세스 권한이 개인 읽기로 되어 있지만, 서명이 유효하지 않음
> 서명이 포함된 COS 파일 링크만 한번 액세스될 수 있습니다.
>
* 다른 리전의 COS 링크를 입력함
> 이미지 가져오기 시 내부 네트워크를 통해 로컬 리전의 COS 서버로 액세스합니다.
>
* 사용자의 이미지 파일이 삭제됨
COS 링크 무효에 대한 오류 보고를 받은 후, 상기 원인에 따라 문제를 진단할 수 있습니다.

#### InvalidFormatSize: 형식 또는 크기가 조건에 부합하지 않음

InvalidFormatSize 오류 발생 시 미리 가져온 이미지의 형식 또는 크기가 Tencent Cloud의 이미지 가져오기 기능 조건에 부합하지 않다는 알림이 뜨며, 조건은 아래와 같습니다.
* 가져오기 이미지는 ‘qcow2’, ‘vhd’, ‘vmdk’, ‘raw’ 네 종류의 이미지 파일 형식을 지원합니다.
* 가져오기 이미지의 실제 파일 크기는 50GB를 초과할 수 없습니다(qcow2 형식으로 전환한 이미지 파일 기준).
* 가져오기 이미지의 시스템 디스크 크기는 500GB를 초과할 수 없습니다.

형식 또는 크기가 조건에 부합하지 않는다는 오류 보고를 받은 경우
- [Linux 이미지 생성](https://intl.cloud.tencent.com/document/product/213/17814)의 이미지 형식 전환 콘텐츠에 따라 이미지 파일을 적합한 파일 형식으로 전환하고, 이미지 콘텐츠를 간소화하여 크기 조건을 만족한 후 다시 이미지를 가져올 수 있습니다.
- [오프라인 인스턴스 마이그레이션](https://console.cloud.tencent.com/csm/importOfflineCvm) 기능을 사용하여 인스턴스를 마이그레이션할 수 있습니다. 해당 기능으로 최대 500GB의 이미지 파일을 마이그레이션할 수 있습니다.

#### VirtioNotInstall: Virtio 드라이버가 설치되지 않음

VirtioNotInstall 오류 발생 시 미리 가져온 이미지에 Virtio 드라이버가 설치되어 있지 않다는 알림이 뜹니다. Tencent Cloud의 KVM 가상화 기술은 사용자가 가져온 이미지 내에 virtio 드라이버를 설치하도록 요구합니다. 일부 사용자 정의 Linux 운영 체제 외에, 대부분의 Linux 운영 체제는 이미 Virtio 드라이버가 설치되어 있으며, Windows 운영 체제는 사용자가 수동으로 Virtio 드라이버를 설치해야 합니다.
* Linux 이미지 가져오기는 [Linux 시스템 Virtio 드라이버 확인](https://intl.cloud.tencent.com/document/product/213/9929) 문서를 참조할 수 있습니다.
* Windows 이미지 가져오기는 [Windows 이미지 생성](https://intl.cloud.tencent.com/document/product/213/17815) 문서를 참조하여 Virtio 드라이버를 설치할 수 있습니다.

#### CloudInitNotInstalled: cloud-init 프로그램이 설치되지 않음

CloudInitNotInstalled 오류 발생 시 미리 가져온 이미지에 cloud-init 프로그램이 설치되어 있지 않다는 알림이 뜹니다. Tencent Cloud는 오픈 소스 프로그램 cloud-init를 사용하여 CVM을 초기화하므로, cloud-init 프로그램 미설치 시 사용자의 CVM 초기화에 실패합니다.
* Linux 이미지 가져오기는 [Linux 시스템 cloud-init 설치](https://intl.cloud.tencent.com/document/product/213/12587) 문서를 참조할 수 있습니다.
* Windows 이미지 가져오기는 [Windows 운영 체제 cloudbase-init 설치](https://intl.cloud.tencent.com/document/product/213/32364) 문서를 참조할 수 있습니다.
* cloud-init/cloudbase-init 설치 후, 문서에 따라 구성 파일을 교체하여 CVM을 시작할 수 있을 때, 정확한 데이터 소스에서 데이터를 받으세요.

#### PartitionNotPresent: 파티션 정보가 손실됨

PartitionNotPresent 오류 발생 시 가져온 이미지가 불완전하다는 알림이 뜹니다. 이미지 생성 시 부트 파티션이 포함되어 있는지 확인하세요.

#### RootPartitionNotFound: 루트 파티션이 손실됨

RootPartitionNotFound 오류 발생 시 가져온 이미지가 루트 파티션을 포함하는지 확인되지 않았다는 알림이 뜹니다. 이미지 파일을 확인하시고, 자주 발생하는 원인은 다음을 참조 바랍니다.
* 설치 패키지 파일을 업로드했습니다.
* 데이터 디스크 이미지를 업로드했습니다.
* 부트 파티션 이미지를 업로드했습니다.
* 오류 파일을 업로드했습니다.

#### InternalError: 알 수 없는 오류입니다

InternalError 오류 발생 시 가져온 이미지 서비스에 해당 오류 원인에 대한 기록이 없다는 알림이 뜨며, 이러한 문제는 고객서비스에 문의하여 기술자를 통해 문제를 해결할 수 있습니다.

<a id="errorcode"></a>
## 에러 코드
 
|에러 코드|오류 원인|권장 처리 방식|
|-----|-----|-----|
|InvalidUrl|COS 링크 무효|COS 링크와 가져온 이미지 링크가 같은지 확인합니다.|
|InvalidFormatSize|형식 또는 크기가 조건에 맞지 않음|이미지가 [가져오기 준비](#가져오기 준비) 중의 ‘이미지 형식’과 ‘이미지 크기’ 조건에 부합해야 합니다.|
|VirtioNotInstall|virtio 드라이버 미설치|이미지에 virtio 드라이버를 설치해야 합니다. [가져오기 준비](#가져오기 준비) 중의 ‘드라이버’ 부분을 참조 바랍니다.|
|PartitionNotPresent|파티션 정보 손상|잘못된 생성 방식으로 인해 이미지가 손상되었을 수 있습니다.|
|CloudInitNotInstalled|cloud-init 미설치|Linux 이미지는 cloud-init를 설치해야 합니다. [가져오기 준비](#가져오기 준비) 중의 ‘드라이버’ 부분을 참조 바랍니다.|
|RootPartitionNotFound|루트 파티션 미확인|잘못된 생성 방식으로 인해 이미지가 손상되었을 수 있습니다.|
|InternalError|기타 오류|고객서비스에 문의 바랍니다.|

