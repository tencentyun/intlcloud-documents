## 개요
PHP SDK는 사전 서명된 URL을 가져오는 인터페이스를 제공하며, 요청 예시는 다음과 같습니다.

## 영구 키 사전 서명 요청 예시

### 업로드 요청 예시
[//]: # (.cssg-snippet-get-presign-upload-url)
```php
$secretId = "COS_SECRETID"; //영구 키 SecretId로 대체
$secretKey = "COS_SECRETKEY"; //영구 키 SecretKey로 대체
$region = "ap-beijing"; //기본 버킷 리전 설정
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //프로토콜 헤더, 기본값: http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
### 사전 서명 간편 업로드
try {
    $signedUrl = $cosClient->getPreSignedUrl('putObject', array(
        'Bucket' => "examplebucket-1250000000", //버킷, 형식: BucketName-APPID
        'Key' => "exampleobject", //버킷 내 객체의 위치, 즉 객체 키
        'Body' => 'string' //비어 있거나 임의의 문자열일 수 있습니다.
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
            'Body' => 'string'), '+10 minutes'); //서명 유효기간
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
$secretId = "COS_SECRETID"; //영구 키 SecretId로 대체
$secretKey = "COS_SECRETKEY"; //영구 키 SecretKey로 대체
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
$tmpSecretId = "COS_SECRETID"; //임시 키 SecretId로 대체
$tmpSecretKey = "COS_SECRETKEY"; //임시 키 SecretKey로 대체
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
        'Body' => 'string'), '+10 minutes'); //서명 유효기간
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
        'Body' => ''), '+10 minutes'); //서명 유효기간
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
$tmpSecretId = "COS_SECRETID"; //임시 키 SecretId로 대체
$tmpSecretKey = "COS_SECRETKEY"; //임시 키 SecretKey로 대체
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

