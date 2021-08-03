
## 소개

본 문서는 이미지 고급 압축에 대한 API 개요 및 SDK 예시 코드를 제공합니다.


| API           |  작업 설명               |
| :--------------- |  :--------------------- |
| [이미지 고급 압축](https://intl.cloud.tencent.com/document/product/436/40119)|이미지 고급 압축은 이미지를 TPG 또는 HEIF 등 압축 비율이 높은 형식으로 변환하여 이미지 전송 링크 및 로딩 시 소모되는 시간을 효과적으로 단축하고 대역폭 및 트래픽 비용을 절감합니다. |


## 이미지 고급 압축

#### 기능 설명

CI imageMogr2 인터페이스를 통해 고급 이미지 압축 기능을 제공합니다.


#### 예시 코드

```php
try{
        $imageMogrTemplate = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();//기본 이미지 처리 매개변수 템플릿 인스턴스 생성.
        $imageMogrTemplate->format('tpg');//원본 이미지를 TPG 형식으로 변환,
        $imageMogrTemplate->format('heif');//원본 이미지를 HEIF 형식으로 변환.
        $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'ImageHandleParam' => $imageMogrTemplate->queryString(),//기본 이미지 처리 매개변수 생성
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름             | 유형        | 설명                                                         | 필수 입력 여부 |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket               | String      | 버킷 이름. 형식은 BucketName-APPID                           | 예       |
| Key                  | String      | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | 예       |
| ImageHandleParam  | String      | CI 이미지 처리 매개변수，예시: imageMogr2/format/tpg          | 예          |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [ETag] => "698d51a19d8a121ce581499d7b701668"
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ContentLength] => 100
            [ContentType] => image/jpeg
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
        )

)

```

#### 반환 결과 설명

| 매개변수 이름             | 유형        | 설명                                                         | 부모 노드 |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body                 | File/String | 콘텐츠 다운로드                                                     | 없음     |
| ETag                 | String      | 파일의 MD5 값                                                | 없음     |
| ContentLength        | Int         | 응답 본문 길이                                                 | 없음     |
| ContentType          | String      | 콘텐츠 유형. Content-Type 설정                                  | 없음     |
| RequestId             | String      | ID 식별 요청                                | 아니요     |
| Key                  | String      | 객체 키                                     | 없음     |
| Bucket           | String | 버킷 이름. 형식은 BucketName-APPID      | 없음     |
| Location             | String      | 리소스 주소 요청                                 | 없음     |
