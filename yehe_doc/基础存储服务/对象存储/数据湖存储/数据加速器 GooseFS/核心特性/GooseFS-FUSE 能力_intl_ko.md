GooseFS-FUSE는 Unix 기기의 로컬 파일 시스템에 GooseFS 분산형 파일 시스템을 마운트할 수 있습니다. 이 기능을 사용하면 일부 표준 TCCLI(예: ls, cat 및 echo)가 GooseFS 분산형 파일 시스템의 데이터에 직접 액세스할 수 있습니다. 또한 더 중요한 것은 C, C++, Python, Ruby, Perl, Java와 같은 다른 언어로 구현된 애플리케이션은 모두 GooseFS의 클라이언트 통합 및 설정 없이 표준 POSIX 인터페이스(예시: open, write, read)를 통해 GooseFS를 읽고 쓸 수 있습니다.

GooseFS-FUSE는 [FUSE](http://fuse.sourceforge.net/) 프로젝트를 기반으로 하며 대부분의 파일 시스템 작업을 지원합니다. 그러나 GooseFS의 일회성 불변 파일 데이터 모델과 같은 고유한 속성으로 인해 마운트된 파일 시스템은 POSIX 표준과 완전히 일치하지 않으며 여전히 제한성이 있습니다. 따라서 이 특징의 기능과 제한을 이해하려면 먼저 [제한성](#limit)을 읽으십시오.

## 설치 요구 사항

- JDK 1.8 이상
- Linux 시스템: [libfuse](https://github.com/libfuse/libfuse) 2.9.3 이상(버전 2.8.3은 사용 가능하나 경고 발생 가능성 있음)
- MAC 시스템: [osxfuse](https://osxfuse.github.io/) 3.7.1 이상

## 사용법

### GooseFS-FUSE 마운트

설정을 완료하고 GooseFS 클러스터를 시작한 후 GooseFS를 마운트해야 하는 노드에서 Shell을 실행하고 $GOOSEFS_HOME 디렉터리로 이동하여 다음 명령어를 실행합니다.
```
$ integration/fuse/bin/goosefs-fuse mount mount_point [GooseFS_path]
```
이 명령은 `<mount_point>`로 지정된 경로에 해당 GooseFS 경로를 마운트하기 위해 백엔드 Java 프로세스를 실행합니다. 예를 들어 다음 명령은 GooseFS 경로 /people을 로컬 파일 시스템의 /mnt/people 디렉터리에 마운트합니다.
```
$ integration/fuse/bin/goosefs-fuse mount /mnt/people /people
Starting goosefs-fuse on local host.
goosefs-fuse mounted at /mnt/people. See /lib/GooseFS/logs/fuse.log for logs
```
GooseFS_path를 지정하지 않으면 GooseFS-FUSE는 기본적으로 GooseFS 루트 디렉터리(/)에 마운트됩니다. 이 명령을 여러 번 호출하여 GooseFS를 다른 로컬 디렉터리에 마운트할 수 있습니다. 모든 GooseFS-FUSE는 $GOOSEFS_HOME\logs\fuse.log 로그 파일을 공유합니다. 이 로그 파일은 오류 진단에 유용합니다.
>! `<mount_point>`는 로컬 파일 시스템의 빈 폴더여야 하며 GooseFS-FUSE 프로세스를 실행한 사용자는 마운트 포인트 및 읽기/쓰기 권한이 있습니다.
>


### GooseFS-FUSE 언마운트

GooseFS-FUSE를 언마운트할 때 노드에서 Shell을 실행하고 $GOOSEFS_HOME 디렉터리로 이동하여 다음 명령을 실행해야 합니다.
```
$ integration/fuse/bin/goosefs-fuse umount mount_point
```
이 명령은 goosefs-fuse Java 백엔드 프로세스를 종료하고 파일 시스템을 언마운트합니다. 예시:
```
$ integration/fuse/bin/goosefs-fuse umount /mnt/people
Unmount fuse at /mnt/people (PID: 97626).
```
기본적으로 unmount 작업은 읽기/쓰기 작업이 완료되지 않은 경우 최대 120s 동안 기다립니다. 120s 후에도 읽기/쓰기 작업이 완료되지 않으면 Fuse 프로세스가 강제 종료되어 파일 읽기/쓰기가 실패하게 되므로 -s 매개변수를 추가하여 Fuse 프로세스가 강제 종료되는 것을 방지할 수 있습니다. 예시:
```
$ ${GOOSEFS_HOME}/integration/fuse/bin/goosefs-fuse unmount -s /mnt/people
```

### GooseFS-FUSE가 실행 중인지 확인

모든 마운트 포인트를 나열하려면 노드에서 Shell을 실행하고 $GOOSEFS_HOME 디렉터리로 이동하여 다음 명령을 실행해야 합니다.
```
$ integration/fuse/bin/goosefs-fuse stat
```
이 명령은 pid, mount_point, GooseFS_path를 포함한 정보를 출력합니다.

예를 들어 출력은 다음 형식일 수 있습니다.
```
$ pid    mount_point     GooseFS_path
80846  /mnt/people     /people
80847  /mnt/sales       /sales
```
 

### Goosefs-FUSE 디렉터리 구조

![](https://qcloudimg.tencent-cloud.cn/raw/1711edcd1e0789aed28f6a295dfe5361.png)

conf 디렉터리:
- masters: master 서버의 IP 구성 파일
- worker: worker 서버의 IP 구성 파일
- goosefs-site.properties: goosefs 구성 파일
- libexec: goosefs-fuse 종속 lib 파일 실행
- goosefs-fuse-1.4.0: goosefs-fuse 백엔드에서 실행되는 jar 패키지
- log: 로그 디렉터리

## 설정 옵션

GooseFS-FUSE는 표준 GooseFS-core-client-fs를 기반으로 작업합니다. 다른 애플리케이션을 사용하는 client와 같이 작업하려면, 이 GooseFS-core-client-fs의 동작을 사용자 정의하십시오.

$GOOSEFS_HOME/conf/goosefs-site.properties 구성 파일을 편집하여 클라이언트 옵션을 변경할 수 있습니다.
>! 모든 변경은 GooseFS-FUSE가 실행되기 전에 완료되어야 합니다.
>

<span id=limit></span>

## 제한성

현재 GooseFS-FUSE는 대부분의 기본 파일 시스템 작업을 지원합니다. 그러나 GooseFS의 몇 가지 특징으로 인해 다음 사항에 유의해야 합니다.
- 파일은 랜덤 및 추가로 작성될 수 없습니다.
- 파일은 한 번만 순차적으로 쓸 수 있으며 수정할 수 없습니다. 파일을 수정하려면 먼저 파일을 삭제한 다음 다시 생성하거나 O_TRUNC 식별자로 파일을 open하고 길이를 0으로 설정합니다.
- 마운트 지점에 작성 중인 파일은 읽을 수 없습니다.
- 파일 길이는 truncate할 수 없습니다.
- soft/hard link 미지원; GooseFS는 hard-link 및 soft-link의 개념이 없기 때문에 ln과 같은 관련 명령어는 지원하지 않습니다. 또한 hard-link에 대한 정보는 ll의 출력에 표시되지 않습니다.
- COS(Cloud Object Storage)가 기본 저장소로 사용되는 경우 Rename 작업은 원자가 아닙니다.
- GooseFS의 GooseFS.security.group.mapping.class 옵션이 ShellBasedUnixGroupsMapping 값으로 설정된 경우에만 파일의 사용자 및 그룹 정보가 Unix 시스템의 사용자 그룹에 해당합니다. 그렇지 않으면 chown 및 chgrp의 작업이 적용되지 않으며 ll이 반환하는 사용자 및 그룹은 GooseFS-FUSE 프로세스의 사용자 및 그룹 정보입니다.

## 성능 고려 사항

FUSE와 JNR을 함께 사용하기 때문에 마운트된 파일 시스템을 사용하는 경우 네이티브 파일 시스템 API를 직접 사용하는 경우보다 성능이 상대적으로 떨어집니다.

대부분의 성능 문제의 이유는 read 또는 write 작업을 할 때마다 메모리에 여러 복사본이 있고 FUSE는 쓰기의 최대 데이터 분할 정도를 128KB로 설정하기 때문입니다. kernel 3.15에 연결된 FUSE write-backs 캐시 정책을 이용하면 성능이 크게 향상될 수 있습니다(그러나 libfuse 2.x 사용자 공간 라이브러리는 현재 이 기능을 지원하지 않습니다).

## GooseFS-FUSE 설정 매개변수

GooseFS-FUSE와 관련된 설정 매개변수는 다음과 같습니다.

| **매개변수**                                    | **기본값**   | **설명**                                                     |
| ------------------------------------------- | ------------ | ------------------------------------------------------------ |
| goosefs.fuse.cached.paths.max               | 500          |   내부 GooseFS-FUSE 캐시 크기를 정의하며, 이 캐시는 로컬 파일 시스템 경로와 Alluxio 파일 URI 간의 가장 자주 사용되는 전환을 점검합니다.                                                          |
| goosefs.fuse.debug.enabled                  | false        | `goosefs.logs.dir`로 지정된 디렉터리의 `fuse.out` 로그 파일로 리디렉션되는 FUSE 디버깅 출력을 허용합니다. |
| goosefs.fuse.fs.name                        | goosefs-fuse | FUSE가 파일 시스템을 마운트하는 데 사용하는 설명형 이름입니다.                           |
| goosefs.fuse.jnifuse.enabled                | true         |   더 나은 성능을 위해 JNI-Fuse 라이브러리를 사용합니다. 비활성화되면 JNR-Fuse가 사용됩니다.                                                           |
| goosefs.fuse.shared.caching.reader.enabled  | false        |  (실험용) GooseFS JNI Fuse를 통한 다중 프로세스 파일 읽기 성능 향상을 위해 공유 grpc 데이터 리더를 사용합니다. 블록 데이터는 클라이언트에 캐시되므로 Fuse 프로세스에는 더 많은 메모리가 필요합니다.                                                            |
| goosefs.fuse.logging.threshold              | 10s          |  소요 시간이 임계값을 초과하면 FUSE API 호출을 기록합니다.                                                            |
| goosefs.fuse.maxwrite.bytes                 | 131072       | FUSE 쓰기 작업(bytes)의 데이터 분할 정도. 현재 128KB는 Linux 커널 제한의 상한선입니다. |
| goosefs.fuse.user.group.translation.enabled | false        | FUSE API에서 GooseFS 사용자 및 그룹을 해당 Unix 사용자 및 그룹으로 전환할지 여부입니다. false로 설정하면 모든 FUSE 파일의 사용자 및 그룹이 goosefs-fuse 스레드가 마운트된 사용자 및 그룹으로 표시됩니다.  |

## FAQ

#### libfuse 라이브러리 파일 누락
GooseFS-Fuse를 마운트하기 전에 libfuse를 설치해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7a535eed0fac0da06f530fb04ca9702b.png)
- **방법1**
설치 명령어:
```
yum install fuse-devel
```
설치 완료 여부 조회:
```
find / -name libfuse.so*
```
- **방법2**
이전 버전 libfuse.so.2.9.2를 업데이트합니다. 설치 단계는 다음과 같습니다.
>? CentOS 7에 libfuse를 설치합니다. CentOS 7은 기본적으로 libfuse.so.2.9.2를 설치합니다.
>
먼저 [libfuse 소스 코드](https://github.com/libfuse/libfuse/releases/tag/fuse-2.9.7)를 다운로드하고 libfuse.so.2.9.7을 컴파일 및 생성합니다.
```
tar -zxvf fuse-2.9.7.tar.gz
cd fuse-2.9.7/ && ./configure && make && make install
echo -e '\n/usr/local/lib' >> /etc/ld.so.conf
ldconfig
```
다음으로, libfuse.so.2.9.7을 다운로드, 컴파일 및 생성한 후 아래 단계에 따라 설치 및 교체합니다.
 1. 다음 명령을 실행하여 이전 버전 libfuse.so.2.9.2 라이브러리 링크를 찾습니다.
```
find / -name libfuse.so*
```
 2. 다음 명령을 실행하여 libfuse.so.2.9.7을 이전 ​​버전 라이브러리 libfuse.so.2.9.2 위치에 복사합니다.
```
cp /usr/local/lib/libfuse.so.2.9.7 /usr/lib64/
```
 3. 다음 명령을 실행하여 이전 libfuse.so 라이브러리에 대한 모든 링크를 삭제합니다.
```
rm -f /usr/lib64/libfuse.so
rm -f /usr/lib64/libfuse.so.2
```
 4. 다음 명령을 실행하여 삭제된 이전 버전의 링크와 유사한 libfuse.so.2.9.7 라이브러리를 링크합니다.
```
ln -s /usr/lib64/libfuse.so.2.9.7 /usr/lib64/libfuse.so
ln -s /usr/lib64/libfuse.so.2.9.7 /usr/lib64/libfuse.so.2
```

#### VIM을 사용하여 마운트 지점에서 파일을 편집하는 동안 Write error in swap file? 오류가 발생합니다.
GooseFS-Fuse 마운팅 포인트에서 파일 편집에 VIM 7.4 또는 이전 버전을 사용하도록 VIM 구성을 변경할 수 있습니다. VIM swap 파일은 시스템이 충돌하거나 다시 시작하는 경우 VIM이 swap 파일을 기반으로 저장하지 않은 수정 사항을 복원할 수 있도록 수정 사항을 유지하는 데 사용됩니다. 상기 오류는 VIM swap 파일에 대한 임의 쓰기 작업으로 인해 발생하며 GooseFS에서는 지원하지 않습니다. 솔루션: `:set noswapfile` 명령을 실행하여 swap 파일 생성을 종료하거나 구성 파일(~/.vimrc)에 `set noswapfile`을 추가할 수 있습니다.
