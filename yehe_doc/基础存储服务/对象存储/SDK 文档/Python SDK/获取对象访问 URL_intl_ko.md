## 소개
본 문서는 객체 액세스 URL을 획득하는 코드 예시를 제공합니다.

## 객체 액세스 URL 획득

#### 기능 설명
객체 액세스 URL을 획득하여 익명 다운로드 또는 배포에 사용합니다.

#### 방법 모델

```
get_object_url(Bucket, Key)
```

#### 요청 예시


[//]: # (.cssg-snippet-get-object-url-alias)
```python
response = client.get_object_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket  |버킷 이름은 BucketName-APPID로 구성 |  String |  예 | 
 | Key  | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg | String | 예 | 

#### 반환 결과 설명

해당 방법의 반환값은 객체 액세스 URL입니다.
