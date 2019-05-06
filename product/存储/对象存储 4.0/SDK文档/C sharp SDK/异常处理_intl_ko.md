## 소개

SDK API를 호출하여 COS 서비스 요청에 실패한 경우, 시스템은 CosClientException(클라이언트 비정상) 또는 CosServerException(서버 비정상)을 throw합니다.
- CosClientException은 클라이언트가 COS 서버와 정상적인 상호 작용을 완료하지 못해서 발생합니다. 얘를 들면, 클라이언트가 서버에 연결할 수 없거나, 서버에서 반환한 데이터를 해석할 수 없거나, 로컬 파일 읽기에 IO 예외 등과 같습니다.
- CosServerException은 클라이언트와 COS 서버의 상호 작용이 정상이지만, COS 리소스 조작이 실패할 때 throw됩니다. 예를 들면, 클라이언트가 존재하지 않는 버킷에 액세스하거나, 존재하지 않는 파일을 삭제하거나, 조작할 권한이 없음 등과 같습니다.


## 클라이언트 비정상

CosClientException은 System.ApplicationException으로부터 통합되며, 사용 방법은 System.ApplicationException과 같고, 또한 한개의 예외 멤버 errorCode를 추가합니다. 예:

|멤버|설명|유형|
| ---- | ---- | ---- |
|errorCode|클라이언트 오류 코드, 예를 들어 10000은 매개변수 인증 실패를 나타냅니다|int|



## 서버 비정상

CosServerException은 서버가 반환한 상태 코드, requestid, 오류 세부 정보 등을 포함합니다. 비정상을 캡처한 후, 필수 검사 요소가 포함된 전체 비정상에 대해 인쇄를 하는 것이 좋습니다. 다음은 예외 멤버 변수의 설명입니다.

| 멤버 | 설명 | 유형 |
| ------------ | ---------------------------------------- | --------- |
| requestId   | 요청 ID, 요청을 나타내는 데 사용되며, 문제 검사에 매우 중요합니다 | string    |
| statusCode   | 응답의 상태 코드, 4xx는 클라이언트로 인해 요청이 실패했음을 의미하고, 5xx는 서버 비정상으로 인한 실패입니다. 더 자세한 정보는 [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오 | string    |
| errorCode | 요청 실패 시 본문이 반환한 오류 코드입니다. 더 자세한 정보는 [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. | string |
| errorMessage | 요청 실패 시 본문이 반환한 오류 메시지입니다. 더 자세한 정보는 [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오 | string |


