### C SDK 사용 시 어떻게 중단 후 업로드를 재개하나요?

[C SDK advanced upload](https://intl.cloud.tencent.com/document/product/436/43553) 인터페이스를 사용해 중단 후 업로드 재개 기능을 구현할 수 있습니다. 중단 후 업로드 재개 시, 업로드 제어 매개변수를 **COS_TRUE**로 설정해야 합니다. 예시: `clt_params = cos_create_resumable_clt_params_content(p, 0, 1, COS_TRUE, NULL)`.

### C SDK 사용 시 HttpIOError 오류가 발생했습니다.

SDK 사용 중 어떠한 인터페이스도 정상적으로 사용할 수 없고, requestid를 반환할 수 없는 것으로 확인되었으며, 패킷 분석 결과 HTTP 요청이 전송되지 않은 것으로 나타났습니다. 로그 조건은 다음과 같습니다.
```
transport failure curl code:1 error:Unsupported protocol
status->code: -996
status->error_code: HttpIoError
status->error_msg: Unsupported protocol
status->req_id:
```

원인: HTTPS 프로토콜을 사용하였으나 libcurl 라이브러리가 HTTPS 프로토콜을 지원하지 않아 결과적으로 libcurl 컴파일 시 openssl 라이브러리 미사용 또는 버전 불일치.
**해결 방법**: 실행 환경을 확인하고 libcurl 라이브러리를 다시 설치하거나(소스 코드 컴파일 및 설치를 위해 SSL을 활성화해야 함) openssl 라이브러리를 업데이트합니다.
