

API 호출에 실패하면, 최종 반환 결과 중 오류 코드 code는 0이 아니며, message 필드에는 상세 오류 정보가 표시됩니다. 사용자는 code와 message에 따라 [오류 코드](https://cloud.tencent.com/document/product/1014/31229) 페이지에서 구체적인 오류 정보를 조회할 수 있습니다.
오류 반환 예시는 다음과 같습니다.

```
{
    "code": 5100,
    "message": "(100004)projectId틀렸습니다"
}
```

