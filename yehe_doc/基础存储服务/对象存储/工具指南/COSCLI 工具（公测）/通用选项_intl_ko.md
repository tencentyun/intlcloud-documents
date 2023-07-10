`./coscli --help` 또는 `./coscli -h` 명령을 사용하여 COSCLI에서 지원하는 공통 옵션을 볼 수 있습니다.

## 옵션 설명
다음은 모든 명령에서 사용할 수 있는 COSCLI의 공통 옵션입니다.

>!
>- 보안을 위해 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)의 안내에 따라 임시 키를 사용하여 SDK를 호출하는 것을 권장합니다. 임시 키 신청 시 [최소 권한의 원칙 설명](https://intl.cloud.tencent.com/document/product/436/32972)에 따라 버킷과 객체 이외의 리소스가 유출되지 않도록 하십시오.
>- 영구 키를 사용해야 하는 경우 [최소 권한의 원칙 설명](https://intl.cloud.tencent.com/document/product/436/32972)에 따라 영구 키에 대한 권한 범위를 제한하는 것이 좋습니다.


|  옵션  | 설명 |
|  ----  | ----  |
|-h, --help|도움말 정보를 출력합니다. -h 또는 --help 명령을 사용하여 도구의 help 정보 및 사용법을 볼 수 있습니다. 매개변수를 추가하지 않고 각 명령 뒤에 -h를 입력하여 명령 사용 방법을 확인할 수도 있습니다. 예를 들어 버킷 생성 명령의 특정 사용법을 보려면 `coscli mb -h`를 입력합니다   |
|-c, --config-path|기본적으로 COSCLI의 경우 `~/.cos.yaml`인 구성 파일 경로입니다. 명령 뒤에 `-c`를 추가하여 사용자 정의 구성 파일을 지정합니다|
|-e, --endpoint   |  구성 파일에서 버킷의 리전을 미리 구성하는 것 외에도 COSCLI에서 `-e`를 사용하여 `cos.<region>.myqcloud.com` 형식으로 버킷 endpoint를 지정할 수도 있습니다. 여기서 `<region>`은 `ap-guangzhou` 및 `ap-beijing`과 같은 버킷 리전을 나타냅니다. COS에서 지원하는 리전 목록은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오|
|-i, --sercret-id  |  COS에 액세스하는 데 사용되는 SecretId 지정|
|-k, --sercret-key  |  COS에 액세스하는 데 사용되는 SecretKey 지정 |
|-t, --sesssion-token  |  임시 키로 COS에 액세스하는 경우 `-t`를 사용하여 해당 token 지정|
|-v, --version |   COSCLI 버전 표시 |

## 작업 예시

### 예시1: 버킷을 전환하여 객체 업로드


COSCLI를 통해 다른 리전의 버킷으로 전환해야 하는 경우 -e 옵션을 사용하여 버킷의 Endpoint를 지정할 수 있습니다.

예를 들어, 로컬 파일 test.txt를 엔드포인트가 `cos.ap-chengdu.myqcloud.com`인 청두 리전의 examplebucket-1250000000 버킷에 업로드하려면 다음 명령을 실행합니다.
```
./coscli cp test.txt cos://examplebucket-1250000000/test.txt -e cos.ap-chengdu.myqcloud.com
```

### 예시2: 파일 목록을 보기 위해 사용자 계정 전환

다른 계정의 ID를 사용해야 하는 경우 -i 및 -k 옵션을 사용하여 키의 SecretId 및 SecretKey를 각각 지정할 수 있습니다.

예를 들어 다른 계정의 ID를 사용하여 청두 리전의 examplebucket-1250000000 버킷에 있는 파일을 나열하려면 다음 명령을 실행합니다.

```
./coscli ls cos://examplebucket-1250000000 -e cos.ap-chengdu.myqcloud.com -i AKIDYv3vWrwkHXVDfqkNjoc9PP8anjOm**** -k 4rNbYF1XmmVw67rKWTBernUu66u****
```
