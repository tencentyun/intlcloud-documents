다음 문서는 오프라인 마이그레이션 사용 방법을 소개합니다.


## 작업 시나리오

서비스 마이그레이션은 기업이 운영 체제, 애플리케이션 및 애플리케이션 데이터를 원본 서버에서 클라우드 가상 머신(Cloud Virtual Machine, CVM)또는 클라우드 블록 스토리지(Cloud Block Storage, CBS)로 마이그레이션할 수 있도록 Tencent Cloud에서 개발한 플랫폼입니다. 클라우드화, 클라우드 간 마이그레이션, 계정 간 또는 리전 간 마이그레이션, 하이브리드 클라우드 배포에 대한 엔터프라이즈 요구 사항을 충족하는 데 도움이 됩니다.

서비스 마이그레이션에는 오프라인 마이그레이션과 온라인 마이그레이션이 포함됩니다. 오프라인 마이그레이션에는 다음이 포함됩니다.
- [오프라인 인스턴스 마이그레이션](#cvmStep)을 사용하면 시스템 디스크 이미지(또는 인스턴스에 마운트된 데이터 디스크도 마이그레이션하려는 경우 시스템 디스크 이미지 및 데이터 디스크 이미지)를 특정 CVM으로 마이그레이션할 수 있습니다.
- [오프라인 데이터 마이그레이션](#csmStep)을 사용하면 데이터 디스크 이미지를 특정 CBS로 마이그레이션할 수 있습니다.

## 전제 조건

오프라인 마이그레이션은 Tencent Cloud Object Storage(COS)가 필요하므로 귀하의 리전이 COS 지원 범위에 있는지 확인하십시오.
COS에서 지원하는 리전에 대한 자세한 내용은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오.

## 준비 사항


<dx-alert infotype="notice" title="">
- 현재 Tencent Cloud의 서비스 마이그레이션은 qcow2, vhd, vmdk, raw 형식의 이미지를 지원합니다. 압축된 이미지 형식을 사용하여 전송 및 마이그레이션 시간을 단축하시길 권장합니다.
- 이미지가 업로드되는 COS 리전은 마이그레이션하려는 CVM이 있는 위치와 동일해야 합니다.
- 시스템 디스크 이미지와 데이터 디스크 이미지를 동시에 가져와야 하는 경우 가져온 인스턴스를 해당 양의 데이터 디스크와 함께 마운트해야 합니다.
- 타깃 디스크 용량은 원본 디스크 용량보다 크거나(권장 사항에 따라) 같아야 합니다.
- 오프라인 마이그레이션은 \*-00000\*.vmdk와 유사한 파일 이름을 가진 스냅샷 파일의 마이그레이션을 지원하지 않습니다.
</dx-alert>



- 이미지 생성 문서의 지침에 따라 마이그레이션해야 하는 서버에 대한 이미지를 생성합니다.
  - Windows의 경우 [Windows 이미지 생성](https://intl.cloud.tencent.com/document/product/213/17815)을 참고하십시오.
  - Linux의 경우 [Linux 이미지 생성](https://intl.cloud.tencent.com/document/product/213/17814)을 참고하십시오.
- 생성된 이미지 파일을 COS에 업로드합니다.  
  - 이미지 파일의 크기가 크기 때문에 브라우저를 통한 업로드가 실패할 수 있습니다. COSCMD 도구를 사용하여 이미지를 업로드하는 것이 좋습니다. 자세한 내용은 [COSCMD 툴](https://intl.cloud.tencent.com/document/product/436/10976)을 참고하십시오.  
  - 다른 클라우드 플랫폼에서 내보낸 이미지가 압축된 패키지(예.tar.gz)인 경우 COS에 직접 업로드할 수 있습니다.
- 업로드된 이미지의 COS 주소를 얻습니다.
[COS 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 방금 업로드한 이미지 파일을 찾아 이미지 파일 상세 페이지의 임시 링크를 복사합니다.
- 마이그레이션할 CVM 및 CBS를 준비합니다.
  - [CVM 인스턴스 구매](https://buy.intl.cloud.tencent.com/cvm?regionId=5&projectId=-1)
  - [Purchase Instructions](https://intl.cloud.tencent.com/document/product/362/32414)


## 작업 단계
<dx-tabs>
::: 오프라인 인스턴스 마이그레이션[](id:cvmStep)
1. CVM 콘솔에 로그인한 뒤, 왼쪽 사이드바의 **[서비스 마이그레이션](https://console.cloud.tencent.com/cvm/csm/index?rid=4)**을 클릭합니다.
2. ‘오프라인 마이그레이션’ 페이지에서 **인스턴스 마이그레이션 생성**을 클릭합니다.
3. ‘오프라인 인스턴스 마이그레이션 생성’ 팝업 창에서 준비 단계를 완료하고 확인 후 **다음**을 클릭합니다.
4. 리전을 선택하고 작업 이름, COS 링크 및 마이그레이션할 CVM 인스턴스와 같은 구성 정보를 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7f3beecb92122f70f42fa86e652d35d9.png)
5. **완료**를 클릭하여 마이그레이션 작업을 만듭니다.
마이그레이션하는 동안 ‘[서비스 마이그레이션](https://console.cloud.tencent.com/cvm/csm/index?rid=4)’ 페이지를 종료하거나 닫을 수 있습니다. 또한 언제든지 이 페이지로 돌아와 작업 진행 상황을 확인할 수 있습니다. 



:::
::: 오프라인 데이터 마이그레이션[](id:csmStep)
1. CVM 콘솔에 로그인한 뒤, 왼쪽 사이드바의 **[서비스 마이그레이션](https://console.cloud.tencent.com/cvm/csm/index?rid=4)**을 클릭합니다.
2. ‘오프라인 마이그레이션’ 페이지에서 **데이터 마이그레이션 생성**을 클릭합니다.
3. ‘오프라인 데이터 마이그레이션 생성’ 팝업 창에서 준비 단계를 완료하고 확인 후 **다음**을 클릭합니다.
4. 리전을 선택하고 작업 이름, COS 링크 및 마이그레이션할 클라우드 디스크와 같은 구성 정보를 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7bf477c4a8811b1fe1395fa018762c25.png)
5. **완료**를 클릭하여 마이그레이션 작업을 만듭니다.
마이그레이션하는 동안 ‘[서비스 마이그레이션](https://console.cloud.tencent.com/cvm/csm/index?rid=4)’ 페이지를 종료하거나 닫을 수 있습니다. 또한 언제든지 이 페이지로 돌아와 작업 진행 상황을 확인할 수 있습니다. 


:::
</dx-tabs>

## FAQ
자세한 내용은 [서비스 마이그레이션](https://intl.cloud.tencent.com/document/product/213/32395)을 참고하십시오.





