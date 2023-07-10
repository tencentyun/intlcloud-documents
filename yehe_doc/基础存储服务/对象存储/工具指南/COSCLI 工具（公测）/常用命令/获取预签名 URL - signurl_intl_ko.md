signurl 명령어는 익명으로 객체에 액세스할 수 있는 객체의 사전 서명된 URL을 얻는 데 사용됩니다.

## 명령어 형식

```plaintext
./coscli signurl cos://<bucketAlias>/<key> [flag]
```

>? 
>- bucketAlias 관련 설명은 [다운로드 및 설치 설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>- 이 명령의 다른 범용 옵션(예시: 버킷 전환, 사용자 계정 전환 등)은 [범용 옵션](https://intl.cloud.tencent.com/document/product/436/46273) 문서를 참고하십시오.
>

signurl 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                  |
| --------- | ------------- | ---------------------------- |
| -t        | --time        | URL 만료 시간 설정(기본 값 1000초) |

## 작업 예시

### bucket1에 있는 pictrue.jpg의 사전 서명된 URL을 가져옵니다.

```plaintext
./coscli signurl cos://bucket1/pictrue.jpg
```

### 사전 서명된 pictrue.jpg URL을 bucket2에서 가져와 URL의 만료 시간을 1314초로 설정합니다.

```plaintext
./coscli signurl cos://bucket2/pictrue.jpg --time 1314
```

