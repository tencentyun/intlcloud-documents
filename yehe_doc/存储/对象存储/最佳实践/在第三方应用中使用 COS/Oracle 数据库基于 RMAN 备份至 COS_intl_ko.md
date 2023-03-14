## 소개

무제한 대용량의 COS(Cloud Object Storage)는 CAS 자동 전환 유형 및 DEEP ARCHIVE 유형이 있습니다. 테이프 원가와 비슷한 비용으로, 이 제품은 백업 및 보관 시나리오에 특히 적합합니다.

점점 더 많은 고객이 클라우드에 데이터를 백업하고 있습니다. 이를 용이하게 하기 위해 Oracle의 백업 모듈은 COS와 통합되어 저렴한 비용으로 데이터베이스를 백업 및 복원할 수 있습니다.

## OSB와 Tencent Cloud COS의 접목

Oracle의 Oracle Secure Backup Cloud Module은 Oracle Secure Backup(OSB) 제품군에 속하며, COS와의 연결을 실현하고 Oracle 데이터베이스를 클라우드 및 Tencent Cloud COS에 직접 백업합니다. Oracle Secure Backup Cloud Module 모듈은 RMAN 기능과 통합되어 사용자는 RMAN 스크립트를 사용자 정의하여 Oracle 데이터베이스를 Tencent Cloud COS에 직접 효율적으로 백업할 수 있습니다.

Oracle 9i 이상의 버전에서 Oracle Secure Backup Cloud Module이 지원됩니다. 상세 내용은 [Oracle 공식 문서](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/rcmrf/oracle-secure-backup-osb-cloud-module.html#GUID-6FCF4FD8-861C-4D52-BB41-32E6EF03789F)를 참고하십시오.


## OSB 설치

1. [Oracle 공식 홈페이지](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/rcmrf/oracle-secure-backup-osb-cloud-module.html#GUID-964AADD2-3405-4476-8698-E9F2133CB5B7)로 이동하여 최신 버전을 다운로드하고 OSB를 설치하십시오.
2. 다운로드한 osbws_installer.zip 압축 팩의 압축을 풀고, 실제 COS 서비스의 SecretId, SecretKey, 리전 및 endpoint 매개변수 설정에 따라 아래 명령을 실행하여 OSB를 설치합니다.
>!서브 계정 키를 우선적으로 사용하고 위험을 줄이기 위해 [최소 권한의 원칙 설명](https://intl.cloud.tencent.com/document/product/436/32972)을 따르는 것이 좋습니다. 서브 계정 키를 가져오는 방법에 대한 자세한 내용은 [액세스 키](https://intl.cloud.tencent.com/document/product/598/32675)를 참고하십시오.
>
```
java -jar osbws_install.jar -AWSID <SecretId> -AWSKey <SecretKey> -walletDir $ORACLE_HOME/osbws_wallet -libDir $ORACLE_HOME/lib -location <리전> -awsEndPoint <endpoint>

// 압축 패키지의 저장 디렉터리에 따라 교체
```
예시:
```
java -jar osbws_install.jar -AWSID AKIDxxxx -AWSKey XXXX -walletDir $ORACLE_HOME/osbws_wallet -libDir $ORACLE_HOME/lib -location ap-guangzhou -awsEndPoint cos.ap-guangzhou.myqcloud.com
```
>? Oracle 12 이상에는 OSB 모듈이 자체 포함되어 있으며, 설치 중 오랜 시간 동안 download가 응답하지 않으면 공식 홈페이지에서 최신 OSB 모듈을 다운로드하여 설치하거나 프록시 서버를 사용하여 설치하는 것을 고려하십시오.
>


## RMAN을 통한 COS 데이터베이스 백업

1. 데이터베이스에 로그인하고 다음 명령을 실행하여 RMAN에 연결합니다.
```
rman target / 
```
2. 다음 명령을 실행하여 데이터베이스를 COS 버킷에 백업합니다. 그 중`lib/libcos.so`와 `cosorcl.ora`의 일부는 데이터베이스 이름과 관련이 있으므로 실제 값에 따라 수정하십시오.
```
	run {
	allocate channel ch1 type
	sbt parms='SBT_LIBRARY=/u01/app/oracle/product/11.2.0/dbhome_1/lib/libcos.so,
	SBT_PARMS=(OSB_WS_PFILE=/u01/app/oracle/product/11.2.0/dbhome_1/dbs/cosorcl.ora)';
	backup channel=ch1 database format='ora_%d_%I_%T_%s_%t_%c_%p.dbf' plus archivelog;
	backup channel=ch1  current controlfile  format='%d_%I_%T_%s_%t_%c_%p.conf';
	backup channel=ch1 spfile format='ora_%d_%I_%T_%s_%t_%c_%p.spf' ;
	release channel ch1;
	}
```

## RMAN을 통해 COS로부터 데이터베이스 복구

1. 데이터베이스를 닫고 노마운트 상태로 만듭니다.
 - 다음 명령어를 실행하여 데이터베이스를 비활성화 합니다.
```
shutdown immediate;
```
 - 다음 명령어를 실행하여 데이터베이스를 닫고 nomount 상태로 만듭니다.
```
startup nomount;
```
2. rman 명령어 list backup을 통해 모든 백업 파일을 나열한 후, 복원할 백업 파일을 선택하고, 선택한 백업 파일의 핸들(Handle) 이름과 태그(TAG) 값을 기록합니다.
3. 다음 restore 명령을 실행하여 백업 파일을 연결합니다.
연결 핸들이 "ORACLE_1880733115_20190507_5_1007656283_1_1.conf"인 백업 파일로, list backup을 통해 얻을 수 있습니다. `lib/libcos.so`와 `cosorcl.ora`의 일부는 데이터베이스 이름과 관련이 있고, 실제 값에 따라 수정할 수 있으며 백업할 때와 일치합니다.
```
	run {
	allocate channel ch1 type
	sbt parms='SBT_LIBRARY=/u01/app/oracle/product/11.2.0/dbhome_1/lib/libcos.so,
	SBT_PARMS=(OSB_WS_PFILE=/u01/app/oracle/product/11.2.0/dbhome_1/dbs/cosorcl.ora)';
	restore controlfile from 'ORACLE_1880733115_20190507_5_1007656283_1_1.conf';
	release channel ch1;
	}
```
4. 다음 restore 명령을 실행하여 데이터베이스를 mount 상태 alter database mount로 전환합니다.
```
	run {

	allocate channel ch1 type
	sbt parms='SBT_LIBRARY=/u01/app/oracle/product/11.2.0/dbhome_1/lib/libcos.so,
	SBT_PARMS=(OSB_WS_PFILE=/u01/app/oracle/product/11.2.0/dbhome_1/dbs/cosorcl.ora)';
	restore database from tag='TAG20190507T163102';
	recover database from tag='TAG20190507T163102';
	release channel ch1;
	}
```
 - **TAG20190507T163102**의 tag 값은 각 백업의 ID 번호와 동일합니다. list backup을 통해 획득하며, 이전에 복원된 제어 파일과 일치해야 합니다. 즉, 핸들이 "**ORACLE_1880733115_20190507_5_1007656283_1_1.conf**" 인 백업 파일 tag.
 - `lib/libcos.so`와 `cosorcl.ora`는 일정 부분 데이터베이스 이름과 관련이 있으며 실제 값에 따라 수정하고, 백업할 때와 일치해야 합니다.
5. 데이터베이스를 열면 COS에서 복구된 데이터를 볼 수 있습니다.


## RMAN 동시성 설정 수정

>? RMAN에는 기본적으로 동시성이 없으며 수동으로 수정해야 합니다.
>

RMAN에 로그인하여 동시성 매개변수 설정을 수정합니다. 이 곳에서는 동시성 수 15를 예로 듭니다.
```
	run {
	configure channel device type sbt parms='SBT_LIBRARY=/u01/app/oracle/product/11.2.0/dbhome_1/lib/libcos.so ENV=(OSB_WS_PFILE=/u01/app/oracle/product/11.2.0/dbhome_1/dbs/cosorcl.ora)';
	configure default device type to SBT;
	configure device type SBT parallelism 15;
	}
```

## 관련 참고 내용

더 많은 도움 정보는, [Oracle 공식 문서](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/rcmrf/oracle-secure-backup-osb-cloud-module.html#GUID-6FCF4FD8-861C-4D52-BB41-32E6EF03789F)를 참고하십시오.


