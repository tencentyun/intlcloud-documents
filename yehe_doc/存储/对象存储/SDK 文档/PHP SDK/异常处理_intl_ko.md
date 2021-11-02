## 소개

SDK 인터페이스를 호출하여 Cloud Object Storage(COS) 서비스를 요청하는 데 실패하면(예: 반환 코드가 4xx 또는 5xx) 시스템에서 (Qcloud\Cos\Exception\ServiceResponseException) 예외가 발생합니다.

## 서버측 예외 발생

CosServerException에는 서버에서 반환한 상태 코드, requestid 및 오류 세부 정보가 포함됩니다. 예외 포착 후 전체 예외를 출력할 것을 권장합니다. 예외에는 필수적인 진단 요소가 포함되어 있습니다. 다음은 예외 멤버 변수에 대한 설명과 예외 캐치의 예시입니다.

| 멤버         | 설명             | 유형   |
| ----------- | ---------------- | ------ |
| requestId    | 요청 ID. 요청을 표시하며, 문제 진단에 매우 중요함              | string |
| statusCode   | response의 status 상태 코드. 더 자세한 사항은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | string |
| errorCode    | 요청 실패 시 body 반환 Error Code입니다. 더 자세한 사항은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | string |
| errorMessage | 요청 실패 시 body 반환 Error Message입니다. 더 자세한 사항은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | string |


#### 예외 캐치 예시

```php
try {
   $cosClient->listBuckets() 
} catch (Qcloud\Cos\Exception\ServiceResponseException $e) {
    $statusCode = $e->getStatusCode(); // 오류 코드 획득
    $errorMessage = $e->getMessage(); // 오류 정보 획득
    $requestId = $e->getRequestId(); // 오류 requestId 획득
    $errorCode = $e->getCosErrorCode(); // 오류 이름 획득
    $request = $e->getRequest(); // 전체 요청 획득
    $response = $e->getResponse(); // 완전한 응답 획득
    echo ($e);
} catch (\Exception $e) {

}
```
>! Phar 또는 소스 코드를 사용하여 SDK를 설치하면, 반환되는 예외 정보가 더 정확해집니다. Composer를 사용하여 SDK를 설치하는 경우, 반환된 예외 정보가 요구 사항에 맞지 않으면 vendor/guzzlehttp/guzzle-services/src/SchemaValidator.php를 수정하여 일부 오류 정보를 사용자 정의할 수 있습니다.
>
