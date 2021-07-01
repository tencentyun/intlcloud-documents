
## 소개

본 문서는 기본 이미지 처리에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 설명                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [크기 조정](https://intl.cloud.tencent.com/document/product/436/36366) | 이미지 확대 및 축소                                         |
| [자르기](https://intl.cloud.tencent.com/document/product/436/36367) | 일반 자르기, 크기 조정 자르기, 원형 자르기, 둥근 모서리 자르기, 스마트 얼굴 자르기를 포함한 이미지 편집 |
| [회전](https://intl.cloud.tencent.com/document/product/436/36368) | 일반 회전 및 자동 회전을 포함한 이미지 회전                     |
| [포맷 변환](https://intl.cloud.tencent.com/document/product/436/36369) | 이미지 포맷 변환, gif 포맷 최적화, 점진적 표시                   |
| [품질 변경](https://intl.cloud.tencent.com/document/product/436/36370) | 이미지 품질 조정                                           |
| [가우시안 블러](https://intl.cloud.tencent.com/document/product/436/36371) | 이미지 가우시안 블러 처리                                           |
| [샤프닝](https://intl.cloud.tencent.com/document/product/436/36372) | 이미지 샤프닝 처리                                               |
| [이미지 워터마크](https://intl.cloud.tencent.com/document/product/436/36373) | 이미지 워터마크 처리                                           |
| [문자 워터마크](https://intl.cloud.tencent.com/document/product/436/36374) | 이미지에 실시간 문자 워터마크 처리                                   |
| [이미지 기본 정보 획득](https://intl.cloud.tencent.com/document/product/436/36375) | 포맷, 길이, 폭 등 이미지 기본 정보 조회                         |
| [이미지 EXIF 획득](https://intl.cloud.tencent.com/document/product/436/36376) | EXIF 정보 조회                                               |
| [이미지 메인 컬러 획득](https://intl.cloud.tencent.com/document/product/436/36377) | 이미지 메인 컬러 정보 조회                                           |
| [메타 정보 제거](https://intl.cloud.tencent.com/document/product/436/36378) | exif 정보를 포함한 이미지 메타 정보 제거                               |
| [빠른 썸네일 템플릿](https://intl.cloud.tencent.com/document/product/436/36379) | 이미지 처리 템플릿을 통해 알맞은 썸네일 생성                           |
| [파이프 연산자](https://intl.cloud.tencent.com/document/product/436/36380) | 순서대로 이미지에 여러 처리 효과 구현                                 |

## 크기 조정

#### 기능 설명

Tencent Cloud CI는 **imageMogr2** 인터페이스를 통해 이미지 크기 조정 기능을 제공합니다.

#### 방법 모델
```go
func (s *CIService) Get (ctx context.Context, key string, operation string, opt *ObjectGetOptions, id...string) (*Response, error)

func (s *CIService) GetToFile (ctx context.Context, key, localpath, operation string, opt *ObjectGetOptions, id...string) (*Response, error)
```

#### 요청 예시
```go
name := "test.jpg"
// Case 1 응답 본문에서 객체 가져오기
resp, err := c.CI.Get(context.Background(), name, "imageMogr2/thumbnail/!50px", nil)
if err! = nil {
	//ERROR
}
defer resp.Body.Close()
ioutil.ReadAll(resp.Body)

// Case 2 파일에 객체 다운로드
filepath := "test.jpg"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/thumbnail/! 50px", nil)
```

#### 매개변수 설명

| 매개변수 이름         | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| :--------------- | :----------------------------------------------------------- | :----- | :------- |
| key              | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string | 예       |
| operation        | 해당 매개변수로 크기 조정, 자르기, 회전, 포맷 변환, 품질 변경 등 기본 이미지 처리 기능 | string | 예       |
| ObjectGetOptions | 객체 다운로드 매개변수. 자세한 내용은 [객체 다운로드](https://intl.cloud.tencent.com/document/product/436/31526) 참조 | string | 아니요       |
| id               | 객체 VersionId                                                | string | 아니요       |

## 자르기

#### 기능 설명

Tencent Cloud CI는 **imageMogr2** 인터페이스를 통해 일반 자르기, 크기 조정 자르기, 원형 자르기, 둥근 모서리 자르기, 스마트 얼굴 자르기 등을 포함한 자르기 기능을 제공합니다.

#### 요청 예시

```go
name := "test.jpg"
filepath := "test.jpg"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/cut/600x600x100x10", nil)
```

## 기타 기본 이미지 처리

#### 기능 설명

기본 이미지 처리는 위 방법을 통합적으로 사용합니다. 기타 기본 이미지 처리는 operation 매개변수 값을 수정하면 됩니다. 다음은 이미지를 시계방향으로 90도 회전할 경우의 예시입니다.
```go
name := "test.jpg"
filepath := "test.jpg"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/rotate/90", nil)
```

