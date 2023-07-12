rm 명령어는 파일 삭제에 사용됩니다.

## 명령어 형식

```plaintext
./coscli rm cos://<bucketAlias>[/prefix/] [cos://<bucket-name>[/prefix/]...] [flag]
```

>? 
>- bucketAlias 관련 설명은 [다운로드 및 설치 설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>- 이 명령의 다른 범용 옵션(예시: 버킷 전환, 사용자 계정 전환 등)은 [범용 옵션](https://intl.cloud.tencent.com/document/product/436/46273) 문서를 참고하십시오.
>

rm 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                      |
| --------- | ------------- | ------------------------------------ |
|     없음      | --include     | 특정 패턴이 포함된 파일                |
|     없음      | --exclude     | 특정 패턴이 제외된 파일                |
| -r        | --recursive   | 폴더의 모든 파일 재귀적 순회 여부       |
| -f        | --force       | 강제 삭제(파일 삭제 전 확인 메시지 없음) |

>?
> - `--include` 및 `--exclude`는 표준 정규식 구문을 지원하므로, 파일 특정 조건 필터링에 사용할 수 있습니다.
> - zsh를 사용할 때 pattern 문자열의 양쪽 끝에 큰따옴표를 넣어야 할 수도 있습니다.
```
./coscli rm cos://bucket1/example/ -r --include ".*.mp4"
```

## 작업 예시

### 파일 삭제

```plaintext
./coscli rm cos://bucket1/fig1.png
```

### pictrue 폴더의 모든 파일 삭제

```plaintext
./coscli rm cos://bucket1/pictrue/ -r
```
