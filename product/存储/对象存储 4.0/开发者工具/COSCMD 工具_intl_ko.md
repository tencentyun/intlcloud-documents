## 기능 설명
COSCMD 도구를 사용하면 간단한 명령행으로 객체(Object)의 일괄 업로드, 다운로드, 삭제와 같은 작업을 실행할 수 있습니다.

## 사용 환경

### 운영 체제

Windows, Linux 및 macOS 시스템을 지원합니다.

>?
- 로컬 문자 형식은 UTF-8이어야 하며, 그렇지 않으면 중국어 파일을 조작하는 데 이상이 발생할 수 있습니다.
- 로컬 시간이 국제 표준 시간과 교정되어 있는지 확인하십시오. 오차가 과도하게 클 경우 정상적으로 시용할 수 없습니다.

### 소프트웨어 의존

- Python 2.7/3.5/3.6.
- 최신 버전의 pip.

#### 설치 및 구성

환경 설치 및 구성에 대해 자세한 조작은 [Python 설치 및 구성](https://cloud.tencent.com/document/product/436/10866)을 참조하십시오.

## 다운로드 및 설치
 pip을 설치하는 방식은 다음과 같습니다.

- **pip 설치**
  `pip`명령을 실행하여 설치합니다.
```sh
pip install coscmd
```

 설치가 완료되면 사용자는 `-v` 또는 `--version` 명령을 사용하여 현재 버전 정보를 조회할 수 있습니다.
- **pip 업데이트**
  `pip`명령을 실행하여 업데이트합니다.
```sh
pip install coscmd -U
```
>! pip 버전은 10.0.0 보다 크거나 같은 경우, 의존 라이브러리를 업그레이드하거나 설치하면 실패할 수 있습니다. pip 버전 9.x(pip install pip==9.0.0)을 추천합니다.

- **오리진 코드 설치(추천하지 않음)**
  다운로드 링크: [GitHub 링크](https://github.com/tencentyun/coscmd.git).
```shell
git clone https://github.com/tencentyun/coscmd.git
cd coscmd
python setup.py install
```
>!Python 버전이 2.6인 경우 pip가 의존 라이브러리를 설치할 때 쉽게 실패합니다. 이 방법을 사용하여 설치하는 것을 권장합니다.

- **오프라인 설치**
```sh
# 공중망이 있는 기기에서 다음 명령을 실행하십시오.
mkdir coscmd-packages
pip download coscmd -d coscmd-packages
tar -czvf coscmd-packages.tar.gz coscmd-packages
```
>! 두 대 기기의 python 버전이 일치해야 하며, 그렇지 않으면 설치가 실패할 수 있습니다.
>```sh
># 공용 네트워크가 없는 기기에 설치 패키지를 복사하고 다음 명령을 실행하십시오.
>tar -xzvf coscmd-packages.tar.gz
>pip install coscmd --no-index -f coscmd-packages
```

## 사용 방법

### help 보기

사용자가 `-h` 또는 `--help` 명령으로 도구의 help 정보를 볼 수 있습니다.
```shell
coscmd -h  //해당 버전 정보 보기
```

help 정보는 다음과 같습니다.
```shell
usage: cos_cmd.py [-h] [-d] [-b BUCKET] [-r REGION] [-c CONFIG_PATH]
                  [-l LOG_PATH] [-v]
                  {config,upload,download,delete,copy,list,info,mget,restore,signurl,createbucket,deletebucket,putobjectacl,getobjectacl,putbucketacl,getbucketacl}
                  ...

an easy-to-use but powerful command-line tool. try 'coscmd -h' to get more
informations. try 'coscmd sub-command -h' to learn all command usage, likes
'coscmd upload -h'

positional arguments:
  {config,upload,download,delete,copy,list,info,mget,restore,signurl,createbucket,deletebucket,putobjectacl,getobjectacl,putbucketacl,getbucketacl}
    config              config your information at first.
    upload              upload file or directory to COS.
    download            download file from COS to local.
    delete              delete file or files on COS
    copy                copy file from COS to COS.
    list                list files on COS
    info                get the information of file on COS
    mget                download file from COS to local.
    restore             restore
    signurl             get download url
    createbucket        create bucket
    deletebucket        delete bucket
    putobjectacl        set object acl
    getobjectacl        get object acl
    putbucketacl        set bucket acl
    getbucketacl        get bucket acl

optional arguments:
  -h, --help            show this help message and exit
  -d, --debug           debug mode
  -b BUCKET, --bucket BUCKET
                        set bucket
  -r REGION, --region REGION
                        set region
  -c CONFIG_PATH, --config_path CONFIG_PATH
                        set config_path
  -l LOG_PATH, --log_path LOG_PATH
                        set log_path
  -v, --version         show program's version number and exit
```

또한 사용자가 각 명령 뒤에(매개변수를 추가하지 않음) `-h`를 입력하여 해당 명령 사용 방법을 볼 수 있습니다. 예를 들면:
```shell
coscmd upload -h  //upload 명령 사용 방법 보기
```

### 매개변수 구성

COSCMD 도구를 사용하기 전에 매개변수를 구성해야 합니다. 다음 명령을 실행하여 구성합니다.
```shell
coscmd  config [-h] -a <SECRET_ID> -s <SECRET_KEY> -b <BUCKET>
                         (-r <REGION> | -e <ENDPOINT>) [-m <MAX_THREAD>]
                         [-p <PART_SIZE>] [-u <APPID>] [--do-not-use-ssl]
                         [--anonymous <ANONYMOUS>]      
```
위의 예시에서 "<>"를 사용하는 필드는 필수 매개변수이며 "[]"를 사용하는 필드는 선택 가능 매개변수입니다. 그중에:

| 이름       | 설명                                                         | 유효 값 |
| :--------- | :----------------------------------------------------------- | :----- |
| SECRET_ID  | 필수 매개변수, APPID에 대응하는 키 ID는 COS 콘솔 왼쪽 탐색 창 [키 콘솔] 또는 [클라우드 API 키 콘솔]( https://console.cloud.tencent.com/cam/capi)에서 획득할 수 있습니다 | 문자열
| SECRET_KEY | 필수 매개변수, APPID에 대응하는 키 Key는 COS 콘솔 왼쪽 탐색 창 [키 콘솔] 또는 [클라우드 API 키 콘솔]( https://console.cloud.tencent.com/cam/capi)에서 획득할 수 있습니다 | 문자열
| BUCKET     | 필수 매개변수, 지정한 버킷 이름, 버킷의 명명 규칙은 `<BucketName-APPID>`입니다. 자세한 내용은 [버킷 개요](https://cloud.tencent.com/document/product/436/13312)를 참조하십시오 | 문자열 |
| REGION     | 필수 매개변수, 버킷이 위치한 지역, 자세한 내용은 [가용 지역](https://cloud.tencent.com/doc/product/436/6224)을 참조하십시오 | 문자열 |
| MAX_THREAD |선택 가능 매개변수, 멀티 스레드 업로드 시 최대 스레드 수(기본값은 5이고 범위는 1-10입니다)               | 숫자   |
| PART_SIZE  | 선택 가능 매개변수, 멀티파트 업로드 시 단일 파트 크기(단위는 MB이고 기본값은 1MB이며 범위는 1-100입니다)        | 숫자   |


>!
- `~/.cos.conf`파일(Windows 환경에서 이 파일은 **나의 문서** 아래의 숨기기 파일입니다)을 직접 편집하고, 이 파일은 초기화 시 존재하지 않지만,`coscmd config`명령으로 생성합니다. 사용자는 수동으로 생성할 수도 있습니다.
  구성 완료 후 `.cos.conf` 파일의 내용 예시가 다음과 같습니다.
```shell
 [common]
secret_id = AChT4ThiXAbpBDE
secret_key = WE54wreefvds34
bucket = examplebucket-1250000000
region = ap-guangzhou
max_thread = 5
part_size = 1
schema = https
```
- `http/https`를 선택하기 위해 구성 파일에`schema`를 추가하십시오. 기본값은 `https`입니다.
- `anonymous` 옵션에서 `True/False`를 선택하여 익명 모드를 사용할 수 있습니다. 즉, 서명은 비어 있습니다.
- bucket의 명명 규칙은`<BucketName-APPID>`입니다.


### Bucket 명령 지정
-  `-b <BucketName-APPID>를 통해 Bucket`을 지정하십시오. 특정 Bucket을 지정할 수 있습니다.
-  Bucket의 명명 규칙은 `<BucketName-APPID>`입니다. 입력할 버킷 이름은 반드시 이 형식이어야 합니다.
```sh
#명령 형식
coscmd -b <BucketName-APPID> method ...
#작업 예시-파일 업로드
coscmd -b examplebucket-1250000000 upload a.txt b.txt
#작업 예시-bucket 생성
coscmd -b examplebucket-1250000000 createbucket
```

### 버킷 생성
-  `-b<BucketName-APPID> 지정 Bucket`에 맞춰 사용해야 합니다.
```sh
#명령 형식
coscmd -b <BucketName-APPID> createbucket
#작업 예시
coscmd createbucket
coscmd -b examplebucket-1250000000 createbucket
```

### 버킷 삭제
-  `-b<BucketName-APPID> 지정 Bucket`에 맞춰 사용해야 합니다.
```sh
#명령 형식
coscmd -b <BucketName-APPID> deletebucket
#작업 예시
coscmd deletebucket
coscmd -b examplebucket-1250000000 deletebucket
coscmd -b examplebucket-1250000000 deletebucket -f
```

-  -f 매개변수를 사용하면 모든 파일, 버전 제어 후 기록 폴더 및 업로드의 조각을 포함하여 버킷을 강제로 삭제할 수 있습니다.

### 파일 또는 폴더 업로드
- 파일 업로드 명령은 다음과 같습니다.
```sh
#명령 형식
coscmd upload <localpath> <cospath>
#작업 예시
#로컬 /home/folder1/text.txt 파일을 COS folder2/text.txt 경로에 업로드합니다.
coscmd upload /home/folder1/text.txt folder2/text.txt
coscmd upload /home/folder1/text.txt folder2/
```

- 폴더 업로드 명령은 다음과 같습니다.
```sh
#명령 형식
coscmd upload -r <localpath> <cospath>
#작업 예시
coscmd upload -r /home/folder1/ folder2/folder1
coscmd upload -r /home/folder1/ folder2/
#이 작업은 folder2/디렉터리에 folder1/폴더를 생성합니다.
coscmd upload -r /home/folder1  folder2/
#bucket 루트 디렉터리에 업로드합니다.
coscmd upload -r /home/folder1/ /
#동기화 업로드하고 동일한 파일 md5를 건너 뜁니다.
coscmd upload -rs /home/folder1/ /home/folder1
#.txt 및 .doc 접미사 파일을 무시합니다.
coscmd upload -rs /home/folder1/ /home/folder1 --ignore *.txt,*.doc
```

 "<>"의 매개변수를 업로드할 로컬 파일의 경로(localpath) 및 COS의 스토리지 경로(cospath)로 바꿉니다.

 >!
 >  - 파일을 업로드할 때 COS의 파일(폴더) 이름을 포함한 경로를 보충해야 합니다(예시 참조).
 >  - COSCMD는 대용량 파일의 중단 점에서 재개를 지원합니다. 대용량 파일의 멀티파트로 업로드가 실패한 경우 처음부터 다시 시작하는 대신 업로드에 실패한 파트만 다시 업로드됩니다(다시 업로드할 파일의 디렉터리 및 내용이 업로드된 디렉터리와 일치하는 것을 보장해야 합니다).
 >  - COSCMD 멀티파트 업로드 시 각 파트에 대해 MD5 검증을 실행합니다.
 >  - `x-cos-meta-md5` 헤더는 COSCMD가 파일을 업로드할 때 기본적으로 실행되며 그 값은 파일의 `md5'값입니다.
 >  - -s 매개변수를 사용하여 파일을 동기화 업로드하고 동일한 md5를 가진 파일(COS의 소스 파일이 COSCMD 1.8.3.2 이상을 사용하여 업로드되고 x-cos-meta-md5 헤더가 기본적으로 가져야 합니다)을 건너 뜁니다.
 >  - -H 매개변수를 사용하여 HTTP header를 설정할 경우 형식은 반드시 json이어야 합니다. 예시: `coscmd upload -H '{"Cache-Control":"max-age=31536000","Content-Language":"zh-CN"}' <localpath> <cospath>`.
 >  - 폴더를 업로드할 때 --ignore 매개변수를 사용하여 특정 유형의 파일을 무시할 수 있습니다. shell 와일드카드 규칙 및 여러 규칙을 지원하며, 쉼표 `,`로 분할합니다. 한 유형의 접미사를 무시할 때에는 반드시 마지막에 `,`를 입력하거나 `""`를 추가해야 합니다.
 >  - 단일 파일 업로드의 경우 파일 크기가 최대 40TB로 제한됩니다.

### 파일 또는 폴더 다운로드
- 파일 다운로드 명령은 다음과 같습니다.
```sh
#명령 형식
coscmd download <cospath> <localpath>
#작업 예시
coscmd download folder2/text.txt /home/folder1/text.txt
coscmd download folder2/text.txt /home/folder1/
```
- 폴더 다운로드 명령은 다음과 같습니다.
```sh
#명령 형식
coscmd download -r <cospath> <localpath>
#작업 예시
coscmd download -r /home/folder1/ folder2/folder1
coscmd download -r /home/folder1/ folder2/
#현재 bucket 루트 디렉터리 아래의 모든 파일을 다운로드하고 덮어씁니다.
coscmd download -rf / folder2/folder1
#현재 bucket 루트 디렉터리 아래의 모든 파일을 동기화 다운로드하고 동일한 md5 검증 파일을 건너 뜁니다.
coscmd download -rs / folder2/folder1
#.txt 및 .doc 접미사 파일을 무시합니다.
coscmd download -rs / folder2/folder1 --ignore *.txt,*.doc
```
"<>"의 매개변수를 다운로드할 COS 파일의 경로(cospath) 및 로컬 스토리지 경로(localpath)로 바꿉니다.
>!
> - 동일한 이름의 파일이 로컬에 존재하면 다운로드가 실패됩니다. `-f` 매개변수를 사용하여 로컬 파일을 덮어씁니다.
> - `download` API는 멀티파트 다운로드를 사용합니다. 이전 버전의 `mget` API가 폐지되었으니 `download` API를 사용하십시오.
> - `-s` 또는 `--sync` 매개변수를 사용하여 폴더를 다운로드할 때 로컬에 존재하는 동일한 파일을 건너 뜁니다.(다운로드할 폴더가 `COSCMD`의 `upload` API로 업로드되고 파일에 `x-cos-meta-md5` 헤더가 들어있는 경우에만).
> - 폴더를 다운로드할 때 --ignore 매개변수를 사용하여 특정 유형의 파일을 무시할 수 있습니다. shell 와일드카드 규칙 및 여러 규칙을 지원하며, 쉼표 `,`로 분할합니다. 한 유형의 접미사를 무시할 때에는 반드시 마지막에 `,`를 입력하거나 `""`를 추가해야 합니다.

### 파일 또는 폴더 삭제
- 파일 삭제 명령은 다음과 같습니다.
```sh
#명령 형식
coscmd delete <cospath>
#작업 예시
coscmd delete folder2/text.txt
```
- 폴더 삭제 명령은 다음과 같습니다.
```sh
#명령 형식
coscmd delete -r <cospath>
#작업 예시
coscmd delete -r folder2/
coscmd delete -r /
```

 "<>"의 매개변수를 삭제할 COS 파일의 경로(cospath)로 바꿉니다. 도구는 사용자에게 삭제 작업의 실행을 확인하는지를 안내합니다.

 >!일괄 삭제는 확인을 입력하여 `-f` 매개변수를 사용하여 확인을 건너뛰어야 한다.

### 업로드 파일 조각 지우기
- 명령은 다음과 같습니다.
```sh
#명령 형식
coscmd abort
#작업 예시
coscmd abort
```

### 파일 또는 폴더 복사
- 파일 복사 명령은 다음과 같습니다.
```sh
#명령 형식
coscmd copy <sourcepath> <cospath>
#작업 예시
coscmd copy bucket-appid.cos.ap-guangzhou.myqcloud.com/a.txt folder1/text.txt
```
- 폴더 복사 명령은 다음과 같습니다.
```sh
#명령 형식
coscmd copy -r <sourcepath> <cospath>
#작업 예시
coscmd copy -r bucket-appid.cos.ap-guangzhou.myqcloud.com/coscmd/ folder1
coscmd copy -r bucket-appid.cos.ap-guangzhou.myqcloud.com/coscmd/ folder1/
```

 "<>"의 매개변수를 복사할 COS 파일의 경로(sourcepath)와 COS에 복사할 파일의 경로(cospath)로 바꿉니다.

 >!sourcepath의 형식은 다음과 같습니다```<bucketname>-<appid>.cos.<region>.myqcloud.com/<cospath>```.

### 파일 리스트 인쇄
인쇄 명령은 다음과 같습니다.
```sh
#명령 형식
coscmd list <cospath>

#작업 예시
coscmd list -a
coscmd list folder2/text.txt  -r -n 10
```
"<>"의 매개변수를 파일 리스트를 인쇄할 COS 파일의 경로(cospath)로 바꿉니다.
 - `-a`를 사용하여 모든 파일을 인쇄합니다.
 - `-r`을 사용하여 재귀 인쇄하고, 끝에 열거된 파일의 수량과 크기의 합을 반환합니다.
 - `-n num` 를 사용하여 최대 인쇄량을 설정합니다.

>!`<cospath>`이 비어 있으면 현재 Bucket 루트 디렉터리가 기본적으로 인쇄됩니다.

### 파일 정보 표시
명령은 다음과 같습니다.
```sh
#명령 형식
coscmd info <cospath>

#작업 예시
coscmd info folder2/text.txt
```
"<>"의 매개변수를 표시할 COS 파일의 경로(cospath)로 바꾸십시오.

### 서명된 다운로드 URL 가져오기
명령은 다음과 같습니다.
```sh
#명령 형식
coscmd signurl <cospath>

#작업 예시
coscmd signurl folder2/text.txt
coscmd signurl folder2/text.txt -t 100
```

 "<>"의 매개변수를 다운로드 URL을 가져올 COS 파일의 경로(cospath)로 바꿉니다.
 `-t time`을 사용하여 인쇄할 서명의 유효 기간(단위: 초)을 설정합니다.

### ACL 설정
다음 명령을 사용하여 버킷의 접근 제어를 설정하십시오.
```sh
#명령 형식
coscmd putbucketacl --grant-read <root_uin> --grant-write <root_uin> --grant-full-control <root_uin>/<sub_uin>

#작업 예시
coscmd putbucketacl --grant-read 100000000001,100000000001/100000000002 --grant-write anyone --grant-full-control 100000000001/100000000003
```

다음 명령을 사용하여 객체의 접근 제어를 설정하십시오.
```sh
#명령 형식
coscmd putobjectacl --grant-read <root_uin>,<root_uin>/<sub_uin> --grant-write <root_uin> --grant-full-control <root_uin>/<sub_uin> <cospath>

#작업 예시
coscmd putobjectacl  --grant-read 100000000001,100000000001/100000000002 --grant-write anyone --grant-full-control 100000000001/100000000003 folder1/text.txt
```

#### ACL 설정 가이드

- --grant-read는 읽기 권한을 나타냅니다.
--- grant-write는 쓰기 권한을 나타냅니다.
- --grant-full-control은 읽기 / 쓰기 권한을 나타냅니다.
- 루트 계정에 권한을 부여할 경우, `<root_uin>` 형식으로 사용합니다, 예: 100000000001.
- 서브 계정에 권한을 부여할 경우, `<root_uin>/<sub_uin>` 형식으로 사용합니다, 예: 100000000001/100000000002.
- 모든 계정에 권한을 부여할 경우, anyone 형식으로 사용합니다.
- 동시에 권한이 부여된 계정은 영문 쉼표 `,`로 구분됩니다.
- 매개변수를 COS에서 ACL을 설정할 파일의 경로(cospath)로 바꾸십시오.

### ACL 가져오기
- 다음 명령을 사용하여 버킷의 접근 제어를 설정하십시오.
```sh
#명령 형식
coscmd getbucketacl
#작업 예시
coscmd getbucketacl
```

- 다음 명령을 사용하여 객체의 접근 제어를 설정하십시오.
```sh
#명령 형식
coscmd putbucketacl <cospath>
#작업 예시
coscmd getobjectacl folder1/text.txt
```

### 버전 제어의 시작 및 종료
명령은 다음과 같습니다.
```sh
#명령 형식
coscmd putbucketversioning <status>

#버전 제어 시작
coscmd putbucketversioning Enabled

#버전 제어 종료
coscmd putbucketversioning Suspended
```

"<>"의 매개변수를 필요한 버전 제어 상태(status)로 바꿉니다.
>!버전 제어를 시작하면 복원이 불가능합니다. 그런 다음 bucket은 JSON API(모든 JSON SDK 포함)를 사용할 수 없으므로 신중하게 선택하십시오.

### 보관 파일 복원
- 보관 파일 복원 명령은 다음과 같습니다.
```sh
#명령 형식
coscmd restore <cospath>
#작업 예시
coscmd restore -d 3 -t Expedited a.txt
```
- 보관 파일 일괄 복원 명령은 다음과 같습니다.
```sh
#명령 형식
coscmd restore -r <cospath>
#작업 예시
coscmd restore -r -d 3 -t Bulk folder/
```

 "<>"의 매개변수를 파일 리스트를 인쇄할 COS 파일의 경로(cospath)로 바꿉니다.
 - `-d day`를 사용하여 임시 복제본의 만료 기간을 설정하십시오. 기본값: 7.
 - `-t tier`를 사용하여 과정 유형을 구체적으로 복원합니다. 열거형 값: Expedited ,Standard ,Bulk; 기본값: Standard.

### Debug 모드 실행 명령
모든 명령 앞에 `-d` 또는`-debug`를 추가하면 명령 실행 중 자세한 작업 정보가 나타납니다. 예를 들면 다음과 같습니다.
```sh
#upload 자세한 작업 정보와 명령 형식이 나타납니다.
coscmd -d upload <localpath> <cospath>

#작업 예시
coscmd -d upload /home/folder1/text.txt folder2/text.txt  
```

## FAQ
COSCMD 도구 사용 중에 질문이 있으면 [COSCMD 도구류 FAQ](https://cloud.tencent.com/document/product/436/30744)를 참조하십시오.
