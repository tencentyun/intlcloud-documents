### 이미지란 무엇인가요?
이미지란 일종의 CVM 소프트웨어의 구성(운영 체제, 사전 설치 프로그램 등) 템플릿입니다. Tencent Cloud에서는 이미지를 통해 인스턴스를 실행하시길 권장하고 있습니다. 이미지를 통해 여러 개의 인스턴스를 실행할 수 있으며, 여러 번 다시 사용할 수도 있습니다. 이미지에 대한 자세한 내용은 [이미지 개요](https://intl.cloud.tencent.com/document/product/213/4940)를 참조 바랍니다.

### 이미지를 가져오기 전에 어떤 준비 과정이 필요한가요?
이미지를 가져오기 전에, 권한 신청과 이미지 파일 준비를 완료해야 합니다. 자세한 작업 방식은 [이미지 가져오기 개요](https://intl.cloud.tencent.com/document/product/213/4945)를 참조 바랍니다.

### 이미지를 로컬로 내보낼 수 있는지 테스트하려면 어떻게 해야 하나요?
> 현재 Tencent Cloud 서비스에서 마이그레이션을 지원하는 이미지 형식에는 qcow2, vhd, raw, vmdk가 있습니다.
VMWare vCenter Convert나 Citrix XenConvert 등 가상화 플랫폼의 이미지 내보내기 툴을 사용하여 이미지를 내보낼 수 있으며, 자세한 내용은 각 플랫폼의 내보내기 툴 문서를 참조 바랍니다. 또, [disk2vhd를 사용하여 이미지 내보내기(Windows)](https://intl.cloud.tencent.com/document/product/213/17815)나 [명령어를 사용하여 이미지 내보내기(Linux)](https://intl.cloud.tencent.com/document/product/213/17814)도 가능합니다.

### CVM 인스턴스 생성에 사용한 사용자 정의 이미지를 삭제할 수 있나요?
사용자 정의 이미지를 삭제하면 해당 이미지로는 더 이상 인스턴스를 생성할 수 없지만, 이미 실행 중인 인스턴스에는 영향을 주지 않습니다. 해당 이미지로 실행 중인 모든 인스턴스를 삭제하려면 [인스턴스 회수](https://intl.cloud.tencent.com/document/product/213/4931) 및 [인스턴스 폐기/반환](https://intl.cloud.tencent.com/document/product/213/4930)을 참조 바랍니다.

### 다른 계정에 공유한 특정 사용자 정의 이미지를 삭제할 수 있나요?
공유 중인 이미지는 삭제할 수 없으며, 모든 공유를 취소한 후에 삭제할 수 있습니다. 이미지 공유를 취소하려면 [사용자 정의 이미지 공유 취소](https://intl.cloud.tencent.com/document/product/213/7148)를 참조 바랍니다.


