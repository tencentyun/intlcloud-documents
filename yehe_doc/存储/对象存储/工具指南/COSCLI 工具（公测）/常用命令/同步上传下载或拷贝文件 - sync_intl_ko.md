## 명령어 형식

sync 명령어는 파일을 동기화 업로드, 다운로드 또는 복사에 사용되며 cp 명령어와의 차이점은 sync 명령어는 먼저 같은 이름의 파일의 crc64를 비교하고 crc64 값이 같으면 전송하지 않는다는 것입니다.

```plaintext
./coscli sync <source_path> <destination_path> [flag]
```

>? 
>- bucketAlias 관련 설명은 [다운로드 및 설치 설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>- 이 명령의 다른 범용 옵션(예시: 버킷 전환, 사용자 계정 전환 등)은 [범용 옵션](https://intl.cloud.tencent.com/document/product/436/46273) 문서를 참고하십시오.
>

sync 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                      |
| --------- | ------------- | ------------------------------ |
|    없음       | --include     | 특정 패턴이 포함된 파일             |
|   없음         | --exclude     | 특정 패턴이 제외된 파일             |
| -r        | --recursive   | 폴더의 모든 파일 재귀적 순회 여부 |
|   없음       | --storage-class | 파일 유형 지정(기본값: STANDARD) |
|   없음       | --part-size     | 파일 파트 크기(기본값: 32MB, 최대 5GB 지원)     |
|   없음       | --thread-num    | 동시 스레드 수(기본값: 5)      |
|   없음       | --rate-limiting | 단일 링크 속도 제한(0.1 - 100MB/s)       |


>?
> - sync 명령어는 대용량 파일을 업로드 및 다운로드할 때 동시 업로드/다운로드를 자동으로 활성화합니다.
> - 파일이 `--part-size`보다 큰 경우 COSCLI는 먼저 파일을 `--part-size`로 나눈 다음 `--thread-num` 스레드를 사용하여 업/다운로드 작업을 동시 실행합니다.
> - 각 스레드는 링크를 점검합니다. 각 링크에 대해 `--rate-limiting` 매개변수를 사용하여 단일 링크의 속도를 제한할 수 있습니다. 동시 업/다운로드가 활성화된 경우 총 속도는 `--thread- num * --rate-limiting`입니다.
> - 파일을 파트로 업로드/다운로드할 때 기본적으로 중간 지점 재개가 활성화됩니다.
> - `--include` 및 `--exclude`는 표준 정규식 구문을 지원하므로, 파일 특정 조건 필터링에 사용할 수 있습니다.
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
