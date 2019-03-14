## 작업 생성

작업 관련 설명은 [용어](https://cloud.tencent.com/document/product/599/10396)중 "작업"을 참조하십시오. [BatchCompute 콘솔]()을 통해 작업을 생성할 수 있습니다.

1. [Batch Compute 콘솔]()에 로그인합니다. 아직 Batch Compute 서비스를 개통하지 않았다면 Batch Compute 콘솔 홈페이지 관련 알림을 참조하여 개통하십시오.

2. 왼쪽 탐색 모음 "작업" 옵션을 클릭하고 대상 지역을 선택한 뒤 [생성] 버튼을 클릭하십시오.
![](https://mc.qcloudimg.com/static/img/7bc845062d2b91aac30f548511ab183c/image.jpg)

3. 작업 기본 정보를 구성합니다.
![](https://mc.qcloudimg.com/static/img/adfad5bef466330a4f5583a84531f4af/image.jpg)

4. "태스크 흐름" 왼쪽 태스크 템플릿을 선택하고 마우스를 움직여 오른쪽 캔버스에 배치한 뒤, 앵커 포인트를 드래그하여 연결을 설정하십시오.
 ![](https://mc.qcloudimg.com/static/img/8c2f1e4e4121a5beaf874425c47a243f/image.jpg)

5. "태스크 흐름" 오른쪽 "태스크 세부 정보"를 열어 구성이 정확한지 확인한 뒤, [완료] 버튼을 클릭하십시오.
   + 태스크 흐름 중, 각 태스크는 태스크 템플릿에 기반하여 생성됩니다.
   + 오른쪽 "태스크 정보" 옵션을 열고 태스크 하나를 선택하면 해당 태스크 부분 구성을 편집할 수 있습니다. 편집 작업은 태스크 템플릿에 아무런 영향을 미치지 않습니다.
   ![](https://mc.qcloudimg.com/static/img/7e8faba3818f7ff2ada687ed7602be2e/image.jpg)

## 작업 종료
특정 조건 하에 작업 운행을 종료할 수 있습니다. 종료 관련 설명은 API 문서 [태스크 인스턴스 종료](https://intl.cloud.tencent.com/document/product/599/12688)를 참조하십시오.

## 작업 삭제
작업이 완료 상태, 즉 SUCCEED 또는 FAILED 상태일 경우, 작업 리스트에서 작업을 삭제할 수 있습니다.
![](https://mc.qcloudimg.com/static/img/2abcf3d06f446395c8bafa0c955abd2f/image.jpg)
