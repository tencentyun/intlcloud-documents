## SAML ID 공급업체 삭제

ID 공급업체를 관리하려면 CAM 콘솔을 통해 삭제 또는 CAM API를 통해 삭제와 같은 두가지 방법이 있습니다.

### 콘솔을 통해 삭제
1.	CAM 콘솔에 로그인하고 [ID 공급업체](https://console.cloud.tencent.com/cam/idp) 페이지로 이동합니다.
2.	계정의 ID 공급업체 리스트에서 삭제할 ID 공급업체를 선택하고 [조작]에서 [삭제]를 클릭합니다.
3.	ID 공급업체를 삭제할 때 관련 ID 공급업체를 삭제할지 다시 확인한 후 [확인]을 클릭하여 ID 공급업체를 삭제하면 됩니다.

### API 를 통해 삭제

- (옵션)페이지별로 모든 IDP 정보를 표시하려면 [ListSAMLProviders](https://intl.cloud.tencent.com/document/product/598/30298)를 호출하십시오.
- (옵션)특정 제공업체에 대한 자세한 정보를 획득하려면 [GetSAMLProvider](https://intl.cloud.tencent.com/document/product/598/30297)를 호출하십시오.
- SAML ID 공급업체를 삭제하려면 [DeleteSAMLProvider](https://intl.cloud.tencent.com/document/product/598/30301)를 호출하십시오.

## SAML ID 공급업체 수정

ID 공급업체를 수정하려면 CAM 콘솔을 통해 수정 또는 CAM API를 통해 수정과 같은 두 가지 방법이 있습니다.

### 콘솔을 통해 수정
1.	CAM 콘솔에 로그인하고 [ID 공급업체](https://console.cloud.tencent.com/cam/idp) 페이지로 이동합니다.
2.	계정의 ID 공급업체 리스트에서 수정할 ID 공급업체를 선택하고 공급업체 이름을 클릭하여 세부 정보 페이지로 이동합니다.
3.	메타 데이터 문서를 업로드하여 기존 ID 공급업체를 재정의하거나 기존 메타 데이터 문서를 다운로드할 수 있습니다.

### API 를 통해 수정

SAML ID 공급업체 설명 또는 메타 데이터 문서를 업데이트합니다.
- [UpdateSAMLProvider](https://intl.cloud.tencent.com/document/product/598/30296)를 호출하십시오.
