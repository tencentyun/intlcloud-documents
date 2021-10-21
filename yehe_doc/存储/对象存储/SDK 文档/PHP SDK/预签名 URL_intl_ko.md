## 소개
PHP SDK는 사전 서명된 URL을 가져오는 인터페이스를 제공하며, 요청 예시는 다음과 같습니다.

>?
> - 사용자는 임시 키를 사용하여 사전 서명을 생성하고, 임시 승인을 통해 사전 서명 업로드 및 다운로드 요청의 보안성을 강화할 것을 권장합니다. 임시 키 신청 시, [최소 권한의 원칙 관련 가이드](https://intl.cloud.tencent.com/document/product/436/32972)를 준수하여 타깃 버킷이나 객체 이외의 리소스가 유출되지 않도록 하시기 바랍니다.
> - 사전 서명 생성을 위해 영구 키를 사용해야 하는 경우, 리스크 방지를 위해 영구 키 권한을 업로드 또는 다운로드 작업으로 제한할 것을 권장합니다.
> 



## 영구 키 사전 서명 요청 예시

### 업로드 요청 예시
[//]: # (.cssg-snippet-get-presign-upload-url)
```php
$secretId = "SECRETID"; //영구 키 SecretId로 대체
$secretKey = "SECRETKEY"; //영구 키 SecretKey로 대체
$region = "ap-beijing"; //기본 버킷 리전 설정
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //프로토콜 헤더, 기본값: http
        'credentials'=> array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
### 사전 서명 간편 업로드
try {
    $signedUrl = $cosClient->getPreSignedUrl('putObject', array(
        'Bucket' => "examplebucket-1250000000", //버킷, 형식: BucketName-APPID
        'Key' => "exampleobject", //버킷 내 객체의 위치, 즉 객체 키
        'Body' => 'string', //비어 있거나 임의의 문자열일 수 있습니다.
        'Params' => array(), //서명을 삽입할 요청 매개변수
        'Headers' => array() //서명을 삽입할 요청 헤더
    ), '+10 minutes'); //서명 유효기간
    // 요청 완료
    echo ($signedUrl);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}

### 멀티파트 업로드 사전 서명
try {
    $signedUrl = $cosClient->getPreSignedUrl('uploadPart', array(
            'Bucket' => "examplebucket-1250000000", //버킷, 형식: BucketName-APPID
            'Key' => "exampleobject", //버킷 내 객체의 위치, 즉 객체 키
            'UploadId' => 'string',
            'PartNumber' => '1',
            'Body' => 'string',
            'Params' => array(), //서명을 삽입할 요청 매개변수
            'Headers' => array() //서명을 삽입할 요청 헤더
            ), '+10 minutes'); //서명 유효기간
    // 요청 완료
    echo ($signedUrl);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

### 다운로드 요청 예시
[//]: # (.cssg-snippet-get-presign-download-url)
```php
$secretId = "SECRETID"; //영구 키 SecretId로 대체
$secretKey = "SECRETKEY"; //영구 키 SecretKey로 대체
$region = "ap-beijing"; //기본 버킷 리전 설정
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //프로토콜 헤더, 기본값: http
        'credentials'=> array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
### 사전 서명 간편 다운로드
try {
    $signedUrl = $cosClient->getPreSignedUrl('getObject', array(
        'Bucket' => "examplebucket-1250000000", //버킷, 형식: BucketName-APPID
        'Key' => "exampleobject", //버킷 내 객체의 위치, 즉 객체 키
        'Params' => array(), //서명을 삽입할 요청 매개변수
        'Headers' => array() //서명을 삽입할 요청 헤더
        ), '+10 minutes'); //서명 유효기간
    // 요청 완료
    echo ($signedUrl);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}

### 캡슐화된 getObjectUrl을 사용하여 다운로드 서명 가져오기
try {    
    $bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
    $key = "exampleobject"; //버킷 내 객체의 위치, 즉 객체 키
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes'); //서명 유효기간
    // 요청 완료
    echo $signedUrl;
} catch (\Exception $e) {
    // 요청 실패
    print_r($e);
}
```

## 임시 키 사전 서명 요청 예시

### 업로드 요청 예시
[//]: # (.cssg-snippet-get-presign-sts-upload-url)
```php
$tmpSecretId = "SECRETID"; //임시 키 SecretId로 대체
$tmpSecretKey = "SECRETKEY"; //임시 키 SecretKey로 대체
$tmpToken = "COS_TOKEN"; //임시 키 token으로 대체
$region = "ap-beijing"; //기본 버킷 리전 설정
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //프로토콜 헤더, 기본값: http
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
### 사전 서명 간편 업로드
try {
    $signedUrl = $cosClient->getPreSignedUrl('putObject', array(
        'Bucket' => "examplebucket-1250000000", //버킷, 형식: BucketName-APPID
        'Key' => "exampleobject", //버킷 내 객체의 위치, 즉 객체 키
        'Body' => 'string',
        'Params' => array(), //서명을 삽입할 요청 매개변수
        'Headers' => array() //서명을 삽입할 요청 헤더
        ), '+10 minutes'); //서명 유효기간
    // 요청 완료
    echo ($signedUrl);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}

### 멀티파트 업로드 사전 서명
try {
    $signedUrl = $cosClient->getPreSignedUrl('uploadPart', array(
        'Bucket' => "examplebucket-1250000000", //버킷, 형식: BucketName-APPID
        'Key' => "exampleobject", //버킷 내 객체의 위치, 즉 객체 키
        'UploadId' => '',
        'PartNumber' => '1',
        'Body' => '',
        'Params' => array(), //서명을 삽입할 요청 매개변수
        'Headers' => array() //서명을 삽입할 요청 헤더
        ), '+10 minutes'); //서명 유효기간
    // 요청 완료
    echo ($signedUrl);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

### 다운로드 요청 예시
[//]: # (.cssg-snippet-get-presign-sts-download-url)
```php
$tmpSecretId = "SECRETID"; //임시 키 SecretId로 대체
$tmpSecretKey = "SECRETKEY"; //임시 키 SecretKey로 대체
$tmpToken = "COS_TOKEN"; //임시 키 token으로 대체
$region = "ap-beijing"; //기본 버킷 리전 설정
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //프로토콜 헤더, 기본값: http
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
### 사전 서명 간편 다운로드
try {
    $signedUrl = $cosClient->getPreSignedUrl('getObject', array(
        'Bucket' => "examplebucket-1250000000", //버킷, 형식: BucketName-APPID
        'Key' => "exampleobject" //버킷 내 객체의 위치, 즉 객체 키
        'Params' => array(), //서명을 삽입할 요청 매개변수
        'Headers' => array() //서명을 삽입할 요청 헤더
    ), '+10 minutes'); //서명 유효기간
    // 요청 완료
    echo ($signedUrl);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}

### 캡슐화된 getObjectUrl을 사용하여 다운로드 서명 가져오기
try {    
    $bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
    $key = "exampleobject"; //버킷 내 객체의 위치, 즉 객체 키
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes'); //서명 유효기간
    // 요청 완료
    echo $signedUrl;
} catch (\Exception $e) {
    // 요청 실패
    print_r($e);
}
```

