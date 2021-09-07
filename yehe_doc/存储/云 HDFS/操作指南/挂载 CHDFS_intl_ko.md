
CHDFS와 마운트 포인트 생성 후, 마운트 포인트를 통해 CHDFS를 마운트할 수 있습니다. 본 문서는 CHDFS 마운트 방법을 소개합니다.  

## 전제 조건
- 마운트할 기기 또는 컨테이너에 Java 1.8이 설치되어 있어야 합니다. 
- 마운트할 기기 또는 컨테이너의 VPC와 마운트 포인트 지정 VPC가 같아야 합니다. 
- 마운트할 기기 또는 컨테이너의 VPC IP가 마운트 포인트 지정 권한 그룹중 하나의 권한 규칙 라이선스 주소에 매칭되어야 합니다. 

## 작업 절차
1. [CHDFS-Hadoop](https://github.com/tencentyun/chdfs-hadoop-plugin) JAR 패키지를 다운로드합니다. 
2. JAR 패키지를 해당 디렉터리로 이동합니다. EMR 클러스터의 경우 모든 노드의 `/usr/local/service/hadoop/share/hadoop/common/lib/`디렉터리로 동기화할 수 있습니다. 
3.core-site.xml 파일을 편집하고 다음 기본 설정을 추가합니다. 
```
<!--chdfs 구현 유형-->
<property>
		 <name>fs.AbstractFileSystem.ofs.impl</name>
		 <value>com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter</value>
</property>
<property>
		 <name>fs.ofs.impl</name>
		 <value>com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter</value>
</property>
<!--로컬 cache의 임시 디렉터리로, 데이터 읽기/쓰기의 경우, 메모리 cache 부족 시, 로컬 디스크에 쓰기 하며, 이 경로가 존재하지 않을 경우 자동 생성됩니다. -->
<property>
		 <name>fs.ofs.tmp.cache.dir</name>
		 <value>/data/chdfs_tmp_cache</value>
</property>
<!--appId-->      
<property>
		 <name>fs.ofs.user.appid</name>
		 <value>1250000000</value>
</property>
```
4. core-site.xml을 모든 hadoop 노드로 동기화 합니다. 
>? EMR 클러스터의 경우, 앞의 절차 3, 4를 통해 EMR 콘솔 컴포넌트 관리에서 HDFS 설정을 수정할 수 있습니다. 
5. hadoop fs 명령 라인 툴을 사용하여, `hadoop fs –ls ofs://${mountpoint}/` 명령을 실행하며, 이 때 mountpoint는 마운트 주소입니다. 파일 리스트가 정상적으로 표시되면 CHDFS 마운트가 완료되었음을 의미합니다. 
6.사용자도 hadoop 기타 설정 항목 또는 mr 작업을 통해 CHDFS에서 데이터 작업을 실행할 수 있습니다.  mr 작업의 경우, `-Dfs.defaultFS=ofs://${mountpoint}/`를 통해 이번 작업의 기본 입출력 FS를 CHDFS로 수정할 수 있습니다. 

## 기타 설정 항목

|        설정 항목      |                             설명                             |  기본값   | 필수 입력 여부 |
| :------------------------------| :----------------------------------------------------| :-------| :------ |
|       fs.ofs.tmp.cache.dir        |   임시 데이터 저장    |    없음     |    예    |
|       fs.ofs.map.block.size       | chdfs 파일 시스템의 block 크기, 단위는 바이트. 기본값은 128MB(map 분할에만 영향을 주며, chdfs 기본 스토리지 블럭 사이즈와 무관) | 134217728 |    아니오    |
| fs.ofs.data.transfer.thread.count |               chdfs 데이터 전송 시의 병행 스레드 수                |    32     |    아니오    | 
| fs.ofs.block.max.memory.cache.mb  | chdfs 플러그 인이 사용하는 메모리 buffer 크기, 단위는 MB. (읽기/쓰기에 모두 가속 효과) |    16     |    아니오    |
|  fs.ofs.block.max.file.cache.mb   |  chdfs 플러그 인이 사용하는 디스크 buffer 크기, 단위는 MB임. (읽기/쓰기에 모두 가속 효과)  |    256    |    아니오    |
|   fs.ofs.prev.read.block.count    | 읽기 할 때, 미리 읽어 오는 chdfs block 수량(chdfs의 기본 block 크기는 일반적으로 4MB임）|     4     |    아니오    |
|      fs.ofs.plugin.info.log       |          플러그 인의 디버깅 로그 출력 여부, 로그는 info 레벨로 출력. 선택값은 true、false |   false   |    아니오    |

