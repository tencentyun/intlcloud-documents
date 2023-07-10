## 소개

본문은 버킷 Referer 에 대한 화이트/블랙리스트의 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름         | 작업 설명                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://cloud.tencent.com/document/product/436/32492) | 버킷 Referer 설정 | 버킷 Referer 화이트 또는 블랙리스트 설정 |
| [GET Bucket referer](https://cloud.tencent.com/document/product/436/32493) | 버킷 Referer 쿼리| 버킷 Referer 화이트 또는 블랙리스트 쿼리 |

## 버킷 Referer 설정

#### 기능 설명

버킷 Referer 화이트 또는 블랙리스트를 설정합니다(PUT Bucket referer).

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model putBucketReferer(array $args = array());
```

#### 요청 예시

```php
try {
    $result = $cosClient->putBucketReplication(array(
            'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
            'Status' => 'Enabled', //링크 도용 방지 활성화 여부를 나타내며 열거 값은 Enabled, Disabled입니다.
            'RefererType' => 'White-List', //링크 도용 방지 유형을 나타내며 열거 값은 Black-List, White-List입니다.
            'DomainList' => array(
                'Domains' => array(
                     '*.qq.com', //단일 적용 도메인
                     '*.qcloud.com', //단일 적용 도메인
                )
            ), //적용 도메인 리스트
            'EmptyReferConfiguration' => 'Allow', //비어 있는 Referer 액세스 허용 여부를 나타내며 열거 값은 Allow, Deny로 기본값은 Deny입니다.
        ),      
    ); 
    // 요청 완료    
    print_r($result);
} catch (\Exception $e) {   
    // 요청 실패
    echo($e);
}
```
#### 매개변수 설명

| 매개변수 이름  | 매개변수 설명                                                     | 유형    | 필수 입력 여부 |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | 버킷의 이름. 이름 생성 규칙은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 형식을 따라야 합니다. | String  | 예   |
| Status         | 링크 도용 방지 활성화 여부, 열거 값: Enabled, Disabled           | String | 필수   |
| RefererType    | 링크 도용 방지 유형 열거 값: Black-List, White-List          | String | 필수   |
| DomainList | 적용 도메인 리스트 | Array |필수   |
| EmptyReferConfiguration | 빈 Refer 액세스 허용 여부, 열거 값: Allow, Deny, 기본값: Deny | String | 옵션  |

## 버킷 Referer 쿼리

#### 기능 설명

버킷의 Referer의 화이트 또는 블랙리스트를 쿼리합니다(PUT Bucket referer).

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model getBucketReferer(array $args = array());
```

#### 요청 예시

```php
try {
    $result = $cosClient->getBucketReferer(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름  | 매개변수 설명                                                     | 유형    | 필수 입력 여부 |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | 버킷의 이름. 이름 생성 규칙은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 형식을 따라야 합니다. | String  | 예   |

#### 반환 결과 예시
```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjE0NTk2ZWVfZmQzNDJjMGJfMWNiNmVfN2Y1MWQx
    [ContentType] => application/xml
    [ContentLength] => 260
    [Status] => Enabled
    [RefererType] => White-List
    [EmptyReferConfiguration] => Allow
    [DomainList] => Array
        (
            [Domain] => Array
                (
                    [0] => *.qq.com
                    [1] => *.qcloud.com
                )

        )

    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/
)
```
