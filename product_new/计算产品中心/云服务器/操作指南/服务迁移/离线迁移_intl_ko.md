## 작업 시나리오

서비스 마이그레이션은 Tencent Cloud가 기업 사용자의 클라우드에 쉽게 액세스할 수 있도록 연구 개발한 마이그레이션 플랫폼입니다. 해당 마이그레이션 플랫폼은 소스 단말기 호스트의 운영 체제, 애플리케이션 및 애플리케이션 데이터 등을 Tencent Cloud CVM(Cloud Virtual Machine) 및 CBS(Cloud Block Storage) 마이그레이션하여 기업의 클라우드 액세스, 클라우드 플랫폼 간의 마이그레이션, 계정/지역 간의 마이그레이션 및 하이브리드 클라우드 배포 등 업무 수요를 실현합니다.

서비스 마이그레이션은 현재 오프라인 마이그레이션 및 온라인 마이그레이션을 포함하며 이 중에서 오프라인 마이그레이션은 다음과 같이 두 가지가 있습니다：
- [오프라인 인스턴스 마이그레이션](#cvmStep)，시스템 디스크 미러 이미지를 지정된 CVM으로 이동합니다.
- [오프라인 데이터 마이그레이션](#csmStep)，데이터 디스크 미러 이미지를 지정된 CVM으로 이동합니다.

## 전제 조건

오프라인 마이그레이션은 Tencent Cloud의 오브젝트 스토리지(Cloud Object Storage, COS)의 지원이 필요하므로 위치한 리전이 COS 지원 범위에 있는지 확인하십시오.
현재 COS가 지원하는 리전 범위는 [도메인 이름 리전 및 액세스](https://intl.cloud.tencent.com/document/product/436/6224)에서 참조하십시오.

## 준비 사항

> 
> 현재 Tencent Cloud의 서비스 마이그레이션에서 지원하는 미러 이미지 형식은 qcow2, vhd, vmdk 및 raw입니다. 압축된 미러 이미지 형식을 사용하여 전송 및 마이그레이션 시간을 절약할 것을 권장합니다.
> - 업로드된 미러 이미지의 COS 리전은 이동된 CVM 리전과 일치해야 합니다.
> - 오프라인 마이그레이션 시 업로드된 미러 이미지 파일은 이동할 디스크 용량보다 작아야 합니다. 미러 이미지 파일이 50G인 경우 이동할 인스턴스의 시스템 디스크는 최소 50G 입니다.

- 미러 이미지의 문서 생성에 따라 마이그레이션 서버의 미러 이미지 파일을 생성하십시오.
 - Windows 시스템인 경우 [Windows 미러 이미지 문서 생성](https://intl.cloud.tencent.com/document/product/213/17815)을 참조하십시오.
 - Linux 시스템인 경우 [Linux 미러 이미지 문서 생성](https://intl.cloud.tencent.com/document/product/213/17814)을 참조하십시오.
- 생성한 미러 이미지 파일을 COS에 업로드합니다.  
 - 미러 이미지 문서는 비교적 커서 웹 페이지에 업로드할 때 끊기기 쉬우므로 COSCMD를 사용하여 미러 이미지 업로드를 권장합니다. 작업에 대한 자세한 내용은 [COSCMD 툴 문서](https://intl.cloud.tencent.com/document/product/436/10976)를 참조하십시오.  
 - 다른 클라우드 플랫폼에서 내보낸 미러 이미지가 압축 패키지 형식(예.tar.gz）이면 압축을 해제하지 않고 직접 COS에 업로드 및 마이그레이션하면 됩니다.
- 미러 이미지에 업로드한 COS 주소를 가져옵니다.
[COS 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 방금 업로드한 미러 이미지 파일을 찾아 파일 정보를 조회하고 파일 링크를 가져옵니다.
- 마이그레이션할 CVM 및 CBS를 준비합니다.
[CVM 구매 클릭>>](https://buy.cloud.tencent.com/cvm?tab=custom&step=1®ionId=8)
[CBS 구매 가이드는 클릭>>](https://cloud.tencent.com/document/product/362/2732)


## 작업 순서

<span id="cvmStep"></span>
### 오프라인 인스턴스 마이그레이션

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/overview)에 로그인하십시오.
2. 왼쪽 사이드 바에서 [서비스 마이그레이션]>[[오프라인 인스턴스 마이그레이션](https://console.cloud.tencent.com/csm/cvm)]을 클릭하십시오.
3. [생성]을 클릭하십시오.
4. 이동 준비 확인 및 완료되면 [다음 단계]를 클릭하십시오.
5. 작업 이름, COS 링크 및 마이그레이션할 CVM 등 마이그레이션 구성 정보를 입력하고[완료]를 클릭하면 마이그레이션 작업을 성공적으로 완료합니다. 아래 이미지를 참조하십시오.
>  
> - COS 파일을 먼저 [공개 읽기 및 개인 쓰기 권한](https://intl.cloud.tencent.com/document/product/436/13327)으로 설정해야 합니다.
> - 마이그레이션한 인스턴스의 시스템 디스크 용량이 업로드한 미러 이미지 파일 크기보다 작으면 작업은 실패할 수 있습니다.
>   오프라인 데이터 마이그레이션 관리 페이지로 돌아가면 마이그레이션 작업 프로그레스를 조회할 수 있습니다. 아래 이미지를 참조하십시오.


<span id="csmStep"></span>
### 오프라인 데이터 마이그레이션

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/overview)에 로그인하십시오.
2. 왼쪽 사이드 바에서 [서비스 마이그레이션]>[[오프라인 데이터 마이그레이션](https://console.cloud.tencent.com/csm/cbs?rid=1)]을 클릭하십시오.
3. [생성]을 클릭하십시오.
4. 이동 준비 확인 및 완료되면 [다음 단계]를 클릭하십시오.
5. 작업 이름, COS 링크 및 마이그레이션할 CBS 등 마이그레이션 구성 정보를 입력하고[완료]를 클릭하면 마이그레이션 작업을 성공적으로 완료합니다. 아래 이미지를 참조하십시오.
> 마이그레이션한 CBS 용량이 업로드한 미러 이미지 파일 크기보다 작으면 작업이 실패할 수 있습니다.
>

## FAQ

자세한 내용은 [서비스 마이그레이션 유형](https://cloud.tencent.com/document/product/213/32962)을 참조하십시오.

