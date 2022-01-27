signurl 명령어는 익명으로 객체에 액세스할 수 있는 객체의 사전 서명된 URL을 얻는 데 사용됩니다.

## 명령어 형식

```plaintext
./coscli signurl cos://<bucketAlias>/<key> [flag]
```

>? bucketAlias 관련 내용은 [설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>

signurl 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                  |
| --------- | ------------- | ---------------------------- |
| -h        | --help        | 도움말 정보 출력             |
| -c        | --config-path | 사용할 프로파일 경로 지정       |
| -t        | --time        | URL 만료 시간 설정(기본 값 1000초) |

## 작업 예시

### bucket1에 있는 picture.jpg의 사전 서명된 URL을 가져옵니다.

```plaintext
./coscli signurl cos://bucket1/picture.jpg
```

### 사전 서명된 picture.jpg URL을 bucket2에서 가져와 URL의 만료 시간을 1314초로 설정합니다.

```plaintext
./coscli signurl cos://bucket2/picture.jpg --time 1314
```

