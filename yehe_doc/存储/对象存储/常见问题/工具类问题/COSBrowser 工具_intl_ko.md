### COSBrowser 툴이란 무엇입니까?

COSBrowser는 Tencent Cloud COS가 출시한 시각화 인터페이스 툴로, COS 리소스 조회, 전송, 관리를 간편하고 인터랙티브하게 실현할 수 있습니다. 현재 COSBrowser는 데스크톱 버전(Windows, macOS, Linux) 및 모바일 버전(Android, iOS)을 제공하며, 자세한 내용은 [COSBrowser 소개](https://intl.cloud.tencent.com/document/product/436/11366)를 참조하십시오.


### COSBrowser 툴은 어떻게 다운로드합니까?

다운로드 주소 및 사용 설명은 [COSBrowser 소개](https://intl.cloud.tencent.com/document/product/436/11366)를 참조하십시오.

### CentOS 그래픽 인터페이스를 더블 클릭했는데도 COSBrowser 클라이언트가 실행되지 않습니다.

단말에서 `./cosbrowser.AppImage --no-sandbox` 명령어를 실행하여 클라이언트를 실행할 수 있습니다.


### 서브 계정으로 COSBrowser에 로그인하면 스토리지 경로가 나타나지 않는 이유는 무엇입니까?

1. 서브 계정에 COS 액세스 관련 권한이 있는지 확인합니다. 관련 문서는 [서브 계정에 COS 액세스 권한 부여](https://intl.cloud.tencent.com/document/product/436/11714)를 참조하십시오.
2. 서브 계정에 특정 버킷 또는 버킷의 특정 디렉터리에 대한 권한만 있는 경우 COSBrowser 툴에 로그인 시 수동으로 스토리지 경로를 추가하고 버킷이 속한 리전을 선택해야 합니다. 버킷 형식 경로는 Bucket 또는 Bucket/Object-prefix로, 예를 들면 examplebucket-1250000000 형식입니다.
![](https://main.qcloudimg.com/raw/bf6b59f824af9413fbe83bb8968f926d.png)


### 대량 파일의 전송 속도는 어떻게 높입니까?

Windows 버전 COSBrowser 툴을 예로 들면, [고급 설정]에 들어가 [업로드], [다운로드] 파일의 동시 접속 수와 멀티파트 블록 수를 조정하여 전송 속도를 높일 수 있습니다.
![](https://main.qcloudimg.com/raw/d74eae3fb53dce13fee5c6b6e517e526.png)


### 시스템이 macOS인데 COSBrowser에서 "업데이트 실패, 권한이 거부되었습니다."가 팝업됩니다. 어떻게 처리해야 합니까?
![](https://main.qcloudimg.com/raw/b07cd00819c3f27b05ac361ed561c52a.png)

**오류 발생 원인**
`/Users/username/Library/Caches/` 디렉터리에는 `com.tencent.cosbrowser`와 `com.tencent.cosbrowser.ShipIt` 2개의 파일이 있으며, 해당 두 파일의 소유자가 각각 root 사용자와 user 사용자인 경우 권한 문제로 업데이트 실패 오류가 발생합니다.

**해결 방법**
Mac 단말에서 다음 명령 라인을 실행합니다.
```plaintext
sudo chown $USER ~/Library/Caches/com.tencent.cosbrowser.ShipIt/
```

### “no such file or directory, stat 'C:\Users\XXX\AppData\Local\Temp\cosbrowser\logs\cosbrowser.log'” 오류가 팝업되고 애플리케이션을 사용할 수 없는 경우 어떻게 해야 합니까?

![](https://main.qcloudimg.com/raw/42629a0686b7a892fef8946e547c9ef6.png)

**해결 방법**: 2.1.x 이상의 버전을 다운로드하시기 바랍니다.

### cosbrowser.exe 설치 패키지 실행 중 설치가 중단되었습니다. 어떻게 해야 합니까?

**오류 발생 원인**
이는 이전에 COSBrowser를 설치한 적이 있는 경우, 이후 수동으로 애플리케이션을 삭제했지만 시스템에 잔여 파일이 제거되지 않았기 때문입니다. 다시 설치하면 프로그램에서 잔여 파일을 발견하여 실제로 애플리케이션이 없지만 존재하는 것으로 인식해 설치를 중단하여 발생하는 문제입니다.

**해결 방법**
수동으로 제거하거나 기타 정리 툴(예: Tencent 보안 관리자의 소프트웨어 관리)을 사용하여 COSBrowser 애플리케이션 설치 잔여 파일을 삭제합니다.

