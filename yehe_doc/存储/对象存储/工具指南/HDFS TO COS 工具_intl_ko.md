## 기능 설명
HDFS TO COS 툴은 HDFS 상의 데이터를 Tencent Cloud COS로 복사하는 데 사용합니다.

## 사용 환경
### 시스템 환경
Linux 또는 Windows 시스템

### 소프트웨어 종속
JDK 1.7 또는 1.8 

#### 설치 및 설정
환경에 따른 설치 및 설정에 대한 자세한 사항은 [Java 설치 및 설정](https://cloud.tencent.com/document/product/436/10865)을 참조하십시오.

## 설정 및 사용 방법
### 설정 방법
1. Hadoop-2.7.2 이상의 버전을 설치합니다. 자세한 설치 방법은 [Hadoop 설치 및 테스트](https://cloud.tencent.com/document/product/436/10867)를 참조하십시오.
2. [GitHub](https://github.com/tencentyun/hdfs_to_cos_tools)에서 HDFS TO COS 툴을 다운로드하고 압축을 해제합니다.
3. 동기화할 HDFS 클러스터의 core-site.xml을 conf 폴더에 복사합니다. core-site.xml에는 NameNode 설정 정보가 포함되어 있습니다.
4. 구성 파일 `cos_info.conf`에서 버킷(Bucket), 리전(Region), API 키 정보를 편집합니다. 이 때 버킷의 이름은 사용자 지정 문자열과 시스템에서 생성한 APPID 숫자열이 하이픈으로 연결되어 구성(예: examplebucket-1250000000)됩니다.
5. 명령 라인 매개변수에서 구성 파일 위치를 지정합니다. 기본 위치는 `conf/cos_info.conf`입니다.
>!명령 라인 매개변수의 매개변수와 구성 파일이 중첩되는 경우 명령 라인을 기준으로 합니다.

### 사용 방법

Linux 환경을 예시로 하며, 사용 방법은 다음과 같습니다.

#### 도움말 조회
```
./hdfs_to_cos_cmd -h
```
실행 결과는 다음 이미지와 같습니다.
![WeChat 이미지_20170807163035](//mc.qcloudimg.com/static/img/dcff34d37928c0d8b9c4b45c25ac116e/image.png)

#### 파일 복사
- HDFS에서 COS로 복사하며, COS에 동일한 이름의 파일이 존재하는 경우 원본 문서를 덮어씁니다.
```
./hdfs_to_cos_cmd --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/
```
-  HDFS에서 COS로 복사하며, COS에 이름과 길이가 동일한 파일이 존재하는 경우 업로드를 생략(한 번 복사한 후 다시 복사할 때 사용)합니다.
```
./hdfs_to_cos_cmd --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/ -skip_if_len_match
```
여기에서는 길이만 판단하며, Hadoop 상의 파일 개요를 계산할 경우 부하가 비교적 크기 때문입니다.

- HDFS에서 COS로 복사하며, HDFS에 Har 디렉터리(Hadoop Archive 아카이브 파일)가 존재하는 경우 --decompress_har 매개변수를 지정하여 자동으로 har 파일을 압축 해제할 수 있습니다.
```
./hdfs_to_cos_cmd --decompress_har --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/
```
`--decompress_har` 매개변수를 지정하는 경우, 기본적으로 일반 HDFS 디렉터리와 동일하게 복사를 진행합니다. 즉, `.har` 디렉터리 하위에 있는 `index` 및 `masterindex`등의 파일을 원본 포맷으로 복사합니다.

#### 디렉터리 정보
```shell
conf : 구성 파일이며, core-site.xml과 cos_info.conf를 저장하는 데 사용됩니다.
log  : 로그 디렉터리
src  : Java 소스 프로그램
dep  : 컴파일 생성된 실행 가능한 JAR 패키지
```
## 문제 및 도움말
#### 설정 정보 관련
버킷(Bucket), 리전(Region), API 키 정보를 포함한 설정 정보를 정확하게 입력하십시오. 이 때 버킷의 이름은 사용자 지정 문자열과 시스템에서 생성한 APPID 숫자열이 하이픈으로 연결되어 구성(예: examplebucket-1250000000)됩니다. 또한 기기의 시간과 베이징 시간을 동일하게(1분 정도 차이가 있는 것은 정상임) 유지하고, 차이가 큰 경우 기기의 시간을 다시 설정하십시오.

#### DateNode 관련
DateNode에 대한 액세스를 보장하십시오. 프로그램 사본이 있는 기기를 연결해도 됩니다. NameNode는 공인 IP로 연결할 수 있지만 획득하는 block이 존재하는 DateNode 기기는 개인 IP로, 직접 연결할 수 없습니다. 따라서 동기화 프로그램을 Hadoop의 특정 노드에 저장하여 실행해 NameNode와 DateNode에 모두 액세스할 수 있도록 보장하는 것을 권장합니다.

#### 권한 관련
Hadoop 명령어를 사용하여 파일을 다운로드하고 정상 여부를 검사한 후, 동기화 툴을 사용해 Hadoop 상에 있는 데이터를 동기화하도록 지원합니다.

#### 파일 덮어쓰기 관련
COS 상에 이미 존재하는 파일은 재전송 시 사용자가 명확하게 `-skip_if_len_match`를 지정하여 파일 길이가 동일한 경우 업로드를 건너뛰는 경우를 제외하고 기본적으로 덮어씁니다.

#### cos path 관련
 cos path은 기본적으로 디렉터리로 설정되어 있으며, 최종적으로 HDFS에서 복사하는 파일은 모두 해당 디렉터리로 저장됩니다.
