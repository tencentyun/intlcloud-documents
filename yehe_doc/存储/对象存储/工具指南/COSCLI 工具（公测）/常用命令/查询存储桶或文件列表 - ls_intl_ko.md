ls 명령어는 모든 버킷 리스트, 버킷의 파일 리스트 및 폴더의 파일 리스트 쿼리에 사용됩니다.

## 명령어 형식

```plaintext
./coscli ls [cos://bucketAlias[/prefix/]] [flag]
```

>? bucketAlias 관련 내용은 [설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>

ls 명령어에는 다음과 같은 매개변수 옵션이 포함됩니다.

| 매개변수 형식          | 매개변수 용도       | 예시                 |
| ----------------- | -------------- | -------------------- |
| cos://bucketAlias | 버킷 지정     | cos://bucket1          |
| /prefix/          | 폴더 지정 | /picture/ |

ls 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭   | flag 용도                            |
| --------- | ----------- | ------------------------------------ |
| -h        | --help      | 도움말 정보 출력                         |
|     없음      | --include   | 특정 패턴이 포함된 파일                   |
|     없음       | --exclude   | 특정 패턴이 제외된 파일                   |
| -r        | --recursive | 폴더를 재귀적으로 순회하고 모든 파일을 나열할지 여부 |

>? 
> - `--include` 및 `--exclude`는 표준 정규식 구문을 지원하므로 파일 특정 조건 필터링에 사용할 수 있습니다.
> - zsh 사용 시 pattern 문자열의 양쪽 끝에 큰따옴표를 넣어야 할 수도 있습니다.
```plaintext
./coscli ls cos://bucket1 -r --include ".*.mp4"
```

## 작업 예시


### 현재 계정의 모든 버킷 나열

```plaintext
./coscli ls
```

### 파일 나열

#### bucket1의 모든 파일 나열

```plaintext
./coscli ls cos://bucket1
```

#### bucket1의 picture 폴더에 있는 모든 파일 및 폴더 나열

```plaintext
./coscli ls cos://bucket1/picture/
```

#### bucket1의 picture 폴더에 있는 모든 파일을 재귀적으로 나열

```plaintext
./coscli ls cos://bucket1/picture/ -r
```

#### bucket1의 모든 .mp4 유형 파일을 재귀적으로 나열

```plaintext
./coscli ls cos://bucket1 -r --include .*.mp4
```



#### bucket1의 파일 중 .mp4 형식이 아닌 모든 파일을 재귀적으로 나열

```plaintext
./coscli ls cos://bucket1 -r --exclude .*.mp4
```

#### bucket1의 picture 폴더 내 test로 시작하고 .jpg 형식이 아닌 모든 파일을 재귀적으로 나열

```plaintext
./coscli ls cos://bucket1/picture -r --include ^picture/test.* --exclude .*.jpg
```
