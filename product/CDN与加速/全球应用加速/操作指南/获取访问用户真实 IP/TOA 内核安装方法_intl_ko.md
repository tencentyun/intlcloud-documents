## CentOS TOA 커널 설치 방법
### rpm 패키지 설치 방식
아래의 rpm 패키지를 직접 다운로드하기:
- CentOS 6 TOA 패키지([클릭하여 다운로드하기](http://toakernel-1253438722.cossh.myqcloud.com/kernel-2.6.32-220.23.1.el6.toa.x86_64.rpm));
- CentOS 7 TOA 패키지([클릭하여 다운로드하기](http://toakernel-1253438722.cossh.myqcloud.com/kernel-3.10.0-693.el7.centos.toa.x86_64.rpm));  

다운로드 및 설치한 후, 시스템을 다시 시작하면 설치가 완료됩니다.

또는 rpm 패키지를 직접 만들 수도 있습니다. 구체적인 방법은 다음과 같습니다.
1. kernel-2.6.32-220.23.1.el6.src.rpm 설치:
```
rpm -hiv kernel-2.6.32-220.23.1.el6.src.rpm
```

2. 커널 오리진 코드 디렉터리 생성:
```
rpmbuild -bp ~/rpmbuild/SPECS/kernel.spec
```

3. 오리진 코드 디렉터리 1개 복사:
```
cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/
cp -a linux-2.6.32-220.23.1.el6.x86_64/ linux-2.6.32-220.23.1.el6.x86_64_new
```

4. 복사한 오리진 코드 디렉터리에서 아래의 toa 패치 제작:
```
cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/linux-2.6.32-220.23.1.el6.x86_64_new/
patch -p1 < /usr/local/src/linux-2.6.32-220.23.1.el6.x86_64.rs/toa-2.6.32-220.23.1.el6.patch
```

5. .Config를 편집하여 SOURCE 디렉터리로 복사:
```
sed -i 's/CONFIG_IPV6=m/CONFIG_IPV6=y/g' .config
echo -e '\n# toa\nCONFIG_TOA=m' >> .config
cp .config ~/rpmbuild/SOURCES/config-x86_64-generic
```

6. 기존 오리진 코드의 .config 삭제:
```
cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/linux-2.6.32-220.23.1.el6.x86_64
rm -rf .config
```

7. 최종 patch 생성:
```
cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/
diff -uNr linux-2.6.32-220.23.1.el6.x86_64 linux-2.6.32-220.23.1.el6.x86_64_new/ >
~/rpmbuild/SOURCES/toa.patch
```

8. kernel.spec 편집:
`vim ~/rpmbuild/SPECS/kernel.spec`
ApplyOptionPath에서 다음 내용(buildid 등 사용자 지정 커널 패키지 이름 수정 가능) 추가:
```
Patch999999: toa.patch
ApplyOptionalPatch toa.patch
```
9. rpm 패키지 제작:
```
rpmbuild -bb --with baseonly --without kabichk --with firmware --without debuginfo --target=x86_64 ~/rpmbuild/SPECS/kernel.spec
```

10. 커널 rpm 패키지 설치:
```
rpm -hiv kernel-xxxx.rpm --force
```

11. 다시 시작하고 toa 모듈 로딩하면, 설치가 완료됩니다.

### 오리진 코드 설치 방식

필요한 운영 체제 버전이 CentOS 6보다 낮지 않으면, 소스 코드 컴파일을 다운로드하면 해당하는 설치 패키지도 획득할 수 있습니다. 절차는 다음과 같습니다.
1. toa 패치를 제작란 오리진 코드 패키지를 다운로드합니다([클릭하여 다운로드하기](http://kb.linuxvirtualserver.org/images/3/34/Linux-2.6.32-220.23.1.el6.x86_64.rs.src.tar.gz))
2. 압축을 해제합니다.
3. `.config`를 편집하고 `CONFIG_IPV6=M`을 `CONFIG_IPV6=y`로 변경합니다.
4. 사용자 지정 설명을 추가해야 할 경우, ` Makefile`을 편집할 수 있습니다.
5. `make -jn`(n은 스레드 수입니다)
6. `make modules_install`을 실행합니다.
7. `make install`을 실행합니다.
8. `/boot/grub/menu.lst`를 수정하고 default를 새로 설치한 커널(title 순서는 0에서 시작)로 변경합니다.
9. `Reboot` 다시 시작을 실행하면 toa 커널이 됩니다.
10. `lsmod | grep toa`를 실행하여 toa 모듈이 로딩 여부를 검사합니다. 로딩되지 않았다면, `modprobe toa` 명령을 통해 시작합니다.

## Ubuntu TOA 커널 설치 방법
아래 링크를 클릭하여 커널 패키지와 Headers 패키지를 다운로드합니다.
- 커널 패키지([클릭하여 다운로드하기](http://toakernel-1253438722.cossh.myqcloud.com/linux-image-4.4.87.toa_1.0_amd64.deb)) 
- 커널 Headers 패키지([클릭하여 다운로드하기](http://toakernel-1253438722.cossh.myqcloud.com/linux-headers-4.4.87.toa_1.0_amd64.deb)) 

Headers 패키지는 옵션으로 관련 개발 시 다시 설치할 수 있습니다. 우선 커널 패키지를 설치하십시오. 구체적인 절차는 다음과 같습니다.

1. 아래 명령을 실행하고 커널 패키지를 설치합니다.  
```
dpkg -i linux-image-4.4.87.toa_1.0_amd64.deb
```
2. 설치를 완료하면 CVM을 다시 시작합니다.

3. `lsmod | grep toa`를 실행하여 toa 모듈이 로딩 여부를 검사합니다. 로딩되지 않았다면, `modprobe toa`로 시작할 수 있습니다. 실행 명령은 다음과 같습니다.
```
echo “modprobe toa” >> /etc/rc.d/rc.local
```

## Debian TOA 커널 설치 방법
아래 링크를 클릭하여 커널 패키지와 Headers 패키지를 다운로드합니다.
- 커널 패키지([클릭하여 다운로드하기](http://toakernel-1253438722.cossh.myqcloud.com/linux-image-3.16.43.toa_1.0_amd64.deb))
- 커널 Headers 패키지([클릭하여 다운로드하기](http://toakernel-1253438722.cossh.myqcloud.com/linux-headers-3.16.43.toa_1.0_amd64.deb))

Headers 패키지는 옵션으로 관련 개발 시 다시 설치할 수 있습니다. 우선 커널 패키지를 설치하십시오. 구체적인 절차는 다음과 같습니다.

1. 아래 명령을 실행하고 커널 패키지를 설치합니다.  
```
dpkg -i linux-image-4.4.87.toa_1.0_amd64.deb
```
2. 설치를 완료하면 CVM을 다시 시작합니다.

3. `lsmod | grep toa`를 실행하여 toa 모듈이 로딩 여부를 검사합니다. 로딩되지 않았다면, `modprobe toa` 로 시작할 수 있습니다. 실행 명령은 다음과 같습니다.
```
echo “modprobe toa” >> /etc/rc.d/rc.local
```

