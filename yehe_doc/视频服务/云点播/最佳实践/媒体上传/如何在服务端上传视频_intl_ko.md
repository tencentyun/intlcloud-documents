## 사용 수칙

### 내용 소개

본문은 로컬 서버에 있는 동영상 파일을 VOD에 업로드하는 방법을 설명합니다.

### 요금

본문에서 제공된 코드는 오픈 소스이며 무료이지만 사용 중 다음과 같은 비용이 발생할 수 있습니다.

- 업로드 스크립트를 실행하기 위한 Tencent Cloud CVM 인스턴스 구입 요금입니다. 자세한 내용은 [CVM 과금](https://intl.cloud.tencent.com/document/product/213/2180)을 참고하십시오.
- 업로드된 동영상이 차지하는 VOD 스토리지 공간입니다. 자세한 내용은 [스토리지 가격](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.AD.98.E5.82.A8.3Cspan-id.3D.22media_storage.22.3E.3C.2Fspan.3E)을 참고하십시오.

## CVM 동영상을 VOD에 업로드
<span id="p1"></span>
### 1단계: CVM 인스턴스 준비

업로드 스크립트는 다음 요건에 부합하는 Tencent Cloud CVM에서 실행되어 야 합니다.

- 리전: 랜덤
- 모델: 공식 웹 사이트의 최저 사양(1코어 1GB).
- 공용 네트워크: 공용 IP를 보유해야 하며 대역폭은 1Mbps 이상.
- 운영 체제: 공식 웹 사이트의 공용 이미지 `Ubuntu Server 16.04.1 LTS 64비트` 또는 `Ubuntu Server 18.04.1 LTS 64비트`.

CVM 구매 방법은 [운영 가이드 - 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하십시오. 시스템 재설치 방법은 [운영 가이드 - 시스템 재설치](https://intl.cloud.tencent.com/document/product/213/4933)를 참고하십시오.

>!위 조건에 부합하는 Tencent Cloud CVM이 없을 경우, 다른 공인 네트워크의 Linux(예: CentOS, Debian 등) 또는 Mac 디바이스에서도 스크립트를 실행할 수 있으나 운영 체제에 따라 스크립트의 개별 명령을 수정해야 합니다. 자세한 수정 방법은 개발자가 직접 검색하시기 바랍니다.
<span id="p2"></span>
### 2단계: VOD 활성화

[시작하기 - 1단계](https://intl.cloud.tencent.com/document/product/266/8757)를 참고하여 VOD 서비스를 활성화하십시오.
<span id="p3"></span>
### 3단계: API 키 가져오기

동영상 업로드에는 API 키 (예: SecretId 및 SecretKey)가 필요합니다. API 키를 아직 생성하지 않은 경우 [키 문서 생성](https://intl.cloud.tencent.com/document/product/598/34228)에 따라 생성하십시오. 이미 키를 생성한 경우 동일한 [키 문서 보기](https://intl.cloud.tencent.com/document/product/598/34228)에 따라 키를 받으십시오.
<span id=“p4”></span>
### 4단계: 코드 다운로드 및 SDK 설치

[1단계](#p1)에서 준비한 CVM(로그인 방식은 [운영 가이드 - Linux 로그인](https://intl.cloud.tencent.com/document/product/213/5436)참고)에 로그인하여, 원격 터미널에 다음 명령어를 입력하고 실행합니다.

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/server_upload.sh
```

>?[3단계](#p3)에서 얻은 해당 값을 명령어의 SECRET_ID와 SECRET_KEY에 할당하십시오.

해당 명령은 Github로부터 Demo 소스 코드를 다운로드하고 설치 스크립트를 자동 실행합니다. 설치 프로세스는 수 분(실제 시간은 CVM 네트워크 조건에 따라 다름)이 소요되며, 그 동안 원격 터미널은 다음과 같은 유사한 정보를 출력합니다.

```
[2020-06-23 19:56:31] pip3 설치 시작.
[2020-06-23 19:56:34]pip3 설치 성공.
[2020-06-23 19:56:34]Python용 VOD 업로드 SDK 설치 시작.
[2020-06-23 19:56:36]Python용 VOD 업로드 SDK 설치 완료.
[2020-06-23 19:56:36]SDK 매개변수 설정 시작.
[2020-06-23 19:56:36]SDK 파라미터 설정 완료.
```
<span id="p5"></span>
### 5단계: 동영상 업로드

업로드를 시작하기 전에 CVM 인스턴스에서 동영상 파일과 커버 이미지(선택 사항)를 준비해야 합니다. CVM 인스턴스에 동영상을 업로드하는 것이 불편한 경우, 원격 터미널에서 다음 명령을 실행하여 테스트 동영상과 커버를 CVM에 다운로드합니다.

```
ubuntu@VM-69-2-ubuntu:~$ wget http://1400329073.vod2.myqcloud.com/d62d88a7vodtranscq1400329073/7a9b2b565285890804459281865/v.f100010.mp4 -O ~/vod-server-demo/server_upload/tencent_cloud.mp4; wget http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/8aa658d15285890804459940822/5285890804459940825.jpg -O ~/vod-server-demo/server_upload/tencent_cloud.jpg
```

`server.upload.py` 스크립트를 실행하여 업로드를 시작합니다.

```
ubuntu@VM-69-2-ubuntu:~$ cd ~/vod-server-demo/server_upload/; python3 server_upload.py ./tencent_cloud.mp4 ./tencent_cloud.jpg
```

>?명령어에 있는 영상과 커버 이미지의 경로를 실제 파일 경로로 교체하십시오. 여기에서 커버 이미지 경로 매개변수는 선택 사항이며 비워두면 업로드된 동영상에 커버가 없습니다.

이 명령은 tencent_cloud.mp4 동영상을 VOD에 업로드하고 tencent_cloud.jpg 이미지를 커버로 업로드합니다. 업로드가 완료되면 원격 터미널은 다음과 유사한 정보를 인쇄합니다.

```
{"CoverUrl": "http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/8aa658d15285890804459940822/5285890804459940825.jpg", "FileId": "5285890804459940822", "MediaUrl": "http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/8aa658d15285890804459940822/f0.mp4", "RequestId": "84a7fb42-9f05-4acd-9cc8-843690b188ce"}
```

>?자신의 동영상을 테스트용으로 사용하려면 CVM 대역폭이 부족하여 업로드에 너무 많은 시간이 소요되지 않도록 작은 동영상 파일(몇 MB 크기)을 사용하는 것이 좋습니다.
<span id="p6"></span>
### 6단계: 결과 보기

콘솔의 [비디오 관리](https://console.cloud.tencent.com/vod/media) 페이지에서 업로드된 동영상 파일과 커버를 보실 수 있습니다.

## 코드 해석

1. `main()`은 스크립트 항목입니다.
2. `parse_conf_file()`을 호출하고 `config.json` 파일에서 구성 정보를 읽습니다. 구성 항목은 다음과 같습니다.
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
<td>procedure</td>
<td>String</td>
<td>태스크 플로우 이름입니다. 동영상 업로드 완료 후 지정된 태스크 플로우가 자동으로 트리거됩니다. 기본적으로 비어 있습니다.</td>
</tr>
<tr>
<td>subappid</td>
<td>String</td>
<td>동영상을 <a href="https://intl.cloud.tencent.com/document/product/266/33987" target="_blank">VOD 서브 애플리케이션</a>에 업로드할지 여부</td>
</tr>
</tbody></table>

	>?이 Demo는 `procedure` 및 `subappid`의 두 가지 업로드 매개변수만 지원합니다. 전체 기능은 [Python용 SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)를 참고하십시오.
3. 명령 라인 매개변수에서 업로드할 동영상 파일의 로컬 경로와 커버 이미지의 경로(있는 경우)를 가져오고 `upload_media()`를 호출하여 업로드를 시작합니다.
```
       if len(sys.argv) < 2:
           usage()
           return
       video_path = sys.argv[1]
       cover_path = sys.argv[2] if len(sys.argv) > 2 else ""
   
       # 업로드 시작
       rsp = upload_media(configuration, video_path, cover_path)
   ```
4. `upload_media()`에서 Python용 SDK에서 제공하는 메소드를 사용하여 업로드 인스턴스 `client`를 설정하고, `req`에서 업로드 매개변수를 설정한 후 업로드를 시작합니다.
   ```
           client = VodUploadClient(conf["secret_id"], conf["secret_key"])
           req = VodUploadRequest()
   
           req.MediaFilePath = video
           if cover != "":
               req.CoverFilePath = cover
           if conf["procedure"] != "":
               req.Procedure = conf["procedure"]
           req.SubAppId = int(conf["subappid"])
   
           rsp = client.upload("ap-guangzhou", req)
           return rsp
   ```
>!`client.upload()`의 첫 번째 매개변수(`"ap-guangzhou"`)는 업로드된 동영상의 스토리지 리전이 아니라 업로드 인스턴스의 액세스 리전입니다. 매개변수 값을 `"ap-guangzhou"`로 간단히 고정할 수 있습니다. 업로드된 동영상의 스토리지 리전을 지정하려면 `req.StorageRegion` 매개변수를 설정하십시오.

## 기타 기능

서버에서 VOD SDK는 동영상 이름, 카테고리, 만료 시간 설정과 같은 기타 업로드 기능을 지원합니다. 자세한 내용은 해당 프로그래밍 언어에 대한 SDK 개발 가이드를 참고하십시오.

- [Java](https://intl.cloud.tencent.com/document/product/266/33914)
- [C#](https://intl.cloud.tencent.com/document/product/266/33915)
- [PHP](https://intl.cloud.tencent.com/document/product/266/33916)
- [Python](https://intl.cloud.tencent.com/document/product/266/33917)
- [Node.js](https://intl.cloud.tencent.com/document/product/266/33918)
- [Golang](https://intl.cloud.tencent.com/document/product/266/33919)

