## 소개

INTELLIGENT TIERING 유형은 데이터에 핫/콜드 티어링 메커니즘을 구분해 사용자 데이터의 액세스 모드에 따라 자동으로 데이터의 콜드/핫 레이어를 전환함으로써 사용자 데이터의 스토리지 비용을 줄일 수 있습니다.

INTELLIGENT TIERING은 액세스 모드가 가변적이거나 데이터의 액세스 모드를 예측할 수 없는 경우에 활용할 수 있습니다. 표준 스토리지와 동일한 수준의 낮은 딜레이와 높은 처리량을 제공하지만, 비용은 표준 스토리지보다 저렴합니다. 비즈니스 요구사항에 맞춰 액세스 모드가 가변적인 데이터를 표준 스토리지 유형에서 INTELLIGENT TIERING 유형으로 전환하여 클라우드 내 스토리지 비용을 절약할 수 있습니다.

> !
> - INTELLIGENT TIERING 유형은 현재 베이징, 상하이, 광저우, 충칭, 도쿄 리전만 지원합니다.
>- INTELLIGENT TIERING 유형은 독립적인 스토리지 유형입니다. 사용 시 INTELLIGENT TIERING 용량 요금이 발생하므로 INTELLIGENT TIERING 용량 패키지를 선택해 요금을 차감할 수 있습니다. 자세한 과금 정보는 [제품 가격](https://buy.cloud.tencent.com/price/cos)을 참조하십시오.

## 장점

사용자가 데이터를 업로드할 때 INTELLIGENT TIERING 유형을 선택해 COS에 보관할 경우, COS는 주기적으로 데이터 액세스 횟수를 모니터링하며 데이터 액세스가 일정 기간 지속되지 않을 경우 데이터를 스토리지 비용이 더 저렴한 액세스 레이어로 이동합니다. 데이터가 다시 액세스되면, 다시 고빈도 액세스 레이어로 이동해 데이터 읽기 성능을 보장합니다. 데이터 핫/콜드 티어링 스토리지를 통해 사용자는 스토리지 비용을 고려하여 읽기 성능을 적절히 선택할 수 있습니다. INTELLIGENT TIERING은 다음과 같은 장점이 있습니다.

- **비용 절감**: 데이터를 지속적으로 INTELLIGENT TIERING 유형으로 저장할 경우, 저장 시간이 길어질수록 표준 스토리지 비용은 상대적으로 낮아져 최대 20% 정도의 스토리지 비용을 절약할 수 있습니다. INTELLIGENT TIERING 유형은 객체 스토리지 라이프사이클 프로세스에 관여하므로, 사용자는 필요에 따라 INTELLIGENT TIERING을 CAS로 전환해 데이터 저장 비용을 더 낮출 수 있습니다.
- **지속적 안정화**: INTELLIGENT TIERING은 표준 스토리지와 동일한 짧은 딜레이 시간, 높은 처리량의 체험을 제공합니다. 또한 이레이저 코딩의 중복 스토리지 방식을 택하여 99.999999999%(11개의 9)의 데이터 신뢰성을 제공하며, 데이터 멀티파트 스토리지, 동시 읽기/쓰기 등 99.95%의 비즈니스 가용성을 제공합니다. 다중AZ 아키텍처는 INTELLIGENT TIERING의 특성을 동기화하여 99.9999999999%(12개의 9)의 데이터 설계 신뢰성과 99.995%의 비즈니스 설계 가용성을 자랑합니다.
- **편리한 사용**: 데이터에 객체 스토리지 유형만 지정하면 INTELLIGENT TIERING의 특징을 적용할 수 있습니다. 일종의 스토리지 유형인 INTELLIGENT TIERING은 COS의 API, SDK, 툴 및 생태 애플리케이션에 자연스럽게 결합되어 필요에 따라 클라우드에 저장된 데이터를 쉽게 관리할 수 있도록 지원합니다.

## 사용 방법

데이터를 INTELLIGENT TIERING 유형으로 COS에 저장하려면 먼저 버킷의 INTELLIGENT TIERING 설정을 활성화해야 합니다. 활성화 후, 사용자가 객체를 업로드할 때 **스토리지 유형**을 INTELLIGENT TIERING 유형으로 지정하면 됩니다.

### COS 콘솔 사용

#### 객체 업로드 시 INTELLIGENT TIERING으로 설정

다음 단계를 참고하여 객체를 INTELLIGENT TIERING 유형으로 저장할 수 있습니다.

1. 버킷 설정 페이지에서 INTELLIGENT TIERING 설정을 활성화합니다. 자세한 내용은 [INTELLIGENT TIERING 설정](https://intl.cloud.tencent.com/document/product/436/38306) 문서를 참조하십시오.
2. 파일 업로드 시 CFS 유형을 지정합니다. 파일의 업로드 가이드는 [객체 업로드](https://intl.cloud.tencent.com/document/product/436/13321) 문서를 참조하십시오.

> !버킷의 INTELLIGENT TIERING 설정 활성화 후에는 비활성화할 수 없으니 신중하게 설정하십시오.

#### 클라우드 상의 데이터를 INTELLIGENT TIERING으로 전환

다음 단계를 참고하여 업로드된 기존 저장 콘텐츠 데이터를 INTELLIGENT TIERING 유형으로 전환할 수 있습니다.

1. 버킷 설정 페이지에서 라이프사이클 규칙을 생성합니다. 자세한 내용은 [라이프사이클 설정](https://intl.cloud.tencent.com/document/product/436/14605) 문서를 참조하십시오.
2. 지정된 규칙의 응용 범위를 설정하고 데이터를 INTELLIGENT TIERING으로 전환합니다.



### REST API 사용

다음 API를 통해 INTELLIGENT TIERING을 직접 설정할 수 있습니다.

1. 먼저 REST API를 사용해 버킷의 INTELLIGENT TIERING을 활성화합니다. 다음 API 문서를 참조하십시오.
	- [PUT Bucket IntelligentTiering](https://intl.cloud.tencent.com/document/product/436/38314)
	- [GET Bucket IntelligentTiering](https://intl.cloud.tencent.com/document/product/436/38315)
2. 버킷에 INTELLIGENT TIERING이 활성화되면, 다음 API 문서를 참조하여 객체를 INTELLIGENT TIERING 유형으로 업로드할 수 있습니다.
	- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
	- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)
	- [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)
	- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
3. 객체의 스토리지 유형 및 속한 스토리지 레이어를 조회해야 할 경우, 다음 API 문서를 참조하십시오.
	- [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)
	- [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745)
4. REST API를 직접 사용하여 INTELLIGENT TIERING 유형의 객체를 삭제할 수 있습니다. 다음 API 문서를 참조하십시오.
	- [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)
	- [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289)

### SDK 사용

현재 COS에서 배포하는 SDK는 모두 INTELLIGENT TIERING 유형을 지원합니다. 구체적인 방법은 파일 업로드 시, StorageClass 매개변수를 INTELLIGENT_TIERING으로 설정하여 다이렉트 업로드 INTELLIGENT TIERING을 구현하는 것입니다. 자세한 내용은 [SDK 개요](https://intl.cloud.tencent.com/document/product/436/6474)를 참조하십시오.



## 사용 제한

INTELLIGENT TIERING 사용에는 다음과 같은 제한이 있습니다.

- **설정 제한**: 초기 설정 후 변경이 불가능합니다. 변경이 필요한 경우 [고객센터](https://intl.cloud.tencent.com/contact-sales)로 문의하십시오.
- **초기 스토리지 레이어 제한**: INTELLIGENT TIERING 유형의 신규 객체는 기본적으로 고빈도 액세스 레이어에 저장됩니다. 일정 기간 동안 액세스가 없는 상태가 지속되어야만 저빈도 액세스 레이어로 전환됩니다.
- **최단 저장 시간제한**: INTELLIGENT TIERING 유형의 객체는 최단 저장 시간이 30일로, 30일 이하는 30일로 과금됩니다.
- **최소 스토리지 단위 제한**: 64KB 이하 객체는 고빈도 액세스 레이어에 영구 저장되며, 고빈도 액세스 레이어와 저빈도 액세스 레이어 간 전환은 불가합니다.
- **작업 제한**: 추가 업로드 인터페이스 통해 객체를 INTELLIGENT TIERING 유형으로 업로드하는 기능은 지원하지 않습니다.
- **라이프사이클 제한**: INTELLIGENT TIERING 유형은 CAS 또는 DEEP ARCHIVE 유형으로만 전환될 수 있습니다. 표준 스토리지 유형이 INTELLIGENT TIERING 유형으로 전환될 때는 고빈도 액세스 레이어에 저장되며, 표준IA 스토리지 유형이 INTELLIGENT TIERING 유형으로 전환될 때는 표준IA 스토리지 액세스 레이어에 저장됩니다.
- **버킷 복사 제한**: 버킷 복사 시, 타깃 버킷의 INTELLIGENT TIERING 설정이 활성화되지 않았을 경우 객체를 INTELLIGENT TIERING 유형으로 복사할 수 없습니다.
