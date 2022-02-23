COSCLI 툴은 간단한 설치 및 설정 후에 사용할 수 있는 Windows, Mac 및 Linux 운영 체제 바이너리 패키지를 제공합니다.

## 다운로드 주소

- [Windows](https://github.com/tencentyun/coscli/releases/download/v0.10.2-beta/coscli-windows.exe)
- [Mac](https://github.com/tencentyun/coscli/releases/download/v0.10.2-beta/coscli-mac)
- [Linux](https://github.com/tencentyun/coscli/releases/download/v0.10.2-beta/coscli-linux)

## 설치

### Windows

1. [Windows 버전 COSCLI 다운로드](https://github.com/tencentyun/coscli/releases/download/v0.10.2-beta/coscli-windows.exe).
2. 다운로드한 COSCLI 실행 파일을 `C:\Users\<사용자 이름>` 디렉터리로 이동합니다.
3. `coscli-windows.exe`의 이름을 `coscli.exe`로 변경합니다.
4. `win+r` 키를 눌러 `실행` 프로그램을 엽니다.
5. 대화 상자에서 `cmd`를 입력하고 `Enter`를 눌러 명령 라인 창을 엽니다.
6. 명령 라인 창에서 `coscli --version`을 입력하고 다음 정보가 출력되면 설치가 완료된 것입니다.
>? `Windows` 시스템에서는 명령 라인 클라이언트에 따라 COSCLI를 사용하는 방식이 약간 다를 수 있습니다. `coscli [command]` 입력 후 COSCLI가 정상적으로 작동하지 않을 경우 `./coscli [command]` 형식으로 시도하시기 바랍니다.
>
```
coscli version v0.10.2-beta
```

### Mac

1. 다음 명령어를 실행하여 COSCLI를 다운로드합니다.
```bash
wget https://github.com/tencentyun/coscli/releases/download/v0.10.2-beta/coscli-mac
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
coscli version v0.10.2-beta
```
>? Mac 시스템에서 COSCLI 사용 시 `개발자를 인증할 수 없기 때문에 ‘coscli’를 열 수 없습니다`라는 팝업창이 뜨면 `설정 > 보안성 및 개인정보 보호 > 일반`으로 이동하여 `계속 coscli 열기`를 선택하여 COSCLI를 정상적으로 사용할 수 있습니다.
>


### Linux

1. [Linux 버전 COSCLI 다운로드](https://github.com/tencentyun/coscli/releases/download/v0.10.2-beta/coscli-linux)를 클릭하거나 다음 명령어를 실행하여 COSCLI를 다운로드합니다.
```bash
wget https://github.com/tencentyun/coscli/releases/download/v0.10.2-beta/coscli-linux
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
coscli version v0.10.2-beta
```


## 매개변수 설정

COSCLI 사용 방법을 빠르게 보려면 `./coscli --help` 명령어를 사용할 수 있습니다.

최초 사용 시 COSCLI는 기본적으로 `~/.cos.yaml` 위치에 설정 파일을 생성합니다. 또한 `./coscli config init` 명령어를 사용하여  다른 위치에 COSCLI에 대한 구성 파일을 인터랙티브식으로 생성할 수 있습니다.

설정 파일의 각 설정 항목에 대한 설명은 다음과 같습니다.

<span id="alias"></span>

| 설정 항목        | 설명                                                         |
| ------------- | ------------------------------------------------------------ |
| Secret ID     | 키 ID. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에서 생성 및 획득할 수 있습니다. |
| Secret Key    | 키 Key. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에서 생성 및 획득할 수 있습니다. |
| Session Token | 임시 키 Token. 임시 키를 사용할 때 설정해야 하며, 사용하지 않을 경우 `Enter`를 눌러 건너뛸 수 있습니다. |
| APP ID        | APP ID는 Tencent Cloud 계정 신청 후 부여되는 계정으로 시스템에서 자동으로 할당되며, [계정 정보](https://console.cloud.tencent.com/developer)에서 가져올 수 있습니다. 버킷의 전체 이름은 `<BucketName-APPID>` 형식으로 `Bucket Name`과 `APP ID`의 두 가지 요소로 구성됩니다. 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. |
| Bucket Name   | 버킷의 이름. `<BucketName-APPID>`형식으로 버킷 이름과 APP ID로 구성됩니다. 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. |
| Bucket Region | 버킷이 위치한 리전. 자세한 내용은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. |
| Bucket Alias  | 버킷 별칭. 설정 시 `BucketName-APPID` 대신 `BucketAlias`를 사용하여 입력해야 하는 명령어의 길이를 줄일 수 있습니다. 이 항목이 설정되어 있지 않으면 `BucketAlias`의 값은 `BucketName-APPID` 값입니다. |

### 기타 설정 방법

`./coscli config init`을 사용하여 설정 파일을 인터랙티브식으로 생성하는 것 외에도, 수동으로 COSCLI 설정 파일을 작성할 수 있습니다. COSCLI의 설정 파일 형식은 `yaml` 형식입니다. 설정 파일의 예시는 다음과 같습니다.

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

>!COSCLI는 기본적으로 ~/.cos.yaml의 설정 항목을 읽어옵니다. 사용자 정의 설정 파일을 사용하려면 명령어 뒤에 -c (--config-path) 옵션을 사용합니다.



### 다수의 버킷 설정

COSCLI는 여러 개의 버킷을 지원하지만 초기 설정 시 COSCLI는 하나의 버킷에 대한 정보만 설정하도록 요구합니다. `./coscli config add` 명령어를 사용하여 추후에 버킷 설정을 추가할 수 있습니다.

>? 설정 파일 작업 관련 자세한 내용은 [config 명령어](https://intl.cloud.tencent.com/document/product/436/43251)를 참고하십시오.
