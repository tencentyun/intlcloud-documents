## 작업 시나리오
Tencent Cloud는 CVM 구매 페이지에서 선택한 구성에 대응하는 인스턴스를 생성하기 위한 OpenAPI 모범 사례 스크립트 코드 생성을 지원합니다. 코드를 저장하여 동일한 구성의 CVM 구매에 사용할 수 있습니다.

### 전제 조건
- Tencent Cloud 공식 사이트에 로그인 후 CVM의 [사용자 정의 구성 구매 페이지](https://buy.cloud.tencent.com/cvm?tab=custom)에 들어가세요.
- 필요에 따라 CVM 구성을 선택하고 구성 정보 확인 페이지에 들어가세요. CVM 구매에 대한 구성 사항을 알고 싶으시면 [구매 페이지로 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참조하세요.

### 작업 순서
1. 구성 정보 확인 페이지에서 [API Explorer 모범 사례 스크립트 생성]을 클릭하세요. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/7c095b6809c8815b15d4fe2c45b89305.png)
2. “API Explorer 모범 사례 스크립트 생성”팝업 창에서 다음과 같은 정보를 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/5fba656be4ee0977245a7778f6a4c910.png)
 - **API 작업 흐름** : 인스턴스 생성 인터페이스 RunInstances 및 선택한 구성에 대응한 인터페이스의 실제 매개변수를 조회할 수 있습니다. 그 중 `*`로 표시된 매개변수는 인터페이스의 필수 매개변수입니다. 상세한 데이터 내용을 확인하려면 마우스를 데이터 위로 이동하면 완전히 표시됩니다.
 - **API 스크립트**：필요에 따라 Java 및 Python 프로그래밍 언어를 선택해서 코드를 생성할 수 있습니다. 오른쪽 상단에 있는 [스크립트 복사]를 클릭하여 스크립트 코드를 얻습니다. 코드를 저장하여 동일한 구성의 CVM 구매에 사용할 수 있습니다.
>?
>- 비밀번호는 민감한 정보이라서 인스턴스 비밀번호를 설정했다면 페이지 및 생성된 스크립트 코드에서는 표시하지 않습니다. 스스로 수정하세요. 
>- API Explorer 실천 스크립트는 만료일 통일을 지원하지 않습니다. 인스턴스 생성 후 개별적으로 설정할 수 있습니다.
