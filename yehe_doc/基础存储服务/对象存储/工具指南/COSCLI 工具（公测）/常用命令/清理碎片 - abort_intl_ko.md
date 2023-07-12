abort 명령어는 멀티파트 업로드 프로세스 중에 생성된 파일 조각을 정리하는 데 사용됩니다.

## 명령어 형식

```plaintext
./coscli abort cos://<bucketAlias>[/prefix/] [flag]
```

>? 
>- bucketAlias 관련 설명은 [다운로드 및 설치 설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>- 이 명령의 다른 범용 옵션(예시: 버킷 전환, 사용자 계정 전환 등)은 [범용 옵션](https://intl.cloud.tencent.com/document/product/436/46273) 문서를 참고하십시오.
>

abort 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                |
| --------- | ------------- | ------------------------ |
|     없음      | --include     | 특정 패턴이 포함된 파일       |
|     없음      | --exclude     | 특정 패턴이 제외된 파일       |

## 작업 예시

### bucket1의 모든 파일 조각 지우기

```plaintext
./coscli abort cos://bucket1
```

### bucket1 버킷의 pictrue 폴더 아래에 있는 모든 조각 지우기

```plaintext
./coscli abort cos://bucket1/pictrue/
```
