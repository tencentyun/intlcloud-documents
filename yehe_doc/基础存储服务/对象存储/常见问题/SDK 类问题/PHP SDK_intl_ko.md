### PHP SDK 실행 시 `Call to undefined method GuzzleHttp\Utils::chooseHandler()` 오류가 발생합니다. 어떻게 처리해야 하나요?


PHP SDK는 Guzzle에 종속되므로 Composer 방식을 사용한 SDK 설치를 권장합니다.
- Composer 방식을 사용해 설치할 경우 `php composer.phar install` 명령어를 실행해 SDK를 설치하고 종속시켜야 합니다.
- 소스 코드 방식을 사용해 설치할 경우 `composer install` 명령어를 실행해 SDK를 설치하고 종속시켜야 합니다. 자세한 내용은 [PHP SDK - 다운로드 및 설치](https://intl.cloud.tencent.com/document/product/436/12266)를 참조하십시오.


### COS에서 PHP SDK에 액세스하여 파일 업로드 시 `cURL error 60: See http://curl.haxx.se/libcurl/c/libcurl-errors.html` 오류가 보고됩니다. 어떻게 처리해야 하나요?

사용자의 PHP 환경 인증서에 문제가 있는 경우 `cURL error 60: See http://curl.haxx.se/libcurl/c/libcurl-errors.html`과 유사한 오류가 보고될 수 있습니다. 다음 순서에 따라 해결을 시도하십시오.

1. `https://curl.haxx.se/ca/cacert.pem`에 액세스하여 인증서 파일 cacert.pem을 다운로드 받은 후 PHP 설치 경로에 저장합니다.
2. php.ini 파일을 편집하고 curl.cainfo 설정 항목 앞의 세미콜론(;)을 삭제합니다. 해당 값은 저장된 인증서 파일 cacert.pem의 절대 경로로 설정됩니다.
3. PHP에 종속된 서비스를 재시작합니다.

