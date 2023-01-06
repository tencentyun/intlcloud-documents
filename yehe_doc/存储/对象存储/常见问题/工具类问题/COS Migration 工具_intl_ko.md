### 마이그레이션 툴에서 작업 중 오류가 발생해 종료되었습니다. 어떻게 해야 하나요?

툴에서는 업로드 시 중단된 시점부터 이어 올리기를 지원합니다. 대용량 파일 작업 도중에 종료되었거나 서비스 장애가 발생하였을 경우 다시 툴을 실행하여 업로드가 완료되지 않은 파일을 계속 업로드할 수 있습니다.

### 마이그레이션이 완료된 파일을 콘솔 또는 기타 방법을 통해 COS에서 삭제하면 마이그레이션 툴에서 해당 파일을 다시 업로드하나요?

다시 업로드하지 않습니다. 마이그레이션이 완료된 모든 파일은 db에 기록되어 마이그레이션 툴 실행 전에 db 목록을 스캔하기 때문에 기록된 파일은 다시 업로드하지 않습니다. 자세한 원인은 [마이그레이션 메커니즘 및 프로세스](https://intl.cloud.tencent.com/document/product/436/15392)를 참조하십시오.

### 마이그레이션에 실패하고 로그에 403 Access Deny가 표시됩니다. 어떻게 처리해야 하나요?

키 정보, Bucket 정보, Region 정보가 정확한지, 작업 권한이 있는지 확인합니다. 서브 계정인 경우 루트 계정에서 해당 권한을 부여받아야 하며, 로컬 마이그레이션 및 기타 클라우드 스토리지 마이그레이션인 경우 Bucket에 대한 데이터 쓰기와 읽기 권한이 있어야 합니다. Bucket copy인 경우에는 원본 Bucket에 대한 데이터 쓰기 권한이 필요합니다.

### 기타 클라우드 스토리지에서 COS로 마이그레이션에 실패하고 Read timed out이 표시됩니다. 어떻게 처리해야 하나요?

일반적으로 이 오류는 네트워크 대역폭이 부족하여 발생하며, 다른 클라우드 스토리지에서 데이터를 다운로드할 때 시간 초과가 발생합니다. 예를 들어 AWS 해외 데이터를 COS로 마이그레이션하는 경우, 데이터를 로컬로 다운로드할 때 대역폭이 부족하면 딜레이 시간 발생률이 높아 read time out이 발생할 수 있습니다. 따라서 기기의 네트워크 대역폭을 넓혀야 하며, 마이그레이션 전에 wget을 사용하여 다운로드 속도를 테스트하는 것을 권장합니다.

### 마이그레이션에 실패하고 로그에 503 Slow Down이 표시됩니다. 어떻게 처리해야 하나요?

이 오류는 주파수 제어가 트리거될 때 발생합니다. COS의 계정에는 초당 30000QPS 제한이 있습니다. 구성에서 작은 파일의 동시성을 줄이는 것이 좋습니다. 그런 다음 툴을 다시 실행하여 마이그레이션을 재개하십시오.

### 마이그레이션에 실패하고 로그에 404 NoSuchBucket이 표시됩니다. 어떻게 처리해야 하나요?

키 정보, Bucket 정보, Region 정보가 정확한지 확인하십시오.

### 실행에 오류가 발생해 다음과 같은 정보가 표시됩니다. 어떻게 해야 하나요?

![img](https://main.qcloudimg.com/raw/9fdac231af66c991c13fe0440e8d7366.png)
가능한 이유는 이 툴이 64비트 JDK가 필요한 rocksdb를 사용하기 때문입니다. JDK 버전이 X64인지 확인하십시오.

### Windows 환경에서 rocksdb의 jni 라이브러리를 찾을 수 없다고 합니다. 어떻게 처리해야 하나요?
Windows 환경의 경우 Microsoft Visual Studio 2015 환경에서 컴파일해야 합니다. 해당 오류가 보고되는 경우 [Visual C++ Redistributable for Visual Studio 2015](https://www.microsoft.com/zh-CN/download/details.aspx?id=48145) 설치가 필요합니다.

### 로그 레벨은 어떻게 수정하나요?
src/main/resources/log4j.properties 파일을 수정합니다. DEBUG, INFO, ERROR와 같은 log4j.rootLogger의 값을 해당하는 로그 레벨에 복사합니다.

### Linux 환경에서 /tmp/librocksdbjnixxx.so: ELF file OS ABI invalid 오류가 보고됩니다. 어떻게 처리해야 하나요?
IFUNC는 Linux에서 지원되어야 하며 실행 환경의 binutils 버전은 2.20 이상이어야 합니다.

### 작업이 완전히 실행되지 않고 error.log에 "java.nio.file.FileSystemLoopException"이 보고되면 어떻게 처리해야 하나요?
error.log의 예외 정보는 다음과 유사합니다.

```
2022-XX-XX XX:XX:XX [ERROR] [main:xxx] [com.qcloud.cos_migrate_tool.task.MigrateLocalTaskExecutor:] [MigrateLocalTaskExecutor.java:183]
walk file tree error
java.nio.file.FileSystemLoopException: /dataseal/xx1/file1
at java.nio.file.FileTreeWalker.visit(FileTreeWalker.java:294)
at java.nio.file.FileTreeWalker.next(FileTreeWalker.java:372)
at java.nio.file.Files.walkFileTree(Files.java:2706)
at com.qcloud.cos_migrate_tool.task.MigrateLocalTaskExecutor.buildTask(MigrateLocalTaskExecutor.java:176)
at com.qcloud.cos_migrate_tool.task.TaskExecutor.run(TaskExecutor.java:244)
at com.qcloud.cos_migrate_tool.app.App.main(App.java:135)
```
마이그레이션할 "/dataseal/xx1/file1" 파일이 parent 디렉터리의 리소스를 가리키는 소프트 링크일 수 있기 때문입니다. 다음 명령으로 확인할 수 있습니다.

```
[root@TENCENT64 /dataseal/cos_migrate_tool_v5-master/log]# ll /dataseal/xx1/file1
lrwxrwxrwx 1 xx xx xx xx   x xxxx /dataseal/xx1/file1 -> ../xx1/
```

위에 표시된 것처럼 소프트 링크 파일 "/dataseal/xx1/file1"은 parent 디렉터리에서 "/dataseal/xx1/"을 가리키며 순회 시 무한 루프를 일으킵니다. 따라서 마이그레이션 작업이 자동으로 종료됩니다.
이러한 파일은 미리 삭제하는 것이 좋습니다(참고: 구성 항목 ‘excludes’에서 해당 파일을 제외하는 방법은 유효하지 않음).

다른 문제가 발생하면 마이그레이션 툴을 재실행해 보십시오. 문제가 지속되면 구성(키가 숨겨진 상태)과 log 디렉터리를 압축하고 [문의하기](https://intl.cloud.tencent.com/contact-sales)로 문의하십시오.
