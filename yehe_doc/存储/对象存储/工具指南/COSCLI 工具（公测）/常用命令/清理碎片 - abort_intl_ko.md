abort 명령어는 멀티파트 업로드 프로세스 중에 생성된 파일 조각을 정리하는 데 사용됩니다.

## 명령어 형식

```plaintext
./coscli abort cos://<bucketAlias>[/prefix/] [flag]
```

>? bucketAlias 관련 내용은 [설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>

abort 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                |
| --------- | ------------- | ------------------------ |
| -h        | --help        | 도움말 정보 출력             |
| -c        | --config-path | 사용할 프로파일 경로 지정       |
|     없음      | --include     | 특정 패턴이 포함된 파일       |
|     없음      | --exclude     | 특정 패턴이 제외된 파일       |

## 작업 예시

### bucket1의 모든 파일 조각 지우기

```plaintext
./coscli abort cos://bucket1
```

### bucket1 버킷의 picture 폴더 아래에 있는 모든 조각 지우기

```plaintext
./coscli abort cos://bucket1/picture/
```
