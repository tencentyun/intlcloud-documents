## 다운로드 및 설치

#### 관련 리소스
- COS의 XML PHP SDK 소스 코드 다운로드 주소: [XML PHP SDK](https://github.com/tencentyun/cos-php-sdk-v5/releases).
- SDK 고속 다운로드 주소: [XML PHP SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-php-sdk-v5/latest/cos-php-sdk-v5.zip).
- 예시 Demo 프로그램 주소: [PHP sample](https://github.com/tencentyun/cos-php-sdk-v5/tree/master/sample).
- SDK 문서의 모든 예시 코드는 [SDK 코드 예시](https://github.com/tencentyun/cos-snippets/tree/master/php)를 참고하십시오.
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/cos-php-sdk-v5/blob/master/CHANGELOG.md)를 참고하십시오.
- SDK FAQ는 [PHP SDK FAQ](https://intl.cloud.tencent.com/document/product/436/40543)를 참고하십시오.


>? XML 버전의 SDK를 사용할 때 함수나 메소드가 존재하지 않는 등의 오류가 발생하는 경우, SDK의 XML 버전을 최신 버전으로 업그레이드한 후 다시 시도하십시오.
>

#### 환경 종속

-   PHP 5.6+
`php -v` 명령어를 통해 현재의 PHP 버전을 확인할 수 있습니다.
>! PHP 버전`>=5.3` 및 `<5.6`인 경우 [v1.3](https://github.com/tencentyun/cos-php-sdk-v5/tree/1.3) 버전을 사용하십시오.
>
-  cURL 확장
`php -m` 명령어를 통해 cURL 확장 설치 여부를 확인할 수 있습니다.
 - Ubuntu 시스템에서는 apt-get 패키지 관리자를 사용해 PHP의 cURL 확장을 설치할 수 있으며, 설치 명령어는 다음과 같습니다.
```shell
sudo apt-get install php-curl
```
 - CentOS 시스템에서는 yum 패키지 관리자를 사용해 PHP의 cURL 확장을 설치할 수 있습니다.
```shell
sudo yum install php-curl
```

#### SDK 설치
SDK 설치에는 [Composer 방식](#composer), [Phar 방식](#phar), [소스 코드 방식](#Source)의 세 가지 방법이 있습니다.

<span id="composer"></span>

#### Composer 방식

Composer를 사용한 cos-php-sdk-v5 설치를 권장합니다. Composer는 PHP의 종속 관리 툴로, 프로젝트에 필요한 종속에 대한 선언을 허용한 후 자동으로 귀하의 프로젝트에 설치됩니다.

>? [Composer 공식 홈페이지](https://getcomposer.org/)에서 Composer 설치 방법 및 자동 로딩 설정, 종속 항목 정의에 사용하는 기타 모범 사례 등에 대한 자세한 정보를 확인할 수 있습니다.
>

**설치 순서**

1. 터미널을 엽니다.
2. 다음 명령어를 실행하여 Composer를 다운로드합니다.
```shell
curl -sS https://getcomposer.org/installer | php
```
3. 파일 이름이 `composer.json`인 파일을 생성합니다. 내용은 다음과 같습니다.
```json
{
    "require": {
        "qcloud/cos-sdk-v5": ">=2.0"
    }
}
```
4. 다음 명령어를 실행하여 Composer를 사용해 설치합니다.
```shell
php composer.phar install
```
해당 명령어를 사용하면 현재 디렉터리에 vendor 폴더가 생성됩니다. 폴더 안에는 SDK의 종속 라이브러리와 autoload.php 스크립트가 포함되어 있어 프로젝트에서 편리하게 호출할 수 있습니다.
>! Composer로 현재 PHP 버전에 따라 guzzle6 또는 guzzle7을 다운로드할 수 있으며 guzzle7 버전은 laravel8 프레임워크를 지원합니다. PHP 7.2.5 이후 버전은 guzzle7 버전을, 이전 버전은 guzzle6 버전을 자동 다운로드합니다.
>
5. autoloader 스크립트를 통해 cos-php-sdk-v5를 호출합니다.
```php
require '/path/to/sdk/vendor/autoload.php';
```
>! composer 설치 실행 후, 경로를 autoload.php 파일에 해당하는 경로로 변경해야 합니다. 그렇지 않으면 관련 메소드가 호출되지 않습니다. 설치한 경로가 /Users/username/project인 경우 프로젝트의 인용 경로는 /Users/username/project/vendor/autoload.php로 입력해야 합니다.
>

이제 프로젝트에서 COS XML PHP SDK를 사용할 수 있습니다.

<span id="phar"></span>
#### Phar 방식
Phar 방식으로 SDK를 설치하는 방법은 다음과 같습니다.
1. [GitHub 배포 페이지](https://github.com/tencentyun/cos-php-sdk-v5/releases)에서 상응하는 phar 파일을 다운로드합니다.
>? 
> - PHP 버전 `>= 5.6` 및 `<7.2.5`인 경우 Guzzle6 버전 사용을 위해 `cos-sdk-v5-6.phar`를 다운로드하십시오. 
> - PHP 버전 `>=7.2.5`인 경우 Guzzle7 버전 사용을 위해 `cos-sdk-v5-7.phar`를 다운로드하십시오.
> 
2. 코드에 phar 파일을 가져옵니다.
```php
require  '/path/to/cos-sdk-v5-x.phar';
```

<span id="Source"></span>
#### 소스 코드 방식
소스 코드 방식으로 SDK를 설치하는 방법은 다음과 같습니다.
1. [SDK 다운로드 페이지](https://github.com/tencentyun/cos-php-sdk-v5/releases)에서 `cos-sdk-v5.tar.gz` 압축 파일을 다운로드합니다.
>? 
> - PHP 버전 `>= 5.6` 및 `<7.2.5`인 경우 Guzzle6 버전 사용을 위해 `cos-sdk-v5-6.tar.gz`를 다운로드하십시오. 
> - PHP 버전 `>=7.2.5인 경우 Guzzle7 버전 사용을 위해 `cos-sdk-v5-7.tar.gz`를 다운로드하십시오.
> 
2. 압축 해제 후, `autoload.php` 스크립트를 통해 SDK를 로딩합니다.
```php
require '/path/to/sdk/vendor/autoload.php';
```
>! `Source code` 압축 패키지는 Github 기본 패키지의 코드 패키지이며 `vendor` 디렉터리가 포함되어 있지 않습니다. Source 패키지가 아닌 release 패키지(cos-sdk-v5-x.tar.gz 패키지)를 다운로드하십시오. 전체 라이브러리를 직접 clone하지 마십시오. 그렇지 않으면 index.php 및 vendor 패키지가 누락될 수 있습니다.
>

## 사용하기
COS PHO SDK를 사용한 클라이언트 초기화, 버킷 생성, 버킷 리스트 조회, 객체 업로드, 객체 리스트 조회, 객체 다운로드, 객체 삭제 등의 기본 작업 방법은 아래와 같습니다. 예시에 나온 매개변수 설명은 [버킷 작업](https://intl.cloud.tencent.com/document/product/436/31470) 및 [객체 작업](https://intl.cloud.tencent.com/document/product/436/31542) 문서를 참고하십시오.

### 초기화
영구 키를 사용해 COSClient를 초기화하는 경우, 먼저 CAM 콘솔의 [API 키 관리 페이지](https://console.cloud.tencent.com/cam/capi)에서 SecretId, SecretKey를 획득합니다. 영구 키는 대부분의 응용 시나리오에 적용될 수 있습니다.

[//]: # ".cssg-snippet-global-init"
```php
// SECRETID와 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리
$secretId = "SECRETID"; //"Tencent Cloud API 키 SecretId";
$secretKey = "SECRETKEY"; //"Tencent Cloud API 키 SecretKey";
$region = "COS_REGION"; //기본 버킷 리전 설정
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //프로토콜 헤더, 기본값: http
        'credentials'=> array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
```

>! HTTPS 인증서를 미설정한 경우, schema 매개변수를 삭제하거나 `'schema' => 'http'`를 입력해야 합니다. https를 입력하면 certificate problem이 발생합니다. 인증서를 설정하려면 [PHP SDK FAQ](https://intl.cloud.tencent.com/document/product/436/40543)를 참고하십시오.
>

[임시 키](https://intl.cloud.tencent.com/document/product/436/14048)를 사용하여 초기화하는 경우, 다음 방법으로 인스턴스를 생성하십시오.

[//]: # ".cssg-snippet-global-init-sts"
```php
$tmpSecretId = "SECRETID"; //"임시 키 SecretId";
$tmpSecretKey = "SECRETKEY"; //"임시 키 SecretKey";
$tmpToken = "COS_TOKEN"; //"임시 키 token";
$region = "COS_REGION"; //기본 버킷 리전 설정
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //프로토콜 헤더, 기본값: http
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
```

### 버킷 생성

[//]: # ".cssg-snippet-put-bucket"
```php
try {
    $bucket = "examplebucket-1250000000"; //버킷 이름 형식: BucketName-APPID
    $result = $cosClient->createBucket(array('Bucket' => $bucket));
    //요청 완료
    print_r($result);
} catch (\Exception $e) {
    //요청 실패
    echo($e);
}
```

### 버킷 리스트 조회

[//]: # ".cssg-snippet-get-service"
```php
try {
    //요청 완료
    $result = $cosClient->listBuckets();
    print_r($result);
} catch (\Exception $e) {
    //요청 실패
    echo($e);
}
```


### 객체 업로드
>!
> - putObject 인터페이스를 사용하여 파일을 업로드(최대 5G)합니다.
> - Upload 인터페이스를 사용하여 파일을 멀티파트 업로드합니다. Upload 인터페이스는 복합 업로드 인터페이스로, 용량이 작은 파일은 간편 업로드를 진행하고, 용량이 큰 파일은 멀티파트 업로드를 진행합니다.
> - 매개변수 설명은 [객체 작업](https://intl.cloud.tencent.com/document/product/436/31542#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1) 문서를 참고하십시오.
> 

[//]: # ".cssg-snippet-put-object-comp"
```php
# 파일 업로드
## putObject(업로드 인터페이스, 최대 5G 파일까지 업로드 가능)
### 메모리에 있는 문자열 업로드
try {
    $bucket = "examplebucket-1250000000"; //버킷 이름 형식: BucketName-APPID
    $key = "exampleobject"; //여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자임
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => 'Hello World!'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### 파일 스트림 업로드
try {
    $bucket = "examplebucket-1250000000"; //버킷 이름 형식: BucketName-APPID
    $key = "exampleobject"; //여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자임
    $srcPath = "path/to/localFile";//로컬 파일의 절대 경로
    $file = fopen($srcPath, "rb");
    if ($file) {
        $result = $cosClient->putObject(array(
            'Bucket' => $bucket,
            'Key' => $key,
            'Body' => $file));
        print_r($result);
    }
} catch (\Exception $e) {
    echo "$e\n";
}

## Upload(고급 업로드 인터페이스, 기본적으로 멀티파트 업로드를 사용하며 최대 50TB까지 업로드 지원)
### 메모리에 있는 문자열 업로드
try {    
    $bucket = "examplebucket-1250000000"; //버킷 이름 형식: BucketName-APPID
    $key = "exampleobject"; //여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자임
    $result = $cosClient->Upload(
        $bucket = $bucket,
        $key = $key,
        $body = 'Hello World!');
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### 파일 스트림 업로드
try {    
    $bucket = "examplebucket-1250000000"; //버킷 이름 형식: BucketName-APPID
    $key = "exampleobject"; //여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자임
    $srcPath = "path/to/localFile";//로컬 파일의 절대 경로
    $file = fopen($srcPath, 'rb');
    if ($file) {
        $result = $cosClient->Upload(
            $bucket = $bucket,
            $key = $key,
            $body = $file);
    }
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

### 객체 리스트 조회

[//]: # ".cssg-snippet-get-bucket"
```php
try {
    $bucket = "examplebucket-1250000000"; //버킷 이름 형식: BucketName-APPID
    $result = $cosClient->listObjects(array(
        'Bucket' => $bucket
    ));
    // 요청 완료
    if (isset($result['Contents'])) {
        foreach ($result['Contents'] as $rt) {
            print_r($rt);
        }
    }
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

`listObjects` 인터페이스 1회 호출당 조회 가능한 객체 수는 1000개입니다. 모든 객체를 조회할 경우 순환 호출이 필요합니다.

[//]: # ".cssg-snippet-get-bucket-recursive"
```php
try {
    $bucket = "examplebucket-1250000000"; //버킷 이름 형식: BucketName-APPID
    $prefix = ''; //객체의 접두사 나열
    $marker = ''; //이전에 나열한 객체의 중단 지점
    while (true) {
        $result = $cosClient->listObjects(array(
            'Bucket' => $bucket,
            'Marker' => $marker,
            'MaxKeys' => 1000 //조회 시 출력할 최대 수량 설정, 최대값: 1000
        ));
        if (isset($result['Contents'])) {
            foreach ($result['Contents'] as $rt) {
                // key 출력
                echo($rt['Key'] . "\n");
            }
        }
        $marker = $result['NextMarker']; //새로운 중단 지점 설정
        if (!$result['IsTruncated']) {
            break; //조회 완료 여부 판단
        }
    }
} catch (\Exception $e) {
    echo($e);
}
```

### 객체 다운로드
- getObject 인터페이스를 사용해 파일을 다운로드합니다.
- getObjectUrl 인터페이스를 사용해 파일 다운로드 URL을 획득합니다.

[//]: # ".cssg-snippet-get-object-comp"
```php
# 파일 다운로드
## getObject(파일 다운로드)
### 메모리에 다운로드
try {
    $bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
    $key = "exampleobject"; //여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자임
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key));
    // 요청 완료
    echo($result['Body']);
} catch (\Exception $e) {
    // 요청 실패
    echo "$e\n";
}

### 로컬에 다운로드
try {
    $bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
    $key = "exampleobject"; //여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자임
    $localPath = @"path/to/localFile";//지정된 로컬 경로에 다운로드
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'SaveAs' => $localPath));
} catch (\Exception $e) {
    // 요청 실패
    echo "$e\n";
}

### 다운로드 범위 지정
/*
 * Range 필드 형식: 'bytes=a-b'
 */
try {
    $bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
    $key = "exampleobject"; //여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자임
    $localPath = @"path/to/localFile";//지정된 로컬 경로에 다운로드
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Range' => 'bytes=0-10',
        'SaveAs' => $localPath));
} catch (\Exception $e) {
    // 요청 실패
    echo "$e\n";
}

## getObjectUrl(파일 UrL 획득)
try {    
    $bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
    $key = "exampleobject"; //여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자임
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes');
    // 요청 완료
    echo $signedUrl;
} catch (\Exception $e) {
    // 요청 실패
    print_r($e);
}
```

### 객체 삭제

[//]: # ".cssg-snippet-delete-object-comp"
```php
# object 삭제
## deleteObject
try {
    $bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
    $key = "exampleobject"; //여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자임
    $result = $cosClient->deleteObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'VersionId' => 'string'
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
# 여러 object 삭제
## deleteObjects
try {
    $bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
    $key1 = "exampleobject1";  //여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자임
    $key2 = "exampleobject2";  //여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자임
    $result = $cosClient->deleteObjects(array(
        'Bucket' => $bucket,
        'Objects' => array(
            array(
                'Key' => $key1,
            ),
            array(
                'Key' => $key2,
            ),
            //...
        ),
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```
