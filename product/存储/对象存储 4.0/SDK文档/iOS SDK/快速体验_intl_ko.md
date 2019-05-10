## 소개

모든 도구 및 Demo는 [Github 저장소](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/OOTB-XML)에 있습니다.

본 문서는 사용자 그룹 서버 및 사용자 클라이언트 두 부분을 차례로 소개합니다.

## 사용자 서버 구축
이 예시에서 응용프로그램은 임시 키 기능만 제공합니다. cos\_signer\_lite는 flask 서비스 프레임워크를 기반으로 하는 임시 키 서비스입니다. 해당 프로젝트는 python3으로 작성되어 자체 클라이언트 또는 가상 서버에서 해당 Python 프로젝트를 운행하며, COS 터미널 (Android/iOS)SDK에 임시 키 서비스를 제공합니다.
>!해당 프로젝트는 예시에만 사용되며, 직접 생산 환경에 사용해서는 안 됩니다. 생산 환경에서는 COS 서버 SDK의 임시 키 API를 사용할 수 있습니다.

### 환경 구성

cossign는 현재 Python3만 지원하며, 임시 키 서비스를 제공할 수 있습니다. 직접 pip 명령을 사용하여 설치할 수 있습니다.
```
pip3 install cossign
```

### 서비스 시동
설치 완료 후, 다음 명령을 실행하여 임시 키 서비스를 시동할 수 있습니다.
```
cossign --secret_id your_secret_id --secret_key your_secret_key --port 5000
```
>?포트 기본값은 5000이며, 명령 실행 시 포트 번호를 지정하지 않아도 됩니다.
>키 정보는 [Cloud API 키 콘솔](https://console.cloud.tencent.com/cam/capi)에서 조회할 수 있습니다.


### 테스트 서비스
브라우저를 통해 `http://your_server_ip:5000/sign` 링크에 접근하거나 아래 명령을 실행하여 테스트할 수 있습니다.
```
curl http://your_server_ip:5000/sign
```    
다음 정보가 반환되면 서비스가 성공적으로 실행된 것입니다.
```
{
 "code":0,
 "message":"",
 "codeDesc":"Success",
 "data":{
  "credentials":{
   "sessionToken":"634aa09dccc3274045ba413ec081c1df64007f0a30001",
   "tmpSecretId":"AKIDwxHZGTUvXAfcbLaOedJUQuwBXWUXG4m3",
   "tmpSecretKey":"kriDdZsOuuF9zrZPlSAVVG0Sg4RXZu6M"},
  "expiredTime":1530515889}
 }
```

### 문제 해결 가이드
임시 키 구축 과정에서 오류가 발생하면 다음 가이드를 참조하여 문제를 해결하십시오.
1.  **문제: **설치 명령 `pip3 install flask` 실행 시 `comment not found pip3`가 표시됩니다.    
**분석: **Python 3를 설치하지 않았거나 Python 3를 설치했지만 path 설정이 정확하지 않기 때문입니다.
**해결 방안: **시스템에 따라 해당하는 Python3 설치 방법을 찾아 설치하거나 path 설정을 확인하십시오.

2. **문제: **서비스 실행을 시작한 이후, 임시 키 획득 시 `URLError: urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed` 오류가 표시됩니다.
**해결 방안: **해당 문제는 MAC OS X 시스템에서 일반적으로 발생하며, certifi 모듈을 설치하면 됩니다. 구체적인 조작 방법은 [Stack Overflow FAQ](https://stackoverflow.com/questions/27835619/urllib-and-ssl-certificate-verify-failed-error/42334357#42334357)를 참조하십시오.

## 사용자 클라이언트 구축
### 클라이언트 구성
QCloudCOSXMLDemo/QCloudCOSXMLDemo/TestCommonDefine.h 파일을 수정하고, APPID 및 앞에 배포된 임시 키를 획득할 수 있는 주소를 입력한 후 다음 명령을 실행하십시오.
```
pod install
```
명령을 실행한 후 QCloudCOSXMLDemo.xcworkspace를 열면 바로 Demo를 체험할 수 있습니다.
### 예시 Demo 실행
#### Bucket 리스트 조회 및 Bucket 생성
1, 예시 App 시동 후, 다음 그림과 같이 현재 사용 가능한 모든 Region이 표시됩니다.    
![choose region](https://main.qcloudimg.com/raw/c7cdd4171e7ab4314299df399954942c.png)

2, 해당 Region에 대응하도록 선택하여 들어가면 다음 그림과 같이 현재 계정이 해당 Region의 모든 Bucket이 표시됩니다.  
![bucket](https://main.qcloudimg.com/raw/9dae084c02f2e19cc6682588cada1e28.png)

이 인터페이스에서 오른쪽 상단 코너의 Bucket 생성 버튼을 클릭하여 현재 Region에서 다음 그림과 같이 Bucket을 생성할 수 있습니다. 
![](https://main.qcloudimg.com/raw/fefd8a545c2a0924d3d60722b8d2affb.png)


#### 파일 업로드
제일 아래의 버튼 [앨범]>[업로드]>[일시 중지]>[전송 재개]> [취소]를 클릭하여 다음 그림과 같이 업로드 테스트를 진행할 수 있습니다. 
![](https://main.qcloudimg.com/raw/7050892158c428a9c5470eb472680844.png)

#### 파일 다운로드
다운로드 인터페이스에 들어가면 현재 Bucket에 있는 모든 파일이 표시됩니다. [다운로드]를 클릭하여 다음 그림과 같이 다운로드 테스트를 진행할 수 있습니다.
![](https://main.qcloudimg.com/raw/25fc6b09c7b6f3da7f1a427ecabb4ecb.png)

