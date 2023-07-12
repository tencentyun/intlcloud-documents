## 기능 설명
HDFS TO COS 툴은 HDFS의 데이터를 Tencent Cloud COS에 복사하는 데 사용됩니다.

## 사용 환경
#### 시스템 환경
Linux 또는 Windows 시스템

#### 소프트웨어 종속
JDK 1.7 또는 1.8 

#### 설치 및 설정
구체적인 환경 설치 및 설정은 [Java 설치 및 설정](https://intl.cloud.tencent.com/document/product/436/10865)을 참조하십시오.

## 설정 방법
1. Hadoop-2.7.2 이상의 버전을 설치합니다. 구체적인 설치 절차는 [Hadoop 설치 및 테스트](https://intl.cloud.tencent.com/document/product/436/10867)를 참조하십시오.
2. [GitHub](https://github.com/tencentyun/hdfs_to_cos_tools)에서 HDFS TO COS 툴을 다운로드한 후 압축을 해제하십시오.
3. 동기화할 HDFS 클러스터의 core-site.xml을 conf 폴더에 복사합니다. core-site.xml에는 NameNode의 설정 정보가 포함되어 있습니다.
4. 구성 파일 cos_info.conf의 버킷(Bucket), 리전(Region) 및 API 키 정보를 편집합니다. 버킷의 이름은 사용자 정의 문자열과 시스템에서 생성한 APPID 숫자열이 하이픈으로 연결되어 구성됩니다(예시: examplebucket-1250000000).
5. 명령 라인 매개변수에서 구성 파일 위치를 지정합니다. 기본 위치는 conf/cos_info.conf입니다.
>!명령 라인 매개변수의 매개변수와 구성 파일이 겹치는 경우, 명령 라인을 기준으로 합니다.

## 사용 방법

>?다음은 Linux를 예시로 한 사용 방법입니다.

### 도움말 조회

```
./hdfs_to_cos_cmd -h
```


### 파일 복사

- HDFS에서 COS로 복사합니다. COS에 동일한 이름의 파일이 존재하는 경우 원본 문서를 덮어씁니다.
```
./hdfs_to_cos_cmd --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/
```
-  HDFS에서 COS로 복사합니다. COS에 이름과 길이가 동일한 파일이 존재하는 경우 업로드를 무시합니다(1회 복사 후 다시 복사 시 적용).
```
./hdfs_to_cos_cmd --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/ -skip_if_len_match
```
여기에서는 길이만 판단합니다. Hadoop 상의 파일 개요를 계산할 경우 부하가 비교적 크기 때문입니다.

- HDFS에서 COS로 복사합니다. HDFS에 Har 디렉터리(Hadoop Archive 보관 파일)가 존재하는 경우 --decompress_har 매개변수를 지정하여 자동으로 har 파일을 압축 해제할 수 있습니다.
```
./hdfs_to_cos_cmd --decompress_har --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/
```
--decompress_har 매개변수를 지정하지 않는 경우, 기본적으로 일반 HDFS 디렉터리에 따라 복사를 진행합니다. 즉, .har 디렉터리에 있는 index 및 masterindex 등의 파일을 그대로 복사합니다.

### 디렉터리 정보

```shell
conf : core-site.xml과 cos_info.conf를 저장하는 데 사용되는 구성 파일
log: 로그 디렉터리
src: Java 소스 프로그램
dep: 컴파일 생성된 실행 가능한 JAR 패키지
```

## 문제 및 도움말
#### 설정 정보 관련
버킷(Bucket), 리전(Region) 및 API 키 정보를 포함한 설정 정보가 정확하게 입력되었는지 확인하십시오. 버킷의 이름은 사용자 정의 문자열과 시스템에서 생성한 APPID 숫자열이 하이픈으로 연결되어 구성됩니다(예시: examplebucket-1250000000). 또한 기기의 시간과 베이징 시간을 동일하게(1분 정도의 차이는 정상) 유지하고, 차이가 큰 경우 기기의 시간을 다시 설정하십시오.

#### DataNode 관련
DataNode에 복사 프로그램이 있는 기기도 연결할 수 있도록 보장하십시오. NameNode는 공인 IP로 연결할 수 있지만, 획득하는 block이 위치한 DataNode 기기는 내부 IP이므로 직접 연결할 수 없습니다. 따라서 동기화 프로그램을 Hadoop의 노드에서 실행해 NameNode와 DataNode에 모두 액세스할 수 있도록 보장하는 것을 권장합니다.

#### 권한 관련
Hadoop 명령어를 사용해 파일을 다운로드하고 정상인지 확인한 후에, 동기화 툴을 사용해 Hadoop의 데이터 지원을 동기화하십시오.

#### 파일 덮어쓰기 관련
COS에 존재하는 파일은 기본적으로 재전송 시 덮어쓰게 됩니다. 사용자가 명확하게 -skip_if_len_match를 지정한 경우 외에, 파일 길이가 동일한 경우 업로드를 건너뜁니다.

#### cos path 관련
cos path는 기본적으로 디렉터리로 설정되어 있으며, 최종적으로 HDFS에서 복사하는 파일은 모두 해당 디렉터리에 저장됩니다.


### Tencent Cloud EMR HDFS로부터의 데이터 복사 관련
Tencent Cloud EMR HDFS에서 COS로 데이터를 복사할 때 고성능 Distcp 툴 사용을 권장합니다. [Hadoop 파일 시스템과 COS 간 데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/436/34076)을 참조하십시오.
