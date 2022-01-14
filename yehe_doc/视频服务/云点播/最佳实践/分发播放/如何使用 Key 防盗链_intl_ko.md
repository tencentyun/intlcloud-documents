

## 사용 수칙

### Demo 기능 소개
본 Demo에서는 개발자에게 콘솔에서의 Key 링크 도용 방지 활성화, 링크 도용 방지 서명 배포 서비스 구축 및 링크 도용 방지 서명을 사용한 비디오 재생을 포함한 VOD [Key 링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33986) 메커니즘의 사용 방법을 제시합니다.

### 아키텍처와 프로세스

Demo는 클라이언트에서 전송한 링크 도용 방지 서명 획득 요청을 수신하기 위해 SCF를 기반으로 HTTP 서비스를 구축합니다. 서비스는 요청 Body에서 VOD의 비디오 원본 URL을 가져와 링크 도용 방지 서명을 계산하고 링크 도용 방지 서명이 있는 URL을 클라이언트에게 반환합니다.

시스템은 크게 개발자, API 게이트웨이, SCF 및 VOD의 네 가지 요소로 구성되어 있으며, 그중 API 게이트웨이와 SCF는 다음 이미지와 같이 본 Demo에서 배포하는 객체입니다.
<img src="https://main.qcloudimg.com/raw/f30d9b832b388c9ffe35551ef26743b4.png" width="600">

자세한 서비스 프로세스는 다음과 같습니다.

1. 개발자가 VOD 콘솔에서 비디오의 원본 URL(실제 생성 환경에서는 플레이어에서 서비스 백그라운드로 비디오를 요청하는 URL이어야 하나, 본 문서에서는 프로세스를 단순화하기 위해 개발자가 해당 비즈니스 동작을 시뮬레이션 함)을 가져옵니다.
2. 개발자가 비디오의 원본 URL을 사용해 SCF에 링크 도용 방지 서명을 요청합니다.
3. 개발자가 링크 도용 방지 서명이 있는 비디오 URL을 사용해 VOD CDN을 요청하고 비디오를 재생합니다.

>? Demo의 SCF 코드는 Python3.6을 기반으로 개발되었습니다. 또한 SCF는 Python2.7, Node.js, Golang, PHP, Java 등 여러 프로그래밍 언어를 지원하며, 개발자가 상황에 따라 자유롭게 선택할 수 있습니다. 자세한 내용은 [SCF 개발 가이드](https://intl.cloud.tencent.com/document/product/583/11061)를 참고하십시오.

### 요금
본 문서에서 제공되는 VOD Key 링크 도용 방지 서명 배포 서비스 Demo는 무료 오픈 소스이나, 구축 및 사용 과정에서 다음과 같은 비용이 발생할 수 있습니다.

- 서비스 배포 스크립트 실행을 위해 Tencent Cloud CVM 구매 시 비용이 발생합니다. 자세한 내용은 [CVM 과금](https://intl.cloud.tencent.com/document/product/213/2180)을 참고하십시오.
- Tencent Cloud SCF를 사용하여 서명 배포 서비스 제공 시 비용이 발생합니다. 자세한 내용은 [SCF 과금](https://intl.cloud.tencent.com/document/product/583/12284) 과 [SCF 무료 한도](https://intl.cloud.tencent.com/document/product/583/12282)를 참고하십시오.
- Tencent Cloud API 게이트웨이를 사용하여 SCF에 공인 네트워크 인터페이스를 제공 시 비용이 발생합니다. 자세한 내용은 [API 게이트웨이 과금](https://intl.cloud.tencent.com/document/product/628/11771)을 참고하십시오.
- 업로드된 동영상이 차지하는 VOD 저장 공간입니다.

## Key 링크 도용 방지 서명 배포 서비스의 빠른 배포

<span id="p1"></span>
### 1단계: CVM 인스턴스 준비

배포 스크립트는 다음 요건에 부합하는 Tencent Cloud CVM에서 실행되어 야 합니다.

- 리전: 랜덤
- 모델: 공식 웹 사이트의 최저 사양(1코어 1Gb).
- 공용 네트워크: 공용 IP를 보유해야 하며 대역폭은 1Mbps 이상.
- 운영 체제: 공식 웹 사이트의 공용 이미지 `Ubuntu Server 16.04.1 LTS 64비트` 또는 `Ubuntu Server 18.04.1 LTS 64비트`.

CVM 구매 방법은 [운영 가이드 - 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하십시오. 시스템 재설치 방법은 [운영 가이드 - 시스템 재설치](https://intl.cloud.tencent.com/document/product/213/4933)를 참고하십시오.

>!
>- Key 링크 도용 방지 서명 배포 서비스 Demo 자체는 CVM에 의존하지 않고, 배포 스크립트 실행에만 CVM을 사용합니다.
>- 위 조건에 부합하는 Tencent Cloud CVM이 없을 경우, 다른 공인 네트워크의 Linux(예: CentOS, Debian 등) 또는 Mac 디바이스에서도 배포 스크립트를 실행할 수 있으나 운영 체제에 따라 스크립트의 개별 명령을 수정해야 합니다. 자세한 수정 방법은 개발자가 직접 검색하시기 바랍니다.

<span id="p2"></span>
### 2단계: VOD 활성화 및 주요 링크 도용 방지 구성

1. [시작하기 - 1단계](https://intl.cloud.tencent.com/document/product/266/8757)를 참고하여 VOD 서비스를 활성화합니다.
2. 활성화 후 [링크 도용 방지 설정](https://intl.cloud.tencent.com/document/product/266/14060) 문서를 참고하여 Key 링크 도용 방지를 활성하고 링크 도용 방지 Key를 기록합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c43642ea12afda47aff5ca5205f63f4f.png)
>!여기에서는 Referer 링크 도용 방지가 아닌 Key 링크 도용 방지를 활성화합니다. Referer 링크 도용 방지를 동시에 활성화했을 경우, 다음 테스트 방법이 Referer 링크 도용 방지의 요건에 부합하지 않아 요청이 실패할 수 있습니다.

<span id="p3"></span>

### 3단계: API 키 및 APPID 가져오기

Key 링크 도용 방지 서명 배포 서비스 Demo의 배포 및 실행을 위해 개발자의 API 키(SecretId와 SecretKey)와 APPID를 사용해야 합니다.

- 아직 API 키를 생성하지 않았다면 [보안키 생성 파일](https://intl.cloud.tencent.com/document/product/598/34228)을 참고하여 새로운 API 키를 생성하십시오. 이미 키를 생성했다면 [보안키 조회 파일](https://intl.cloud.tencent.com/document/product/598/34228)을 참고하여 API 키를 가져옵니다.
- 다음 이미지와 같이 콘솔의 [계정 정보](https://console.cloud.tencent.com/developer) 페이지에서 APPID를 조회할 수 있습니다.
  ![](https://main.qcloudimg.com/raw/6c9fe4238232392c8d914f9ebf0f53aa.png)

### 4단계: 링크 도용 방지 서명 배포 서비스 배포

[1단계에서 준비된 CVM](#p1)(로그인 방식은 [운영 가이드 - Linux 로그인](https://intl.cloud.tencent.com/document/product/213/5436)참고)에 로그인하여, 원격 터미널에 다음 명령어를 입력하고 실행합니다.

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;export APPID=125xxxxxxx;export ANTI_LEECH_KEY=xxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/anti_leech_sign_scf.sh
```

>?명령 중 SECRET_ID, SECRET_KEY와 APPID를 [3단계](#p3)에서 가져온 내용에 할당하고, ANTI_LEECH_KEY를 [2단계](#p2)에서 가져온 링크 도용 방지 Key에 할당합니다.

해당 명령은 Github로부터 Demo 소스 코드를 다운로드하고 설치 스크립트를 자동 실행합니다. 설치 프로세스는 수 분(실제 시간은 CVM 네트워크 상태에 따라 다름)이 소요되며, 원격 터미널에서 다음과 같은 정보를 인쇄합니다.

```
[2020-06-04 15:57:10] pip3 설치 시작.
[2020-06-04 15:57:18]pip3 설치 성공.
[2020-06-04 15:57:18]Tencent Cloud SCF 툴 설치 시작.
[2020-06-04 15:57:19]scf 설치 성공.
[2020-06-04 15:57:19]scf 구성 시작.
[2020-06-04 15:57:20]scf 구성 완료.
[2020-06-04 15:57:20]VOD Key 링크 도용 방지 서명 배포 서비스 구성 시작.
[2020-06-04 15:57:30]VOD Key 링크 도용 방지 서명 배포 서비스 구성 완료.
[2020-06-04 15:57:32]서비스 주소: https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/anti_leech_sign
```

출력 로그에 서명 배포 서비스의 주소(예: `https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/anti_leech_sign`)를 복사합니다.

> !출력 로그에 다음과 같은 경고가 표시되는 경우는 일반적으로 CVM가 방금 배포된 서비스 도메인을 즉시 분석할 수 없기 때문으로, 해당 경고를 무시할 수 있습니다.
> ```
> [2020-04-25 17:18:44]경고: Key 링크 도용 방지 서명 배포 서비스 테스트에 실패했습니다.
> ```

### 5단계: Key 링크 도용 방지 테스트

[비디오 업로드 - 로컬 업로드 단계](https://intl.cloud.tencent.com/document/product/266/33890)의 설명에 따라 테스트 비디오 하나를 VOD에 업로드합니다. 업로드가 완료되면 [빠른 조회]를 클릭하고 오른쪽의 [주소 복사]를 클릭하여 해당 비디오의 URL을 복사합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ac27b65a2bb0cc91ac9f71b141a31cb2.png)
CVM 명령 줄에서 `curl` 명령을 실행하여 해당 URL에 직접 액세스를 시도해 보십시오. Key 링크 도용 방지 규칙에 부합하지 않을 경우, 서버가 액세스를 거부하며 HTTP 반환 코드는 403입니다(다음과 같이 테스트 시 명령의 URL을 실제 URL로 바꿉니다).

```
ubuntu@VM-69-2-ubuntu:~$ curl -I "http://125xxxxxxx.vod2.myqcloud.com/f888c998vodcq125xxxxxxx/c849148f528xxxxxxxxxxxxxxxx/xxxxxxxxxx.mp4"
HTTP/1.1 403 Forbidden
Server: NWS_VP
Connection: keep-alive
Date: Thu, 04 Jun 2020 08:27:54 GMT
Content-Type: text/plain
Content-Length: 14
```
CVM 명령 줄에서 `curl` 명령을 실행하여 4단계에서 배포한 서비스를 요청하고 링크 도용 방지 서명이 있는 URL을 가져옵니다(`-d`는 POST 방식을 사용하여 요청을 시작하는 것을 의미하며, 비디오 URL 매개변수를 가지고 있습니다).
```
ubuntu@VM-69-2-ubuntu:~$ curl -d 'http://125xxxxxxx.vod2.myqcloud.com/f888c998vodcq125xxxxxxx/c849148f528xxxxxxxxxxxxxxxx/xxxxxxxxxx.mp4' https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/anti_leech_sign; echo
http://125xxxxxxx.vod2.myqcloud.com/f888c998vodcq125xxxxxxx/c849148f528xxxxxxxxxxxxxxxx/xxxxxxxxxx.mp4?t=5ed8b8d2&exper=0&rlimit=0&us=455041&sign=fe6394007c2e7aef39fc70a02e897f69
```
curl 명령을 다시 실행하여 이전 단계에서 얻은 링크 도용 방지 서명을 가지고 있는 URL에 액세스하면 정상적으로 액세스할 수 있습니다(HTTP 반환 코드는 200).
```
ubuntu@VM-69-2-ubuntu:~$ curl -I "http://125xxxxxxx.vod2.myqcloud.com/f888c998vodcq125xxxxxxx/c849148f528xxxxxxxxxxxxxxxx/xxxxxxxxxx.mp4?t=5ed8b8d2&exper=0&rlimit=0&us=455041&sign=fe6394007c2e7aef39fc70a02e897f69"
HTTP/1.1 200 OK
Server: tencent-cos
Connection: keep-alive
Date: Thu, 04 Jun 2020 08:37:17 GMT
Last-Modified: Fri, 22 May 2020 15:06:15 GMT
Content-Type: video/mp4
Content-Length: 232952632
Accept-Ranges: bytes
ETag: "1da6be3a0d1da5edae4ff0b1feff02cf-223"
x-cos-hash-crc64ecma: 16209801220610226954
x-cos-request-id: NWVkOGIyYmVfZDUyMzYyNjRfYWMwMF85YjkyNzA=
X-Daa-Tunnel: hop_count=4
X-NWS-LOG-UUID: b404f43e-3c86-4c54-8a78-fb78e4e85cf2 add71e19fb08c6d9dbe1b21a2fb157bf
Access-Control-Allow-Credentials: true
Access-Control-Allow-Headers: Origin,No-Cache,X-Requested-With,If-Modified-Since,Pragma,Last-Modified,Cache-Control,Expires,Content-Type,X_Requested_With,Range
Access-Control-Allow-Methods: GET,POST,OPTIONS
Access-Control-Allow-Origin: *
```
>?브라우저에서 링크 도용 방지 서명이 있는 URL에 액세스할 수 있으며, 비디오 재생을 통해 링크 도용 방지 서명을 확인할 수 있습니다. 그러나 이러한 방식은 비디오 포맷에 대한 요구 사항이 있습니다. 일반적으로 호환성이 높은 H.264로 인코딩한 MP4 파일 사용을 권장합니다. 또는 Postman 등의 3rd party 툴을 사용하여 HTTP 요청을 전송할 수도 있습니다. 자세한 사용 방법은 직접 검색해 보시기 바랍니다. 

## 시스템 설계 설명

### 인터페이스 프로토콜

Key 링크 도용 방지 서명 배포 SCF는 API 게이트웨이를 통해 인터페이스를 제공하며, 자세한 인터페이스 프로토콜은 다음과 같습니다.

| 서비스               | SCF 이름        | 인터페이스 형식  | 요청 내용     | 반환 내용         |
| ------------------ | --------------- | --------- | ------------ | ---------------- |
| Key 링크 도용 방지 서명 배포 | anti_leech_sign | HTTP POST | 비디오 원본 URL | 링크 도용 방지 서명 URL |

### 서명 배포 서비스 코드 해석

1. `Main_handler()`는 엔트리 함수입니다.
2. `parse_conf_file ()`을 호출하고, `config.json` 파일에서 설정 정보를 읽어옵니다. 설정 항목에 대한 설명은 다음과 같습니다(자세한 매개변수는 [Key 링크 도용 방지 서명 매개변수](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)를 참고하십시오).
<table>
<thead>
<tr>
<th>필드</th>
<th>데이터 유형</th>
<th>기능</th>
</tr>
</thead>
<tbody>
<tr>
<td>key</td>
<td>String</td>
<td>Key 링크 도용 방지 키</td>
</tr>
<tr>
<td>t</td>
<td>Integer</td>
  <td>서명 유효 시간으로, 단위는 초입니다. 요청 처리 시, 해당 매개변수와 SCF 서버의 현재 시간을 더하면 링크 도용 방지 매개변수의 t가 됩니다.</td>
</tr>
<tr>
<td>exper</td>
<td>Integer</td>
<td>미리보기 시간</td>
</tr>
<tr>
<td>rlimit</td>
<td>Integer</td>
<td>서명에 액세스 할 수 있는 최대 클라이언트 IP 수</td>
</tr>
</tbody></table>
3. 요청 Body에서 `Dir` 매개변수를 분석하여, 로컬에서 `t`와 `us` 매개변수를 생성하고, 구성 파일에서 `exper`와 `rlimit` 매개변수를 읽어옵니다.
```
       original_url = event["body"]
       parse_result = urlparse(original_url)
       directory = path.split(parse_result.path)[0] + '/'
       # 서명 매개변수
       timestamp = int(time.time())
       rand = random.randint(0, 999999)
       sign_para = {
           "t": hex(timestamp + configuration['t'])[2:],
           "exper": configuration['exper'],
           "rlimit": configuration['rlimit'],
           "us": rand
       }	
```
4. `Generate_sign()`를 호출하여 링크 도용 방지 서명을 계산합니다. 자세한 알고리즘은 [Key 링크 도용 방지 서명](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)을 참고하십시오.
5. QueryString을 생성하고, 원본 URL 뒤에 연결하여 링크 도용 방지 서명이 있는 URL을 구성합니다.
```
       sign_para["sign"] = signature
       query_string = urlencode(sign_para)
       new_parse_result = parse_result._replace(query=query_string)
       signed_url = urlunparse(new_parse_result)
```
6. 서명을 반환합니다. 반환된 데이터 포맷 및 의미는 [SCF 통합 응답](https://intl.cloud.tencent.com/document/product/583/12513)을 참고하십시오.
```
       return {
           "isBase64Encoded": False,
           "statusCode": 200,
           "headers": {"Content-Type": "text/plain; charset=utf-8",
                       "Access-Control-Allow-Origin": "*",
                       "Access-Control-Allow-Methods": "POST,OPTIONS"},
           "body": signed_url
       }
```

   
