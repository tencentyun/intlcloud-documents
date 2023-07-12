### COSBrowser 툴이란 무엇입니까?

COSBrowser는 Tencent Cloud Object Storage(COS)가 출시한 시각화 인터페이스 툴로, COS 리소스 조회, 전송, 관리를 간편하고 인터랙티브하게 실현할 수 있습니다. 현재 COSBrowser는 데스크톱 버전(Windows, macOS, Linux) 및 모바일 버전(Android, iOS)을 제공하며, 자세한 내용은 [COSBrowser 소개](https://intl.cloud.tencent.com/document/product/436/11366)를 참고하십시오.


### COSBrowser 툴은 어떻게 다운로드합니까?

다운로드 주소 및 사용 설명은 [COSBrowser 소개](https://intl.cloud.tencent.com/document/product/436/11366)를 참고하십시오.

### COSBrowser에 어떻게 로그인하나요?

자세한 내용은 [데스크톱 사용 설명서](https://intl.cloud.tencent.com/document/product/436/32565) 또는 [모바일 버전 기능](https://intl.cloud.tencent.com/document/product/436/41616) 문서를 참고하십시오.

**데스크톱 로그인**

COSBrowser 데스크톱은 Tencent Cloud API 키를 통한 로그인만 지원합니다.

매개변수 설명:

1. TencentCloud API **secretID** 및 **secretKey** : CAM 콘솔의 [API Key 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 얻을 수 있습니다. 성공적으로 로그인하면 키가 나중에 사용할 수 있도록 기록 키에 저장됩니다.

2. 버킷/액세스 경로: 루트 계정으로 로그인할 때 비워 둘 수 있습니다. 로그인을 위해 서브 계정을 사용하는 경우 `example-1250000000/test/`와 같은 인증된 경로를 입력해야 합니다.
>!COSBrowser는 프로젝트 키를 통한 로그인을 지원하지 않습니다.

**모바일 버전 로그인**
COSBrowser 모바일에서는 다음 세 가지 방식의 로그인 방법을 지원합니다.

- **WeChat 빠른 로그인**: WeChat Tencent Cloud 계정을 생성하거나 연결하여 WeChat 빠른 로그인 방식을 이용해 COSBrowser에 빠르게 로그인할 수 있습니다.
- **이메일 로그인**: 이메일 Tencent Cloud 계정을 생성하거나 연결하여 이메일 계정 비밀번호를 입력해 로그인할 수 있습니다.
- **영구 키 로그인**: 사용자는 Tencent Cloud API 키의 SecretId와 SecretKey(프로젝트 키는 지원하지 않음)를 이용해 로그인할 수 있으며, 해당 키는 액세스 관리 콘솔의 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 획득할 수 있습니다. 로그인 후 해당 계정은 영구적으로 로그인 상태가 유지됩니다.

>?
>- 사용자의 Tencent Cloud 계정을 QQ 계정으로 생성한 경우에도 WeChat 빠른 로그인을 통해 로그인할 수 있으며, WeChat 미니프로그램 인터페이스에서 QQ 로그인을 선택하면 됩니다.
>- 서브 계정 사용자는 키를 사용하거나 WeChat 빠른 로그인 방식으로 로그인할 수 있으며, WeChat 로그인을 선택하는 경우 WeChat 미니프로그램 인터페이스에서 서브 계정을 선택하면 됩니다.

자세한 내용은 [COSBrowser 소개](https://intl.cloud.tencent.com/document/product/436/11366)를 참고하십시오.

### 서브 계정으로 COSBrowser에 로그인하면 스토리지 경로가 나타나지 않는 이유는 무엇입니까?

1. 서브 계정에 COS 액세스 관련 권한이 있는지 확인합니다. 관련 문서는 [서브 계정에 COS 액세스 권한 부여](https://intl.cloud.tencent.com/document/product/436/11714)를 참고하십시오.
2. 서브 계정에 특정 버킷 또는 버킷의 특정 디렉터리에 대한 권한만 있는 경우 COSBrowser 툴에 로그인 시 수동으로 스토리지 경로를 추가하고 버킷이 속한 리전을 선택해야 합니다. 버킷 형식 경로는 Bucket 또는 Bucket/Object-prefix로, 예를 들면 examplebucket-1250000000 형식입니다.
   ![](https://main.qcloudimg.com/raw/bf6b59f824af9413fbe83bb8968f926d.png)

### 임시 키로 COSBrowser에 로그인할 수 있습니까?

임시 키로 로그인할 수 없습니다.

### COSBrowser 체험판은 어떻게 들어가나요?

**체험 참고사항**

**애플리케이션 체험 규정:**

- 체험판 이동 후 COSBrowser는 자동으로 임시 계정을 생성하여 로그인합니다. 임시 계정은 1회용입니다. 종료 후 자동으로 로그아웃되며 모든 데이터가 지워집니다.
- 임시 계정은 24시간 동안 유효합니다. 만료 후에도 체험판을 계속하려면 이 페이지에서 다시 클릭하십시오.

**애플리케이션 체험 제한 사항:**

체험판은 파일 업로드, 파일 다운로드, 링크 공유와 같은 기본적인 데이터 관리 기능만 제공합니다. 더 많은 기능을 사용해 보려면 개인 계정으로 로그인하십시오. 자세한 내용은 [COSBrowser 시작하기](https://intl.cloud.tencent.com/document/product/436/35276)를 참고하십시오.

### CentOS 그래픽 인터페이스를 더블 클릭했는데도 COSBrowser 클라이언트가 실행되지 않습니다.

단말에서 `./cosbrowser.AppImage --no-sandbox` 명령어를 실행하여 클라이언트를 실행할 수 있습니다.

### COSBrowser 설치를 위한 시스템 요구 사항은 무엇입니까?

현재 COSBrowser는 데스크톱 버전과 모바일 버전에서 사용할 수 있습니다.

**데스크톱 버전**

- **Windows 요구 사항**: Windows 7 32/64비트 이상 또는 Windows Server 2008 R2 64비트 이상
- **macOS 요구 사항**: macOS 10.13 이상
- **Linux 요구 사항**: 그래픽 인터페이스 및 AppImage 지원 배포


**모바일 버전**

- **Android 요구 사항**: Android 4.4 이상	
- **iOS 요구 사항**: iOS 11 이상

다운로드 주소는 [COSBrowser 다운로드 주소](https://intl.cloud.tencent.com/document/product/436/11366#.E4.B8.8B.E8.BD.BD.E5.9C.B0.E5.9D.80)를 참고하십시오.

### COSBrowser의 파일 동기화 기능은 무엇입니까?

COSBrowser 데스크톱 버전의 **파일 동기화 기능**을 사용하여 로컬 폴더의 지정된 파일을 버킷에 실시간으로 업로드할 수 있습니다. 자세한 지침은 [데스크톱 버전 사용 설명서](https://intl.cloud.tencent.com/document/product/436/32565#.E5.9F.BA.E6.9C.AC.E5.8A.9F.E8.83.BD)의 파일 동기화 기능에 대한 설명을 참고하십시오.

### COSBrowser의 파일 목록에서 모든 파일 썸네일을 한 번에 볼 수 있습니까?

COSBrowser는 현재 모든 파일의 썸네일을 직접 표시할 수 없습니다.

### COSBrowser 모바일 버전의 목록에 3개의 버킷만 표시되는 이유는 무엇입니까?

COSBrowser 모바일 버전의 개요 페이지는 기본적으로 3개의 버킷을 표시합니다. 아래로 스크롤하여 더 많은 버킷을 볼 수 있습니다.

### COSBrowser를 사용하여 스탠다드IA 스토리지 유형에 객체를 직접 업로드할 수 있습니까?

COSBrowser는 기본적으로 스탠다드 스토리지 유형에 객체를 업로드합니다. 객체를 업로드할 때 스토리지 유형 및 액세스 권한을 선택할 수 있습니다.

### 대량 파일의 전송 속도는 어떻게 높입니까?

Windows 버전 COSBrowser 툴을 예로 들면, **고급 설정**으로 이동하여 **업로드**, **다운로드** 파일의 동시 접속 수와 멀티파트 블록 수를 조정하여 전송 속도를 높일 수 있습니다.


### COSBrowser에서 파일 링크를 복사하려면 어떻게 합니까?

다음과 같이 파일 링크를 복사할 수 있습니다.
1. 파일 목록에서 대상 파일을 선택하고 **링크 복사**를 마우스 오른쪽 버튼으로 클릭하여 **사용자 정의 링크 복사** 창을 엽니다.
2. 파일 목록에서 **세부 정보**를 클릭하여 **세부 정보** 창을 열거나 ‘객체 주소’를 직접 복사하거나 ‘임시 링크를 생성’합니다.



>?
>- 파일에 대해 공개 읽기가 활성화된 경우 서명되지 않은 링크, 즉 ‘객체 주소’(영구적으로 유효함)를 사용하여 액세스할 수 있습니다.
>- 파일에 대해 비공개 읽기가 활성화된 경우 서명된 링크를 사용하여 액세스해야 합니다. **링크 복사** 창에서 링크 유효 기간을 사용자 정의할 수 있으며 기본적으로 2시간입니다.


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

![](https://qcloudimg.tencent-cloud.cn/raw/f9853506ab0eed890c74b8ec8b788005.png)

**해결 방법**: 2.1.x 이상의 버전을 다운로드하시기 바랍니다.

### cosbrowser.exe 설치 패키지 실행 중 설치가 중단되면 어떻게 해야 합니까?

**오류 발생 원인**
이는 이전에 COSBrowser를 설치한 적이 있는 경우, 이후 수동으로 애플리케이션을 삭제했지만 시스템에 잔여 파일이 제거되지 않았기 때문입니다. 다시 설치하면 프로그램에서 잔여 파일을 발견하여 실제로 애플리케이션이 없지만 존재하는 것으로 인식해 설치를 중단하여 발생하는 문제입니다.

**해결 방법**
수동으로 제거하거나 기타 정리 툴(예: Tencent 보안 관리자의 소프트웨어 관리)을 사용하여 COSBrowser 애플리케이션 설치 잔여 파일을 삭제합니다.

### COSBrowser에서 파일 목록으로 이동했을 때 DNS 오류가 보고되면 어떻게 해야 하나요?

DNS 오류는 COS 도메인이 로컬 네트워크에서 확인되지 않았음을 나타냅니다. 로컬 DNS 서버 주소를 114.114.114.114와 같은 공용 주소로 변경하고 다시 시도하거나 테스트를 위해 네트워크 환경을 변경하는 것이 좋습니다.
