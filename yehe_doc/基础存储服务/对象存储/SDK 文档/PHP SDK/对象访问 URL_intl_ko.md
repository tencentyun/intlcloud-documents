## 소개

본 문서는 객체 액세스 URL을 획득하는 코드 예시를 제공합니다.

## 객체 액세스 URL 가져오기

#### 기능 설명

객체 액세스 URL을 쿼리합니다.

#### 사용 예시

#### 예시 1
```php
//서명이 있는 객체 다운로드 링크 가져오기
try {    
    $bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
    $key = "exampleobject";  //여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자임
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, ’+10 minutes’);
    // 요청 완료
    echo $signedUrl;
} catch (\Exception $e) {
    // 요청 실패
    print_r($e);
}
```

#### 예시 2

```php
//익명 다운로드 또는 배포를 위해 서명이 없는 객체 다운로드 링크 가져오기
try {
    $bucket = ’examplebucket-125000000’; //버킷. 형식: BucketName-APPID
    $key = "exampleobject"; //여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자임
    $Url = $cosClient -> getObjectUrlWithoutSign($bucket, $key);
    // 요청 완료
    echo $Url;
} catch (\Exception $e) {
    // 요청 실패
    print_r($e);
}
```

>?더 많은 예시는 [사전 서명된 URL](https://intl.cloud.tencent.com/document/product/436/31544)을 참고하시기 바랍니다.

#### 매개변수 설명

| 매개변수 이름  | 매개변수 설명                                                     | 유형    | 필수 입력 여부 |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | 버킷의 이름. 이름 생성 규칙은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 형식을 따라야 합니다. | String  | Yes   |
| Key     | 객체 키(Object 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String  | Yes   |
| Expires | 서명은 몇 초 후에 만료되며 기본값은 1800초입니다.                                  | String  | Yes   |

#### 반환 결과 설명

메소드 반환값은 객체 액세스 URL입니다.
