## 태스크 템플릿 생성

태스크 템플릿 관련 설명은 [용어집]() 중 ‘태스크 템플릿’을 참조하십시오. [Batch Compute 콘솔]()을 통해 작업 템플릿을 생성할 수 있으며 구체적인 절차는 다음과 같습니다.
1. [ Batch Compute 콘솔]()에 로그인합니다. 아직 Batch Compute 서비스를 개통하지 않았다면 Batch Compute 콘솔 홈페이지 관련 알림을 참조하여 개통하십시오.

2. 왼쪽 탐색 모음 ‘태스크 템플릿’ 옵션을 클릭하고 대상 지역을 선택한 뒤 [생성] 버튼을 클릭합니다.
![](https://mc.qcloudimg.com/static/img/b6d89f6a4b4e0c8cc0469606948b8e41/image.jpg)

3. 기본 정보를 구성합니다.
   - 리소스 구성: ‘CVM 세부 구성’ 옵션을 클릭하여 한 단계 더 선택할 수 있으며, 관련 구성 설명은 [CVM 제품 문서](https://intl.cloud.tencent.com/document/product/213)를 참조하십시오. 
   - 리소스 수량: 동시 발생 실행 태스크를 결정하는 리소스 수이며 관련 설명은 [용어집](https://intl.cloud.tencent.com/document/product/599/10396) 중 ‘태스크 인스턴스’를 참조하십시오.
   - 이미지: 관련 설명은 [용어집](https://intl.cloud.tencent.com/document/product/599/10396) '이미지'를 참조하십시오.
   ![](https://mc.qcloudimg.com/static/img/2e4c9a7879539ae70b907f669e4a8b78/image.jpg)

4. 프로그램 구성 정보를 설정합니다.
   - 실행 방식: "Package"를 선택할 때 "프로그램 패킷 주소"를 입력해야 합니다. "프로그램 패킷 주소"를 [COS](https://intl.cloud.tencent.com/document/product/436)에 저장합니다.
   - 프로그램 패킷 주소/ Stdout 로그/ Stderr 로그: 고정 형식을 만족시켜야 하며 [COS, CFS 경로 입력]()을 참조하십시오.
![](https://mc.qcloudimg.com/static/img/ed418b2351814d567c0beceb3183ec9d/image.jpg)

5. 스토리지 매핑을 구성합니다.
   - 경로 매핑 입력: LINUX 운영 체제의 경우, [COS](https://intl.cloud.tencent.com/document/product/436)와 [파일 저장](https://intl.cloud.tencent.com/document/product/582)을 지원합니다. Windows 운영 체제의 경우, [파일 저장](https://intl.cloud.tencent.com/document/product/582)을 지원합니다. COS와 파일 저장 형식에 대한 사항은 [COS, CFS 경로 입력]()을 참조하십시오. 또한 다른 운영 체제에 대해서는 로컬 경로의 형식이 달라야 합니다.
   - 경로 매핑 출력: [COS](https://intl.cloud.tencent.com/document/product/436)를 지원합니다. COS 형식은 [COS, CFS 경로 입력]()을 참조하십시오.
   ![](https://mc.qcloudimg.com/static/img/b86945c2ee04dcb89d1ce9aa2a62955c/image.jpg)

6. 작업 템플릿 JSON 파일에 오류가 없을 경우, [저장] 버튼을 클릭하여 태스크 템플릿 생성을 완료합니다.
![](https://mc.qcloudimg.com/static/img/779bfc1f07af787612d2fb1db5ce70d1/image.jpg)

## 태스크 템플릿 삭제
더 이상 태스크 템플릿을 사용할 필요가 없을 경우, 태스크 템플릿 리스트에서 삭제할 수 있습니다.
![](https://mc.qcloudimg.com/static/img/9d207da685ef89b75a93818851f5050f/image.jpg)

## 태스크 템플릿 수정
기존 태스크 템플릿을 편집해야 할 경우, 태스크 템플릿 ID를 클릭하여 태스크 템플릿 구성 페이지에 들어가 항목별로 편집할 수 있습니다.
![](https://mc.qcloudimg.com/static/img/bab3f74591f80db4022716f897d57893/image.jpg)

