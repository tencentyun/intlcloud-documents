## 사용 수칙

### Demo 기능 소개

본문은 동영상 업로드 및 트랜스코딩 프로세스를 예로 VOD의 [이벤트 알림 메커니즘](https://intl.cloud.tencent.com/document/product/266/33948) 사용 방법을 설명합니다.

### 아키텍처와 프로세스

HTTP 서비스는 Demo의 SCF를 기반으로 구축되어 VOD에서 이벤트 알림 요청을 수신합니다. NewFileUpload([비디오 업로드 완료 알림](https://intl.cloud.tencent.com/document/product/266/33950)) 및 ProcedureStateChanged([태스크 플로우 상태 변경](https://intl.cloud.tencent.com/document/product/266/33953)) 이벤트 알림을 처리하여 동영상 트랜스코딩을 시작하고 트랜스코딩 결과를 가져옵니다.

시스템은 주로 콘솔, API 게이트웨이, SCF 및 VOD의 네 가지 구성 요소로 구성됩니다. 여기에서 API Gateway 및 SCF는 아래와 같이 이 Demo의 배포 객체입니다.
<img src="https://main.qcloudimg.com/raw/faad90288240a98d34071ad5845aeb76.png" width="550">

자세한 서비스 프로세스는 다음과 같습니다.

1. 콘솔에서 VOD에 동영상을 업로드합니다.
2. VOD 백엔드는 Demo에 대한 NewFileUpload 이벤트 알림 요청을 시작합니다.
3. Demo는 이벤트 알림 콘텐츠를 구문 분석하고 VOD의 [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) API를 호출하여 100010 및 100020 [사전 설정 트랜스코딩 템플릿](https://intl.cloud.tencent.com/document/product/266/33932)으로 업로드된 동영상에 대한 트랜스코딩을 시작합니다.
4. 트랜스코딩 작업을 완료한 후 VOD는 Demo에 대한 ProcedureStateChanged 이벤트 알림 요청을 시작합니다.
5. Demo는 이벤트 알림 콘텐츠를 구문 분석하고 트랜스코딩 출력 파일의 URL을 SCF 로그에 인쇄합니다.

> ?Demo의 SCF 코드는 Python3.6을 기반으로 개발되었습니다. 또한 SCF는 Python2.7, Node.js, Golang, PHP, Java 등 여러 프로그래밍 언어를 지원하며, 개발자가 상황에 따라 자유롭게 선택할 수 있습니다. 자세한 내용은 [SCF 개발 가이드](https://intl.cloud.tencent.com/document/product/583/11061)를 참고하십시오.

### 요금

본 문서에서 제공하는 VOD 이벤트 알림 수신 서비스 Demo는 오픈소스로 무료로 제공되지만 서비스 구축 및 사용 시 다음과 같은 비용이 발생할 수 있습니다.

- 서비스 배포 스크립트 실행을 위해 Tencent Cloud CVM 구매 시 비용이 발생합니다. 자세한 내용은 [CVM 과금](https://intl.cloud.tencent.com/document/product/213/2180)을 참고하십시오.
- SCF에서 제공하는 서명 배포 서비스 이용 요금입니다. 자세한 내용은 [SCF 과금](https://intl.cloud.tencent.com/document/product/583/12284) 과 [SCF 무료 한도](https://intl.cloud.tencent.com/document/product/583/12282)를 참고하십시오.
- Tencent Cloud API 게이트웨이를 사용하여 SCF에 공인 네트워크 인터페이스를 제공 시 비용이 발생합니다. 자세한 내용은 [API 게이트웨이 과금](https://intl.cloud.tencent.com/document/product/628/11771)을 참고하십시오.
- 업로드된 동영상이 차지한 VOD 저장 공간입니다. 자세한 내용은 [스토리지 가격](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.AD.98.E5.82.A8.3Cspan-id.3D.22media_storage.22.3E.3C.2Fspan.3E)을 참고하십시오.
- 동영상 VOD 트랜스코딩 시간입니다. 자세한 내용은 [트랜스코딩 가격](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.A4.84.E7.90.86.3Cspan-id.3D.22media_edit.22.3E.3C.2Fspan.3E)을 참고하십시오.

<span id="p0"></span>
### 프로덕션 환경 영향 방지

이벤트 알림 수신 서비스 Demo의 비즈니스 로직은 VOD 이벤트 알림 메커니즘을 사용합니다. 따라서 배포하는 동안 이벤트 알림 주소를 설정해야 합니다. 계정에 이미 VOD 기반 프로덕션 환경이 있는 경우 이벤트 알림 주소를 변경하면 비즈니스 예외가 발생할 수 있습니다. **운영하기 전에 이것이 프로덕션 환경에 영향을 미치지 않는지 확인하십시오. 확실하지 않은 경우 새 계정을 사용하여 Demo를 배포하십시오**.

## 이벤트 알림 수신 서비스의 빠른 배포
<span id="p1"></span>
### 1단계: CVM 인스턴스 준비

배포 스크립트는 다음 요건에 부합하는 Tencent Cloud CVM에서 실행되어 야 합니다.

- 리전: 랜덤
- 모델: 공식 웹 사이트의 최저 사양(1코어 1GB).
- 공용 네트워크: 공용 IP를 보유해야 하며 대역폭은 1Mbps 이상.
- 운영 체제: 공식 웹 사이트의 공용 이미지 `Ubuntu Server 16.04.1 LTS 64비트` 또는 `Ubuntu Server 18.04.1 LTS 64비트`.

CVM 구매 방법은 [운영 가이드 - 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하십시오. 시스템 재설치 방법은 [운영 가이드 - 시스템 재설치](https://intl.cloud.tencent.com/document/product/213/4933)를 참고하십시오.

>!
>- 이벤트 알림 수신 서비스 Demo 자체는 CVM에 의존하지 않고 CVM을 사용하여 배포 스크립트를 실행합니다.
>- 위 조건에 부합하는 Tencent Cloud CVM이 없을 경우, 다른 공인 네트워크의 Linux(예: CentOS, Debian 등) 또는 Mac 디바이스에서도 배포 스크립트를 실행할 수 있으나 운영 체제에 따라 스크립트의 개별 명령을 수정해야 합니다. 자세한 수정 방법은 개발자가 직접 검색하시기 바랍니다.
<span id="p2"></span>
### 2단계: VOD 활성화

[시작하기 - 1단계](https://intl.cloud.tencent.com/document/product/266/8757)를 참고하여 VOD 서비스를 활성화합니다.
<span id="p3"></span>
### 3단계: API 키 및 APPID 가져오기

이벤트 알림 수신 서비스 Demo의 배포 및 실행을 위해 개발자의 API 키(SecretId와 SecretKey)와 APPID를 사용해야 합니다.

- 아직 API 키를 생성하지 않았다면 [보안키 생성 파일](https://intl.cloud.tencent.com/document/product/598/34228)을 참고하여 새로운 API 키를 생성하십시오. 이미 키를 생성했다면 [보안키 조회 파일](https://intl.cloud.tencent.com/document/product/598/34228)을 참고하여 API 키를 가져옵니다.
- 다음 이미지와 같이 콘솔의 [계정 정보](https://console.cloud.tencent.com/developer) 페이지에서 APPID를 조회할 수 있습니다.
  ![](https://main.qcloudimg.com/raw/6c9fe4238232392c8d914f9ebf0f53aa.png)
<span id=“p4”></span>
### 4단계: 이벤트 알림 수신 서비스 배포

[1단계에서 준비된 CVM](#p1)(로그인 방식은 [운영 가이드 - Linux 로그인](https://intl.cloud.tencent.com/document/product/213/5436)참고)에 로그인하여, 원격 터미널에 다음 명령어를 입력하고 실행합니다.

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;export APPID=125xxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/callback_scf.sh
```

>?명령에서 SECRET_ID, SECRET_KEY, APPID에 [3단계](#p3)에서 얻은 값을 할당합니다.

해당 명령은 Github로부터 Demo 소스 코드를 다운로드하고 설치 스크립트를 자동 실행합니다. 설치 프로세스는 수 분(실제 시간은 CVM 네트워크 상태에 따라 다름)이 소요되며, 원격 터미널에서 다음과 같은 정보를 인쇄합니다.

```
[2020-06-05 17:16:08] pip3 설치 시작.
[2020-06-05 17:16:12]pip3 설치 성공.
[2020-06-05 17:16:12]Tencent Cloud SCF 툴 설치 시작.
[2020-06-05 17:16:13]scf 설치 성공.
[2020-06-05 17:16:13]scf 구성 시작.
[2020-06-05 17:16:14]scf 구성 완료.
[2020-06-05 17:16:14]VOD의 이벤트 알림 수신 서비스 배포 시작.
[2020-06-05 17:16:24]VOD의 이벤트 알림 수신 서비스 배포 완료.
[2020-06-05 17:16:26]서비스 주소: https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/callback
```

출력 로그에서 이벤트 알림 수신 서비스의 주소(예: `https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/callback`)를 복사합니다.

> !출력 로그에 다음과 같은 경고가 표시되는 경우는 일반적으로 CVM가 방금 배포된 서비스 도메인을 즉시 분석할 수 없기 때문으로, 해당 경고를 무시할 수 있습니다.
> ```
> [2020-04-25 17:18:44]경고: 이벤트 알림 수신 서비스 테스트 실패.
> ```

### 5단계: 이벤트 알림 주소 구성

[프로덕션 환경에 영향을 주지 않기](#p0)에 설명된 대로 다음 작업을 수행하기 전에 프로덕션 환경에서 비즈니스가 VOD 이벤트 알림에 의존하지 않는지 확인하십시오.

[VOD 콘솔](https://console.cloud.tencent.com/vod/callback)에 로그인하여 설정을 클릭하고 콜백 모드로 [일반 콜백]을 선택하고, 콜백 URL로 [4단계](#p4)에서 얻은 이벤트 알림 수신 서비스 주소를 입력하고, 모든 콜백 이벤트를 확인하고 아래와 같이 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/4664c0b6d1991eb136fde116881d7467.png)
>!두 개의 콜백 URL 설정 항목(v2.0 형식과 v3.0 형식)이 콘솔에 동시에 표시되는 경우 v3.0 형식으로 설정하십시오.

### 6단계: Demo 테스트

[비디오 업로드 - 로컬 업로드](https://intl.cloud.tencent.com/document/product/266/33890)에 따라 테스트 동영상을 VOD에 업로드합니다. 업로드하는 동안 기본 옵션인 [업로드 후 처리 안 함]을 선택합니다. 업로드가 완료된 후 ‘업로드됨’ 탭에서 동영상 상태가 ‘처리 중’임을 확인할 수 있습니다. 이는 Demo가 NewFileUpload 이벤트 알림을 수신하고 트랜스코딩 요청을 시작했음을 나타냅니다.


비디오 처리가 완료될 때까지 기다렸다가(‘정상’ 상태로 표시됨) [빠른 보기]를 클릭하면 페이지 오른쪽에 업로드된 동영상에 대한 출력 동영상이 두 개 있는 것을 볼 수 있습니다.

[SCF 콘솔 로그 페이지](https://console.cloud.tencent.com/scf/list-detail?rid=1&ns=vod_demo&id=callback&menu=log)에 로그인하고 입력하여 SCF 로그를 확인합니다. 최신 로그에서 두 개의 출력 파일의 URL이 인쇄된 것을 볼 수 있습니다. 실제 사용 사례에서 SCF를 사용하여 데이터베이스에 URL을 기록하거나 다른 채널을 통해 시청자에게 게시할 수 있습니다.
>?SCF 로그 생성은 특정 지연이 있을 수 있습니다. 페이지에 로그가 표시되지 않으면 1 - 2분 동안 기다렸다가 [재설정]을 클릭하여 새로고침하십시오.
<span id="design"></span>
## 시스템 설계 설명

### 인터페이스 프로토콜

이벤트 알림 수신 기능은 API Gateway를 사용하여 API를 제공합니다. 특정 API 프로토콜에 대해서는 [비디오 업로드 완료](https://intl.cloud.tencent.com/document/product/266/33950) 및 [태스크 플로우 상태 변경](https://intl.cloud.tencent.com/document/product/266/33953)을 참고하십시오.

### 이벤트 알림 수신 서비스 코드 해석

1. `Main_handler()`는 엔트리 함수입니다.
2. ‘parse_conf_file()’을 호출하고 ‘config.json’ 파일에서 설정 정보를 읽습니다. 설정 항목은 다음과 같습니다.
<table>
<thead>
<tr>
<th>필드</th>
<th>데이터 유형</th>
<th>기능</th>
</tr>
</thead>
<tbody><tr>
<td>secret_id</td>
<td>String</td>
<td>API 키</td>
</tr>
<tr>
<td>secret_key</td>
<td>String</td>
<td>API 키</td>
</tr>
<tr>
<td>region</td>
<td>String</td>
<td>Tencent Cloud API 요청 리전. VOD에 임의 리전 입력.</td>
</tr>
<tr>
<td>definitions</td>
<td>Array of Integer</td>
<td>트랜스코딩 템플릿</td>
</tr>
<tr>
<td>subappid</td>
<td>Integer</td>
<td>이벤트 알림 출처가 <a href="https://intl.cloud.tencent.com/document/product/266/33987" target="_blank">VOD 서브 애플리케이션</a>인지의 여부</td>
</tr>
</tbody></table>
3. NewFileUpload 이벤트 알림의 경우 ‘deal_new_file_event()’를 호출하여 요청을 구문 분석하고 새로 업로드된 동영상의 FileId를 가져옵니다.
```
           if event_type == "NewFileUpload":
               fileid = deal_new_file_event(body)
               if fileid is None:
                   return ERR_RETURN
```
4. ‘trans_media()’를 호출하여 트랜스코딩을 시작하고 Tencent Cloud API의 응답 패킷을 SCF 로그로 출력하고 응답 패킷을 VOD의 이벤트 알림 서비스로 보냅니다.
```
               rsp = trans_media(configuration, fileid)
               if rsp is None:
                   return ERR_RETURN
               print(rsp)
```
5. ‘trans_media()’에서 Tencent Cloud API SDK를 호출하여 ‘ProcessMedia’ 요청을 시작합니다.
```
        cred = credential.Credential(conf["secret_id"], conf["secret_key"])
        client = vod_client.VodClient(cred, conf["region"])

        method = getattr(models, API_NAME + "Request")
        req = method()
        req.from_json_string(json.dumps(params))

        method = getattr(client, API_NAME)
        rsp = method(req)
        return rsp
```
6. ProcedureStateChanged 이벤트 알림의 경우, ‘deal_procedure_event()’를 호출하여 트랜스코딩 출력 동영상 URL을 가져오고 SCF 로그에 인쇄하라는 요청을 구문 분석합니다.
```
           elif event_type == "ProcedureStateChanged":
               rsp = deal_procedure_event(body)
               if rsp is None:
                   return ERR_RETURN
```

   
