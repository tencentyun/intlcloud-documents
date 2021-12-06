
cp 명령어는 파일 업로드, 다운로드 또는 복사에 사용됩니다

## 명령어 형식

```plaintext
./coscli cp <source_path> <destination_path> [flags]
```

>? bucketAlias 관련 내용은 [설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>

cp 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭       | flag 용도                            |
| --------- | --------------- | ------------------------------------ |
| -h        | --help          | 도움말 정보 출력                         |
| -c        | --config-path   | 사용할 프로파일 경로 지정             |
|   없음        | --include       | 특정 패턴이 포함된 파일                   |
|   없음          | --exclude       | 특정 패턴이 제외된 파일                   |
| -r        | --recursive     | 폴더의 모든 파일 재귀적 순회 여부       |
|    없음         | --srotage-class | 파일 유형 지정(기본값 STANDARD) |


>?
> - cp 명령어는 대용량 파일을 업로드 및 다운로드할 때 동시 업로드/다운로드를 자동으로 활성화합니다.
> - 파일이 32MB보다 크면 COSCLI는 먼저 파일을 32MB로 나눈 다음 5개의 스레드를 사용하여 업로드/다운로드 작업을 동시에 실행합니다.
> - 파일을 파트로 업로드/다운로드할 때 기본적으로 중간 지점 재개가 활성화됩니다.
> - `--include` 및 `--exclude`는 표준 정규식 구문을 지원하므로 파일 특정 조건 필터링에 사용할 수 있습니다.
> - zsh를 사용할 때 pattern 문자열의 양쪽 끝에 큰따옴표를 넣어야 할 수도 있습니다.
```
./coscli cp ~/test/ cos://bucket1/example/ -r --include ".*.mp4"
```

## 작업 예시

### 업로드 작업

#### 단일 파일 업로드

```plaintext
./coscli cp ~/example.txt cos://bucket1/example.txt
```

#### 로컬 test 폴더의 모든 파일을 bucket1의 example 폴더에 업로드

```plaintext
./coscli cp ~/test/ cos://bucket1/example/ -r
```

#### 로컬 test 폴더의 모든 .mp4 형식 파일을 bucket1의 example 폴더에 업로드

```plaintext
./coscli cp ~/test/ cos://bucket1/example/ -r --include .*.mp4
```

#### 로컬 test 폴더의 파일 중 .md 형식이 아닌 모든 파일을 bucket1의 example 폴더에 업로드

```plaintext
./coscli cp ~/test/ cos://bucket1/example/ -r --exclude .*.md
```

#### 로컬 dir 폴더에 dirA, dirB, dirC, dirD 4개의 폴더가 있으며 dirD 폴더를 제외한 dir 폴더의 모든 콘텐츠를 업로드

```plaintext
./coscli cp dir/ cos://bucket1/example/ -r --exclude dirD/.*
```

#### 로컬 test 폴더의 모든 파일을 bucket1의 example 폴더에 업로드하고 아카이브 유형으로 저장

```plaintext
./coscli cp ~/test/ cos://bucket1/example/ -r --storage-class ARCHIVE
```

### 다운로드 작업

#### 단일 파일 다운로드

```plaintext
./coscli cp cos://bucket1/example.txt ~/example.txt
```

#### bucket1의 example 폴더에 있는 모든 파일을 로컬 test 폴더로 다운로드

```plaintext
./coscli cp cos://bucket1/example/ ~/test/ -r
```

#### bucket1의 example 폴더에 있는 모든 .mp4 형식 파일을 로컬 test 폴더로 다운로드

```plaintext
./coscli cp cos://bucket1/example/ ~/test/ -r --include .*.mp4
```

#### bucket1의 example 폴더에 있는 파일 중 .md 형식이 아닌 모든 파일을 로컬 test 폴더로 다운로드

```plaintext
./coscli cp cos://bucket1/example/ ~/test/ -r --exclude .*.md
```

### 복사 작업

#### 버킷의 단일 파일 복사

```plaintext
./coscli cp cos://bucket1/example.txt cos://bucket1/example_copy.txt
```

#### 버킷 간 단일 파일 복사

```plaintext
./coscli cp cos://bucket1/example.txt cos://bucket2/example_copy.txt
```

#### bucket1 버킷의 example1 폴더에 있는 모든 파일을 bucket2 버킷의 example2 폴더에 복사

```plaintext
./coscli cp cos://bucket1/example1/ cos://bucket2/example2/ -r
```

#### bucket1 버킷의 example1 폴더에 있는 모든 .mp4 형식 파일을 bucket2 버킷의 example2 폴더에 복사

```plaintext
./coscli cp cos://bucket1/example1/ cos://bucket2/example2/ -r --include .*.mp4
```

#### bucket1 버킷의 example1 폴더에 있는 파일 중 .md 형식이 아닌 모든 파일을 bucket2 버킷의 example2 폴더에 복사

```plaintext
./coscli cp cos://bucket1/example1/ cos://bucket2/example2/ -r --exclude .*.md
```
