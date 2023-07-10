
du 명령은 각 스토리지 클래스의 객체 크기 및 수를 포함한 버킷 또는 디렉터리의 각 스토리지 클래스에 대한 통계를 얻는 데 사용됩니다.

## 명령어 형식

```plaintext
./coscli du cos://<bucketAlias>[/prefix/] [flag]
```

>? 
>- bucketAlias 관련 설명은 [다운로드 및 설치 설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>- 이 명령의 다른 일반 옵션(예시: 버킷 및 사용자 계정 전환)은 [Common Options](https://intl.cloud.tencent.com/document/product/436/46273)를 참고하십시오.
>

ls 명령어에는 다음과 같은 매개변수 옵션이 포함됩니다.

| 매개변수 형식 | 매개변수 용도       | 예시                 |
| -------- | -------------- | -------------------- |
| /prefix/ | 폴더 지정 | cos://bucket1/picture/ |

du 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                |
| --------- | ------------- | ------------------------ |
|    없음       | --include     | 특정 패턴이 포함된 파일       |
|      없음       | --exclude     | 특정 패턴이 제외된 파일       |

>? 
>- `--include`는 표준 정규식을 지원합니다. 정규식을 사용하여 요구 사항을 충족하는 객체를 필터링할 수 있습니다.
>- zsh를 사용할 때 pattern 문자열의 양쪽 끝에 큰따옴표를 넣어야 할 수도 있습니다.
```plaintext
./coscli du cos://bucket1/picture/ --include ".*.mp4"
```

## 작업 예시

### bucket1 버킷의 객체에 대한 통계 나열

```plaintext
./coscli du cos://bucket1
```

### bucket1 버킷의 picture 디렉터리에 있는 객체에 대한 통계 나열

```plaintext
./coscli du cos://bucket1/picture/
```

### bucket1 버킷의 picture 디렉터리에 있는 모든 MP4 객체에 대한 통계 나열

```plaintext
./coscli du cos://bucket1/picture/ --include .*.mp4
```

### bucket1 버킷의 picture 디렉터리에 있는 모든 비 .md 객체에 대한 통계 나열

```plaintext
./coscli du cos://bucket1/picture/ --exclude .*.md
```
