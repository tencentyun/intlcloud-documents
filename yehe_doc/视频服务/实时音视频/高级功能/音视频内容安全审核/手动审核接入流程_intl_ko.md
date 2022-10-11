본 문서는 특정 방에 대한 콘텐츠 조정을 구현 방법을 소개합니다. 이를 위해서는 조정 작업을 수동으로 시작하고 종료해야 합니다. 
## 조정 실행 과정
### 액세스 워크플로
![](https://qcloudimg.tencent-cloud.cn/raw/af96d1a900603c441fce5cde5c972ec9.jpg)

### 액세스 단계
1. TRTC SDK로 방을 생성하면 애플리케이션 ID(sdk_app_id)와 방 ID(room_id)를 얻을 수 있습니다. 사용자 ID(user_id)를 생성하면 조정 시스템이 방에 들어가 조정을 위해 라이브 콘텐츠를 가져올 수 있습니다. 각 방에 대한 콘텐츠 조정을 위해 각각 다른 user_id를 생성하는 것이 좋습니다. user_id 외에도 중재 시스템에 대한 서명(user_sig)도 받을 수 있습니다.
2. 이전 단계에서 얻은 sdk_app_id, room_id, user_id 및 user_sig를 사용하여 조정 URL을 다음 형식으로 연결합니다.[](id:step2)
```
trtc://trtc.tencentcloudapi.com/moderation?sdk_app_id=xxxx&room_id=xxxx&user_id=xxxx&user_sig=xxxx
```
>! 
>- 특수 문자로 인한 구문 분석 실패를 방지하려면 URL, 특히 user_sig를 스플라이싱하기 전에 매개변수 값을 escape하십시오.
>- 본 문서에서 언급된 매개변수 sdk_app_id, user_id, user_sig 및 room_id는 TRTC SDK와 함께 사용하는 SdkAppId, UserId, UserSig 및 RoomId에 해당합니다.
<table>
<thead><tr><th>매개변수 dlfma</th><th>필수</th><th>설명</th></tr></thead>
<tbody><tr>
<td>sdk_app_id</td>
<td>Yes</td>
<td>TRTC 콘솔에서 애플리케이션을 생성 시 할당되는 ID입니다.</td>
</tr><tr>
<td>room_id</td>
<td>Yes</td>
<td>방이 생성 시 할당되는 room_id입니다. 이 매개변수의 데이터 유형은 문자열 또는 숫자(기본값)일 수 있습니다. 문자열 형식의 room_id를 사용하려면 room_id_type을 string으로 설정하십시오.</td>
</tr><tr>
<td>user_id</td>
<td>Yes</td>
<td>조정 시스템에서 방에 들어가 데이터를 가져오는 데 사용하는 사용자 ID입니다. 방마다 다른 user_id를 생성하는 것이 좋습니다.</td>
</tr><tr>
<td>user_sig</td>
<td>Yes</td>
<td>sdk_app_id 및 user_id를 기반으로 생성된 보안 서명입니다.</td>
</tr><tr>
<td>mix</td>
<td>No</td>
<td>true로 설정하면 조정 이전에 방의 스트림이 먼저 믹싱됩니다. false인 경우 방의 스트림은 별도로 검토됩니다.<br>단일 스트림 조정을 사용하면 스트림에 비준수 콘텐츠가 포함된 특정 사용자(user_id)를 조정 콜백에서 가져올 수 있습니다. 혼합 스트림 조정에서는 이 작업을 수행할 수 없습니다.</td>
</tr><tr>
<td>room_id_type</td>
<td>No</td>
<td>방 ID 매개변수의 데이터 유형입니다. 유효 값: string/number.</td>
</tr></tbody></table>

3. [CreateAudioModerationTask](https://intl.cloud.tencent.com/document/product/1139/46101) API를 호출하여 방에 대한 콘텐츠 조정 작업을 시작합니다.
<table>
<thead><tr><th>매개변수 이름</th><th>필수</th><th>유형</th><th>설명</th></tr></thead>
<tbody><tr>
<td>Action</td>
<td>Yes</td>
<td>String</td>
<td>공용 매개변수입니다. 이 API의 경우 값은 CreateAudioModerationTask입니다.</td>
</tr><tr>
<td>Version</td>
<td>Yes</td>
<td>String</td>
<td>공용 매개변수입니다. 이 API의 경우 값은 2020-12-29입니다.</td>
</tr><tr>
<td>Region</td>
<td>No</td>
<td>String</td>
<td>공용 매개변수입니다. 중국 본토 이외의 리전을 지정하는 데 사용됩니다. 현재 싱가포르(ap-singapore)만 지원됩니다.</td>
</tr><tr>
<td>Tasks.N</td>
<td>Yes</td>
<td>Array of <a href="https://intl.cloud.tencent.com/document/product/1139/46098">TaskInput</a></td>
<td>오디오 조정 작업에 대한 정보입니다. 자세한 내용은 TaskInput 설명을 참고하십시오. <br>참고: 최대 <strong>10개의 작업</strong>을 생성할 수 있습니다.</td>
</tr><tr>
<td>BizType</td>
<td>No</td>
<td>String</td>
<td>CMS 콘솔에서 구성된 조정 정책의 ID입니다. 특정 조정 정책을 사용하려면 이 매개변수를 지정하십시오. 이 Biztype 매개변수를 전달하지 않으면(비워둠) 기본 조정 정책이 사용됩니다.<br>참고: Biztype은 3자-32자 길이이며 숫자, 문자 및 언더바를 포함할 수 있습니다. 다른 Biztype 값은 다른 비즈니스 시나리오와 연결됩니다. 올바른 Biztype을 사용하고 있는지 확인하십시오.</td>
</tr><tr>
<td>Type</td>
<td>No</td>
<td>String</td>
<td>조정할 오디오 유형입니다. 유효 값:<b>AUDIO</b>(VOD 오디오) 및 <b>LIVE_AUDIO</b>(라이브 오디오). 기본값은 AUDIO입니다.</td>
</tr><tr>
<td>Seed</td>
<td>No</td>
<td>String</td>
<td>데이터 보안을 보장하는 콜백 서명 키입니다. HTTP 응답 헤더에 X-Signature 필드를 추가합니다. 필드 값은 Hex로 표시되는 seed + body의 SHA256 해시입니다. 콜백을 받은 후 <b>sha256(seed + body)</b>을 사용하여 검증을 위한 <code>X-Signature</code>를 계산합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1139/46091">Signature v3</a>을 참고하십시오.</td></tr>
<tr>
<td>CallbackUrl</td>
<td>No</td>
<td>String</td>
<td>조정 결과를 받을 주소입니다. 기본 형식은 URL입니다. 구성 후 감지된 비호환 오디오 세그먼트의 정보가 이 주소로 전송됩니다. 콜백 형식은 <a href="https://intl.cloud.tencent.com/document/product/1139/46101#.E7.A4.BA.E4.BE.8B2-.E5.9B.9E.E8.B0.83.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B">Sample callback signature</a>를 참고하십시오.</td></tr>
</tbody></table>


위 단계에서 CreateAudioModerationTask API가 호출되어 오디오 조정 작업을 생성합니다. 비디오 조정 작업을 시작하려면 [CreateVideoModerationTask](#appendix)를 호출하십시오.
	다음에 주의하십시오.

   - **BizType**
      CMS 콘솔의 [정책 관리](https://chttps://console.intl.cloud.tencent.com/cms/video/strategy)에서 다양한 조정 정책을 생성할 수 있습니다. CMS를 활성화하면 BizType이 ‘default’인 정책이 자동으로 생성됩니다. 테스트를 위해 이 값을 전달할 수 있습니다.
      ![](https://qcloudimg.tencent-cloud.cn/raw/46e0ce41f8f49998e93b2ff0d5f79849.png)
   - **Type**
      TRTC 애플리케이션의 시나리오에 따라 이 매개변수를 설정하십시오. 예를 들어 음성 채팅방의 경우 ams(Audio Moderation System)의 API를 사용하며, 이 매개 변수 Type은 LIVE_AUDIO로 설정해야 합니다. 비디오 채팅의 경우 vm(Video Moderation System)의 API를 사용하며, 이 매개 변수 Type은 LIVE_VIDEO로 설정해야 합니다.
   - **CallbackUrl**
      이 주소는 라이브 스트림 중 또는 이후에 조정 결과의 콜백을 수신하는 데 사용됩니다. 콘솔에서 이 주소를 구성하거나 API에 전달할 수 있습니다. 콜백 형식은 [DescribeTaskDetail](https://intl.cloud.tencent.com/document/product/1139/46100)의 응답 매개변수를 참고하십시오.
   - **Tasks.N.Input.Url**
      [2단계](#step2)에서 스플라이싱한 조정 URL을 전달합니다.
      ![](https://qcloudimg.tencent-cloud.cn/raw/64bc723804a0d30610870bb034701084.png)
4. 조정 작업이 성공적으로 생성되면 고유한 작업 ID(TaskId)가 반환됩니다.
5. 조정 프로세스 동안 조정 시스템은 방에 있는 각 사용자의 오디오 세그먼트와 비디오 스크린샷을 검토하고 결과를 계속해서 콜백 서버로 전송합니다. 결과에 따라 방을 차단할지 경고를 보낼지 결정할 수 있습니다.
6. 라이브 스트림이 종료되면 API를 호출(TaskId 전달)하여 조정 작업을 종료해야 합니다.
7. 조정 종료 요청을 받은 후 조정 시스템은 방에서 데이터 가져오기를 중지하고 최종 조정 결과를 생성하며 조정 종료를 나타내는 콜백을 보냅니다. 식별된 비준수 오디오/비디오 세그먼트는 cos에 저장되고 다음과 같이 이름이 지정됩니다.
```
trtc/{{sdk_app_id}}/screenshot_{{room_id}}_{{user_id}}{{timestamp}}.jpg(이미지 형식)
trtc/{{sdk_app_id}}/audio{{room_id}}_{{user_id}}_{{timestamp}}.mp3(오디오 형식)
```
>!
>-  **혼합 스트림 조정 모드에서 user_id는 mixer입니다**.
>- 조정 프로세스 중에 스트림이 중단되거나 방에서 데이터를 가져오지 못하는 경우 조정 시스템이 다시 시도합니다. 일정 시간(오류 코드에 따라 다름) 후에도 데이터를 풀링하지 못하면 라이브 스트림이 종료된 것으로 간주되고 조정 시스템에서 조정이 중지되었음을 알리는 콜백을 보냅니다. 이 콜백을 받은 후 방의 스트림을 계속 조정하려면 다른 조정 작업을 시작할 수 있습니다.

## FAQ

### 1. 조정 시스템 user_id가 방의 다른 사용자에게 표시됩니까?
아니요. 조정을 위해 데이터를 가져오기 위해 조정 시스템이 TRTC 방에 시청자로 입장합니다. 조정 시스템은 방의 다른 사용자에게 표시되지 않습니다.

### 2. TRTC에서 데이터를 풀링하면 요금이 발생합니까?

조정 시스템은 시청자로 TRTC 방에 들어가 데이터를 풀링하므로 TRTC의 과금 방식이 적용됩니다. 요금은 구독(풀링)된 오디오/비디오의 지속 시간을 기준으로 합니다. 자세한 내용은 [TRTC 기본 서비스 과금](https://intl.cloud.tencent.com/document/product/647/42734)을 참고하십시오.
>!
>- 조정 시스템의 user_id는 회의실의 다른 user_id와 동일할 수 없습니다.
>- room_id는 uint이고 값 범위는 1 - 4294967295입니다. 방 ID를 할당하고 유지 관리해야 합니다.

### 3. 조정 시스템은 조정 데이터를 가져오기 위해 시청자로 TRTC 방에 입장합니다. 다른 사용자를 생성할 때와 같은 방식으로 사용자를 생성해야 합니까?
예. 조정 시스템이 데이터를 가져오기 위해 TRTC 방에 들어갈 때 방의 다른 사용자와 동일한 것으로 간주됩니다.

### 4. 오디오 및 비디오 조정은 일반적으로 각각 얼마나 걸립니까?
비준수 오디오/비디오 세그먼트는 즉시 반환됩니다. 오디오 조정의 RTF는 0.2이며 이미지 인식 결과는 데이터 도착 후 1s 이내에 반환됩니다.

### 5. user_sig는 무엇입니까?
자세한 내용은 [user_sig 관련](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

### 6. TRTC에서 생성된 user_sig가 정확한지 어떻게 검사합니까? 방 입장 시 -3319, -3320 오류가 보고되었는데 어떻게 해결합니까?

TRTC 콘솔에 로그인하여 **개발 지원** > **[user_sig 생성&인증](https://console.cloud.tencent.com/trtc/user_sigtool)**을 선택해 user_sig를 인증합니다.

### 7. 멀티 스트림이 있는 오디오 채팅방에서 비준수 콘텐츠가 포함된 스트림을 어떻게 알 수 있습니까?

비준수 오디오/비디오 세그먼트는 cos에 저장되고 이름은 `trtc_[room_id]_[user_id]_timestamp` 형식입니다. 세그먼트의 cos 주소에서 세그먼트가 속한 사용자를 알 수 있습니다.

### 8. 조정 URL을 연결할 때 주의해야 할 사항이 있습니까?
user_sig에는 특수 문자가 포함될 수 있으므로 url에 포함하기 전에 먼저 escape 처리해야 합니다.

>?더 많은 질문은[기능 관련 FAQ](https://intl.cloud.tencent.com/document/product/647/36057)를 참고하십시오.

[](id:appendix)

## 부록
- **오디오 조정**을 위해 다음 네 가지 API를 사용해야 할 수 있습니다.
     - [CreateAudioModerationTask](https://intl.cloud.tencent.com/document/product/1139/46101 )
     - [CancelTask](https://intl.cloud.tencent.com/document/product/1139/46097)
     - [DescribeTasks](https://intl.cloud.tencent.com/document/product/1139/46096) 
     - [DescribeTaskDetail](https://intl.cloud.tencent.com/document/product/1139/46100)
- **비디오 조정**을 위해 다음 네 가지 API를 사용해야 할 수 있습니다.
     - [CreateVideoModerationTask](https://intl.cloud.tencent.com/document/product/1140/46113)
     - [CancelTask](https://intl.cloud.tencent.com/document/product/1140/46114)
     - [DescribeTasks](https://intl.cloud.tencent.com/document/product/1140/46111)
     - [DescribeTaskDetail](https://intl.cloud.tencent.com/document/product/1140/46112)
