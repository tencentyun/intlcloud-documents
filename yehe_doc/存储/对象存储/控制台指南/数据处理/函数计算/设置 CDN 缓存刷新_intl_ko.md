## 소개

CDN(Content Delivery Network) 캐시 퍼지는 [Serverless Cloud Function(SCF)](https://www.tencentcloud.com/document/product/583)을 기반으로 하는 Tencent Cloud COS(Cloud Object Storage) 기능으로 사용자가 CDN 엣지 서버에 캐시된 데이터를 자동으로 퍼지할 수 있도록 합니다. 버킷에 트리거 규칙을 추가하면 버킷의 파일을 업데이트할 때 COS에서 프로비저닝한 SCF 기능이 자동으로 트리거되어 캐시된 데이터를 퍼지합니다.

> !
> - COS 콘솔에서 버킷에 캐시 퍼지 규칙을 추가한 적이 있는 경우 [SCF 콘솔](https://console.cloud.tencent.com/scf/list?rid=1&ns=default)에서 기존에 생성한 CDN 캐시 퍼지 함수를 볼 수 있습니다. 이 함수를 삭제하지 **마십시오.** 삭제할 경우 규칙이 적용되지 않을 수 있습니다.
> - 이미 런칭된 SCF의 리전에서는 CDN 캐시 퍼지 기능을 지원합니다. 이에는 광저우, 상하이, 베이징, 청두, 중국홍콩, 싱가포르, 뭄바이, 토론토, 실리콘밸리 등이 포함되어 있으며, 지원하는 리전에 대한 자세한 내용은 [SCF 제품 문서](https://www.tencentcloud.com/document/product/583)를 참고하십시오.
> - CDN 캐시 퍼지 기능은 네트워크 링크 불안정 등 실패를 일으킬 수 있습니다. 기능이 귀하의 기대에 부합하지 않을 경우, COS 콘솔에서 생성된 함수 오른쪽의 **로그 조회**를 클릭해 SCF 콘솔로 리디렉션한 후, 로그 오류 세부 사항 조회를 통해 오류 발생 원인을 진단할 수 있습니다.
> - CDN 캐시 퍼지 기능은 SCF 서비스에 종속돼 있습니다. SCF 서비스는 사용자에게 [무료 한도](https://intl.cloud.tencent.com/document/product/583/12282)를 제공하며, 무료 한도를 초과한 부분은 [SCF Pricing](https://intl.cloud.tencent.com/document/product/583/12281)에 따라 과금됩니다. CDN 캐시 퍼지 기능을 사용할 경우, 제거 횟수가 많을수록 더 많은 호출 횟수를 소모하게 됩니다.

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 메뉴에서 **버킷 리스트**를 클릭한 후, CDN 캐시 퍼지 규칙 추가가 필요한 버킷을 선택 및 클릭해 버킷 관리 페이지로 이동합니다.
3. 왼쪽 메뉴에서 **함수 계산 > CDN 캐시 퍼지 함수**를 클릭합니다.
![](https://main.qcloudimg.com/raw/b6618ad14cff7d6daf37520d78371cd2.png)
> !SCF 서비스가 활성화되지 않은 경우 [SCF 콘솔](https://console.cloud.tencent.com/scf)에서 SCF 서비스를 활성화하고 안내에 따라 서비스 라이선스를 완료하십시오.
4. **함수 추가**를 클릭한 후, 팝업창에서 다음 정보를 설정합니다.
![](https://main.qcloudimg.com/raw/9881bbc4d5cf620c4cfac9060b061ce5.png)
	- **함수 이름**: 함수 이름은 함수의 고유한 식별자로, 생성 후에는 수정할 수 없습니다. [SCF 콘솔](https://console.cloud.tencent.com/scf/list?rid=1&ns=default)에서 해당 함수를 확인할 수 있습니다.
	- **이벤트 유형**: 이벤트는 SCF 트리거 작업을 의미합니다. 업로드 작업을 예로 들면, 업로드 방식은 [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) 인터페이스 호출일 수 있고, [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) 인터페이스 호출일 수도 있습니다. 이벤트를 `PUT 유형`으로 선택할 경우, `PUT Object` 인터페이스를 통해서만 파일 업로드 작업이 SCF를 트리거하여 CDN 엣지 노드의 캐시를 퍼지할 수 있습니다.
	- **트리거 조건**: 트리거 이벤트의 파일 소스 범위(예: 전체 버킷 또는 지정된 접두사 또는 지정된 접미사)를 지정할 수 있습니다. 접두사 또는 접미사를 지정한 후, 규칙은 매칭된 파일 소스에만 적용됩니다.
	- **도메인 지정**: 제거가 필요한 CDN 도메인을 의미합니다.
	- **SCF 라이선스**: CDN 캐시 퍼지는 SCF에 CDN을 호출할 수 있는 `PurgeUrlsCache` 인터페이스 라이선스을 부여해야 합니다. 이 라이선스는 CDN이 COS로 Origin-pull하여 최신 데이터를 가져올 수 있도록, CDN 캐시 퍼지에서 데이터를 삭제하는 데 쓰입니다.
5. 설정을 추가한 후 **확인**을 클릭하면 추가된 함수를 확인할 수 있습니다.
 - CDN 캐시 퍼지 기록을 보려면 **로그**를 클릭합니다.
 - 필요 없는 CDN 캐시 퍼지 규칙을 삭제하려면 **삭제**를 클릭합니다.
