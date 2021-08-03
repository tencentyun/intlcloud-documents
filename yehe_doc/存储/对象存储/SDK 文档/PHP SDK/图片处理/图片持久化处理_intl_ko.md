## 소개

본 문서는 이미지 영속화 처리에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 설명                                 |
| :----------------------------------------------------------- | :----------------------------------- |
| [이미지 영속화 처리](https://cloud.tencent.com/document/product/436/54050) |  COS(Cloud Object Storage)에서 제공하는 업로드 처리 기능은 사용자가 업로드 시 이미지 처리를 진행할 수 있도록 도와줍니다. 또한 COS에 저장된 사진에 대해 해당 처리 작업을 수행하고 결과를 COS에 저장할 수 있습니다. |


## 업로드 시 처리

#### 예시 코드

```php
try{
        $imageMogrTemplate = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();//기본 이미지 처리 매개변수 템플릿 인스턴스 생성
        $imageMogrTemplate->thumbnailByScale(50);//이미지의 너비와 높이를 원본 이미지의 50%로 지정.
        $picOperationsTemplate = new \Qcloud\Cos\ImageParamTemplate\PicOperationsTemplate();//이미지 영속화 처리 매개변수 템플릿 인스턴스 생성
        $picOperationsTemplate->setIsPicInfo(1);//원본 사진 정보 반환 여부 설정, 0은 원본 사진 정보 반환하지 않음, 1은 원본 사진 정보 반환, 기본값은 0.
        $picOperationsTemplate->addRule($imageMogrTemplate, "resultobject");//이미지 처리 규칙 설정.
        $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'Body' => fopen('path/to/localFile', 'rb'), 
        'PicOperations' => $picOperationsTemplate->queryString(),//이미지 영속화 처리 매개변수 생성
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
| Body                 | File/String | 업로드한 콘텐츠                                                   | 예       |
| PicOperations    | Json/String      | 이미지 영속화 처리 정보                                  | 예       |


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
            [ContentLength] => 238186
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
            [Data] => Array
            (
                [OriginalInfo] => Array
                (
                    [Key] => exampleobject
                    [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
                    [ETag] => "7037fb6fb4cca43b958a28789605e73d98088720"
                    [ImageInfo] => Array
                    (
                            [Format] => JPEG
                            [Width] => 600
                            [Height] => 500
                            [Quality] => 90
                            [Ave] => 0x46442e
                            [Orientation] => 0
                     )

                )
                [ProcessResults] => Array
                (
                    [Object] => Array
                    (
                        [0] => Array(
                            [Key] => resultobject
                            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/resultobject
                            [Format] => JPEG
                            [Width] => 300
                            [Height] => 200
                            [Size] => 30000
                            [Quality] => 90
                            [ETag] => "87c153bc2909aa0ba111ca126b675c510d36b817"
                        )
                    )
                )
            )
    )
)

```

#### 반환 결과 설명

| 매개변수 이름             | 유형        | 설명                                                         | 부모 노드 |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body                 | File/String | 응답 본문                                                     | 없음     |
| ETag                 | String      | 파일의 MD5 값                                                | 없음     |
| RequestId             | String      | ID 식별 요청                                | 아니요     |
| ContentLength        | Int         |  응답 본문 길이                                                 | 없음     |
| Key                  | String      | 객체 키                                     | 없음     |
| Bucket           | String | 버킷 이름. 형식은 BucketName-APPID      | 없음     |
| Location             | String      | 리소스 요청 주소                                 | 없음     |
| Data                 | Array      | 이미지 처리 결과 정보                              | 없음     |

## 클라우드 데이터 처리

#### 예시코드

```php
try{
        $imageMogrTemplate = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();//기본 이미지 처리 매개변수 템플릿 인스턴스 생성.
        $imageMogrTemplate->thumbnailByScale(50);//이미지의 너비와 높이를 원본 이미지의 50%로 지정.
        $picOperationsTemplate = new \Qcloud\Cos\ImageParamTemplate\PicOperationsTemplate();//이미지 영속화 처리 매개변수 템플릿 인스턴스 생성.
        $picOperationsTemplate->setIsPicInfo(1);//원본 사진 정보 반환 여부 설정, 0은 원본 사진 정보 반환하지 않음, 1은 원본 사진 정보 반환, 기본값은 0.
        $picOperationsTemplate->addRule($imageMogrTemplate, "resultobject");//이미지 처리 규칙 설정.
        $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'PicOperations' => $picOperationsTemplate->queryString(),//이미지 영속화 처리 매개변수 생성.
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
| PicOperations    | Json/String      | 이미지 영속화 처리 정보                                  | 예       |


#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
    (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
            [OriginalInfo] => Array
            (
                [Key] => exampleobject
                [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
                [ETag] => "7037fb6fb4cca43b958a28789605e73d98088720"
                [ImageInfo] => Array
                (
                        [Format] => JPEG
                        [Width] => 600
                        [Height] => 500
                        [Quality] => 90
                        [Ave] => 0x46442e
                        [Orientation] => 0
                    )

            )
            [ProcessResults] => Array
            (
                [Object] => Array
                (
                    [0] => Array(
                        [Key] => resultobject
                        [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/resultobject
                        [Format] => JPEG
                        [Width] => 300
                        [Height] => 200
                        [Size] => 30000
                        [Quality] => 90
                        [ETag] => "87c153bc2909aa0ba111ca126b675c510d36b817"
                    )
                )
            )
    )
)

```

#### 반환 결과 설명

| 매개변수 이름             | 유형        | 설명                                                         | 부모 노드 |
| ------------------ | --------- | --------------------------------| ------ |
| RequestId             | String      | ID 식별 요청                                | 아니요     |
| Key                  | String      | 객체 키                                     | 없음     |
| Bucket           | String | 버킷 이름. 형식은 BucketName-APPID      | 없음     |
| Location             | String      | 리소스 주소 요청                                 | 없음     |
| OriginalInfo         | Array      | 원본 이미지 정보                                    | 없음     |
| ProcessResults       | Array      | 이미지 처리 결과 정보                              |  없음     |

