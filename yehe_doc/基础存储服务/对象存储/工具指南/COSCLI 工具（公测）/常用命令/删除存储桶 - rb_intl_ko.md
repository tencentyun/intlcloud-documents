rb 명령어는 버킷 삭제에 사용됩니다.

## 명령어 형식

```plaintext
./coscli rb cos://<BucketName-APPID> -r <Region> [flag]
```

rb 명령어에는 다음과 같은 선택적 flag가 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                |
| --------- | ------------- | ------------------------ |
| 없음 |  BucketName-APPID |   examplebucket-1250000000과 같이 삭제할 버킷의 이름 지정  |
| -r        | --region      | 버킷 리전               |

>? 이 명령의 다른 일반 옵션(예시: 버킷 및 사용자 계정 전환)은 [Common Options](https://intl.cloud.tencent.com/document/product/436/46273)를 참고하십시오.
>
## 작업 예시

```plaintext
// bucket3 버킷 삭제
./coscli rb cos://bucket3-1250000000 -r ap-chengdu
// 프로파일 업데이트
./coscli config delete -a bucket3
```
