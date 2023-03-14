## 개요

COS 콘솔을 사용하면 버킷의 문서를 미리 볼 수 있습니다. 이 문서는 콘솔에서 문서 미리보기 기능을 사용하는 방법을 설명합니다. 문서 미리보기에 대한 자세한 내용은 [문서 미리보기 개요](https://intl.cloud.tencent.com/document/product/436/49159)를 참고하십시오.


>!
>- 문서 미리보기 기능은 중국 본토와 실리콘밸리, 버지니아, 프랑크푸르트 및 싱가포르의 퍼블릭 클라우드 리전에서 사용할 수 있습니다. 현재 싱가포르와 실리콘밸리에서는 문서에서 이미지로의 변환 미리보기만 지원됩니다.
>- 문서 미리보기는 CI(Cloud Infinite)로 과금됩니다. 자세한 과금 설명은 [Billing Overview](https://intl.cloud.tencent.com/document/product/1045/33431)를 참고하십시오.


## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 목록**을 클릭한 다음 문서 미리보기 기능을 활성화할 버킷을 클릭합니다.
3. **데이터 처리 > 문서 처리**를 클릭합니다. **문서 미리보기** 영역에서 **편집**을 클릭하고 상태를 전환합니다.
4. 문서를 미리 보려면 문서 URL에 매개변수를 추가하십시오. 매개변수는 다음과 같이 설명됩니다.
```plaintext
<BucketName-APPID>.cos.<Region>.myqcloud.com/<objectkey>?ci-process=doc-preview&page=<page>&srcType=<srcType>
```
 - objectkey: 파일 경로로 이해할 수 있는 객체 키입니다.
 - ci-process: 문서 미리보기를 위해 doc-preview에서 고정된 CI의 처리 기능입니다.
 - page: 변환할 페이지의 번호로 1부터 카운트됩니다.
 - srcType: 소스 데이터 유형. 현재 파일 변환 기능은 COS 객체의 파일 확장자에 따라 소스 데이터 유형을 결정합니다. 객체에 확장자가 없는 경우 이 값을 설정할 수 있습니다.


>! URL 모드를 사용하는 경우 단일 페이지 문서 또는 여러 페이지 문서의 첫 페이지만 처리할 수 있습니다. 더 많은 콘텐츠를 미리 보려면 [문서 미리보기 API](https://intl.cloud.tencent.com/document/product/436/49404)를 사용하십시오.
>
