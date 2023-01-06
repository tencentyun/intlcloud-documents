
cp 명령어는 파일 업/다운로드 또는 복사에 사용됩니다.

## 명령어 형식

```plaintext
./coscli cp <source_path> <destination_path> [flags]
```

>? 
>- bucketAlias에 대한 자세한 내용은 [다운로드 및 설치 설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>- 이 명령의 다른 일반 옵션(예시: 버킷 및 사용자 계정 전환)은 [범용 옵션](https://intl.cloud.tencent.com/document/product/436/46273)을 참고하십시오.
>

cp 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭       | flag 용도                            |
| --------- | --------------- | ------------------------------------ |
|   없음       | --include     | 특정 패턴이 포함된 파일             |
|   없음       | --exclude     | 특정 패턴이 제외된 파일             |
| -r        | --recursive     | 폴더의 모든 파일 재귀적 순회 여부       |
|   없음       | --storage-class | 파일 유형 지정(기본값: STANDARD) |
|   없음       | --part-size     | 파일 파트 크기(기본값: 32MB), 단위 MB     |
|   없음       | --thread-num    | 동시 스레드 수(기본값: 5)      |
|   없음       | --rate-limiting | 단일 링크 속도 제한(0.1~100MB/s), 단위 MB/s       |
| 없음 | --meta | 특정 HTTP 표준 속성(HTTP Header) 및 `x-cos-meta-` 접두사가 붙은 사용자 정의 메타데이터(User Meta)를 포함한 업로드된 파일의 메타데이터입니다. 파일 메타데이터는 `header:value#header:value` 형식으로 `Expires:2022-10-12T00:00:00.000Z#Cache-Control:no-cache#Content-Encoding:gzip#x-cos-meta-x:x`와 같습니다. |


>?
> - cp 명령어는 대용량 파일을 업로드 및 다운로드할 때 동시 업로드/다운로드를 자동으로 활성화합니다.
> - 파일이 `--part-size`보다 큰 경우 COSCLI는 먼저 파일을 `--part-size`로 나눈 다음 `--thread-num` 스레드를 사용하여 업/다운로드 작업을 동시 실행합니다.
> - 각 스레드는 링크를 점검합니다. 각 링크에 대해 `--rate-limiting` 매개변수를 사용하여 단일 링크의 속도를 제한할 수 있습니다. 동시 업/다운로드가 활성화된 경우 총 속도는 `--thread- num * --rate-limiting`입니다.
> - 파일을 파트로 업로드/다운로드할 때 기본적으로 중간 지점 재개가 활성화됩니다.
> - `--include` 및 `--exclude`는 표준 정규식 구문을 지원하므로, 파일 특정 조건 필터링에 사용할 수 있습니다.
> - zsh를 사용할 때 pattern 문자열의 양쪽 끝에 큰따옴표를 넣어야 할 수도 있습니다.
```plaintext
./coscli cp ~/test/ cos://bucket1/example/ -r --include ".*.txt" --meta=x-cos-meta-a:a#ContentType:text#Expires:2022-10-12T00:00:00.000Z
```

## 작업 예시

### 업로드

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

#### 로컬 file.txt 파일을 bucket1 버킷에 업로드하고 단일 URL 속도 제한을 1.3MB/s로 설정

```plaintext
./coscli cp ~/file.txt cos://bucket1/file.txt --rate-limiting 1.3
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
