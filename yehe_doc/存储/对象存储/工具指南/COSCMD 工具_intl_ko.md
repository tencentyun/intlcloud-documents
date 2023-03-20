
## 기능 설명

COSCMD 툴을 사용하여 간단한 명령 라인을 통해 객체(Object)의 일괄 업로드, 다운로드, 삭제 등의 작업을 구현합니다.


## 사용 환경

#### 시스템 환경

Windows, Linux, macOS 시스템을 지원합니다.

> ?
> - 로컬 문자 형식을 UTF-8로 유지하십시오. 그렇지 않을 경우 중국어 버전의 파일 작업 시 오류가 발생합니다.
> - 해당 기기의 시간을 국제 표준 시간과 동일하게 조정합니다. 오차가 큰 경우 정상적으로 사용할 수 없습니다.

#### 소프트웨어 종속

- Python 2.7/3.5/3.6/3.9.
- pip 최신 버전.
>?pip의 최신 Python 버전(예: 3.9.0 버전)을 직접 설치 및 통합하는 것을 권장합니다.

#### 설치 및 설정

- 환경에 따른 설치 및 설정에 대한 자세한 작업 방법은 [Python 설치 및 설정](https://intl.cloud.tencent.com/document/product/436/10866)을 참고하십시오.
- pip 환경에서의 설치 및 설정에 대한 자세한 작업 방법은 [공식 홈페이지 pip 설치 설명](https://pip.pypa.io/en/stable/installation/)을 참고하십시오.


## 다운로드 및 설치

다음 세 가지 방법으로 COSCMD를 설치할 수 있습니다.

#### 1.1 pip를 통한 설치 

`pip` 명령어를 실행하여 설치합니다.
```plaintext
pip install coscmd
```
설치 완료 후 `-v` 또는 `--version` 명령어를 통해 현재 버전 정보를 확인할 수 있습니다.
>! Windows를 통해 설치한 후에는 `C:\python_install_dir;` 및 `C:\python_install_dir\Scripts` 두 개의 경로를 환경 변수에 추가해야 합니다. 

#### 1.2 pip 업데이트

설치 완료 후 다음 명령어를 실행하여 업데이트합니다.
```plaintext
pip install coscmd -U
```

#### 2. 소스 코드 설치(권장하지 않음)

소스 코드 다운로드 주소: [다운로드](https://github.com/tencentyun/coscmd.git).

```plaintext
git clone https://github.com/tencentyun/coscmd.git
cd coscmd
python setup.py install
```

>! Python 2.6 버전의 경우 pip로 종속 라이브러리 설치 시 실패할 수 있으므로 본 방법을 통해 설치하기를 권장합니다. 

#### 3. 오프라인 설치

>! 두 기기의 Python 버전은 동일해야 하며, 동일하지 않을 경우 설치에 실패합니다.

```sh
# 공인 네트워크가 연결된 기기에서 다음 명령어 실행
mkdir coscmd-packages
pip download coscmd -d coscmd-packages
tar -czvf coscmd-packages.tar.gz coscmd-packages



# 설치 패키지를 공인 네트워크가 연결되지 않은 기기에 복사한 후 다음 명령어 실행
tar -xzvf coscmd-packages.tar.gz
pip install coscmd --no-index -f coscmd-packages
```

## 매개변수 설정

### help 옵션 조회

사용자는 `-h` 또는 `--help` 명령어를 통해 툴의 help 정보 및 사용법을 확인할 수 있습니다.
```plaintext
coscmd -h  
```
help 정보는 다음과 같습니다.
```plaintext
usage: coscmd [-h] [-d] [-s] [-b BUCKET] [-r REGION] [-c CONFIG_PATH]
              [-l LOG_PATH] [--log_size LOG_SIZE]
              [--log_backup_count LOG_BACKUP_COUNT] [-v]
              {config,upload,download,delete,abort,copy,move,list,listparts,info,restore,signurl,createbucket,deletebucket,putobjectacl,getobjectacl,putbucketacl,getbucketacl,putbucketversioning,getbucketversioning,probe}
              ...

an easy-to-use but powerful command-line tool. try 'coscmd -h' to get more
informations. try 'coscmd sub-command -h' to learn all command usage, likes
'coscmd upload -h'

positional arguments:
  {config,upload,download,delete,abort,copy,move,list,listparts,info,restore,signurl,createbucket,deletebucket,putobjectacl,getobjectacl,putbucketacl,getbucketacl,putbucketversioning,getbucketversioning,probe}
    config              Config your information at first
    upload              Upload file or directory to COS
    download            Download file from COS to local
    delete              Delete file or files on COS
    abort               Aborts upload parts on COS
    copy                Copy file from COS to COS
    move                move file from COS to COS
    list                List files on COS
    listparts           List upload parts
    info                Get the information of file on COS
    restore             Restore
    signurl             Get download url
    createbucket        Create bucket
    deletebucket        Delete bucket
    putobjectacl        Set object acl
    getobjectacl        Get object acl
    putbucketacl        Set bucket acl
    getbucketacl        Get bucket acl
    putbucketversioning
                        Set the versioning state
    getbucketversioning
                        Get the versioning state
    probe               Connection test

optional arguments:
  -h, --help            show this help message and exit
  -d, --debug           Debug mode
  -s, --silence         Silence mode
  -b BUCKET, --bucket BUCKET
                        Specify bucket
  -r REGION, --region REGION
                        Specify region
  -c CONFIG_PATH, --config_path CONFIG_PATH
                        Specify config_path
  -l LOG_PATH, --log_path LOG_PATH
                        Specify log_path
  --log_size LOG_SIZE   specify max log size in MB (default 1MB)
  --log_backup_count LOG_BACKUP_COUNT
                        specify log backup num
  -v, --version         show program's version number and exit
```
이외에도 사용자는 모든 명령어 뒤에(매개변수 입력하지 않음) `-h`를 입력하여 해당 명령어의 구체적인 사용 방법을 확인할 수 있습니다. 예시:
```plaintext
coscmd upload -h  //upload 명령어 사용 방법 조회
```

### 설정 파일 생성

COSCMD 툴은 실행 전에 먼저 구성 파일에서 실행 시 필요한 필수 정보를 읽어옵니다. COSCMD는 `~/.cos.conf`으로부터 설정 항목을 읽어오도록 기본 설정되어 있습니다.

>? 설정 전, 먼저 COS 콘솔에서 매개변수 설정용 버킷(예: configure-bucket-1250000000)을 생성하여 키 정보를 생성해야 합니다.

설정 파일의 예시는 다음과 같습니다.
```plaintext
[common]
secret_id = AKIDA6wUmImTMzvXZNbGLCgtusZ2E8mG****
secret_key = TghWBCyf5LIyTcXCoBdw1oRpytWk****
bucket = configure-bucket-1250000000
region = ap-chengdu
max_thread = 5
part_size = 1
retry = 5
timeout = 60
schema = https
verify = md5
anonymous = False
```

>?
>- 구성 파일 중 `schema` 항목에서 http, https를 선택할 수 있으며, 기본값은 https입니다.
>- 구성 파일 중 `anonymous` 항목에서 True, False를 선택할 수 있으며, 이는 익명 모드의 사용 여부를 나타냅니다. 즉, 서명이 비어 있습니다.
>- 매개변수 설정에 대한 자세한 설명은 명령어 `coscmd config -h`를 사용해 확인할 수 있습니다.
>

### config 명령어를 통한 설정 파일 생성



>!
>- 사용자는 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 통해 SDK를 호출하고 임시 인증을 통해 SDK 사용의 보안을 더욱 강화할 것을 권장합니다. 임시 키 신청 시 대상 버킷이나 객체 외부로 리소스가 유출되지 않도록 [최소 권한의 원칙 설명](https://intl.cloud.tencent.com/document/product/436/32972)을 준수하시기 바랍니다.
>- 영구 키를 사용해야 하는 경우 [최소 권한의 원칙 설명](https://intl.cloud.tencent.com/document/product/436/32972)에 따라 영구 키의 권한 범위를 제한하는 것이 좋습니다.



config 명령어로 `~/.cos.conf`에서 구성 파일을 자동 생성할 수 있습니다. 구체적인 명령어 형식은 다음과 같습니다.
```plaintext
coscmd config [OPTION]...<FILE>...
			  [-h] --help
			  [-a] <SECRET_ID>
			  [-s] <SECRET_KEY>
			  [-t] <TOKEN>
			  [-b] <BucketName-APPID>
              [-r] <REGION> | [-e] <ENDPOINT>
              [-m] <MAX_THREAD>
              [-p] <PART_SIZE>
              [--do-not-use-ssl]
              [--anonymous]   
```

>? 그 중 '[]' 필드는 옵션 항목이며, '<>' 필드는 반드시 매개변수를 입력해야 합니다.
>

매개변수 설정 설명:

| 옵션 항목             | 매개변수 설명                                                     | 유효값 | 필수 여부 |
| ---------------- | ------------------------------------------------------------ | ------ | -------- |
| -a               | 키 ID는 [API Keys 콘솔](https://console.cloud.tencent.com/cam/capi)에서 획득하십시오. | 문자열 | Yes       |
| -s               | 키(Key)는 [API Keys 콘솔](https://console.cloud.tencent.com/cam/capi)에서 획득하십시오. | 문자열 | Yes       |
| -t               | 임시 키 token. 임시 키 사용 시 설정해야 하며 x-cos-security-token 헤더를 설정해야 합니다. | 문자열 | No       |
| -b               | 지정한 버킷 이름. 버킷 이름 형식은 BucketName-APPID이며 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. 처음 설정 사용 시 COS 콘솔에서 버킷을 생성해야 하며 툴 설정에 사용합니다. | 문자열 | Yes       |
| -r               | 버킷이 위치한 리전. [리전 및 액세스 도메인](https://www.tencentcloud.com/document/product/436/6224)을 참고하십시오. | 문자열 | Yes       |
| -e               | 요청한 ENDPOINT를 설정합니다. ENDPOINT 매개변수를 설정하면 REGION 매개변수는 유효하지 않습니다. 기본 도메인을 사용한 경우 `cos.<region>.myqcloud.com`으로 설정하고, 글로벌 가속 도메인을 사용한 경우 `cos.accelerate.myqcloud.com`으로 설정합니다. | 문자열 | No       |
| -m               | 멀티 스레드 작업의 최대 스레드 수(기본값: 5, 설정 가능 범위: 1~30)입니다.             | 숫자   | No       |
| -p               | 멀티파트 작업의 단일 파트 크기(단위: MB, 기본값: 1MB, 설정 가능 범위: 1~1000)입니다.     | 숫자   | No       |
| --do-not-use-ssl | HTTP 프로토콜을 사용하고 HTTPS는 사용하지 않습니다.                              | 문자열 | No       |
| --anonymous      | 익명 작업(서명 없음)                                       | 문자열 | No       |

config 명령어 사용 예시는 다음과 같습니다.

```shell
coscmd config -a AChT4ThiXAbpBDEFGhT4ThiXAbp**** -s WE54wreefvds3462refgwewe**** -b configure-bucket-1250000000 -r ap-chengdu
```

## 범용 명령어

### Bucket 및 Region을 지정하는 명령어

사용자가 버킷 이름과 소속 리전을 지정하지 않고 명령어를 실행하는 경우 기본적으로 매개변수 설정 시 입력한 버킷에 적용됩니다. 각 버킷 별로 작업을 실행해야 할 경우 버킷 이름과 소속 리전을 지정해야 합니다.

>?
> - `-b <BucketName-APPID>` 매개변수를 통해 버킷 이름을 지정하며, 버킷의 이름 생성 형식은 BucketName-APPID입니다. 입력하는 버킷 이름은 반드시 해당 형식이어야 합니다.
> - `-r <region>`을 통해 Region을 지정합니다. 버킷의 소속 리전을 지정할 수 있습니다. 

- 명령어 형식
```plaintext
coscmd -b <BucketName-APPID> -r <region> <action> ...
```
- 작업 예시 - 이름이 examplebucket이며 소속 리전이 베이징인 버킷 생성
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing createbucket
```
- 작업 예시 - D 드라이브의 picture.jpg 파일을 이름이 examplebucket인 버킷에 업로드
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing upload D:/picture.jpg /
```

### 설정 파일 및 로그 파일 경로 지정 명령어

사용자가 설정 파일의 경로를 지정하지 않을 경우 기본 설정 파일 경로인 `~/.cos.conf`를 사용하며, 로그 파일 경로를 지정하지 않을 경우 기본 로그 파일 경로인 `~/.cos.log`를 사용합니다.

>?
> - `-c <conf_path>` 매개변수를 통해 설정 파일의 경로를 지정합니다. COSCMD는 실행 시 해당 경로에서 설정 정보를 읽어옵니다.
> - `-l <log_conf>`매개변수를 통해 로그 경로를 지정합니다. COSCMD 실행 과정에서 발생되는 로그는 해당 경로의 로그 파일에 저장됩니다.
>

- 명령어 형식
```plaintext
coscmd -c <conf_path> -l <log_conf> <action> ...
```
- 작업 예시 - 설정 파일 경로를 /data/home/cos_conf로, 로그 출력 경로를 /data/home/cos_log로 지정하고, 이름이 examplebucket이며 소속 리전이 베이징인 버킷 생성
```plaintext
coscmd -c /data/home/cos_conf -l /data/home/cos_log -b examplebucket-1250000000 -r ap-beijing createbucket
```


### Debug 모드에서 명령어 실행

각 명령어 앞에 `-d` 또는 `--debug`를 추가하면 명령어 실행 과정에서 상세한 작업 정보를 표시합니다. 예시:

- 명령어 형식
```plaintext
coscmd -d upload <localpath> <cospath>
```

- 작업 예시 - 업로드 시 세부 정보 출력
```plaintext
coscmd -d upload -rs D:/folder/ /
```

### Silence 모드에서 명령어 실행

각 명령어 앞에 `-s` 또는 `--silence`를 추가하면 명령어 실행 과정에서 어떠한 정보도 출력되지 않습니다.

>?이 명령어는 최소 1.8.6.24 버전 이상이어야 합니다.

- 명령어 형식
```plaintext
coscmd -s upload <localpath> <cospath>
```
- 작업 예시
```plaintext
coscmd -s upload D:/picture.jpg /
```

## 자주 사용하는 버킷 명령어

### 버킷 생성

>? 버킷 생성 명령어 실행 시, 매개변수 `-b <BucketName-APPID>`로 버킷 이름을 지정하고 `-r <Region>`으로 소속 리전을 지정하십시오. 직접 coscmd createbucket 실행 시 오류가 발생하며, 이는 버킷 이름과 소속 리전을 지정하지 않아 이미 존재하는 버킷(즉, 매개변수 설정 시 입력하는 버킷)을 생성하는 것으로 인식하기 때문입니다.

- 명령어 형식
```plaintext
coscmd -b <BucketName-APPID> createbucket
```
- 작업 예시 - 이름이 examplebucket이고 소속 리전이 베이징인 버킷 생성
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing createbucket
```

### 버킷 삭제

>? `coscmd deletebucket`은 매개변수 설정 시의 버킷에만 적용됩니다. `-b <BucketName-APPID>`로 Bucket을 지정하고 `-r <region>`으로 Region을 지정하여 사용하기를 권장합니다.

- 명령어 형식
```plaintext
coscmd -b <BucketName-APPID> deletebucket
```
- 작업 예시 - 비어 있는 버킷 삭제
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing deletebucket
```
- 작업 예시 - 비어 있지 않은 버킷 강제 삭제
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing deletebucket -f
```
>! `-f` 매개변수를 사용하여 해당 버킷을 강제로 삭제할 수 있습니다. 여기에는 모든 파일, 버전 제어를 활성화한 이전 폴더, 업로드로 생성된 조각이 포함됩니다. 작업에 유의하시기 바랍니다.

## 자주 쓰는 객체 명령어

### 파일 업로드

- 파일 업로드 명령어 형식
```plaintext
coscmd upload <localpath> <cospath>
```
>! "<>"의 매개변수를 업로드할 로컬 파일 경로(localpath) 및 COS 저장 경로(cospath)로 대체하십시오.
>
- 작업 예시 - D 드라이브의 picture.jpg 파일을 COS의 doc 디렉터리로 업로드
```plaintext
coscmd upload D:/picture.jpg doc/
```
- 작업 예시 - D 드라이브 doc 폴더의 picture.jpg 파일을 COS의 doc 디렉터리로 업로드
```plaintext
coscmd upload D:/doc/picture.jpg doc/
```
- 작업 예시 - 객체 유형을 지정하여 아카이브 유형의 파일을 COS의 doc 디렉터리에 업로드
```plaintext
coscmd upload D:/picture.jpg doc/ -H "{'x-cos-storage-class':'Archive'}"
```
>! -H 매개변수를 사용하여 HTTP header 설정 시, JSON 형식을 유지해야 합니다. 예시: `coscmd upload -H "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`. 헤더에 대한 자세한 내용은 [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) 문서를 참고하십시오.
>
- 작업 예시 - meta 메타데이터를 설정하여 파일을 COS의 doc 디렉터리에 업로드
```plaintext
coscmd upload D:/picture.jpg doc/ -H "{'x-cos-meta-example':'example'}"
```


### 폴더 업로드

- 폴더 업로드 명령어 형식
```plaintext
coscmd upload -r <localpath> <cospath>
```
>! Windows 사용자는 시스템 자체의 cmd 툴이나 PowerShell에 COSCMD의 upload 명령을 사용하는 것을 권장합니다. 다른 툴(git bash 등)은 명령 경로에 대한 해석 정책이 PowerShell과 달라 사용자의 파일이 잘못된 경로에 업로드될 수 있습니다.
>
- 작업 예시 - D 드라이브의 doc 폴더 및 해당 파일을 COS의 루트 경로로 업로드
```plaintext
coscmd upload -r D:/doc /
```
- 작업 예시 - D 드라이브의 doc 폴더 및 해당 파일을 COS의 doc 경로로 업로드
```plaintext
coscmd upload -r D:/doc doc
```
- 작업 예시 - 동기화 업로드하고 md5, 파일 크기 및 이름이 동일한 파일은 건너뛰기
```plaintext
coscmd upload -rs D:/doc doc
```
>! -s 매개변수를 사용하여 동기화 업로드를 진행할 수 있으며, md5가 동일한 파일(COS 상의 원본 파일은 반드시 1.8.3.2 버전 이상의 COSCMD로 업로드해야 하며, 기본적으로 x-cos-meta-md5의 header가 존재)은 건너뜁니다.
>
- 작업 예시 - 동기화 업로드하고, 파일 크기 및 이름이 동일한 파일은 건너뛰기
```plaintext
coscmd upload -rs --skipmd5 D:/doc doc
```
>! -s 매개변수를 사용하여 동기화 업로드를 진행할 수 있습니다. --skipmd5 매개변수를 수반하면 동일한 이름의 파일 크기만 대조하고, 크기가 동일한 경우 업로드를 건너뜁니다.
>
- 작업 예시 - 동기화 업로드하고 'D 드라이브 doc 폴더에서 이미 삭제한 파일' 삭제
```plaintext
coscmd upload -rs --delete D:/doc /
```
- 작업 예시 - D 드라이브 doc 폴더의 .txt 및 .doc 접미사가 있는 파일은 업로드 생략
```plaintext
coscmd upload -rs D:/doc / --ignore *.txt,*.doc
```
- 작업 예시 - D 드라이브 doc 폴더의 .txt 접미사가 있는 파일은 업로드 생략
```plaintext
coscmd upload -rs D:/doc / --ignore "*.txt"
```
>! 
> - 폴더 업로드 시 `--ignore` 매개변수를 사용하여 특정 유형의 파일을 무시하거나 `--include` 매개변수를 사용하여 특정 유형의 파일을 필터링할 수 있습니다. 여러 shell 와일드카드 규칙(쉼표 `,`로 구분)이 지원됩니다. 지정된 확장자를 무시하려면 끝에 `,`를 추가하거나 앞뒤에 `""`를 추가해야 합니다. `""`에 쉼표로 구분된 규칙이 여러 개 있으면 첫 번째 규칙이 우선합니다.
> - `--ignore`를 사용하여 특정 폴더의 모든 파일을 필터링하려면 절대 경로를 사용하고 경로 앞뒤에 `""`를 추가해야 합니다. 예시 `coscmd upload -rs D:/doc / --ignore "D:/doc/ignore_folder/*"`.
>
- 작업 예시 - D 드라이브 doc 폴더의 .txt 및 .doc 확장명을 가진 파일 업로드
```plaintext
coscmd upload -rs D:/doc / --include *.txt,*.doc
```
- 작업 예시 - D 드라이브 doc 폴더에 있는 .txt 파일 업로드
```plaintext
coscmd upload -rs D:/doc / --include "*.txt"
```

> !
> - 10MB 이상의 파일을 업로드할 경우 COSCMD는 멀티파트 업로드를 사용하며, 명령어는 간편 업로드와 동일하게 `coscmd upload <localpath> <cospath>`를 사용합니다.
> - COSCMD는 대용량 파일 업로드가 중단된 지점부터 이어 올리는 기능을 지원합니다. 대용량 파일 멀티파트 업로드에 실패한 경우, 해당 파일 업로드를 재시도하면 실패한 파트만 업로드하고 처음부터 시작하지 않습니다. 이때 재시도하는 파일의 디렉터리 및 콘텐츠, 디렉터리가 동일해야 합니다.
> - COSCMD 멀티파트 업로드 시 모든 파트에 MD5 검사를 실행합니다.
> - COSCMD 업로드는 기본적으로 `x-cos-meta-md5` 헤더가 수반되며 값은 해당 파일의 md5 값입니다. --skipmd5 매개변수를 사용하면 해당 헤더를 수반하지 않습니다.


### 파일 리스트 쿼리

쿼리 명령어는 다음과 같습니다.
- 명령어 형식
```plaintext
coscmd list <cospath>
```
- 작업 예시 - 해당 버킷에서 접두사가 doc/인 모든 파일 리스트 재귀 쿼리
```plaintext
coscmd list doc/
```
- 작업 예시 - 해당 버킷의 모든 파일 리스트 및 파일 수, 파일 크기를 재귀 쿼리
```plaintext
coscmd list -ar
```
- 작업 예시 - 접두사가 examplefolder인 모든 파일 리스트 재귀 쿼리
```plaintext
coscmd list examplefolder/ -ar
```
- 작업 예시 - 해당 버킷의 모든 파일의 이전 버전 쿼리
```plaintext
coscmd list -v
```

>?
> - "<>" 매개변수를 파일 리스트를 쿼리할 COS 파일 경로(cospath)로 대체하십시오. `<cospath>`를 입력하지 않을 경우 현재 버킷의 루트 디렉터리를 쿼리합니다.
> - `-a`를 사용하여 모든 파일을 쿼리합니다.
> - `-r`을 사용하여 재귀 쿼리를 실행하고 마지막에 파일의 수량 및 크기의 합을 반환합니다.
> - `-n num`을 사용하여 쿼리 수의 최대값을 설정합니다.

### 파일 정보 조회

명령어는 다음과 같습니다.

- 명령어 형식
```plaintext
coscmd info <cospath> 
```
- 작업 예시 - doc/picture.jpg의 메타 정보 조회
```plaintext
coscmd info doc/picture.jpg
```

>? "<>"의 매개변수를 표시할 COS 파일 경로(cospath)로 대체하십시오.


### 파일 또는 폴더 다운로드


#### 파일 다운로드 명령어 형식
```plaintext
coscmd download <cospath> <localpath>
```
>! "<>"의 매개변수를 다운로드할 COS 파일 경로(cospath)와 로컬 저장 경로(localpath)로 대체하십시오.
>
- 작업 예시 - COS의 doc/picture.jpg를 D:/picture.jpg로 다운로드
```plaintext
coscmd download doc/picture.jpg D:/picture.jpg
```
- 작업 예시 - COS의 doc/picture.jpg를 D 드라이브로 다운로드
```plaintext
coscmd download doc/picture.jpg D:/
```
- 작업 예시 - 버전 ID가 있는 picture.jpg 파일을 D 드라이브에 다운로드
```plaintext
coscmd download picture.jpg --versionId MTg0NDUxMzc2OTM4NTExNTg7Tjg D:/
```

#### 폴더 다운로드 명령어 형식
```plaintext
coscmd download -r <cospath> <localpath>
```
- 작업 예시 - doc 디렉터리를 D:/folder/doc로 다운로드
```plaintext
coscmd download -r doc D:/folder/
```
- 작업 예시 - 루트 디렉터리의 doc 디렉터리를 제외한 파일 다운로드
```plaintext
coscmd download -r / D:/ --ignore "doc/*"
```
- 작업 예시 - 현재 버킷의 루트 디렉터리에 있는 모든 파일을 다운로드하고 덮어쓰기
```plaintext
coscmd download -rf / D:/examplefolder/
```
>! 로컬에 동일한 이름의 파일이 존재하는 경우 다운로드에 실패합니다. `-f` 매개변수를 사용하여 로컬 파일을 덮어쓰십시오.
>
- 작업 예시 -현재 bucket의 루트 디렉터리에 있는 모든 파일 동기화 다운로드, md5 검사가 동일한 동명의 파일은 제외
```plaintext
coscmd download -rs / D:/examplefolder
```
>! `-s` 또는 `--sync` 매개변수를 사용하여 폴더 다운로드 시 로컬에 존재하는 동일한 파일(다운로드하는 파일이 COSCMD의 upload 인터페이스를 통해 업로드되었고, 파일이 `x-cos-meta-md5` 헤더를 가지고 있어야 함)을 건너뜁니다.
>
- 작업 예시 - 현재 bucket의 루트 디렉터리에 있는 모든 파일 동기화 다운로드, 파일 크기가 동일한 동명의 파일은 제외
```plaintext
coscmd download -rs --skipmd5 / D:/examplefolder
```
- 작업 예시 - 현재 bucket의 루트 디렉터리에 있는 모든 파일 동기화 다운로드, 동시에 '클라우드에서는 삭제했지만 로컬에서 삭제하지 않은 파일' 삭제
```plaintext
coscmd download -rs --delete / D:/examplefolder
```
- 작업 예시 - .txt 및 .doc 확장명 파일 생략
```plaintext
coscmd download -rs / D:/examplefolder --ignore *.txt,*.doc
```
- 작업 예시 - .txt 파일 무시
```plaintext
coscmd download -rs / D:/examplefolder --ignore "*.txt"
```
>! 
> - 폴더 업로드 시 `--ignore` 매개변수를 사용하여 특정 유형의 파일을 무시하거나 `--include` 매개변수를 사용하여 특정 유형의 파일을 필터링할 수 있습니다. 여러 shell 와일드카드 규칙(쉼표 `,`로 구분)이 지원됩니다. 지정된 확장자를 무시하려면 끝에 `,`를 추가하거나 앞뒤에 `""`를 추가해야 합니다. `""`에 쉼표로 구분된 규칙이 여러 개 있으면 첫 번째 규칙이 우선합니다.
> - `--ignore`를 사용하여 특정 디렉터리의 모든 파일을 필터링하려면 절대 경로를 사용하고 경로 앞뒤에 `""`를 추가해야 합니다. 예시 `coscmd upload -rs D:/doc / --ignore "D:/doc/ignore_folder/*"`.
>
- 작업 예시 - .txt 및 .doc 확장명 파일 필터링
```plaintext
coscmd download -rs / D:/examplefolder --include *.txt,*.doc
```
- 작업 예시 - .txt 파일 필터링
```plaintext
coscmd download -rs / D:/examplefolder --include "*.txt"
```
>! 이전 버전의 mget 인터페이스는 폐기되었으며, download 인터페이스가 멀티파트 다운로드를 이용합니다. download 인터페이스를 사용하십시오.


### 서명이 있는 다운로드 URL 획득

- 명령어 형식
```plaintext
coscmd signurl <cospath>
```
- 작업 예시 - doc/picture.jpg 경로에 서명이 있는 URL 생성
```plaintext
coscmd signurl doc/picture.jpg
```
- 작업 예시 - doc/picture.jpg 경로에 100s의 서명이 있는 URL 생성
```plaintext
coscmd signurl doc/picture.jpg -t 100
```

>?
> - '<>'의 매개변수를 다운로드 URL을 획득해야 할 COS 파일 경로(cospath)로 대체하십시오.
> - `-t time`을 사용하여 해당 URL 서명의 유효 시간(단위: 초)을 설정하며 기본값은 10000s입니다.


### 파일 또는 폴더 삭제

#### 파일 삭제 명령어 형식
```plaintext
coscmd delete <cospath>
```
>! "<>"의 매개변수를 삭제할 COS 파일 경로(cospath)로 대체하십시오. 툴에서 사용자에게 삭제 진행 여부를 안내해 작업을 수행합니다.

- 작업 예시 - doc/exampleobject.txt 삭제
```plaintext
coscmd delete doc/exampleobject.txt
```
- 작업 예시 - 버전 ID가 있는 파일 삭제
```plaintext
coscmd delete doc/exampleobject.txt --versionId MTg0NDUxMzc4ODA3NTgyMTErEWN
```

#### 폴더 삭제 명령어 형식
```plaintext
coscmd delete -r <cospath>
```
- 작업 예시 - doc 디렉터리 삭제
```plaintext
coscmd delete -r doc
```
- 작업 예시 - folder/doc 디렉터리 삭제
```plaintext
coscmd delete -r folder/doc
```
- 작업 예시 - doc 폴더의 모든 버전 제어 파일 삭제
```plaintext
coscmd delete -r doc/ --versions
```
>?
>- 일괄 삭제 시에는 `y`를 입력하여 확인해야 하며, `-f` 매개변수를 사용하는 경우 확인을 건너뛰고 직접 삭제합니다.
>- 주의: 폴더 삭제 명령어 실행 시, 현재 폴더 및 하위 파일을 삭제합니다. 단, 버전 제어 파일을 삭제하는 경우 버전 ID를 지정하여 삭제해야 합니다.

### 멀티파트 업로드 파일의 조각 쿼리

- 명령어 형식
```plaintext
coscmd listparts <cospath>
```
- 작업 예시 - 접두사가 doc/인 파일 조각 쿼리
```plaintext
coscmd listparts doc/
```

### 멀티파트 업로드 파일의 조각 삭제

- 명령어 형식
```plaintext
coscmd abort
```
- 작업 예시 - 모든 업로드 파일의 조각 삭제
```plaintext
coscmd abort
```

### 파일 또는 폴더 복사

#### 파일 복사 명령어 형식
```plaintext
coscmd copy <sourcepath> <cospath>
```
- 작업 예시 - 동일한 버킷 내에서 복사: examplebucket-1250000000 버킷에 있는 picture.jpg 파일을 doc 폴더로 복사
```plaintext
coscmd -b examplebucket-1250000000 -r ap-chengdu copy examplebucket-1250000000.ap-chengdu.myqcloud.com/picture.jpg doc/
```
- 작업 예시 - 다른 버킷으로 복사: examplebucket2-1250000000 버킷의 doc/picture.jpg 객체를 examplebucket1-1250000000 버킷의 doc/examplefolder/로 복사
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/doc/picture.jpg doc/examplefolder/
```
- 스토리지 유형 수정: 파일 유형을 표준IA 스토리지로 수정
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/doc/picture.jpg doc/examplefolder/ -H "{'x-cos-storage-class':'STANDARD_IA'}"
```
- 스토리지 유형 수정: 파일 유형을 CAS로 수정하고 photo.jpg로 이름 변경
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/doc/picture.jpg doc/examplefolder/photo.jpg -H "{'x-cos-storage-class':'Archive'}"
```

#### 폴더 복사 명령어 형식
```plaintext
coscmd copy -r <sourcepath> <cospath>
```
- 작업 예시 - examplebucket2-1250000000 버킷의 examplefolder 디렉터리를 examplebucket1-1250000000 버킷의 doc 디렉터리로 복사
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy -r examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/examplefolder doc/
```

> ?
> - "<>"의 매개변수를 복사할 COS 파일 경로(sourcepath)와 붙여 넣을 COS 파일 경로(cospath)로 대체하십시오.
> - sourcepath 형식: `<BucketName-APPID>.cos.<region>.myqcloud.com/<cospath>`.
> - -d 매개변수를 사용하여 `x-cos-metadata-directive` 매개변수를 설정할 수 있으며, Copy 및 Replaced로 선택할 수 있고 기본값은 Copy입니다.
> - -H 매개변수를 사용하여 HTTP header로 설정 시, JSON 형식을 유지해야 합니다. 예시: `coscmd copy -H -d Replaced "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`. 헤더에 대한 자세한 내용은 [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) 문서를 참고하십시오.

### 파일 또는 폴더 이동
>! 이동 명령의 `<sourcepath>`와 `<cospath>`는 같을 수 없습니다. 그렇지 않으면 파일이 삭제됩니다. 그 이유는 move 명령이 먼저 복사되고 나중에 삭제되기 때문입니다. `<sourcepath>` 경로에 있는 파일은 결국 삭제됩니다.
#### 파일 이동 명령어 형식
```plaintext
coscmd move <sourcepath> <cospath> 
```
- 작업 예시 - 동일한 버킷 내에서 이동: examplebucket-1250000000 버킷에 있는 picture.jpg 파일을 doc 폴더로 이동 
```plaintext
coscmd -b examplebucket-1250000000 -r ap-chengdu move examplebucket-1250000000.ap-chengdu.myqcloud.com/picture.jpg doc/
```
- 작업 예시 - 다른 버킷으로 이동: examplebucket2-1250000000 버킷의 picture.jpg 객체를 examplebucket1-1250000000 버킷의 doc/folder/로 이동
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/picture.jpg doc/folder/
```
- 작업 예시 - 스토리지 유형 수정: 파일 유형을 표준IA 스토리지로 수정
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/picture.jpg doc/folder/ -H "{'x-cos-storage-class':'STANDARD_IA'}"
```
- 작업 예시 - 스토리지 유형 수정: 파일 유형을 CAS로 수정
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/data/exampleobject data/examplefolder/exampleobject -H "{'x-cos-storage-class':'Archive'}"
```

#### 폴더 이동 명령어 형식
```plaintext
coscmd move -r <sourcepath> <cospath>
```
- 작업 예시 - examplebucket2-1250000000 버킷의 examplefolder 디렉터리를 examplebucket1-1250000000 버킷의 doc 디렉터리로 이동
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move -r examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/examplefolder doc/
```

> ?
> - "<>"의 매개변수를 이동할 COS 파일 경로(sourcepath)와 이동될 COS 파일 경로(cospath)로 대체하십시오.
> - sourcepath 형식: `<BucketName-APPID>.cos.<region>.myqcloud.com/<cospath>`.
> - -d 매개변수를 사용하여 `x-cos-metadata-directive` 매개변수를 설정할 수 있으며, Copy 및 Replaced로 선택할 수 있고 기본값은 Copy입니다.
> - -H 매개변수를 사용하여 HTTP header로 설정 시, JSON 형식을 유지해야 합니다. 예시: `coscmd move -H -d Replaced "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`. 헤더에 대한 자세한 내용은 [PUT Object - copy](https://intl.cloud.tencent.com/document/product/436/10881) 문서를 참고하십시오.

### 객체 액세스 권한 설정

- 명령어 형식
```plaintext
coscmd putobjectacl --grant-<permissions> <UIN> <cospath>
```
- 작업 예시 - 계정100000000001에 picture.jpg의 읽기 권한 부여
```plaintext
coscmd putobjectacl --grant-read 100000000001 picture.jpg
```
- 작업 예시 - 파일 액세스 권한 쿼리
```plaintext
coscmd getobjectacl picture.jpg
```

### 버전 제어 활성화/일시 중지

- 명령어 형식
```plaintext
coscmd putbucketversioning <status>
```
- 작업 예시 - 버전 제어 활성화
```plaintext
coscmd putbucketversioning Enabled
```
- 작업 예시 - 버전 제어 일시 중지
```plaintext
coscmd putbucketversioning Suspended
```
- 작업 예시 - 버전 제어 쿼리
```plaintext
coscmd getbucketversioning
```

> !
>- '<>'의 매개변수를 버전 제어가 필요한 상태(status)로 대체하십시오.
>- 버킷에 버전 제어를 활성화하면 버전 제어 미활성화 상태(초기 상태)로 돌아갈 수 없습니다. 단, 해당 버킷의 버전 제어를 일시 중지할 수 있으며, 이 이후 업로드하는 객체는 여러 버전이 생성되지 않습니다.

### 보관된 파일 복구

- 보관된 파일 복구 명령어 형식
```plaintext
coscmd restore <cospath>
```
- 작업 예시 - 고속 검색 모드를 사용하여 picture.jpg 복구(3일간 유효)
```plaintext
coscmd restore -d 3 -t Expedited picture.jpg
```
- 보관된 파일 일괄 복구 명령어 형식
```plaintext
coscmd restore -r <cospath>
```
- 작업 예시 - 고속 검색 모드를 사용하여 examplefolder/ 폴더 복구(3일간 유효)
```plaintext
coscmd restore -r -d 3 -t Expedited examplefolder/
```

>?
> - '<>'의 매개변수를 파일 리스트를 쿼리할 COS 파일 경로(cospath)로 대체하십시오.
> - `-d <day>`를 사용하여 임시 사본의 만료 시간을 설정하며, 기본값은 7입니다.
> - `-t <tier>`를 사용하여 복구 모드를 지정합니다. 열거 값: Expedited(고속 검색 모드), Standard(표준 검색 모드), Bulk(일괄 검색 모드), 기본값: Standard.

## FAQ

COSCMD 툴 사용 중 문의 사항이 있는 경우 [COSCMD 툴 관련 FAQ](https://intl.cloud.tencent.com/document/product/436/30586)를 참고하십시오.



