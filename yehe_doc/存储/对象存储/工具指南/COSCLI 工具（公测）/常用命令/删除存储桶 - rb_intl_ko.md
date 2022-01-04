rb 명령어는 버킷 삭제에 사용됩니다.

## 명령어 형식

```plaintext
./coscli rb cos://<BucketName-APPID> -r <Region> [flag]
```

rb 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                |
| --------- | ------------- | ------------------------ |
| -h        | --help        | 도움말 정보 출력             |
| -c        | --config-path | 사용할 프로파일 경로 지정 |
| -r        | --region      | 버킷 리전               |

## 작업 예시

```plaintext
// bucket3 버킷 삭제
./coscli rb cos://bucket3-1250000000 -r ap-chengdu
// 프로파일 업데이트
./coscli config delete -a bucket3
```
