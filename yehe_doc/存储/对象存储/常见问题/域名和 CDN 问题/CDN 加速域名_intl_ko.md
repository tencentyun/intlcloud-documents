### COS에서 CDN은 어떻게 활성화하나요?

자세한 내용은 [사용자 정의 CDN 가속 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31506)를 참조하십시오.

### COS에서 CDN HTTPS Origin-pull COS를 지원하나요?

지원합니다. 자세한 작업 방법은 [Origin-pull 설정](https://intl.cloud.tencent.com/document/product/436/31508) 문서를 참조하십시오.

### COS와 CDN의 차이점은 무엇인가요?

COS와 CDN은 두 개의 서로 다른 제품입니다.

 [COS](https://intl.cloud.tencent.com/document/product/436/6222)는 Tencent Cloud가 제공하는 대용량 파일 저장용 분산형 스토리지 서비스입니다. 다양한 포맷의 파일을 업로드, 다운로드 및 관리할 수 있으며 대량의 데이터를 저장 및 관리할 수 있습니다.
[CDN](https://intl.cloud.tencent.com/document/product/228)은 전 세계에 분포한 고성능 가속 노드로 구성됩니다. 고성능 서비스 노드는 정해진 캐시 정책에 따라 비즈니스 콘텐츠를 저장합니다. 사용자가 비즈니스 콘텐츠에 대한 요청을 발송한 경우, 요청은 사용자와 가장 가까운 서비스 노드에 스케쥴링된 후 해당 노드에서 즉시 응답하므로 사용자의 액세스 딜레이를 줄이고 가용성을 높일 수 있습니다.

COS 서비스를 사용하면 CDN 기능을 활성화하지 않아도 됩니다. COS에서 CDN은 다음 시나리오에 적합합니다.
- 응답 딜레이를 줄이고 다운로드 속도를 높이려는 경우
- 지역, 국가, 대륙 간 GB~TB 용량의 데이터를 전송할 경우
- 같은 콘텐츠를 짧은 시간에 반복적으로 다운로드할 경우

자세한 소개는 [CDN 가속 개요](https://intl.cloud.tencent.com/document/product/436/18669)를 참조하십시오.

### 프런트 엔드 비즈니스에서 CDN과 임시 키 방식으로 COS의 콘텐츠에 액세스할 수 있나요?

CDN과 임시 키 방식의 COS 액세스는 지원하지 않습니다. COS 개인 읽기/쓰기 상태에서 CDN에 액세스하려는 경우, [CDN Origin-pull 인증](https://intl.cloud.tencent.com/document/product/436/18670)을 참조하십시오.

### CDN 가속을 통해 개인 읽기 버킷에 액세스할 수 있나요?

가능합니다. 단, 권한 관련 설정이 필요합니다. 자세한 설정 방법은 CDN 가속 개요 문서의 [개인 읽기 버킷](https://intl.cloud.tencent.com/document/product/436/18669#.E7.A7.81.E6.9C.89.E8.AF.BB.E5.AD.98.E5.82.A8.E6.A1.B6) 부분을 참조하십시오.


### COS 파일 업데이트(재업로드 또는 삭제) 시, CDN에 여전히 저장되어 있는 캐시 콘텐츠로 인해 원본 서버와 불일치하는 상황이 발생합니다. COS 업데이트 시 자동으로 CDN 캐시를 퍼지할 수 있나요?

COS 자체에서는 CDN 캐시 자동 퍼지를 지원하지 않지만, SCF로 CDN 캐시를 자동 퍼지할 수 있습니다. 자세한 내용은 [CDN 캐시 퍼지 설정](https://intl.cloud.tencent.com/document/product/436/37273) 문서를 참조하십시오.

### COS에서 CDN 가속 도메인을 사용해 파일을 업로드할 수 있나요?

CDN의 가속 도메인을 사용자 정의 도메인으로 파일 업로드 시나리오에 사용하는 것은 권장하지 않습니다. CDN은 원래 가속 업로드에 사용되지 않기 때문입니다. COS의 글로벌 가속 기능을 사용하면 데이터 업로드 가속 및 다운로드 가속이 가능합니다. [글로벌 가속 개요](https://intl.cloud.tencent.com/document/product/436/33409)를 참조하십시오.

### COS 자체에 CDN 기능이 있나요?

COS 자체에는 CDN 기능이 없으며 사용자가 직접 설정해야 합니다. 자세한 내용은 [사용자 정의 CDN 가속 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31506)를 참조하십시오.

