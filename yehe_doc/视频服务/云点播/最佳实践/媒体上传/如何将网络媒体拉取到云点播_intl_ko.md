## 사용 수칙

### 내용 소개

이 문서는 온라인 동영상(URL 형식으로 제공)을 VOD로 가져오는 방법을 설명합니다.

### 요금

이 문서에 제공된 코드는 오픈 소스이며 무료이지만 사용 중 다음과 같은 비용이 발생할 수 있습니다.

- API 요청 스크립트를 실행하기 위한 Tencent Cloud CVM 인스턴스 구입 요금입니다. 자세한 내용은 [CVM 과금](https://intl.cloud.tencent.com/document/product/213/2180)을 참고하십시오.

- VOD 저장 공간은 풀링을 통해 업로드된 동영상이 차지하게 됩니다. 자세한 내용은 동영상 [스토리지 가격](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.AD.98.E5.82.A8.3Cspan-id.3D.22media_storage.22.3E.3C.2Fspan.3E)을 참고하십시오.


### 제한

VOD에서 제공하는 URL에서 가져오기 기능에는 다음과 같은 제한이 있습니다.

- URL은 동영상 파일을 직접 가리켜야 하지만 동영상 웹사이트 페이지에 대한 링크가 될 수 없습니다.
- URL에 링크 도용 방지를 위한 타임스탬프가 있는 경우 링크 도용 방지 제한(예: 유효 기간 및 허용된 액세스 요청 수)이 적절한지 확인하십시오. 그렇지 않으면 액세스가 실패할 수 있습니다.
- Referer 링크 도용 방지가 활성화된 URL은 지원되지 않습니다.
- DASH(MPD 파일 형식)는 지원되지 않습니다.
- 풀링 대상이 HLS(m3u8 파일 형식) 파일인 경우 미디어 세그먼트의 URI(일반적으로 TS 파일 형식)는 매개변수가 없는 상대 경로여야 합니다.

## 콘솔에서 풀링으로 업로드
<span id="p11"></span>
### 1단계: VOD 활성화

[시작하기 - 1단계](https://intl.cloud.tencent.com/document/product/266/8757)를 참고하여 VOD 서비스를 활성화합니다.
<span id="p12"></span>
### 2단계: 풀링 작업 만들기

VOD 콘솔의 [업로드 페이지](https://console.cloud.tencent.com/vod/media/upload)로 이동하여 업로드 방법으로 [동영상 풀링]을 선택하고 [행 추가]를 클릭하고 가져올 동영상의 URL을 입력합니다(여기에서는 [테스트 URL](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4)이 예로 사용됩니다. 기타 구성 항목은 선택 사항이며, 필요에 따라 입력 가능합니다). 그런 다음 왼쪽 하단 모서리에 있는 [동영상 가져오기]를 클릭합니다.

![](https://main.qcloudimg.com/raw/3871a2c05ca1f26f62e0518cb3943309.png)
>?동영상을 가져오는 데 걸리는 시간은 동영상 파일 크기와 정비례합니다. 긴 대기 시간을 피하기 위해 테스트에 작은 동영상(수십 메가바이트 크기)를 사용하는 것이 좋습니다.
<span id="p13"></span>
### 3단계: 풀링 결과 보기

1 - 2분 동안 기다린 후(동영상 파일 크기에 따라 다름) [미디어 자산 페이지](https://console.cloud.tencent.com/vod/media)에서 가져온 동영상을 볼 수 있습니다.

![](https://main.qcloudimg.com/raw/7329a44db45f6cc11fa48ac41ae9cf7c.png)
>?가져오기 프로세스 중 브라우저가 미디어 자산 페이지에서 멈춘 경우, 가져온 동영상을 보려면 페이지를 새로고침해야 합니다.

## Cloud API 호출하여 풀링 업로드
<span id="p21"></span>
### 1단계: Tencent Cloud CVM 준비

Tencent Cloud API 요청 스크립트는 다음 요구 사항을 충족하는 CVM 인스턴스에서 실행해야 합니다.

- 리전: 랜덤
- 모델: 공식 웹 사이트의 최저 사양(1코어 1Gb).
- 공용 네트워크: 공용 IP를 보유해야 하며 대역폭은 1Mbps 이상.
- 운영 체제: 공식 웹 사이트의 공용 이미지 `Ubuntu Server 16.04.1 LTS 64비트` 또는 `Ubuntu Server 18.04.1 LTS 64비트`.

CVM 구매 방법은 [운영 가이드 - 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하십시오. 시스템 재설치 방법은 [운영 가이드 - 시스템 재설치](https://intl.cloud.tencent.com/document/product/213/4933)를 참고하십시오.

>!상기 조건에 부합하는 Tencent Cloud CVM이 없을 경우, 다른 공인 네트워크의 Linux(예: CentOS, Debian 등) 또는 Mac 디바이스에서도 스크립트를 실행할 수 있으나 운영 체제에 따라 스크립트의 개별 명령을 수정해야 합니다. 자세한 수정 방법은 개발자가 직접 검색하시기 바랍니다.
<span id="p22"></span>
### 2단계: API 키 가져오기

Tencent Cloud API 요청에는 API 키(즉, SecretId 및 SecretKey)가 필요합니다. API 키를 아직 생성하지 않은 경우 [키 문서 생성](https://intl.cloud.tencent.com/document/product/598/34228)에 따라 생성하십시오. 이미 키를 생성한 경우 [키 문서 보기](https://intl.cloud.tencent.com/document/product/598/34228)에 따라 키를 받으십시오.
<span id="p23"></span>
### 3단계: VOD 활성화

[시작하기 - 1단계](https://intl.cloud.tencent.com/document/product/266/8757)를 참고하여 VOD 서비스를 활성화하십시오.
<span id="p24"></span>
### 4단계: 풀링 작업 시작

[1단계](#p21)에서 준비한 CVM(로그인 방식은 [운영 가이드 - Linux 로그인](https://intl.cloud.tencent.com/document/product/213/5436)참고)에 로그인하여, 원격 터미널에 다음 명령어를 입력하고 실행합니다.

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/pull_upload_api.sh
```

>?[2단계](#p22)에서 얻은 값을 명령어의 SECRET_ID와 SECRET_KEY에 할당하십시오.

해당 명령은 Github로부터 Demo 소스 코드를 다운로드하고 설치 스크립트를 자동 실행합니다. 설치 프로세스는 수 분(실제 시간은 CVM 네트워크 상태에 따라 다름)이 소요되며, 원격 터미널에서 다음과 같은 정보를 인쇄합니다.

```
[2020-07-15 17:40:13] pip3 설치 시작.
[2020-07-15 17:40:39]pip3 설치 성공.
[2020-07-15 17:40:39]Python용 Tencent Cloud API SDK 설치 시작.
[2020-07-15 17:40:42]Python용 Tencent Cloud API SDK 설치 완료.
[2020-07-15 17:40:42]API 매개변수 설정 시작.
[2020-07-15 17:40:42]API 파라미터 설정 완료.
```

pull_upload.py 스크립트를 실행하여 업로드를 시작합니다.

```
ubuntu@VM-69-2-ubuntu:~$ cd ~/vod-server-demo/pull_upload_api/; python3 pull_upload.py http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4 API-PullUpload
```

>?명령의 URL을 가져올 동영상의 실제 주소로 바꾸십시오.

이 명령은 지정된 URL에 대한 [PullUpload](https://intl.cloud.tencent.com/document/product/266/34118) 요청을 시작하고 다음과 유사한 응답을 출력합니다.

```
{"TaskId": "1400329073-PullUpload-4ea60158fc6f8e611bbfa750eb1fd0a9t0", "RequestId": "4e821b4a-9a29-409f-99cb-b703fa184e50"}
```
<span id="p25"></span>
### 5단계: 풀링 결과 보기

1 - 2분 동안 기다린 후(동영상 파일 크기에 따라 다름) [미디어 자산 페이지](https://console.cloud.tencent.com/vod/media)에서 가져온 동영상을 볼 수 있습니다.

![](https://main.qcloudimg.com/raw/b5d62be7e0f70654483513a6885ff65b.png)
> ?가져오기 프로세스 중에 브라우저가 미디어 자산 페이지에서 멈춘 경우, 가져온 동영상을 보려면 페이지를 새로고침해야 합니다.
