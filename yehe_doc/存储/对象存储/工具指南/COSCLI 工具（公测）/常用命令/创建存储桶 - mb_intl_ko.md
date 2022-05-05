mb 명령어는 버킷 생성에 사용됩니다.

## 명령어 형식

```plaintext
./coscli mb cos://<BucketName-APPID> -r <Region> [flag]
```

mb 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                |
| --------- | ------------- | ------------------------ |
| 없음 |  BucketName-APPID |   examplebucket-1250000000과 같은 버킷 이름 사용자 지정  |
| -r        | --region      | 버킷 리전               |

>! 
>- COSCLI에서 mb 명령을 사용하여 버킷을 생성하려면 mb 명령을 성공적으로 실행한 후 config add 명령을 실행하여 구성 파일의 버킷 구성을 업데이트해야 합니다.
>- 이 명령의 다른 일반 옵션(예시: 버킷 및 사용자 계정 전환)은 [Common Options](https://intl.cloud.tencent.com/document/product/436/46273)를 참고하십시오.
>

## 작업 예시

```plaintext
// bucket3 버킷 생성
./coscli mb cos://bucket3-1250000000 -r ap-chengdu
// 프로파일 업데이트
./coscli config add -b bucket3-1250000000 -r ap-chengdu -a bucket3
// 업데이트 후 cos://bucket3을 통해 이 버킷에 액세스할 수 있습니다.
```
