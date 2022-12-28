## 소개

다양한 시나리오에서 비즈니스 요구 사항을 충족하기 위해 언제든지 콘솔을 통해 COS에 업로드된 객체의 스토리지 유형을 수정할 수 있습니다. COS는 STANDARD(다중 AZ), STANDARD IA(다중 AZ), INTELLIGENT TIERING, STANDARD, STANDARD IA, ARCHIVE 및 DEEP ARCHIVE를 비롯한 다양한 스토리지 유형을 제공합니다. 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오. 다음 섹션에서는 객체의 스토리지 유형을 수정하는 방법을 안내합니다.

> ?
> - 객체가 STANDARD(다중 AZ) 또는 STANDARD IA(다중 AZ) 유형인 경우 스토리지 유형을 STANDARD IA 또는 CAS 유형으로 전환하는 것은 현재 지원되지 않습니다.
> - **ARCHIVE/DEEP ARCHIVE**에 저장된 객체의 스토리지 유형을 수정하려면 먼저 STANDARD로 복원해야 합니다. 자세한 내용은 [아카이브된 객체 복구](https://intl.cloud.tencent.com/document/product/436/30961)를 참고하십시오.
> - 5GB 이상 객체는 스토리지 유형 수정을 지원하지 않습니다.

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭합니다.
3. 객체가 속한 버킷을 찾아 해당 버킷 이름을 클릭합니다.
4. 왼쪽 사이드바에서 **파일 리스트**를 클릭합니다.
5. 대상 객체를 찾고 오른쪽의 작업 열에서 **더 보기 > 스토리지 유형 수정**을 클릭합니다.

여러 객체의 스토리지 유형을 일괄 수정하려면 여러 객체를 선택하고 상단의 **추가 작업 > 스토리지 유형 수정**을 클릭합니다.

6. 대상 스토리지 유형을 선택하고 팝업 창에서 **확인**을 클릭합니다.
