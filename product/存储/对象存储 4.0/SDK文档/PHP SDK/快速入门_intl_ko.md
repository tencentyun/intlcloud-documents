본 문서는 COS PHP SDK V5 버전 시작 가이드를 사용하는 방법을 소개합니다. XML API는 [XML API 소개](https://cloud.tencent.com/document/product/436/7751)를 참조하십시오.

## 환경 준비
*   PHP 5.3+
    `php -v` 명령을 통해 현재의 PHP 버전을 볼 수 있습니다.
*   cURL 확장
    `php -m` 명령을 통해 cURL 확장이 설치되었는지 확인할 수 있습니다.

>- Ubuntu 시스템에서 apt-get 패키지 매니저를 사용하여 PHP의 cURL 확장을 설치할 수 있으며 설치 명령은 다음과 같습니다.
```
sudo apt-get install php-curl
```
>- CentOS 시스템에서 yum 패키지 매니저를 사용하여 PHP의 cURL 확장을 설치할 수 있습니다.
```
sudo yum install php-curl
```

## SDK 설치
SDK 설치는 세 가지 방식이 있습니다.
* Composer 방식.
* Phar 방식.
* 소스 코드 방식

### Composer 방식
사용자가 Composer를 사용하여 cos-php-sdk-v5를 설치할 것을 권장합니다. Composer는 PHP의 중속성 관리 도구로서, 프로젝트가 필요로 하는 종속성을 선언하고, 자동으로 프로젝트에 설치할 수 있습니다.
>?[Composer 공식 웹사이트](https://getcomposer.org/)에서 Composer 설치 방법, 자동 로드 구성 및 의존 항목을 정의하는 데 사용하는 기타 모범 사례 등에 관한 더 많은 내용을 찾을 수 있습니다.

#### 설치 절차:
1. 터미널을 엽니다.
2. Composer를 다운로드합니다. 다음 명령을 실행합니다.
```
curl -sS https://getcomposer.org/installer | php
```
3. 이름이 `composer.json`인 파일을 생성합니다. 내용은 다음과 같습니다.
```
{
    "require": {
        "qcloud/cos-sdk-v5": "1.*"
    }
}
```
4. Composer를 사용하여 설치합니다. 다음 명령을 실행합니다.
```
php composer.phar install
```
해당 명령을 사용한 후 현재 디렉터리에서 vendor 폴더를 생성하여, 그 안에 SDK의 의존 라이브러리 및 autoload.php 스크립트를 포함하여 프로젝트에서 편리하게 호출할 수 있습니다.
5. autoloader 스크립트를 통해 cos-php-sdk-v5를 호출합니다.
```
require '/path/to/sdk/vendor/autoload.php';
```

이제 프로젝트는 COS V5 버전 SDK를 사용할 준비가 되었습니다.

### Phar 방식
Phar 방식으로 SDK를 설치하는 절차는 다음과 같습니다.
1. [GitHub 릴리스 페이지](https://github.com/tencentyun/cos-php-sdk-v5/releases)에서 해당하는 phar 파일을 다운로드합니다.
2. 코드에 phar 파일을 가져옵니다.
```
require  '/path/to/cos-sdk-v5.phar';
```

### 소스 코드 방식
소스 코드 방식으로 SDK를 설치하는 절차는 다음과 같습니다.
1. [GitHub 릴리스 페이지](https://github.com/tencentyun/cos-php-sdk-v5/releases)에서 해당하는 cos-sdk-v5.tar.gz 압축 파일을 다운로드합니다.
2. 압축을 플고 autoload.php 스크립트를 통해 SDK를 로드합니다.
```
require '/path/to/sdk/vendor/autoload.php';
```

## 시작 가이드
데모를 참조할 수 있습니다. 자세한 내용은 [sample.php](https://github.com/tencentyun/cos-php-sdk-v5/blob/master/sample.php)를 참조하십시오.

## API 문서
자세한 정보는 PHP SDK [API 문서](https://cloud.tencent.com/document/product/436/12267)를 참조하십시오.

### 구성 파일
```php
$cosClient = new Qcloud\Cos\Client(array('region' => '<Region>',
    'credentials'=> array(
        'secretId'    => '<SecretId>',
        'secretKey' => '<SecretKey>')));
```

[임시 키](https://cloud.tencent.com/document/product/436/14048)를 사용하여 초기화하는 경우, 다음의 방식을 사용하여 인스턴스를 생성하십시오.

```
$cosClient = new Qcloud\Cos\Client(array('region' => '<Region>',
    'credentials'=> array(
        'secretId'    => '<SecretId>',
        'secretKey' => '<SecretKey>',
        'token' => '<XCosSecurityToken>')));
```

### 파일 업로드
* putObject API를 사용하여 파일 업로드(최대 5GB)
* Upload API를 사용하여 파일 멀티파트 업로드

```php
# 파일 업로드
## putObject(업로드 API, 최대 5GB 파일 업로드 지원)
### 업로드 메모리의 문자열
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
try {
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => 'Hello World!'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### 업로드 파일 스트림
try {
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => fopen($local_path, 'rb')));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### header 및 meta 설정
try {
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => fopen($local_path, 'rb'),
        'ACL' => 'string',
        'CacheControl' => 'string',
        'ContentDisposition' => 'string',
        'ContentEncoding' => 'string',
        'ContentLanguage' => 'string',
        'ContentLength' => integer,
        'ContentType' => 'string',
        'Expires' => 'mixed type: string (date format)|int (unix timestamp)|\DateTime',
        'GrantFullControl' => 'string',
        'GrantRead' => 'string',
        'GrantWrite' => 'string',
        'Metadata' => array(
            'string' => 'string',
        ),
        'StorageClass' => 'string'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

## Upload(고급 업로드 API, 기본으로 멀티파트 업로드이며 최대 50TB 지원)
### 업로드 메모리의 문자열
try {
    $result = $cosClient->Upload(
        $bucket = $bucket,
        $key = $key,
        $body = 'Hello World!');
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### 업로드 파일 스트림
try {
    $result = $cosClient->Upload(
        $bucket = $bucket,
        $key = $key,
        $body = fopen($local_path, 'rb'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### header 및 meta 설정
try {
    $result = $cosClient->Upload(
        $bucket= $bucket,
        $key = $key,
        $body = fopen($local_path, 'rb'),
        $options = array(
            'ACL' => 'string',
            'CacheControl' => 'string',
            'ContentDisposition' => 'string',
            'ContentEncoding' => 'string',
            'ContentLanguage' => 'string',
            'ContentLength' => integer,
            'ContentType' => 'string',
            'Expires' => 'mixed type: string (date format)|int (unix timestamp)|\DateTime',
            'GrantFullControl' => 'string',
            'GrantRead' => 'string',
            'GrantWrite' => 'string',
            'Metadata' => array(
                'string' => 'string',
            ),
            'StorageClass' => 'string'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

### 파일 다운로드
* getObject API를 사용하여 파일 다운로드
* getObjectUrl API를 사용하여 파일 다운로드 URL 획득

```php
# 파일 다운로드
## getObject(파일 다운로드)
### 메모리에 다운로드
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key));
    echo($result['Body']);
} catch (\Exception $e) {
    echo "$e\n";
}

### 로컬에 다운로드
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'SaveAs' => $local_path));
} catch (\Exception $e) {
    echo "$e\n";
}

### 다운로드 범위 지정
/*
 * Range 필드 형식은 'bytes=a-b'입니다
 */
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Range' => 'bytes=0-10',
        'SaveAs' => $local_path));
} catch (\Exception $e) {
    echo "$e\n";
}

### 반환 header 설정
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'ResponseCacheControl' => 'string',
        'ResponseContentDisposition' => 'string',
        'ResponseContentEncoding' => 'string',
        'ResponseContentLanguage' => 'string',
        'ResponseContentType' => 'string',
        'ResponseExpires' => 'mixed type: string (date format)|int (unix timestamp)|\DateTime',
        'SaveAs' => $local_path));
} catch (\Exception $e) {
    echo "$e\n";
}

## getObjectUrl(파일 UrL 획득)
try {
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes');
    echo $signedUrl;
} catch (\Exception $e) {
    print_r($e);
}
```
