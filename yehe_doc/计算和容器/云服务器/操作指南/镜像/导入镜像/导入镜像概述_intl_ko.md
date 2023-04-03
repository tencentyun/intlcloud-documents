[사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942) 기능 사용 외에도, Tencent Cloud는 가져오기 기능도 지원합니다. 로컬 또는 기타 플랫폼 서버 시스템 디스크의 미러 이미지 파일을 Cloud Virtual Machine(CVM)에 사용자 정의 이미지로 가져오기 할 수 있습니다. 가져오기 후 가져온 미러 이미지를 사용해 CVM를 생성하거나 이미 존재하는 CVM의 시스템을 재설치할 수 있습니다.


## 가져오기 준비[](id:importPreparation)

가져오기 조건에 부합하는 미러 이미지 파일을 미리 준비해야 합니다.

<dx-tabs>
::: Linux 시스템 유형 이미지 제한
<table>
<tr><th style="width:17%">이미지 속성</th><th>조건</th></tr>
<tr><td>운영 체제</td><td><ul><li>CentOS、CentOS Stream、Ubuntu、Debian、OpenSUSE、CoreOS、FreeBSD、AlmaLinux、Rocky Linux、Fedora、Kylin、UnionTech、TencentOS 버전을 기반으로 한 미러 이미지</li><li>32비트와 64비트를 지원합니다.</li></ul></td></tr>
<tr><td>미러 이미지 형식</td><td><ul><li>RAW, VHD, QCOW2, VMDK 미러 이미지 형식을 지원합니다.</li><li><code>qemu-img info imageName | grep 'file format'</code>을 사용하여 미러 이미지 형식을 조회합니다.</li></ul></td></tr>
<tr><td>파일 시스템 유형</td><td>GPT 파티션은 지원되지 않습니다.</td></tr>
<tr><td>미러 이미지 크기</td><td><ul><li>미러 이미지 실제 크기가 50G 이하인 경우 <code>qemu-img info imageName &#124; grep 'disk size'</code>를 사용해 실제 크기를 조회합니다.</li><li>미러 이미지 vsize가 500G 이하인 경우 <code>qemu-img info imageName &#124; grep 'virtual size'</code>를 사용해 미러 이미지 vsize를 조회합니다.</li></ul><b>주의 사항: </b>미러 이미지 가져오기 시 QCOW2 형식으로 전환한 후 미러 이미지 정보를 기준으로 심사합니다.</td></tr>
<tr><td>네트워크</td><td><ul><li>Tencent Cloud는 기본적으로 인스턴스에 <code>eth0</code> 네트워크 인터페이스를 제공합니다.</li><li>사용자는 인스턴스 내 metadata 서비스를 통해 인스턴스의 네트워크 구성을 쿼리할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/4934">인스턴스 메타데이터 조회</a>를 참고하십시오.</li></ul></td></tr>
<tr><td>드라이버</td><td><ul><li>미러 이미지는 반드시 버츄얼 플랫폼 KVM의 Virtio 드라이버를 설치해야 합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux 시스템 virtio 드라이버 점검</a>을 참고하십시오.</li><li>미러 이미지는 cloudinit을 설치해야 합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/12587">Linux 시스템에서 cloud-init 설치</a>를 참고하십시오.</li><li>다른 원인으로 cloudinit가 설치되지 않을 경우 <a href="https://intl.cloud.tencent.com/document/product/213/12849">이미지 강제 가져오기</a>를 참고하여 자체적으로 인스턴스를 설정하십시오.</li></ul></td></tr>
<tr><td>커널 제한</td><td>미러 이미지는 네이티브 커널일 때 가장 좋으며, 수정 시 CVM로 가져오기가 되지 않을 수 있습니다.</td></tr>
<tr><td>리전 제한</td><td>현재 상하이 금융 구역 및 선전 금융 구역은 다른 리전의 COS 서비스에서 이미지 가져오기를 지원하지 않습니다.</td></tr>
</table>

:::
::: Windows 시스템 유형 미러 이미지 제한
<table>
<tr><th style="width:16%">이미지 속성</th><th>조건</th></tr>
<tr><td>운영 체제</td><td><ul><li>Windows Server 2008 관련 버전, Windows Server 2012 관련 버전, Windows Server 2016 관련 버전, Windows Server 2019 관련 버전, Windows Server 2022 관련 버전</li><li>32비트와 64비트를 지원합니다.</li></ul></td></tr>
<tr><td>미러 이미지 형식</td><td><ul><li>RAW, VHD, QCOW2, VMDK 미러 이미지 형식을 지원합니다.</li><li><code>qemu-img info imageName | grep 'file format'</code>을 사용하여 미러 이미지 형식을 조회합니다.</li></ul></td></tr>
<tr><td>파일 시스템 유형</td><td><ul><li>MBR 파티션을 사용한 NTFS 파일 시스템만 지원합니다.</li><li>GPT 파티션은 지원되지 않습니다.</li><li>논리 볼륨 관리(LVM)는 지원되지 않습니다.</li></ul></td></tr>
<tr><td>미러 이미지 크기</td><td><ul><li>미러 이미지 실제 크기가 50G 이하인 경우 <code>qemu-img info imageName &#124; grep 'disk size'</code>를 사용해 실제 크기를 조회합니다.</li><li>미러 이미지 vsize가 500G 이하인 경우 <code>qemu-img info imageName &#124; grep 'virtual size'</code>를 사용해 미러 이미지 vsize를 조회합니다.</li></ul><b>주의 사항:</b> 미러 이미지 가져오기 시 qcow2 형식 전환 후 미러 이미지 정보를 기준으로 심사합니다.</td></tr>
<tr><td>네트워크</td><td><ul><li>Tencent Cloud는 기본적으로 인스턴스에 <code>로컬 연결</code> 네트워크 인터페이스를 제공합니다.</li><li>사용자는 인스턴스 내 metadata 서비스를 통해 인스턴스의 네트워크 구성을 쿼리할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/4934">인스턴스 메타데이터</a>를 참고하십시오.</li></ul></td></tr>
<tr><td>드라이버</td><td>이미지는 버츄얼 플랫폼 KVM의 Virtio 드라이버가 설치되어야 합니다. Windows 시스템은 기본적으로 Virtio 드라이버를 설치하지 않으며 사용자는 Windows Virtio 드라이버를 설치하고 로컬 이미지를 내보낼 수 있습니다. Windows Virtio 드라이버 다운로드 주소는 다음과 같으며 실제 네트워크 환경에 따라 다운로드하십시오. <ul><li>공용 네트워크 다운로드 주소: <code>http://mirrors.tencent.com/install/windows/virtio_64_1.0.9.exe</code></li><li>내부 네트워크 다운로드 주소: <code>http://mirrors.tencentyun.com/install/windows/virtio_64_1.0.9.exe</code></li></ul></td></tr>
<tr><td>리전 제한</td><td>현재 상하이 금융 구역 및 선전 금융 구역은 다른 리전의 COS 서비스로부터 이미지 가져오기를 지원하지 않습니다.</td></tr>
<tr><td>기타</td><td>가져오기한 Windows 시스템 미러 이미지는 <a href="https://intl.cloud.tencent.com/document/product/213/2757">Windows 활성화</a> 서비스가 <b>제공되지 않습니다.</b></td></tr>
</table>

:::
</dx-tabs>


## 가져오기 단계

 1. [CVM](https://console.cloud.tencent.com/cvm/instance/index?rid=19) 콘솔에 로그인한 뒤, 왼쪽 사이드바의 **[이미지](https://console.cloud.tencent.com/cvm/image)** 를 클릭합니다.
 3. **사용자 정의 이미지**를 선택하고,**이미지 가져오기**를 클릭합니다.
 4. 작업 인터페이스 요구에 따라 먼저 [COS 활성화](https://console.cloud.tencent.com/cos4/index) 후, [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)합니다. 이미지 파일을 bucket에 [객체 업로드](https://www.tencentcloud.com/document/product/436/13321)하고 [이미지 파일 URL 가져오기](https://intl.cloud.tencent.com/document/product/436/13322)합니다.
 5. **다음**을 클릭합니다.
 6. 실제 상황에 따라 서식을 입력하고 **가져오기 시작**을 클릭합니다.
<dx-alert infotype="notice" title="">
입력한 COS 파일 URL이 정확한지 확인하십시오.
</dx-alert>
가져오기 성공 혹은 실패 여부는 <a href="https://console.cloud.tencent.com/message">내부 메시지</a> 형식으로 알림이 발송됩니다.

## 가져오기 실패

콘솔에서 미러 이미지 가져오기 작업 진행 후, 여러 이유로 작업이 실패할 수 있습니다. 작업 실패 상태에서는 아래의 내용에 따라 조사하십시오.

### 주의 사항

실패 원인에 대한 파일 조사 전 [내부 메시지 관리 페이지](https://console.cloud.tencent.com/messageCenter/messageConfig) 소식 구독란의 구독 제품 서비스와 관련된 알림을 확인하십시오. 실패 원인이 포함된 내부 메시지, SMS와 메일 수신을 제공합니다.


<dx-alert infotype="notice" title="">
메시지 센터에서 제품 서비스 관련 정보를 구독하지 않은 경우, 가져오기 성공/실패 내부 메시지를 받을 수 없습니다.
</dx-alert>



### 실패 원인 진단

다음 내용을 참고하여 해당 오류 메시지의 문제 해결을 진행할 수 있습니다. 자세한 오류 안내 및 오류 설명은 [오류 코드](#errorcode)를 참고하십시오.


<dx-accordion>
::: InvalidUrl: COS 링크 무효입니다.
오류 보고 InvalidUrl의 오류 알림: 미러 이미지 가져오기 페이지에 잘못된 COS 링크를 입력했습니다. 예상되는 원인은 아래와 같습니다.
* [Tencent Cloud COS](https://console.cloud.tencent.com/cos4/index)의 미러 이미지 링크가 아닌 것을 입력했습니다.
* COS의 객체 주소는 공개 읽기 및 개인 쓰기 권한이 없습니다.
* COS 파일의 액세스 권한이 사유 읽기이지만, 서명이 유효하지 않습니다.
<dx-alert infotype="notice" title="">
서명이 포함된 COS 파일 링크는 1회만 액세스 가능합니다.
</dx-alert>
* 중국 외 리전에서 이미지 가져오기 시 외부 리전의 COS 링크를 사용하였습니다.
<dx-alert infotype="notice" title="">
현재 중국 외 리전에서 이미지 가져오기 서비스는 동일 리전 COS 서버만 지원하므로 리전 내 COS 링크를 통해 가져와야 합니다.
</dx-alert>
* 사용자의 미러 이미지 파일이 삭제되었습니다.
COS 무효 링크에 대한 오류 보고를 받은 후, 서술된 원인에 따라 문제를 조사할 수 있습니다.
:::
::: InvalidFormatSize: 형식 또는 크기가 조건에 부합하지 않습니다.
오류 보고 InvalidFormatSize의 오류 알림: 가져오기 한 미러 이미지의 형식 또는 크기가 Tencent Cloud의 미러 이미지 가져오기 기능 제한과 부합하지 않습니다. 제한은 아래와 같습니다.
* 이미지 가져오기는 ‘qcow2’, ‘vhd’, ‘vmdk’, ‘raw’ 네 종류의 이미지 파일 형식을 지원합니다.
* 가져오기 미러 이미지의 실제 파일 크기는 50GB를 초과할 수 없습니다(qcow2 형식으로 전환한 미러 이미지 파일 기준).
* 가져오기 미러 이미지의 시스템 디스크 크기는 500GB를 초과할 수 없습니다.

형식 또는 크기가 조건에 부합하지 않는다는 오류 보고를 받는 경우
- [Linux 이미지 생성](https://intl.cloud.tencent.com/document/product/213/17814)의 미러 이미지 형식 전환 콘텐츠에 따라 미러 이미지 파일을 적합한 파일 형식으로 전환할 수 있습니다. 간단한 미러 이미지 콘텐츠로 크기 제한을 만족시킨 후 다시 미러 이미지를 가져오기 할 수 있습니다.
- 또한 [오프라인 인스턴스 마이그레이션](https://intl.cloud.tencent.com/document/product/213/19233) 기능을 사용할 수 있습니다. 최대 500GB의 이미지 파일 마이그레이션을 지원합니다.
:::
::: VirtioNotInstall: Virtio 드라이버가 설치되지 않았습니다.
오류 보고 VirtioNotInstall의 오류 알림: 가져온 미러 이미지에 Virtio 드라이버가 설치돼 있지 않습니다. Tencent Cloud의 KVM 버츄얼화 기술은 사용자가 가져오기 한 미러 이미지 내에 virtio 드라이버가 설치되어 있기를 요구합니다. 일부 사용자 정의 Linux 운영 체제 외에, 대부분의 Linux 운영 체제는 이미 Virtio 드라이버가 설치되어 있습니다. Windows 운영 체제는 사용자가 수동으로 Virtio 드라이버를 설치해야 합니다.
* Linux 미러 이미지 가져오기는 [Linux 시스템 virtio 드라이버 점검](https://intl.cloud.tencent.com/document/product/213/9929) 문서를 참고하십시오.
* Windows 미러 이미지 가져오기는 [Windows 이미지 생성](https://intl.cloud.tencent.com/document/product/213/17815)을 참고하여 Virtio 드라이버를 설치할 수 있습니다.
:::
::: CloudInitNotInstalled: cloud-init 프로그램이 설치되지 않았습니다.
오류 보고 CloudInitNotInstalled의 오류 알림: 가져오기 한 미러 이미지에 cloud-init 프로그램이 설치되어 있지 않습니다. Tencent Cloud는 오픈 소스 프로그램 cloud-init을 사용해 CVM을 초기화합니다. 그러므로 cloud-init 프로그램 미설치 시 사용자의 CVM 초기화가 실패합니다.
* Linux 미러 이미지 가져오기는 [Linux 시스템에서 cloud-init 설치](https://intl.cloud.tencent.com/document/product/213/12587) 문서를 참고하십시오.
* Windows 미러 이미지 가져오기는 [Windows 운영 체제에서 Cloudbase-init 설치](https://intl.cloud.tencent.com/document/product/213/32364) 문서를 참고하십시오.
* cloud-init/cloudbase-init 설치 후, 파일 구성 교체 문서에 따라 사용 가능한 CVM을 시작할 경우, 정확한 데이터 소스에서 데이터를 받으십시오.
:::
::: PartitionNotPresent: 파티션 정보가 손실되었습니다.
오류 보고 PartitionNotPresent의 오류 알림: 가져오기 한 미러 이미지가 불완전합니다. 미러 이미지 생성 시 부트 파티션이 포함되어 있는지 확인하십시오.
:::
::: RootPartitionNotFound: 루트 파티션이 손실되었습니다.
오류 보고 RootPartitionNotFound의 오류 알림: 가져오기 한 미러 이미지가 루트 파티션을 포함하는지 점검되지 않았습니다. 미러 이미지 파일을 점검한 뒤 이미 나타났던 원인은 다음을 참고하십시오.
* 설치 패키지 파일을 업로드했습니다.
* 데이터 디스크 미러 이미지를 업로드했습니다.
* 부트 파티션 미러 이미지를 업로드했습니다.
* 오류 파일을 업로드했습니다.
:::
::: InternalError: 알 수 없는 오류입니다.
오류 보고 InternalError의 오류 알림: 가져온 미러 이미지 서비스에 오류 원인에 대한 기록이 없을 경우, 이런 문제는 고객서비스에 연락하십시오. 기술자가 최대한 빨리 문제를 해결해 줄 것입니다.
:::
</dx-accordion>



## 오류 코드[](id:errorcode)
 
|오류 코드|오류 원인|권장 처리 방식|
|-----|-----|-----|
|InvalidUrl|COS 무효 링크|COS 링크와 가져온 미러 이미지 링크가 같은지 검사하십시오.|
|InvalidFormatSize|형식 또는 크기가 조건에 부적합|미러 이미지가 [가져오기 준비](https://www.tencentcloud.com/document/product/213/4945#.E5.AF.BC.E5.85.A5.E5.87.86.E5.A4.87.3Ca-id.3D.22importpreparation.22.3E.3C.2Fa.3E) 중 ‘미러 이미지 형식’과 ‘미러 이미지 크기’의 제한을 만족시켜야 합니다.|
|VirtioNotInstall|virtio 드라이버 미설치|미러 이미지에 virtio 드라이버를 설치해야 합니다. [가져오기 준비](https://www.tencentcloud.com/document/product/213/4945#.E5.AF.BC.E5.85.A5.E5.87.86.E5.A4.87.3Ca-id.3D.22importpreparation.22.3E.3C.2Fa.3E)의 ‘드라이버’ 부분을 참고하십시오.|
|PartitionNotPresent|파티션 정보 손상|잘못된 생성 방식으로 나타난 미러 이미지 손상됩니다.|
|CloudInitNotInstalled|cloud-init 미설치|Linux 미러 이미지는 cloud-init 설치가 필요합니다. [가져오기 준비](https://www.tencentcloud.com/document/product/213/4945#.E5.AF.BC.E5.85.A5.E5.87.86.E5.A4.87.3Ca-id.3D.22importpreparation.22.3E.3C.2Fa.3E) 중의 ‘드라이버’ 부분을 참고하십시오.|
|RootPartitionNotFound|루트 파티션 미점검|잘못된 생성 방식으로 나타난 미러 이미지 손상됩니다.|
|InternalError|기타 오류|고객서비스에 연락해 주십시오.|

