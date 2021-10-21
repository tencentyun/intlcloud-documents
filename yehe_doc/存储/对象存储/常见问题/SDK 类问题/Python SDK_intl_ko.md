### COS Python SDK 업그레이드 후 ‘파일 이동’ 작업을 실행할 수 없습니다. 어떻게 처리해야 합니까?

[PUT Object](https://intl.cloud.tencent.com/document/product/436/10881)와 [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) 인터페이스를 사용하여 실행할 수 있습니다. 삭제 작업을 실행하기 전에 데이터의 일관성 검증을 권장합니다. 자세한 내용은 [MD5 인증](https://intl.cloud.tencent.com/document/product/436/32467) 문서를 참고하십시오.

### COS Python SDK는 파일 다운로드를 위한 임시 링크를 어떻게 가져옵니까?

Python SDK는 서명 획득 및 사전 서명된 URL 요청 획득 인터페이스, 객체 다운로드의 사전 서명된 URL 획득 인터페이스를 제공합니다. 영구 키 또는 임시 키를 사용해 사전 서명된 URL을 획득하는 호출 방법과 동일하며, 임시 키 사용 시에는 header 또는 query_string에 x-cos-security-token을 추가해야 합니다. 자세한 내용은 [사전 서명된 URL](https://intl.cloud.tencent.com/document/product/436/31548) 문서를 참고하십시오.

### COS Python SDK 사용 시 이상이 발생할 경우 어떻게 처리해야 합니까?

COS XML Python SDK는 작업 성공 시 dict 또는 None을 반환합니다. SDK 인터페이스를 호출하여 COS 서비스를 요청하는 데 실패하면 시스템에 CosClientError(클라이언트 오류) 또는 CosServiceError(서버 오류)가 발생합니다.

- 서버에서 반환된 오류: 요구 사항을 충족하지 않는 일부 클라이언트 요청을 처리할 때 서버에서 반환되는 오류를 가리킵니다. 예를 들어 존재하지 않는 파일에 대한 액세스, 파일에 대한 액세스 권한 없음 등이 있습니다. 서버에서 반환되는 오류 코드에 대한 자세한 내용은 [API 오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오.
- 클라이언트 오류: 주로 네트워크 오류, 파일 읽기 및 쓰기 IO 오류, 매개변수 확인 실패 등을 가리킵니다.

