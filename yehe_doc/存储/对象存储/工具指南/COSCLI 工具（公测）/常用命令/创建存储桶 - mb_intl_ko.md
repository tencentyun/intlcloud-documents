mb 명령어는 버킷 생성에 사용됩니다.

## 명령어 형식

```plaintext
./coscli mb cos://<BucketName-APPID> -r <Region> [flag]
```

mb 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                |
| --------- | ------------- | ------------------------ |
| -h        | --help        | 도움말 정보 출력             |
| -c        | --config-path | 사용할 프로파일 경로 지정 |
| -r        | --region      | 버킷 리전               |

>! mb 명령어로 생성한 버킷을 COSCLI에서 작업하려면 mb 명령어 성공 후 프로파일에서 config add 명령어를 사용하여 버킷 설정을 업데이트 해야합니다.
>

## 작업 예시

```plaintext
// bucket3 버킷 생성
./coscli mb cos://bucket3-1250000000 -r ap-chengdu
// 프로파일 업데이트
./coscli config add -b bucket3-1250000000 -r ap-chengdu -a bucket3
// 업데이트 후 cos://bucket3을 통해 이 버킷에 액세스할 수 있습니다.
```
