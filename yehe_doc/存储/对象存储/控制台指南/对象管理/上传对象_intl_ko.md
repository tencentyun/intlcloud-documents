## 소개

COS 콘솔로 버킷의 파일 리스트 페이지에 객체를 업로드할 수 있습니다. 객체 관련 설명은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오.

>?
> - 현재 MAZ(다중 AZ) 구성은 베이징, 상하이, 광저우 및 싱가포르 리전에서만 사용할 수 있습니다. MAZ_STANDARD와 같은 MAZ 스토리지 클래스에 객체를 업로드하려면 먼저 리전의 버킷에 대해 [Multi-AZ Feature](https://intl.cloud.tencent.com/document/product/436/35208)를 활성화하십시오.
> - 현재 INTELLIGENT TIERING 유형은 베이징, 난징, 상하이, 광저우, 청두, 충칭, 도쿄, 싱가포르 리전만 지원합니다. 해당 유형을 업로드하려면 우선 해당 리전의 버킷 [INTELLIGENT TIERING 설정](https://intl.cloud.tencent.com/document/product/436/38306)을 활성화하십시오.
> - 현재 DEEP ARCHIVE 유형은 베이징, 난징, 상하이, 광저우, 청두, 충칭, 도쿄 및 싱가포르 리전에서만 사용할 수 있습니다. 이 스토리지 유형에 객체를 업로드하려면 먼저 리전에서 버킷을 선택하십시오.
> 

## 전제 조건

객체 업로드 전 생성된 버킷을 확보하십시오. 생성된 버킷이 없을 경우 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 문서를 참고해 작업을 진행하십시오.

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭합니다.
3. 대상 버킷을 클릭하여 파일 목록 페이지로 이동합니다.
4. 파일 목록에서 **파일 업로드**를 클릭합니다.
![](https://main.qcloudimg.com/raw/1f499717168f5559337899f635e19a13.png)
5. 팝업 창에서 **파일 선택** 또는 **폴더 선택**을 클릭하고 필요에 따라 하나 이상의 로컬 파일(또는 폴더)을 선택합니다.
>? 일부 브라우저는 파일 업로드를 지원하지 않으므로 IE10 이상, Firefox, Chrome 등 주요 브라우저를 권장합니다.
>
![](https://main.qcloudimg.com/raw/8489d2bae2ba778bac87386093cd51e7.png)
6. (옵션) **매개변수 설정**을 클릭하고 파일 업로드 창에서 객체 속성을 설정합니다.
 ![](https://main.qcloudimg.com/raw/0b7c7b6297a1098fe43074f85a138fbf.png)
설정은 다음 내용을 참고하십시오.
 - **스토리지 유형**: 비즈니스 시나리오에 따라 객체의 스토리지 유형을 선택합니다. 기본적으로 STANDARD로 설정되어 있습니다. 자세한 내용은 [제품 개요](https://intl.cloud.tencent.com/document/product/436/6222)를 참고하십시오.
>! 버킷에 MAZ 구성이 활성화된 경우 **스토리지 유형**은 MAZ_STANDARD와 같은 MAZ 활성화 스토리지 클래스만 선택할 수 있습니다. INTELLIGENT TIERING 구성도 활성화된 경우 INTELLIGENT TIERING(MAZ)을 선택할 수도 있습니다.
>
 - **액세스 권한**: 필요에 따라 객체에 대한 액세스 권한을 선택합니다. 이 필드는 기본적으로 상속으로 설정됩니다(즉, 버킷의 권한 상속). 자세한 내용은 [액세스 제어 기본 개념](https://intl.cloud.tencent.com/document/product/436/30581)을 참고하십시오.
 - **서버 측 암호화**: 업로드하려는 객체에 대한 서버 측 암호화를 구성합니다. COS는 기록된 데이터를 자동으로 암호화하고 액세스할 때 암호를 해독합니다. 현재 COS는 SSE-KMS(베이징, 상하이, 광저우 리전에서만 사용 가능)와 SSE-COS의 두 가지 암호화 방법을 제공합니다. 자세한 내용은 [서버 암호화 개요](https://intl.cloud.tencent.com/document/product/436/18145)를 참고하십시오.
 - **객체 태그**: 객체 태그는 태그 키(tagKey), 태그 값(tagValue) 및 등호’=’로 구성됩니다(예: group = IT). 지정된 객체의 태그를 설정, 쿼리 및 삭제할 수 있습니다.
 - **메타데이터**: 객체 메타데이터는 또는 HTTP Header는 HTML 데이터를 브라우저로 보내기 전에 HTTP를 통해 서버에서 보내는 문자열입니다. HTTP Header를 수정하면 웹 페이지가 응답하는 방식과 캐싱 시간과 같은 특정 구성을 수정할 수 있습니다. 객체의 HTTP Header를 수정해도 객체 자체는 수정되지 않습니다. 자세한 내용은 [사용자 정의 Headers](https://intl.cloud.tencent.com/document/product/436/13361)를 참고하십시오.
7. **업로드**를 클릭합니다.
페이지 오른쪽 상단의 ‘완료한 작업’에서 업로드 진행 상황을 확인할 수 있습니다. 업로드가 완료되면 업로드된 객체가 ‘파일 목록’에 나타납니다.
![](https://main.qcloudimg.com/raw/eab5784b108fc096dbe317fed25f7925.png)
>? 이미지의 작업 진행률은 현재 업로드 작업에 의해 생성된 작업의 수를 나타냅니다. 예를 들어 10개의 파일이 모두 성공적으로 업로드되면 작업 진행률이 ‘성공 1개, 실패 0개, 일시 중지 0개’로 표시됩니다.
>
