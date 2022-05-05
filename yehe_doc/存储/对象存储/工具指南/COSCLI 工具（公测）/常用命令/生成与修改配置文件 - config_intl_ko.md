
## 명령어 형식

다음 config 명령어는 프로파일 생성 및 수정에 사용됩니다.

```
./coscli config [command] [flag]
```

>? 
>- 구성 항목을 올바르게 설정한 후 `./coscli config show`를 실행하여 구성을 볼 수 있습니다.
>- 이 명령의 다른 일반 옵션(예시: 버킷 및 사용자 계정 전환)은 [Common Options](https://intl.cloud.tencent.com/document/product/436/46273)를 참고하십시오.
>

<span id="config"></span>

config 명령어에는 다음 하위 명령어가 포함됩니다.

| command 이름 | command 용도                               |
| ------------ | ------------------------------------------ |
| add          | 새 버킷 설정 추가.                   |
| delete       | 기존 버킷 설정 삭제.             |
| init         | 인터랙티브식으로 프로파일 생성.                     |
| set          | 프로파일의 base 그룹에서 하나 이상의 설정 항목 수정. |
| show         | 지정된 프로파일의 정보 출력.                 |

config 및 해당 하위 명령어에는 다음과 같은 flag 옵션이 포함됩니다.

| flag 약칭 | flag 전체 명칭     | flag 용도                  |
| --------- | ------------- | -------------------------- |
| -c        | --config-path | 사용할 프로파일 경로 지정. |

config add 하위 명령어에는 다음과 같은 flag 옵션이 포함되어 있습니다.

| flag 약칭 | flag 전체 명칭 | flag 용도    |
| --------- | --------- | ------------ |
| -a        | --alias   | 버킷 별칭. |
| -b        | --bucket  | 버킷 이름. |
| -r        | --region  | 버킷 리전. |

config delete 하위 명령어에는 다음과 같은 flag 옵션이 포함되어 있습니다.

| flag 약칭 | flag 전체 명칭 | flag 용도    |
| --------- | --------- | ------------ |
| -a        | --alias   | 버킷 별칭. |

config set 하위 명령어에는 다음과 같은 flag 옵션이 포함되어 있습니다.

| flag 약칭 | flag 전체 명칭    | flag 용도         |
| --------- | ------------ | ----------------- |
| -i        | --secret_id  | secret ID 설정.  |
| -k        | --secret_key | secret key 설정. |
| -t        | --token      | token 설정.      |

## 작업 예시

### 새 버킷 설정 추가

```
./coscli config add -b examplebucket3-1250000000 -r ap-chengdu -a bucket3
```

### 기존 버킷 설정 삭제

```
./coscli config delete -a bucket3
```

### 기본 프로파일에서 session-token 수정

```
./coscli config set -t test-token123
```

### 지정된 프로파일의 정보 출력

```
./coscli config show -c /your/config/path.yaml
```
