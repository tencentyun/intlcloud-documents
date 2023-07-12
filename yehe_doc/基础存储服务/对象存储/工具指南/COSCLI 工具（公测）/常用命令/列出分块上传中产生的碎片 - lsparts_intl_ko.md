lsparts 명령어는 멀티파트 업로드에서 생성된 파일 조각을 나열합니다.

## 명령어 형식

```plaintext
./coscli lsparts cos://<bucketAlias>[/prefix/] [flag]
```

>? 
>- bucketAlias 관련 설명은 [다운로드 및 설치 설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>- 이 명령의 다른 범용 옵션(예시: 버킷 전환, 사용자 계정 전환 등)은 [범용 옵션](https://intl.cloud.tencent.com/document/product/436/46273) 문서를 참고하십시오.
>

lsparts 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                  |
| --------- | ------------- | ---------------------------- |
|     없음      | --include     | 특정 패턴이 포함된 파일       |
|     없음      | --exclude     | 특정 패턴이 제외된 파일       |
|     없음      | --limit       | 최대 나열 수량 지정(0-1000) |

## 작업 예시

### bucket1의 모든 파일 조각 나열

```plaintext
./coscli lsparts cos://bucket1
```

### bucket1의 pictrue 폴더에 있는 모든 조각 나열

```plaintext
./coscli lsparts cos://bucket1/pictrue/
```
