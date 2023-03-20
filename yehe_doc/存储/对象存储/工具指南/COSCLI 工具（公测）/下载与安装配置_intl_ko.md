COSCLI 툴은 간단한 설치 및 구성 후 사용할 수 있는 Windows, Mac 및 Linux 운영 체제 바이너리 패키지를 제공합니다.

## 다운로드 주소

| Github 주소                                                   | Tencent Cloud 주소                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Windows](https://github.com/tencentyun/coscli/releases/download/v0.12.0-beta/coscli-windows.exe) | [Windows](https://cosbrowser.cloud.tencent.com/software/coscli/coscli-windows.exe) |
| [Mac](https://github.com/tencentyun/coscli/releases/download/v0.12.0-beta/coscli-mac) | [Mac](https://cosbrowser.cloud.tencent.com/software/coscli/coscli-mac) |
| [Linux](https://github.com/tencentyun/coscli/releases/download/v0.12.0-beta/coscli-linux) | [Linux](https://cosbrowser.cloud.tencent.com/software/coscli/coscli-linux) |

>?현재 버전 넘버는 v0.12.0-beta입니다. 툴의 최신 버전, 이전 버전 및 업데이트 로그는 [release](https://github.com/tencentyun/coscli/releases)로 이동하여 확인하십시오.

## 설치

### Windows

1. [Windows 버전 COSCLI 다운로드](https://github.com/tencentyun/coscli/releases/download/v0.12.0-beta/coscli-windows.exe).
2. 다운로드한 COSCLI 실행 파일을 `C:\Users\<사용자 이름>` 디렉터리로 이동합니다.
3. `coscli-windows.exe`의 이름을 `coscli.exe`로 변경합니다.
4. `win+r` 키를 눌러 `실행` 프로그램을 엽니다.
5. 대화 상자에서 `cmd`를 입력하고 `Enter`를 눌러 명령 라인 창을 엽니다.
6. 명령 라인 창에서 `coscli --version`을 입력하고 다음 정보가 출력되면 설치가 완료된 것입니다.
>? `Windows` 시스템에서는 명령 라인 클라이언트에 따라 COSCLI를 사용하는 방식이 약간 다를 수 있습니다. `coscli [command]` 입력 후 COSCLI가 정상적으로 작동하지 않을 경우 `./coscli [command]` 형식으로 시도하시기 바랍니다.
>
```
coscli version v0.12.0-beta
```

### Mac

1. 다음 명령어를 실행하여 COSCLI를 다운로드합니다.
```bash
wget https://github.com/tencentyun/coscli/releases/download/v0.12.0-beta/coscli-mac
```
2. 다음 명령어를 실행하여 파일 이름을 변경합니다.
```bash
mv coscli-mac coscli
```
3. 다음 명령어를 실행하여 파일 실행 권한을 수정합니다.
```bash
chmod 755 coscli
```
4. 명령 라인에 `./coscli --version`을 입력하고 다음 정보가 출력되면 설치가 완료된 것입니다.
```
coscli version v0.12.0-beta
```
>? Mac 시스템에서 COSCLI 사용 시 `개발자를 확인할 수 없기 때문에 ‘coscli’를 열 수 없습니다` 프롬프트가 표시되면 `설정 > 보안성 및 개인 정보 보호 > 일반`으로 이동하여 `계속 coscli 열기`를 선택해야 COSCLI를 정상적으로 사용할 수 있습니다.


### Linux

1. [Linux 버전 COSCLI 다운로드](https://github.com/tencentyun/coscli/releases/download/v0.12.0-beta/coscli-linux)를 클릭하거나 다음 명령어를 실행하여 COSCLI를 다운로드합니다.
```bash
wget https://github.com/tencentyun/coscli/releases/download/v0.12.0-beta/coscli-linux
```
2. 다음 명령어를 실행하여 파일 이름을 변경합니다.
```bash
mv coscli-linux coscli
```
3. 다음 명령어를 실행하여 파일 실행 권한을 수정합니다.
```bash
chmod 755 coscli
```
4. 명령 라인 창에 `./coscli --version`을 입력하고 다음 정보가 출력되면 설치가 완료된 것입니다.
```
coscli version v0.12.0-beta
```


## 매개변수 구성

>!
>- 사용자는 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 통해 SDK를 호출하고 임시 인증을 통해 SDK 사용의 보안을 더욱 강화할 것을 권장합니다. 임시 키 신청 시 대상 버킷이나 객체 외부로 리소스가 유출되지 않도록 [최소 권한의 원칙 설명](https://intl.cloud.tencent.com/document/product/436/32972)을 준수하시기 바랍니다.
>- 영구 키를 사용해야 하는 경우 [최소 권한의 원칙 설명](https://intl.cloud.tencent.com/document/product/436/32972)에 따라 영구 키의 권한 범위를 제한하는 것이 좋습니다.



`./coscli --help` 명령을 실행하면 COSCLI 사용 방법을 빠르게 확인할 수 있습니다.

COSCLI는 처음 사용할 때 기본적으로 `~/.cos.yaml`에 구성 파일을 생성합니다. 나중에 `./coscli config init` 명령을 실행하여 다른 위치에 COSCLI에 대한 구성 파일을 인터랙티브식으로 생성할 수도 있습니다.

구성 파일의 구성 항목은 다음과 같습니다.

<span id="alias"></span>

| 구성 항목        | 설명                                                         |
| ------------- | ------------------------------------------------------------ |
| Secret ID     | 키 ID. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에서 생성 및 획득할 수 있습니다. |
| Secret Key    | 키 Key. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에서 생성 및 획득할 수 있습니다. |
| Session Token | 임시 키를 사용하는 경우 지정해야 하는 임시 키 token입니다. 그렇지 않으면 `Enter`를 눌러 스킵합니다. |
| APP ID        | APP ID는 Tencent Cloud 계정 신청 후 부여되는 계정으로 시스템에서 자동으로 할당되며, [계정 정보](https://console.cloud.tencent.com/developer)에서 가져올 수 있습니다. 버킷의 전체 이름은 `<BucketName-APPID>` 형식으로 `Bucket Name` 및 `APP ID`의 두 가지 요소로 구성됩니다. 버킷 이름 생성 규칙에 대한 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. |
| Bucket Name   | `<BucketName-APPID>` 형식의 APP ID와 함께 버킷의 전체 이름을 구성하는 버킷 이름입니다. 버킷 명명 규칙에 대한 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. |
| Bucket Endpoint | `cos.<region>.myqcloud.com` 형식의 버킷 엔드포인트입니다. 여기서 region은 버킷 리전입니다. 자세한 내용은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. |
| Bucket Alias  | 필수 명령을 단축하기 위해 구성 후 'BucketName-APPID'를 대체하는 데 사용할 수 있는 버킷 별칭입니다. 구성되지 않은 경우 `BucketAlias`의 해당 값은 `BucketName-APPID` 값이 됩니다. |

### 기타 구성 방법

`./coscli config init`을 실행하여 구성 파일을 인터랙티브식으로 생성하는 것 외에도 아래와 같이 COSCLI용 `yaml` 구성 파일을 수동으로 작성할 수도 있습니다.

```yaml
cos:
  base:
    secretid: XXXXXXXXXXXXXXX
    secretkey: XXXXXXXXXXXXXXXXX
    sessiontoken: ""
  buckets:
  - name: examplebucket1-1250000000
    alias: bucket1
    region: ap-shanghai
  - name: examplebucket2-1250000000
    alias: bucket2
    region: ap-guangzhou
  - name: examplebucket3-1250000000
    alias: bucket3
    region: ap-chengdu
```

>! COSCLI는 기본적으로 ~/.cos.yaml에서 구성 항목을 읽습니다. 사용자 정의 구성 파일을 사용하려면 명령 뒤에 -c (--config-path) 옵션을 추가합니다. 구성 파일에 저장된 secretid/secretkey/sessiontoken은 모두 암호화된 문자열입니다.



### 다수의 버킷 구성

COSCLI는 여러 개의 버킷을 지원하지만 구성 중에는 하나의 버킷에 대한 정보만 구성하도록 요청합니다. 나중에 `./coscli config add` 명령을 실행하여 더 많은 버킷의 정보를 추가할 수 있습니다.

>? 구성 파일 작업에 대한 자세한 내용은 [구성 파일 생성 및 수정 - config](https://intl.cloud.tencent.com/document/product/436/43251)를 참고하십시오.
