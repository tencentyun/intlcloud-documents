
du 명령어는 버킷 또는 폴더에 있는 각 스토리지 유형 파일의 통계 정보 나열에 사용됩니다. 통계 정보에는 다양한 스토리지 유형의 총 파일 수와 각 파일 유형의 총 크기가 포함됩니다.

## 명령어 형식

```plaintext
./coscli du cos://<bucketAlias>[/prefix/] [flag]
```

>? bucketAlias 관련 내용은 [설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>

ls 명령어에는 다음과 같은 매개변수 옵션이 포함됩니다.

| 매개변수 형식 | 매개변수 용도       | 예시                 |
| -------- | -------------- | -------------------- |
| /prefix/ | 폴더 지정 | cos://bucket1/picture/ |

du 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                |
| --------- | ------------- | ------------------------ |
| -h        | --help        | 도움말 정보 출력             |
| -c        | --config-path | 사용할 프로파일 경로 지정 |
|    없음       | --include     | 특정 패턴이 포함된 파일       |
|      없음       | --exclude     | 특정 패턴이 제외된 파일       |

>? 
>- `--include`는 표준 정규식 구문을 지원하므로 파일 특정 조건 필터링에 사용할 수 있습니다.
>- zsh를 사용할 때 pattern 문자열의 양쪽 끝에 큰따옴표를 넣어야 할 수도 있습니다.
```plaintext
./coscli du cos://bucket1/picture/ --include ".*.mp4"
```

## 작업 예시

### bucket1에 있는 파일 통계 정보 나열

```plaintext
./coscli du cos://bucket1
```

### bucket1의 pictrue 폴더에 있는 파일 통계 정보 나열

```plaintext
./coscli du cos://bucket1/pictrue/
```

### bucket1 pictrue 폴더에 있는 모든 .mp4 형식 파일 통계 정보 나열

```plaintext
./coscli du cos://bucket1/picture/ --include .*.mp4
```

### bucket1의 pictrue 폴더에 있는 파일 중 .md 형식이 아닌 모든 파일 통계 정보 나열

```plaintext
./coscli du cos://bucket1/picture/ --exclude .*.md
```
