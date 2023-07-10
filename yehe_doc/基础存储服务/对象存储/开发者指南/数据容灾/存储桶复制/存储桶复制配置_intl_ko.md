## 적용 시나리오

버킷 복사 규칙 설정을 통해 객체 데이터를 원본 버킷에서 다른 특정 타깃 버킷으로 복사할 수 있습니다. 버킷 복사 기능은 원격 재해 복구, 업계 컴플라이언스 요건 충족, 데이터 마이그레이션 및 백업, 고객의 액세스 딜레이 단축, 서로 다른 리전의 클러스터에서의 편리한 데이터 액세스 등의 시나리오에 적용할 수 있습니다.

특수 시나리오:
- 다중 지역 백업: 원본 버킷에 대한 복사 규칙을 여러 개 설정하고 다른 리전의 버킷에 객체를 복사하여 다중 리전 백업을 수행할 수 있도록 지원합니다.
- 양방향 복사: 원본 버킷과 대상 버킷에 각각 복사 규칙을 생성하여 두 버킷의 양방향 복사를 지원하고 버킷 데이터의 동기화를 실현합니다.

>!버전 관리 기능 활성화 후 새로 업로드하는 객체에 여러 버전이 생성되고 스토리지 용량을 차지합니다. 따라서 해당 버전의 객체에 대해서도 스토리지 요금이 발생합니다.

## 사용 방법

### COS 콘솔 사용

COS 콘솔에서 버킷 복사 규칙을 설정할 수 있으며, 자세한 방법은 [버킷 복제 설정](https://intl.cloud.tencent.com/document/product/436/19235) 콘솔 가이드 문서를 참조하십시오.

### REST API 사용

직접 REST API를 사용하여 버킷에 대한 버킷 복사 규칙을 설정하고 관리할 수 있습니다. 자세한 내용은 다음의 API 문서를 참조하십시오.

- [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) 
- [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) 
- [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) 

### SDK 사용

직접 SDK의 버킷 복사 방법을 호출할 수 있으며, 자세한 내용은 다음 각 언어별 SDK 문서를 참조하십시오.

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/36196)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31519)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/12301)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/43245)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/30601)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37696)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/10199)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/35805)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/35859)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/34996)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31547)
