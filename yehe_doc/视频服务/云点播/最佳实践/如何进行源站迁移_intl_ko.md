## 소개

VOD 마이그레이션 도구는 데이터 마이그레이션 기능을 통합한 올인원 도구입니다. 간단한 구성 파일을 작성하여 소스 주소의 미디어 파일을 VOD로 빠르게 마이그레이션할 수 있습니다.

## 지원되는 데이터 소스
* [x] 로컬 폴더
* [x] URL 리스트
* [x] Tencent Cloud COS
* [x] AWS S3
* [x] Alibaba Cloud OSS
* [x] Qiniu Kodo COS

## 사용 환경

#### 시스템 환경

Windows, Linux, macOS 시스템을 지원합니다.

#### 소프트웨어 종속

- Python 2.7/3.4+.
- pip 최신 버전.
  
## 설치

### pip를 통해 설치(권장)
pip를 통해 프로젝트에 SDK를 설치할 수 있습니다. 아직 프로젝트 환경에 pip를 설치하지 않았다면 pip 공식 웹사이트에 따라 먼저 설치하십시오.

```
pip install vodmigrate
```


### 소스 패키지를 통해 설치
소스 코드 다운로드 주소: [다운로드](https://github.com/tencentyun/vod-migrate.git)
최신 코드를 다운로드하고 압축을 풉니다.

```shell
git clone https://github.com/tencentyun/vod-migrate.git
cd vod-migrate
python setup.py install
```

## 사용 예시
다음 명령을 실행합니다.
```
vodmigrate config.toml
```
> ?마이그레이션이 완료되면 구성 항목 ‘migrateResultOutputPath’에 해당하는 디렉터리에 결과가 출력되고 파일 이름은 vod_migrate_result.txt가 됩니다.

## 구성 파일 설명
구성 파일은 toml 형식입니다(자세한 내용은 [config_template.toml](https://github.com/tencentyun/vod-migrate/blob/master/test/config_template.toml)을 참고하십시오. 파일이 UTF-8로 인코딩되었는지 확인하십시오). 파일 내용은 다음 부분으로 나눌 수 있습니다.

### 1. 마이그레이션 유형 구성

type은 마이그레이션 유형을 의미합니다. 사용자가 마이그레이션 요건에 따라 해당 표식을 작성합니다. 예를 들어, 로컬 데이터를 VOD에 마이그레이션하는 경우 `[migrateType]`의 설정 내용은 `type=migrateLocal`이 됩니다.
```
[migrateType]
type="migrateLocal"
```
현재 지원하는 마이그레이션 유형은 다음과 같습니다.

| migrateType  |           설명           |
| :----------- | :----------------------: |
| migrateLocal |     로컬 시스템에서 VOD로 마이그레이션     |
| migrateUrl   |   다운로드 URL에서 VOD로 마이그레이션    |
| migrateCos   | Tencent Cloud COS에서 VOD로 마이그레이션|
| migrateAws   |   AWS S3에서 VOD로 마이그레이션   |
| migrateAli   | Alibaba Cloud OSS에서 VOD로 마이그레이션  |
| migrateQiniu      | Qiniu Kodo에서 VOD으로 마이그레이션              |

### 2. 마이그레이션 작업 구성

실제 필요에 따라 VOD에 대한 정보 구성 및 작업 구성 등 마이그레이션 작업을 구성할 수 있습니다.

``` 
# 마이그레이션 툴 공통 구성
[common]
secretId = "SECRETID"
secretKey = "SECRETKEY"
region = 'REGION'
subAppId = 0
concurrency = 5
supportMediaClassification = [ 'video', 'audio', 'image' ]
excludeMediaType = [  ]
migrateDbStoragePath = ''
migrateResultOutputPath = ''
``` 

| 이름                       |                                                                                        설명                                                                                        |
| :------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| secretId                   |             사용자 보안키 SecretId. `SECRETID`를 사용자의 실제 키 정보로 변경합니다. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)의 Tencent Cloud API 키 페이지에서 조회하여 획득할 수 있습니다.  |
| secretKey                  |            사용자 보안키 SecretKey. `SECRETKEY`를 사용자의 실제 키 정보로 변경합니다. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)의 Tencent Cloud API 키 페이지에서 조회하여 획득할 수 있습니다.  |
| region                     | 액세스 포인트 영역, 즉 VOD 서버를 요청할 영역입니다. 이것은 저장 영역과 다릅니다. 자세한 내용은 지원 [리전 리스트](https://intl.cloud.tencent.com/document/product/266/34113)를 참고하십시오. |
| subAppId                   |                VOD [서브 애플리케이션](https://intl.cloud.tencent.com/document/product/266/33987) ID입니다. 서브 애플리케이션에서 파일을 마이그레이션하려면 이 필드에 서브 애플리케이션 ID를 입력합니다. 그렇지 않으면 비워 두십시오.             |
| concurrency                |                                                                            동시에 마이그레이션된 파일의 수입니다. 최대값: 50.                                                                            |
| supportMediaClassification |                                                        마이그레이션에 지원되는 미디어 유형 목록입니다. 유효 값: video, audio, image.                                                         |
| excludeMediaType           |                                                                               제외할 파일 형식 목록입니다.                                                                               |
| migrateDbStoragePath       |                                                                          마이그레이션된 db의 경로를 저장합니다. 이 매개변수가 비어 있으면 현재 디렉터리를 의미합니다.                                                                          |
| migrateResultOutputPath    |                                                      마이그레이션 결과의 경로를 저장합니다(하나의 마이그레이션 레코드는 JSON 문자열의 한 줄에 해당). 이 매개변수가 비어 있으면 현재 디렉터리를 의미합니다.                                                      |

파일 형식 설명:
- 비디오: MP4, TS, FLV, WMV, ASF, RM, RMVB, MPG, MPEG, 3GP, MOV, WEBM, MKV, AVI, **HLS, DASH 미지원**
- 오디오: MP3, M4A, FLAC, OGG, WAV
- 이미지: JPG, JPEG, PNG, GIF, BMP, TIFF, AI, CDR, EPS

### 3. 데이터 소스 구성
[migrateType]의 마이그레이션 유형에 따라 해당 섹션을 설정합니다. 예를 들어, [migrateType]을 type=migrateLocal로 설정한 경우 [migrateLocal] 섹션만 설정하면 됩니다.

#### 3.1 로컬 데이터 소스 migrateLocal 설정

로컬에서 VOD로 마이그레이션하는 경우 해당 부분을 설정합니다. 구체적인 설정 항목 및 설명은 다음과 같습니다.

``` 
# 로컬 시스템에서 VOD로 마이그레이션 시 설정 섹션
[migrateLocal]
localPath = ''
excludes = [ ]
``` 

| 구성 항목    |                                 설명                                  |
| :-------- | :-------------------------------------------------------------------: |
| localPath |                     절대 경로 형식의 로컬 경로                      |
| excludes  | 제외할 디렉터리의 절대 경로. localPath에 있는 디렉터리의 일부 파일은 마이그레이션되지 않습니다. |

#### 3.2 URL 리스트 데이터 소스 migrateUrl 설정
지정한 URL 리스트에서 VOD로 마이그레이션하는 경우 해당 부분을 설정합니다. 구체적인 설정 항목 및 설명은 다음과 같습니다.
```
# URL 리스트에서 VOD로 다운로드 및 마이그레이션 시 설정 섹션
[migrateUrl]
urllistPath = 'D:\folder\urllist.txt'
```

| 구성 항목      |                                    설명                                    |
| :---------- | :------------------------------------------------------------------------: |
| urllistPath | URL 목록을 저장하는 파일의 절대 경로. 파일 내용은 한 줄에 하나의 원래 URL 주소가 포함된 URL 텍스트입니다.|

>?대용량 로컬 파일을 VOD로 마이그레이션해야 하는 경우 [pullUpload](https://intl.cloud.tencent.com/document/product/266/34118) 인터페이스를 사용하여 가져올 것을 권장합니다.
#### 3.3. COS 데이터 소스 migrateCos 구성 

Tencent Cloud COS에서 VOD로 마이그레이션하는 경우 해당 부분을 설정합니다. 구체적인 설정 항목 및 설명은 다음과 같습니다.
``` 
# Tencent Cloud COS에서 VOD로 마이그레이션 시 설정 섹션
[migrateCos]
region = 'ap-shanghai'
bucket = 'examplebucket-1250000000'
secretId = 'COS_SECRETID'
secretKey = 'COS_SECRETKEY'
prefix = ''
``` 

| 구성 항목    |                                                    설명                                                     |
| :-------- | :---------------------------------------------------------------------------------------------------------: |
| region    |        Bucket의 Region 정보. [가용 리전](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오.        |
| bucket    | `<BucketName-APPID>`형식의 Bucket 이름. 예: examplebucket-1250000000 |
| secretId  |   [Tencent Cloud API Key](https://console.cloud.tencent.com/cam/capi)에서 볼 수 있는 Bucket을 소유한 계정 Key의 SecretId  |
| secretKey |  [Tencent Cloud API Key](https://console.cloud.tencent.com/cam/capi)에서 볼 수 있는 Bucket을 소유한 계정 Key의 secret_key  |
| prefix    |                     마이그레이션할 경로의 접두사. Bucket의 모든 데이터를 마이그레이션해야 하는 경우 prefix를 비워 둡니다.                      |

#### 3.4 AWS 데이터 소스 migrateAws 설정
AWS에서 VOD로 마이그레이션하는 경우 해당 부분을 설정합니다. 구체적인 설정 항목 및 설명은 다음과 같습니다.
```
# AWS에서 VOD로 마이그레이션 시 설정 섹션
[migrateAws]
region = 'ap-northeast-2'
bucket = 'bucket-aws'
accessKeyId = 'AccessKeyId'
accessKeySecret = 'AccessKeySecret'
prefix = ''
```

| 구성 항목          |                                설명                                |
| :-------------- | :----------------------------------------------------------------: |
| region          |                        AWS COS Region                         |
| bucket          |                      AWS COS Bucket 이름                      |
| accessKeyId     |                  AccessKeyId를 실제 키 정보로 교체                   |
| accessKeySecret |                AccessKeySecret을 실제 키 정보로 교체                 |
| prefix           |마이그레이션할 경로의 접두사. Bucket의 모든 데이터를 마이그레이션할 경우 prefix는 비워둡니다.|

#### 3.5 Alibaba OSS 데이터 소스 migrateAli 설정
Alibaba Cloud OSS에서 VOD로 마이그레이션하는 경우 해당 부분을 설정합니다. 구체적인 설정 항목 및 설명은 다음과 같습니다.

```
# Alibaba OSS에서 VOD로 마이그레이션 시 설정 섹션
[migrateAli]
bucket = 'bucket-aliyun'
accessKeyId = 'yourAccessKeyId'
accessKeySecret = 'yourAccessKeySecret'
endPoint = 'oss-cn-hangzhou.aliyuncs.com'
prefix = ''
```

| 구성 항목          |                                설명                                |
| :-------------- | :----------------------------------------------------------------: |
| bucket          |                       Alibaba Cloud OSS 버킷 이름                       |
| accessKeyId     |                yourAccessKeyId를 실제 키 정보로 교체                 |
| accessKeySecret |              yourAccessKeySecret을 실제 키 정보로 교체               |
| endPoint        |                        Alibaba Cloud endpoint 주소                        |
| prefix          | 마이그레이션할 경로의 접두사. Bucket의 모든 데이터를 마이그레이션할 경우 prefix는 비워둡니다.|

#### 3.6 Qiniu Kodo 데이터 소스 구성(migrateQiniu)
Qiniu에서 VOD로 마이그레이션하는 경우 해당 부분을 설정합니다. 구체적인 설정 항목 및 설명은 다음과 같습니다.
```
# Qiniu Kodo에서 VOD로 마이그레이션 시 설정 섹션
[migrateQiniu]
bucket = 'bucket-qiniu'
accessKeyId = 'AccessKey'
accessKeySecret = 'SecretKey'
endPoint = 'www.bkt.clouddn.com'
prefix = ''
```

| 구성 항목          |                                설명                                |
| :-------------- | :----------------------------------------------------------------: |
| bucket          |                      Qiniu Kodo Bucket 이름                      |
| accessKeyId     |                   AccessKey를 실제 키 정보로 교체                    |
| accessKeySecret |                   SecretKey를 실제 키 정보로 교체                    |
| endPoint        |                 downloadDomain에 해당하는 Qiniu Kodo의 다운로드 주소                  |
| prefix          | 마이그레이션할 경로의 접두사. Bucket의 모든 데이터를 마이그레이션해야 하는 경우 prefix를 비워 둡니다.|

## 제한 설명
- 이 툴은 일회성 마이그레이션 도구로 설계되었습니다. 마이그레이션은 **원본 서버 파일 스캔**, **마이그레이션**, **마이그레이션 완료**의 3단계로 나뉩니다. 파일 스캔이 완료된 후 구성을 변경하려면 구성 파일 MD5 확인 오류 방지를 위해 db 파일을 지워야 합니다(migrate.db 삭제 또는 db 저장 경로 수정).
- 마이그레이션된 파일은 파일 확장자로 표시되어야 합니다.
- HLS/DASH 파일은 현재 마이그레이션할 수 없습니다.
- 마이그레이션 후에는 원본 비디오 간의 디렉터리 관계를 유지할 수 없으며 각 비디오에는 서로 관련이 없는 독립적인 FileId가 있습니다.

## 마이그레이션 프로세스 개요
1. 구성 파일을 읽어 마이그레이션 type에 따라 해당 설정 섹션을 읽어오고 매개변수 검사를 실행합니다.
2. 마이그레이션 유형에 따라 원본 서버를 스캔하여 마이그레이션 작업을 생성합니다.
3. 스캔이 완료되면 마이그레이션이 수행되고 각 작업의 결과와 전체 진행 상황이 출력됩니다.
4. 마이그레이션이 완료되면 세부 정보가 결과 파일에 출력됩니다.
![](https://main.qcloudimg.com/raw/66946618fe7e54ea19f7a8a78890078b.png)

