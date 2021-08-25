
## 개요

본 문서는 이미지 스타일 관련 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 설명                                 |
| :----------------------------------------------------------- | :--------- |
| [스타일 추가](https://intl.cloud.tencent.com/document/product/1045/33708)  | 버킷 스타일 추가  |
|  [스타일 조회](https://intl.cloud.tencent.com/document/product/1045/33707)  | 버킷 스타일 조회       |
|  [스타일 삭제](https://intl.cloud.tencent.com/document/product/1045/33709)   |  버킷 스타일 삭제 |


## 스타일 추가

#### 기능 설명

버킷에 대한 스타일 기능을 설정하면 이후 버킷에 업로드되는 이미지 파일에 지정된 스타일이 추가됩니다.

#### 예시 코드

```php
try {
        $result = $cosClient->PutBucketImageStyle(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'StyleName' => 'style_name',//스타일 이름
        'StyleBody' => 'imageMogr2/thumbnail/!50px', //스타일 정보
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
| Bucket               | String      | 버킷 이름. 형식: BucketName-APPID                           | 예       |
| StyleName          | String      | 스타일 이름                        | 예       |
| StyleBody          | String      | 스타일 정보                        | 예       |


#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.pic.ap-beijing.myqcloud.com/
        )
)

```

#### 반환 결과 설명

| 매개변수 이름             | 유형        | 설명                                                         | 부모 노드 |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| RequestId             | String      | ID 식별 요청                                | 없음     |
| Bucket           | String | 버킷 이름. 형식: BucketName-APPID      | 없음     |
| Location             | String      | 리소스 주소 요청                                 | 없음     |

## 스타일 조회

#### 기능 설명

버킷 아래의 기존 스타일을 조회합니다.

#### 예시 코드
```php
try {
        $result = $cosClient->GetBucketImageStyle(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'StyleName' => 'style_name', //스타일 이름
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
| Bucket               | String      | 버킷 이름. 형식: BucketName-APPID                           | 예       |
| StyleName       | String      | 스타일 이름                                               | 아니요       |


#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.pic.ap-beijing.myqcloud.com/
            [StyleRule] => Array(
                [0] => Array(
                    [StyleName] => style_name
                    [StyleBody] => imageMogr2/thumbnail/!50px
                )
            )
       )
)

```

#### 반환 결과 설명

| 매개변수 이름             | 유형        | 설명                                                         | 부모 노드 |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| RequestId             | String      | ID 식별 요청                                | 없음     |
| Bucket           | String | 버킷 이름. 형식: BucketName-APPID      | 없음     |
| Location             | String      | 리소스 주소 요청                                 | 없음     |
| StyleRule             | Array      | 스타일 정보 리스트                                 | 없음     |

## 스타일 삭제

#### 기능 설명

특정 스타일을 삭제합니다.

#### 예시 코드
```php
try {
        $result = $cosClient->DeleteBucketImageStyle(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'StyleName' => 'style_name', //스타일 이름
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
| Bucket               | String      | 버킷 이름. 형식: BucketName-APPID                           | 예       |
| StyleName       | String      | 스타일 이름                                               | 예       |


#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.pic.ap-beijing.myqcloud.com/
       )
)

```

#### 반환 결과 설명

| 매개변수 이름             | 유형        | 설명                                                         | 부모 노드 |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| RequestId             | String      | ID 식별 요청                                | 없음     |
| Bucket           | String | 버킷 이름. 형식: BucketName-APPID      | 없음     |
| Location             | String      | 리소스 주소 요청                                 | 없음     |

