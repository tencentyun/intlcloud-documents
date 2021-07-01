
## 소개

본 문서는 이미지 고급 압축에 대한 API 개요 및 SDK 예시 코드를 제공합니다.


|API           |작업 설명               |
| :--------------- |  :--------------------- |
| [이미지 고급 압축](https://intl.cloud.tencent.com/document/product/436/40119)|   이미지 고급 압축은 이미지를 TPG 또는 HEIF 등 압축 비율이 높은 포맷으로 변환하여 이미지 전송 링크 및 로딩 시 소모되는 시간을 효과적으로 단축하고 대역폭 및 트래픽 비용을 절감합니다.|


#### 요청 예시

```
// 원본 이미지를 TPG 포맷으로 변환
name := "test.png"
filepath := "test.tpg"
_, err := c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/format/tpg", nil)
if err! = nil {
	// ERROR
}

// 원본 이미지를 HEIF 포맷으로 변환
filepath = "test.heif"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/format/heif", nil)
if err! = nil {
	// ERROR
}
```
