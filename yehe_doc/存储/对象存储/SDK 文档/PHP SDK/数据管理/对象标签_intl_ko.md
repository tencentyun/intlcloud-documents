
## 소개

본 문서는 객체 태그에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명       | 작업 설명                     |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | 객체 태그 설정 | 객체의 태그 설정       |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | 객체 태그 조회 | 지정한 객체의 기존 태그 조회 |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | 객체 태그 삭제 | 지정한 객체의 기존 태그 삭제 |

## 객체 태그 설정

#### 기능 설명

PUT Object tagging는 객체에 대한 태그를 설정하는 데 사용됩니다.


#### 메소드 프로토타입

```
public Guzzle\Service\Resource\Model PutObjectTagging(array $args = array());
```

#### 요청 예시


```php
try {
    $result = $cosClient->putObjectTagging(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key'    => 'exampleobject',
        'TagSet' => array(
            array('Key'=>'key1',
                  'Value'=>'value1',
            ),  
            array('Key'=>'key2',
                  'Value'=>'value2',
            ),  
        ),  
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo "$e\n";
}
```

#### 매개변수 설명

| 매개변수 이름   | 설명                                                         | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| bucket | 태그를 설정한 객체의 버킷 이름. 형식은 BucketName-APPID이며, 자세한 내용은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key      | 태그를 설정한 객체 키. 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String                  |
| TagSet    | 객체의 태그 구성 집합                                                     | Array |

TagSet 멤버 설명:

| 매개변수 이름        | 설명 | 유형            |
| ----- | ---- | ---- |
| Key | 태그의 key | String |
| Value | 태그의 value | String |

## 객체 태그 조회

#### 기능 설명

GET Object tagging는 지정한 객체의 기존 태그를 조회하는 데 사용합니다.

#### 메소드 프로토타입

```
public Guzzle\Service\Resource\Model GetObjectTagging(array $args = array());
```

#### 요청 예시

```php
try {
    $result = $cosClient->getObjectTagging(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key'    => 'exampleobject',
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름   | 설명                                                         | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| bucket | 태그를 설정한 객체의 버킷. 형식은 BucketName-APPID이며, 자세한 내용은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key      | 태그를 설정한 객체 키. 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String                  |



#### 반환 결과 예시

```php
GuzzleHttp\Command\Result Object
(
    [TagSet] => Array
        (
            [0] => Array
                (
                    [Key] => key1
                    [Value] => value1
                )

            [1] => Array
                (
                    [Key] => key2
                    [Value] => value2
                )

        )
    [RequestId] => NWRmMWVkMjFfMjJiMjU4NjRfNWQ3X2EwMWVj****
)
```

#### 반환 결과 설명

| 멤버 변수   | 설명     | 유형   |
| -------- | -------- | ------ |
| Key      | 태그의 키 | String |
| Value    | 태그의 값 | String |

## 객체 태그 삭제

#### 기능 설명

DELETE Object tagging는 지정한 객체의 기존 태그를 삭제하는 데 사용합니다.

#### 메소드 프로토타입

```
public Guzzle\Service\Resource\Model DeleteObjectTagging(array $args = array());
```

#### 요청 예시

```php
try {
    $result = $cosClient->deleteObjectTagging(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key'    => 'exampleobject',
    );
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름   | 설명                                                         | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| bucket | 태그를 설정한 객체의 버킷. 형식은 BucketName-APPID이며, 자세한 내용은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key        |태그를 설정한 객체 키. 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |


