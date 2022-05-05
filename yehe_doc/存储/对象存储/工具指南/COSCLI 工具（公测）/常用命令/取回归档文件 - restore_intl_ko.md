restore 명령어는 아카이브 파일을 검색하는 데 사용됩니다.

## 명령어 형식


```plaintext
./coscli restore cos://<bucketAlias>[/prefix/] [flag]
```

>? 
>- bucketAlias 관련 설명은 [다운로드 및 설치 설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>- 이 명령의 다른 범용 옵션(예시: 버킷 전환, 사용자 계정 전환 등)은 [범용 옵션](https://intl.cloud.tencent.com/document/product/436/46273) 문서를 참고하십시오.
>

restore 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                      |
| --------- | ------------- | --------------------------------- |
|     없음      | --include     | 특정 패턴이 포함된 파일                |
|     없음      | --exclude     | 특정 패턴이 제외된 파일                |
| -d        | --days        | 임시 파일의 만료 시간 지정(기본 값: 3일) |
| -m        | --mode        | 복구 모드 지정(기본 값: Standard）      |
| -r        | --recursive   | 재귀적으로 폴더 순회                  |

>?
> - `--include` 및 `--exclude`는 표준 정규식 구문을 지원하므로, 파일 특정 조건 필터링에 사용할 수 있습니다.
> - zsh를 사용할 때 pattern 문자열의 양쪽 끝에 큰따옴표를 넣어야 할 수도 있습니다.
```
./coscli restore cos://bucket1/example/ -r --include ".*.mp4"
```

## 작업 예시

### bucket1 버킷의 아카이브 파일 표준 모드로 검색

```plaintext
./coscli restore cos://bucket1/pictrue.jpg
```

### bucket1 버킷의 pictrue 폴더에 있는 모든 아카이브 파일 초고속 모드로 검색

```plaintext
./coscli restore cos://bucket1/pictrue/ -r --mode Expedited
```

>? 이 명령어를 실행하기 전에 폴더의 모든 파일이 동일한 유형(예: ARCHIVE 유형)인지 확인해야 합니다. 다른 유형의 파일이 있는 경우 `--include` 또는 `--exclude`를 사용하여 동일한 유형의 파일을 필터링하십시오.
>

