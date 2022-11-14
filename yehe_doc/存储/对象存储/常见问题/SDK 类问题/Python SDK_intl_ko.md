### Python SDK를 업그레이드한 후 객체를 이동할 수 없으면 어떻게 해야 하나요?

[PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) 및 [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)를 호출하여 객체를 이동할 수 있습니다. [MD5 검증](https://intl.cloud.tencent.com/document/product/436/32467)에 안내된 대로 객체를 삭제하기 전에 데이터 일관성을 확인하는 것이 좋습니다.

### Python SDK로 임시 다운로드 URL을 얻으려면 어떻게 해야 하나요?

Python SDK는 요청 서명, 미리 서명된 URL 및 미리 서명된 다운로드 URL을 가져오기 위한 API를 제공합니다. 영구 키 또는 임시 키를 사용하여 미리 서명된 URL을 가져오는 호출 방법은 동일하지만 임시 키를 사용할 경우 헤더 또는 query_string에 x-cos-security-token을 추가해야 합니다. 자세한 내용은 [사전 서명된 URL 가져오기](https://intl.cloud.tencent.com/document/product/436/31548)를 참고하십시오.

### Python SDK가 예외를 보고하면 어떻게 해야 하나요?

XML Python SDK 작업이 성공하면 dict 또는 None이 반환됩니다. COS 서비스 요청을 위한 SDK API가 실패하면 시스템은 CosClientError 또는 CosServiceError를 리포트합니다.

- CosServiceError: 존재하지 않거나 권한이 없는 객체에 액세스하는 것과 같이 요구 사항을 충족하지 않는 클라이언트 요청으로 인해 반환된 오류입니다. 자세한 내용은 [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오.
- CosClientError: 네트워크 예외, 파일 읽기/쓰기 중 IO 오류, 매개변수 확인 실패 등.

