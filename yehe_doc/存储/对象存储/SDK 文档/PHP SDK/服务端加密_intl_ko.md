
업로드한 객체에 대해 다음과 같은 암호화 방식을 지원합니다.

#### COS에서 호스팅하는 암호화 키를 사용한 서버 암호화(SSE-COS)로 데이터 보호

Tencent Cloud COS에서 마스터 키를 호스팅하고 데이터를 관리합니다. COS는 데이터센터에 데이터를 쓸 때 자동으로 암호화하며, 해당 데이터 사용 시 자동으로 복호화합니다. 현재 COS의 마스터 키를 사용한 AES-256 데이터 암호화를 지원합니다.

[//]: # (.cssg-snippet-put-object-sse)
```php
try {
    $result = $cosClient->putObject(array(
	        'Bucket' => 'examplebucket-125000000', //형식:BucketName-APPID
	        'Key' => 'exampleobject'
	        'Body' => 'string',
	        'ServerSideEncryption' => 'AES256',//SSE-COS 암호화
	    ),
	);
    print_r ($result);
} catch (Qcloud\Cos\Exception\ServiceResponseException $e) {
    echo $e;
}
```

#### 고객이 제공한 암호화 키를 사용한 서버 암호화(SSE-C)로 데이터 보호

암호화 키를 사용자가 제공하며, 사용자가 객체 업로드 시 COS가 사용자가 제공한 암호화 키를 사용하여 사용자 데이터에 대해 AES-256 암호화를 진행합니다. SDK는 업로드 시 `SSE` 관련 헤더 필드 설정을 통해 이를 완료합니다.

> !
>- 해당 암호화로 실행되는 서비스는 HTTPS를 사용해 요청해야 합니다.
>- customerKey: 사용자가 제공한 키로 32 바이트의 문자열입니다. 숫자, 알파벳, 문자 조합을 지원하지만 중국어는 지원하지 않습니다.
>- 업로드하는 원본 파일에서 해당 메소드를 호출하는 경우 GET(다운로드), HEAD(조회) 사용 시, 원본 객체를 작업할 때에도 해당 메소드를 호출합니다.

[//]: # (.cssg-snippet-put-object-sse-c)
```php
require 'vendor/autoload.php';

$secretId = "SECRETID"; //"Tencent Cloud API 키 SecretId";
$secretKey = "SECRETKEY"; //"Tencent Cloud API 키 SecretKey";
$region = "ap-beijing"; //기본 버킷 리전 설정
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //프로토콜 헤더, 기본값: http, SSE-C는 반드시 https 프로토콜 사용
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey
        )
    )
);

$bucket = 'examplebucket-125000000'; //형식: BucketName-APPID
$key = 'exampleobject';
try {
    $customerKey = 'abcdefghijklmnopqrstuvwxyz123456'; //32 바이트의 문자열입니다. 숫자, 알파벳, 문자 조합을 지원하지만 중국어는 지원하지 않습니다.
    $SSECustomerKey = base64_encode($customerKey);
    $SSECustomerKeyMd5 = base64_encode(md5($customerKey, true));
    $result = $cosClient->putObject(array(
            'Bucket' => $bucket, 
            'Key' => $key,
            'Body' => 'string',
            'SSECustomerAlgorithm' => 'AES256',
            'SSECustomerKey' => $SSECustomerKey,
            'SSECustomerKeyMD5' => $SSECustomerKeyMd5,
        )); 
    print_r ($result);
} catch (Qcloud\Cos\Exception\ServiceResponseException $e) {
    echo $e; 
}
```
