Tencent Cloud Linux의 버전에 따라 해당하는 TOA 패키지를 다운로드하여 압축 해제합니다.
-   [CentOS 7.2 64](http://toamodule-1253438722.file.myqcloud.com/CentOS%207.2%2064.zip)
-  [CentOS 7.3 64](http://toamodule-1253438722.file.myqcloud.com/CentOS%207.3%2064.zip)
-  [CentOS 7.4 64](http://toamodule-1253438722.file.myqcloud.com/CentOS%207.4%2064.zip)
- 	[Debian 8.2 64](http://toamodule-1253438722.file.myqcloud.com/Debian%208.2%2064.zip)
-  [Debian 9.0 64](http://toamodule-1253438722.file.myqcloud.com/Debian%209.0%2064.zip) 
-   [SUSE Linux Enterprise Server 11 SP3 64](http://toamodule-1253438722.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2011%20SP3%2064.zip)
-  [SUSE Linux Enterprise Server 12 64](http://toamodule-1253438722.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2012%2064.zip)
-  [Ubuntu Server 14.04.1 LTS 64](http://toamodule-1253438722.file.myqcloud.com/Ubuntu%20Server%2014.04.1%20LTS%2064.zip)
-  [Ubuntu Server 16.04.1 LTS 64](http://toamodule-1253438722.file.myqcloud.com/Ubuntu%20Server%2016.04.1%20LTS%2064.zip) 


1. 압축 해제를 완료한 후, cd 명령을 진행하여 방금 압축 해제한 폴더에 들어가고 로딩 모듈 명령을 실행합니다.
```
insmod toa.ko
``` 
2. 다음 명령을 실행하여 로딩 성공 여부를 확인합니다.
```
lsmod | grep toa
```
3. 로딩에 성공하면 마지막으로 스크립트에 toa.ko 파일을 로딩하기만 하면 됩니다(기계를 재부팅하면 ko 파일을 다시 로딩해야 함).


위의 다운로드 파일에 귀하의 운영 체제 버전에 대응하는 설치 패키지가 없다면 Linux 통용 버전의 오리진 코드 패키지를 다운로드하여 컴파일한 후에 가져오기할 수 있습니다. 해당 버전은 Centos6.9와 Centos7, Ubuntu14.04 등 대부분의 Linux 발행 버전을 지원합니다.

1. 오리진 코드 패키지 획득하기
```
wget http://toamodule-1253438722.file.myqcloud.com/tencenttoa.zip
```

2. 파일 컴파일
```
yum install gcc
yum install kernel-headers
yum install kernel-devel
```

3. toa.ko 파일 로딩
```
tar -zxvf linux_toa.tar.gz
cd toa
make
mv toa.ko /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
insmod /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
```

