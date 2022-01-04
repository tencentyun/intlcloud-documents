## 명령어 형식

sync 명령어는 파일을 동기화 업로드, 다운로드 또는 복사에 사용되며 cp 명령어와의 차이점은 sync 명령어는 먼저 같은 이름의 파일의 crc64를 비교하고 crc64 값이 같으면 전송하지 않는다는 것입니다.

```plaintext
./coscli sync <source_path> <destination_path> [flag]
```

>? bucketAlias 관련 내용은 [설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.

sync 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                      |
| --------- | ------------- | ------------------------------ |
| -h        | --help        | 도움말 정보 출력                   |
| -c        | --config-path | 사용할 프로파일 경로 지정       |
|    없음       | --include     | 특정 패턴이 포함된 파일             |
|   없음         | --exclude     | 특정 패턴이 제외된 파일             |
| -r        | --recursive   | 폴더의 모든 파일 재귀적 순회 여부 |


>?
> - `--include` 및 `--exclude`는 표준 정규식 구문을 지원하므로 파일 특정 조건 필터링에 사용할 수 있습니다.
> - zsh를 사용할 때 pattern 문자열의 양쪽 끝에 큰따옴표를 넣어야 할 수도 있습니다.
```
./coscli sync ~/test/ cos://bucket1/example/ -r --include ".*.mp4"
```

## 작업 예시

### 파일 동기화 업로드

```plaintext
./coscli sync ~/example.txt cos://bucket1/example.txt
```

### 파일 동기화 다운로드

```plaintext
./coscli sync cos://bucket1/example.txt ~/example.txt
```

### 버킷 내 파일 동기화 복사

```plaintext
./coscli sync cos://bucket1/example.txt cos://bucket1/example_copy.txt
```

### 버킷 간 파일 동기화 복사

```plaintext
./coscli sync cos://bucket1/example.txt cos://bucket2/example_copy.txt
```
