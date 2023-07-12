hash 명령어는 로컬 파일의 해시 값을 계산하거나 COS(Cloud Object Storage) 파일의 해시 값을 가져오는 데 사용됩니다.

## 명령어 형식


```plaintext
./coscli hash <object-name> [flag]
```

>? 
>- bucketAlias 관련 설명은 [다운로드 및 설치 설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>- 이 명령의 다른 범용 옵션(예시: 버킷 전환, 사용자 계정 전환 등)은 [범용 옵션](https://intl.cloud.tencent.com/document/product/436/46273) 문서를 참고하십시오.
>

hash 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                      |
| --------- | ------------- | -------------------------------------- |
|     없음      | --type        | 해시 유형(md5 또는 crc64, 기본값: crc64) |

## 작업 예시

### 로컬 파일의 crc64 계산

```plaintext
./coscli hash ~/test.txt
```

### COS 파일의 md5 가져오기

```plaintext
./coscli hash cos://bucket1/example.txt --type=md5
```
