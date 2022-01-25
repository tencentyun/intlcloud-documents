CSS 콘솔은 주소 생성기 기능을 제공하여, 작성된 주소로 정보를 스티칭하여 사용자가 빠르게 푸시 스트림/재생 주소를 생성하도록 돕습니다. 그중 라이브 방송 주소는 주로 도메인(domain), 애플리케이션 이름(AppName), 스트림 이름(StreamName), 인증 Key로 구성됩니다.
![](https://main.qcloudimg.com/raw/55879651fe2ca61a3699ab4ed9de41d4.jpg)

주소 생성 후 **복사 선택**, **복사 버튼 클릭** 또는 **QR 코드 스캔**의 방식으로 주소 정보를 추출할 수 있습니다.


## 주의 사항
- CSS는 현재 주소 생성 이력 기록 기능을 지원하지 않으므로 주소 생성 후 복사하여 저장하십시오.
- 동시에 여러 라이브 방송 주소를 생성하려면 자체 스티칭 방식으로 생성하는 것을 권장합니다. 자세한 작업 방법은 [라이브 방송 URL 직접 조합](https://intl.cloud.tencent.com/document/product/267/38393) 문서를 참고하십시오.
- CSS에서 기본값으로 테스트 도메인 `xxxx.livepush.myqcloud.com`을 제공하며, 이 도메인을 통해 푸시 스트림을 테스트할 수 있습니다. 단, 정식 비즈니스에서 해당 도메인을 푸시 도메인으로 사용하는 것은 권장하지 않습니다.
- 라이브 방송 주소 QR 코드는 [TCToolkit App](https://intl.cloud.tencent.com/document/product/1071/38147)으로 스캔하여 사용할 수 있습니다.
- 스트림 이름 접미사가 트랜스 코딩 템플릿 ID와 충돌하는 경우, 스트림 상태 오류가 발생할 수 있으니 스트림 이름을 변경하십시오.



##  전제 조건
[CSS 콘솔](https://console.cloud.tencent.com/live/livestat)에 로그인되어 있어야 하며 [푸시 스트림/재생 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가되어 있어야 합니다.

## 매개변수 설정 설명

<table>
<thead><tr><th>매개변수 설정</th><th>설명</th></tr></thead>
<tbody><tr>
<td>생성 유형 및 도메인</td>
<td><strong>푸시 도메인</strong> 또는 <strong>재생 도메인</strong>을 선택할 수 있습니다.</td>
</tr><tr><td>AppName</td>
<td>라이브 방송 애플리케이션 이름으로, 라이브 방송 스트림 미디어 파일의 저장 경로를 구분하는 데 사용되며 기본값은 live입니다. <br>영문 알파벳, 숫자, 기호만 지원됩니다.</td>
</tr><tr><td>StreamName</td>
<td>사용자 정의된 스트림 이름으로, 모든 라이브 방송 스트림의 고유 식별자입니다. <br>영문 알파벳, 숫자, 기호만 지원됩니다.</td>
</tr><tr><td>만료 시간</td>
<td><li>재생 주소 만료 시간은 설정한 타임스탬프와 재생 인증 설정의 유효 시간을 더한 값입니다. <li>푸시 스트림 주소 만료 시간은 즉 설정 시간입니다.</td>
</tr><tr><td>트랜스 코딩 템플릿</td>
<td><li>생성 유형을 <strong>재생 도메인</strong>으로 선택한 경우에만 사용합니다. <li><a href="https://intl.cloud.tencent.com/document/product/267/31071">트랜스 코딩 템플릿</a>을 선택한 경우, 생성한 재생 주소는 트랜스 코딩 후의 라이브 방송 재생 주소가 됩니다. 기존의 라이브 방송 스트림을 재생하는 경우, 트랜스 코딩 템플릿을 선택하여 주소를 생성할 필요가 없습니다.</td>
</tr>
</tbody></table>

[](id:push)
## 푸시 스트림 주소 생성
### 작업 단계
1. CSS 콘솔에 로그인하여 [**주소 생성기**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)를 선택해 주소 생성기로 이동합니다.
2. 생성 유형을 **푸시 도메인**으로 선택하고, 도메인 관리에 추가한 푸시 도메인을 선택합니다.
3. AppName을 입력합니다. 기본값은 live입니다.
4. 스트림 이름 StreamName을 입력합니다. 예시: `liveteststream`.
5. 주소 만료 시간을 선택합니다(예시: `2021-12-15 10:06:22`).
6. **주소 생성**을 클릭합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/68d6cc91bb1092b418f5863f7d91e832.png)

[](id:pushurl)
### 푸시 스트림 주소 설명
푸시 스트림은 RTMP, WebRTC, SRT 프로토콜을 지원하며, 주소 생성기 기능을 통해 접두사가 'rtmp://', 'webrtc://' 및 'srt://'인 푸시 스트림 주소를 생성할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d866991901d2c780112da709d4e0ba3c.png)


[](id:play)
## 재생 주소 생성
### 작업 단계
1. CSS 콘솔에 로그인하여 [**주소 생성기**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)를 선택해 주소 생성기로 이동합니다.
2. 생성 유형을 **재생 도메인**으로 선택하고, 도메인 관리에 추가한 재생 도메인을 선택합니다.
3. AppName을 입력합니다. 기본값은 live입니다.
4. 스트림 이름 StreamName을 입력합니다. 예시: `liveteststream`.
5. 주소 만료 시간을 선택합니다(예시: `2021-12-15 10:20:26`).
6. 기존에 생성한 트랜스 코딩 템플릿을 참고할지 여부를 선택합니다.
6. **주소 생성**을 클릭합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/838b4bc6cf9df0c308f9636b1d7c06af.png)

[](id:playurl)
### 재생 주소 설명
트랜스 코딩 템플릿을 사용하는 경우, 생성된 재생 주소는 트랜스 코딩 후의 라이브 방송 재생 주소가 됩니다. 그 중 재생은 RTMP, FLV, HLS, WebRTC 프로토콜을 지원합니다. 주소 생성기를 통해 접두사가 `rtmp://`, `http://` 및 `webrtc://`인 재생 주소를 생성할 수 있습니다.
>! UDP 프로토콜의 재생 주소는 LEB 주소입니다. [LEB 시작하기](https://intl.cloud.tencent.com/document/product/267/41030)를 통해 사용 방법을 알아보실 수 있습니다. 자세한 LEB 요금은 [가격 리스트](https://intl.cloud.tencent.com/document/product/267/2819)를 참고하십시오.

![](https://qcloudimg.tencent-cloud.cn/raw/345cc01a3d77d6816d1789fe60b7184e.png)
