[사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942) 기능을 사용하는 것 이외에도, Tencent Cloud는 가져오기 기능 사용도 지원합니다. 로컬 또는 기타 플랫폼 서버 시스템 디스크의 미러 이미지 파일을 CVM(Cloud Virtual Machine)에 사용자 정의 이미지로 가져오기 할 수 있습니다. 가져오기 후 가져온 미러 이미지를 사용해 CVM를 생성하거나 이미 존재하는 CVM의 시스템을 재설치할 수 있습니다.

<span id="가져오기 준비"></span>
## 가져오기 준비

가져오기 조건에 부합하는 미러 이미지 파일을 미리 준비해야 합니다.
- **Linux 시스템 유형의 미러 이미지 제한**
<table>
<tr><th>미러 이미지 속성</th><th>조건</th></tr>
<tr><td>운영 체제</td><td><ul><li>CentOS, Ubuntu, Debian, CoreOS, openSUSE, SUSE 버전을 기반으로 한 미러 이미지</li><li>32비트와 64비트 지원</li></ul></td></tr>
<tr><td>미러 이미지 형식</td><td><ul><li>RAW, VHD, QCOW2, VMDK 미러 이미지 형식 지원</li><li>사용<code>qemu-img info imageName | grep 'file format'</code>미러 이미지 형식 조회</li></ul></td></tr>
<tr><td>미러 이미지 크기</td><td><ul><li>미러 이미지 실제 크기가 50G미만인 경우 <code>qemu-img info imageName &#124; grep 'disk size'</code>사용해 실제 크기 조회</li><li>미러 이미지 vsize 500G미만인 경우 <code>qemu-img info imageName &#124; grep 'virtual size'</code> 사용해 미러 이미지 vsize 조회</li></ul><b>주의 사항: </b>미러 이미지 가져오기 시 QCOW2 형식으로 전환한 후 미러 이미지 정보를 기준으로 심사합니다.</td></tr>
<tr><td>네트워크</td><td><ul><li>Tencent Cloud는 기본으로 인스턴스를 제공합니다. <code>eth0</code>네트워크 인터페이스</li><li>Tencent Cloud는 잠시 IPV6를 지원하지 않습니다. </li><li>사용자는 인스턴스 내의 metadata 서비스 쿼리를 통해 인스턴스의 네트워크를 구성할 수 있습니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/213/4934">인스턴스 메타데이터</a>를 참조하십시오.</li></ul></td></tr>
<tr><td>드라이버</td><td><ul><li>미러 이미지는 반드시 버츄얼화 플랫폼 KVM의 Virtio 드라이버를 설치해야 합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux 미러 이미지 가져오기로 Virtio 드라이버 검사</a>를 참조하십시오.</li><li>미러 이미지가 cloudinit 설치를 권장합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/12587">Linux 미러 이미지 가져오기로 cloudinit 설치</a>를 참조하십시오.</li><li>다른 원인으로 cloudinit가 설치되지 않을 경우 <a href="https://cloud.tencent.com/document/product/213/12849">미러 이미지 강제 가져오기</a>를 참고하여 자체 인스턴스 구성을 진행하십시오.</li></ul></td></tr>
<tr><td>커널 제한</td><td>미러 이미지는 네이티브 커널일 때 가장 좋으며, 수정 시 CVM로 가져오기가 되지 않을 수 있습니다.</td></tr>
</table>
- **Windows 시스템 유형의 미러 이미지 제한**
<table>
<tr><th>미러 이미지 속성</th><th>조건</th></tr>
<tr><td>운영 체제</td><td><ul><li>Windows Server 2008 관련 버전, Windows Server 2012 관련 버전, Windows Server 2016 관련 버전</li><li>32비트와 64비트 지원</li></ul></td></tr>
<tr><td>미러 이미지 형식</td><td><ul><li>RAW, VHD, QCOW2, VMDK 미러 이미지 형식 지원</li><li>사용<code>qemu-img info imageName | grep 'file format'</code>미러 이미지 형식 조회</li></ul></td></tr>
<tr><td>파일 시스템 유형</td><td><ul><li>MBR 파티션을 사용한 NTFS 파일 시스템만 지원합니다.</li><li>GPT 파티션 지원하지 않습니다.</li><li>논리 볼륨 관리(LVM)는 지원하지 않습니다. </li></ul></td></tr>
<tr><td>미러 이미지 크기</td><td><ul><li>미러 이미지 실제 크기가 50G미만인 경우 <code>qemu-img info imageName &#124; grep 'disk size'</code>사용해 실제 크기 조회</li><li>미러 이미지 vsize 500G미만인 경우 <code>qemu-img info imageName &#124; grep 'virtual size'</code> 사용해 미러 이미지 vsize 조회</li></ul><b>주의 사항: </b>미러 이미지 가져오기 시 qcow2 형식으로 전환한 후 미러 이미지 정보를 기준으로 심사합니다.</td></tr>
<tr><td>네트워크</td><td><ul><li>Tencent Cloud는 기본으로 인스턴스를 제공합니다. <code>로컬 연결</code>네트워크 인터페이스</li><li>Tencent Cloud는 잠시 IPV6를 지원하지 않습니다.</li><li>사용자는 인스턴스 내의 metadata 서비스 쿼리 인스턴스를 통해 네트워크를 구성할 수 있습니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/213/4934">인스턴스 메타데이터 </a>를 참조하십시오.</li></ul></td></tr>
<tr><td>드라이버</td><td>미러 이미지는 반드시 버츄얼화 플랫폼 KVM의 Virtio 드라이버를 설치해야 합니다. Windows 시스템은 Virtio 드라이버가 기본적으로 설치되지 않습니다. 사용자는 <a href="http://windowsvirtio-10016717.file.myqcloud.com/InstallQCloud.exe">Windows Virtio 드라이버</a>를 설치한 뒤 로컬 미러 이미지를 내보내기할 수 있습니다.</td></tr>
<tr><td>기타</td><td>가져오기 한 Windows 시스템 미러 이미지<b>제공하지 않습니다. </b> <a href="https://cloud.tencent.com/document/product/213/2757">Windows 활성화</a>서비스</td></tr>
</table>

## 가져오기 순서

 1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인하십시오.
 2. 왼쪽 사이드바의 [[미러 이미지](https://console.cloud.tencent.com/cvm/image)]를 클릭하십시오.
 3. [사용자 정의 이미지]를 선택하고 [미러 이미지 가져오기]를 클릭하십시오.
 4. 작업 인터페이스 요구에 따라 먼저 [COS 활성화](https://console.cloud.tencent.com/cos5/index)를 한 뒤, [bucket 생성](/doc/product/436/6232)을 할 경우 미러 이미지 파일이 bucket에 업로드되며 [미러 이미지 파일 URL을 획득](/doc/product/436/6260)합니다.
 5. [다음 단계]를 클릭하십시오.
 6. 실제 상황에 따라 서식을 입력하고 [가져오기 시작]을 클릭하십시오.
 > 입력한 COS 파일 URL이 확실한지 확인하십시오.
 >
가져오기 성공, 실패 여부가 [내부 메시지](https://console.cloud.tencent.com/message)를 통해 알림이 발송됩니다.

## 가져오기 실패

콘솔에서 미러 이미지 가져오기 작업 진행 후, 여러 이유로 작업이 실패할 수 있습니다. 작업 실패 상태에서는 아래의 내용에 따라 조사하십시오.

### 주의사항

실패 원인에 대한 파일 조사 전 [내부 메시지 관리 페이지](https://console.cloud.tencent.com/messageCenter/messageConfig) 소식 구독란의 구독 제품 서비스와 관련된 알림을 확인하십시오. 실패 원인이 포함된 내부 메시지, SMS와 메일 수신을 제공합니다.
> 메시지 센터에서 제품 서비스 관련 정보를 구독하지 않은 경우에는 가져오기 성공/실패를 고지하는 내부 메시지를 받지 못할 수 있습니다.

### 실패 원인 조사

자세한 오류 알림 및 오류 설명에 대해 [에러코드](#errorcode)를 참조하십시오.

#### InvalidUrl: COS 링크 무효

오류 보고 InvalidUrl의 오류 알림: 미러 이미지 가져오기 페이지에 잘못된 COS 링크를 입력했습니다. 예상되는 원인은 아래와 같습니다.
* [Tencent Cloud COS](https://console.cloud.tencent.com/cos5/index)의 미러 이미지 링크가 아닌 것을 입력했습니다.
* COS 파일의 액세스 권한이 사유 읽기이지만, 서명이 유효하지 않습니다.
> 서명이 포함된 COS 파일 링크만 액세스될 수 있습니다.
>
* 다른 리전의 COS 링크를 입력했습니다.
> 미러 이미지 가져오기는 내부 네트워크를 통해 로컬 리전의 COS 서버로 액세스됩니다.
>
* 사용자의 미러 이미지 파일이 삭제되었습니다.
COS 무효 링크에 대한 오류 보고를 받은 후, 서술된 원인에 따라 문제를 조사할 수 있습니다.

#### InvalidFormatSize: 형식 또는 크기가 조건에 부합하지 않습니다.

오류 보고 InvalidFormatSize의 오류 알림: 가져오기 한 미러 이미지의 형식 또는 크기가 Tencent Cloud의 미러 이미지 가져오기 기능 제한과 부합하지 않습니다. 제한은 아래와 같습니다.
* 가져온 미러 이미지는 ‘qcow2’, ‘vhd’, ‘vmdk’, ‘raw’ 네 종류의 미러 이미지 파일 형식을 지원합니다.
* 가져오기 미러 이미지의 실제 파일 크기는 50GB를 초과할 수 없습니다(qcow2 형식으로 전환한 미러 이미지 파일 기준).
* 가져오기 미러 이미지의 시스템 디스크 크기는 500GB를 초과할 수 없습니다.

형식 또는 크기가 조건에 부합하지 않는다는 오류 보고를 받는 경우
- [Linux 미러 이미지 생성](https://intl.cloud.tencent.com/document/product/213/17814)의 미러 이미지 형식 전환 콘텐츠에 따라 미러 이미지 파일을 적합한 파일 형식으로 전환할 수 있습니다. 간단한 미러 이미지 콘텐츠로 크기 제한을 만족시킨 후 다시 미러 이미지를 가져오기 할 수 있습니다.
- [오프라인 인스턴스 마이그레이션](https://console.cloud.tencent.com/csm/importOfflineCvm) 기능을 사용해 인스턴스를 마이그레이션할 수 있습니다. 최대 500GB의 미러 이미지 파일 마이그레이션을 지원합니다.

#### VirtioNotInstall: Virtio 드라이버가 설치되지 않았습니다.

오류 보고 VirtioNotInstall의 오류 알림: 가져온 미러 이미지에 Virtio 드라이버가 설치돼 있지 않습니다. Tencent Cloud의 KVM 버츄얼화 기술은 사용자가 가져오기 한 미러 이미지 내에 virtio 드라이버가 설치되어 있기를 요구합니다. 일부 사용자 정의 Linux 운영 체제 외에, 대부분의 Linux 운영 체제는 이미 Virtio 드라이버가 설치되어 있습니다. Windows 운영 체제는 사용자가 수동으로 Virtio 드라이버를 설치해야 합니다.
* Linux 미러 이미지 가져오기는 [Linux 시스템 Virtio 드라이버 검사](https://intl.cloud.tencent.com/document/product/213/9929) 문서를 참조하십시오.
* Windows 미러 이미지 가져오기는 [Windows 미러 이미지 생성](https://intl.cloud.tencent.com/document/product/213/17815)을 참조하여 Virtio 드라이버를 설치할 수 있습니다.

#### CloudInitNotInstalled: cloud-init 프로그램이 설치되지 않았습니다.

오류 보고 CloudInitNotInstalled의 오류 알림: 가져오기 한 미러 이미지에 cloud-init 프로그램이 설치되어 있지 않습니다. Tencent Cloud는 오픈 소스 프로그램 cloud-init을 사용해 CVM을 초기화합니다. 그러므로 cloud-init 프로그램 미설치 시 사용자의 CVM 초기화가 실패합니다.
* Linux 미러 이미지 가져오기는 [Linux 시스템 cloud-init 설치](https://intl.cloud.tencent.com/document/product/213/12587) 문서를 참조하십시오.
* Windows 미러 이미지 가져오기는 [Windows 운영 체제 cloudbase-init 설치](https://intl.cloud.tencent.com/document/product/213/32364) 문서를 참조하십시오.
* cloud-init/cloudbase-init 설치 후, 파일 구성 교체 문서에 따라 사용 가능한 CVM을 시작할 경우, 정확한 데이터 소스에서 데이터를 받으십시오.

#### PartitionNotPresent: 파티션 정보가 손실되었습니다.

오류 보고 PartitionNotPresent의 오류 알림: 가져오기 한 미러 이미지가 불완전합니다. 미러 이미지 생성시 부트 파티션이 포함되어 있는지 확인하십시오.

#### RootPartitionNotFound: 루트 파티션이 손실되었습니다.

오류 보고 RootPartitionNotFound의 오류 알림: 가져오기 한 미러 이미지가 루트 파티션을 포함하는지 점검되지 않았습니다. 미러 이미지 파일을 점검한 뒤 이미 나타났던 원인은 다음을 참조하십시오.
* 설치 패키지 파일을 업로드했습니다.
* 데이터 디스크 미러 이미지를 업로드했습니다.
* 부트 파티션 미러 이미지를 업로드했습니다.
* 오류 파일을 업로드했습니다.

#### InternalError: 알 수 없는 오류입니다.

오류 보고 InternalError의 오류 알림: 가져온 미러 이미지 서비스에 오류 원인에 대한 기록이 없을 경우, 이런 문제는 고객서비스에 연락하십시오. 기술자가 최대한 빨리 문제를 해결해 줄 것입니다.

<a id="errorcode"></a>
## 에러코드
 
|에러코드|오류 원인|권장 처리 방식|
|-----|-----|-----|
|InvalidUrl|COS 무효 링크|COS 링크와 가져온 미러 이미지 링크가 같은지 검사하십시오.|
|InvalidFormatSize|형식 또는 크기가 조건에 부적합|미러 이미지가 [가져오기 준비](#가져오기 준비) 중 ‘미러 이미지 형식’과 ‘미러 이미지 크기’의 제한을 만족시켜야 합니다.|
|VirtioNotInstall|virtio 드라이버 미설치|미러 이미지에 virtio 드라이버를 설치해야 합니다. [가져오기 준비](#가져오기 준비)의 ‘드라이버’ 부분을 참조하십시오.|
|PartitionNotPresent|파티션 정보 손상|잘못된 생성 방식으로 나타난 미러 이미지 손상됩니다.|
|CloudInitNotInstalled|cloud-init 미설치|Linux 미러 이미지는 cloud-init 설치가 필요합니다. [가져오기 준비](#가져오기 준비) 중의 ‘드라이버’ 부분을 참조하십시오.|
|RootPartitionNotFound|루트 파티션 미점검|잘못된 생성 방식으로 나타난 미러 이미지 손상됩니다.|
|InternalError|기타 오류|고객서비스에 연락해 주십시오.|

