## 소개

본문은 객체 액세스 URL을 획득하는 코드 예시를 제공합니다.

## 객체 액세스 URL 획득

#### 기능 설명

객체 액세스 URL을 획득하여 익명 다운로드 또는 배포에 사용합니다.

>! COS Go SDK는 v0.7.26 이후 버전이어야 합니다.

#### 메소드 프로토타입 

```
func (s *ObjectService) GetObjectURL(key string) *url.URL
```

#### 요청 예시


[//]: # (.cssg-snippet-get-object-url-alias)
```go
name := "exampleobject"
ourl := c.Object.GetObjectURL(name)
```

#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
| Key  | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String | 필수 |

#### 반환 결과 설명

해당 메소드의 반환값은 객체 액세스 URL입니다.
