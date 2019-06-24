## 기능 설명
HDFS TO COS 도구는 HDFS의 데이터를 Tencent Cloud COS에 복사하는 데 사용됩니다.
## 사용 환경
### 운영 체제
Linux 또는 Windows
### 소프트웨어 의존
JDK 1.7/1.8
#### 설치 및 구성
환경 설치 및 구성에 대한 자세한 내용은 [Java 설치 및 구성](https://cloud.tencent.com/document/product/436/10865)을 참조하십시오.
## 구성 및 사용방법
### 구성 방법
1. Hadoop-2.7.2 및 이상 버전을 설치하십시오. 설치 절차에 대한 자세한 내용은 [Hadoop 설치 및 테스트](/doc/product/436/10867)를 참조하십시오.
2. [GitHub 주소](https://github.com/tencentyun/hdfs_to_cos_tools)를 통하여 HDFS TO COS 도구를 다운로드하여 압축 해제하십시오.
3. 동기화할 HDFS 클러스터의 core-site.xml을 conf 폴더에 복사하십시오. core-site.xml에는 NameNode 배치 정보가 포함됩니다.
4. 구성 파일 `cos_info.conf`, 버킷(Bucket), 지역(Region), 그리고 API 키 정보를 편집합니다. 버킷의 이름은 사용자 지정 문자열과 시스템 생성 appid 숫자열이 중선으로 연결되어 있습니다(예시: mybucket-1250000000).
5. 명령행 매개변수에서 구성 파일 위치를 지정합니다. 기본 위치는 `conf/cos_info.conf`입니다.
> <font color="#0000cc">**주의:** </font>
명령행 매개변수의 매개변수가 구성 파일과 겹칠 때 명령행을 기준으로 합니다.

### 사용 방법
(Linux를 예로)
#### 도움말 보기
```
./hdfs_to_cos_cmd -h
```
실행 결과는 다음과 같습니다.
![위챗 이미지_20170807163035](//mc.qcloudimg.com/static/img/dcff34d37928c0d8b9c4b45c25ac116e/image.png)

#### 파일 복사
- HDFS에서 COS로 복사한 파일이 원래 COS에 저장된 파일과 이름이 같은 경우 후자가 덮어쓰기 됩니다.
```
./hdfs_to_cos_cmd --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/
```
-  HDFS에서 COS로 복사한 파일이 원래 COS에 저장된 파일과 이름 및 길이가 같은 경우 복사가 무시됩니다(복사 후 재복사 시 적용).
```
./hdfs_to_cos_cmd --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/ -skip_if_len_match
```
Hadoop에 있는 파일 요약을 산출하면 비용이 크기 때문에 길이 판단만 합니다.

#### 디렉터리 정보
```
conf: 구성 파일은 core-site.xml 및 cos_info.conf를 저장하는데 적용합니다.
log: 로그 디렉터리
src: Java 소스 프로그램
dep: 컴파일된 실행 가능한 JAR 패키지
```
## 질문 및 도움말
#### 구성 정보 관련
버킷(Bucket), 지역(Region), 그리고 API 키 정보를 포함하여, 입력한 구성 정보가 정확한지 확인하십시오. 버킷 이름은 사용자 지정 문자열과 시스템 생성 appid 숫자 문자열이 중선으로 연결되어 있으며(예: mybucket-1250000000), CVM 시간과 베이징 시간이 일치하도록 보장하고(1분 정도의 차이가 정상입니다) 차이가 크면 CVM 시간을 재설정하십시오.
#### DateNode 관련
DateNode에 대해 카피 프로세스가 있는 CVM도 연결될 수 있도록 해주십시오. NameNode는 공인 IP로 연결되지만 획득하는 block이 위치한 DateNode CVM은 사설 IP이며 직접 연결될 수 없습니다. 그러므로 동기화 프로그램은 Hadoop의 어느 노드에 실행시켜 NameNode 및 DateNode에 대해 접근 가능하도록 보장합니다.
#### 권한 관련
Hadoop 명령으로 파일을 다운로드하여 정상인지 확인한 다음에 동기화 도구를 사용하여 Hadoop에서 데이터 지원을 동기화하십시오.
#### 파일 덮어쓰기 관련
COS에 이미 존재하는 파일에 대해서 기본적으로 재전송으로 덮어쓰기 됩니다. 사용자가 명시적으로 `-skip_if_len_match`를 지정하지 않으면 파일 길이가 일치할 경우 업로드를 건너뜁니다.
#### cos path 관련
 cos path는 기본적으로 디렉터리이며 HDFS에서 복사한 파일은 해당 디렉터리에 저장됩니다.
