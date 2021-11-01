## 소개

본문은 기본 도메인이 아닌 도메인으로 Cloud Object Storage(COS) 서비스를 요청하는 방법을 제공합니다.

## 관련 매개변수 설명

매개변수 초기화로 요청 도메인을 제어합니다. 매개변수 관련 설명은 아래와 같습니다.

| 매개변수 이름                 | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Domain                 | 버킷 및 객체 작업 API 호출 시 요청 도메인을 사용자 정의합니다. `"{$Bucket}.cos.{Region}.myqcloud.com" `과 같은 템플릿을 사용할 수 있으며, API 호출 시 매개변수에 전달된 Bucket 및 Region으로 대체할 수 있습니다. | String   | 아니요   |
| Protocol               | 요청 시 사용하는 프로토콜. 옵션 항목으로 `https:`와 `http:`가 있습니다. 기본적으로 현재 페이지가 `http:`인 경우 `http:`를 사용하고, 아닌 경우 `https:`를 사용합니다. | String   | 아니요   |

## 기본 CDN 가속 도메인

기본 가속 도메인 활성화 방법은 [기본 CDN 가속 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31505)를 참고하십시오.

기본 가속 도메인을 사용해 COS 서비스에 액세스하는 방법은 다음 예시 코드와 같습니다.

```php
$bucket = "examplebucket-1250000000";

$cosClient = new Qcloud\Cos\Client(
    array(
        'domain' => $bucket . '.file.myqcloud.com', //기본 가속 도메인
        'schema' => 'https', //프로토콜 헤더, 기본값: http
        'credentials'=> array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey
        )
    )
);
```

## 사용자 정의 CDN 가속 도메인

CDN 사용자 정의 가속 도메인 활성화 방법은 [사용자 정의 CDN 가속 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31506)를 참고하십시오.

사용자 정의 가속 도메인을 사용해 COS 서비스에 액세스하는 방법은 다음 예시 코드와 같습니다.

```php
$cosClient = new Qcloud\Cos\Client(
    array(
        'domain' => 'example-cdn-domain.com', //기본 가속 도메인
        'schema' => 'https', //프로토콜 헤더, 기본값: http
        'credentials'=> array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey
        )
    )
);
```

## 사용자 정의 원본 서버 도메인

사용자 정의 원본 서버 도메인 설정 방법은 [사용자 정의 원본 서버 도메인](https://intl.cloud.tencent.com/document/product/436/31507)을 참고하십시오.

사용자 정의 원본 서버 도메인을 사용해 COS 서비스에 액세스하는 방법은 다음 예시 코드와 같습니다.

```php
$cosClient = new Qcloud\Cos\Client(
    array(
        'domain' => 'example-cos-domain.com', //기본 가속 도메인
        'schema' => 'https', //프로토콜 헤더, 기본값: http
        'credentials'=> array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey
        )
    )
);
```

## 글로벌 가속 도메인

글로벌 가속 기능에 대한 자세한 내용은 [글로벌 가속 기능 개요](https://intl.cloud.tencent.com/document/product/436/33409)를 참고하십시오.

글로벌 가속 도메인을 사용해 COS 서비스에 액세스하는 방법은 다음 예시 코드와 같습니다.

```php
//{$bucket}.cos.{$region}.myqcloud.com/key를
//{$bucket}.cos.accelerate.myqcloud.com/key로 전환
$cosClient = new Qcloud\Cos\Client(
    array(
        'schema' => 'https', //프로토콜 헤더, 기본값: http
        'credentials'=> array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey
        ),
        'allow_accelerate' => true // true로 지정 시, 글로벌 가속 도메인 요청 사용
    )
);
```
