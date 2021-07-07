<style>
.markdown-text-box table th,.markdown-text-box table td{text-align: center;}
.inbuttom{height: 30px;width: 150px;min-width: 24px;padding: 0 20px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;vertical-align: middle;white-space: nowrap;}
</style>

## Native Demo
<table>
<tr>
<th>iOS</th><th>Android</th><th>Windows</th><th >Mac OS</th>
</tr>
<tr>
<td><img style="width:150px" src="https://main.qcloudimg.com/raw/a1a6fd4a9bc3ad2b5fe60e31202c8fda.png" data-nonescope="true"></td>
<td><a onclick="window.open('https://dldir1.qq.com/hudongzhibo/liteav/TRTCDemo.apk')"><button style="width:150px;height: 150px;border:none;background-image:url(https://main.qcloudimg.com/raw/8a603ced0a61983018c794df842f7029.png);background-size: cover;">
</button></a></td>
<td><a onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Win_Demo.exe')"><button style="width:150px;height: 150px;border:none;background-image:url(https://main.qcloudimg.com/raw/e80b8f4462e2904b31dcdcaabe71c484.png);background-size: cover;">
</button></a></td>
<td><a onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Mac_Demo.tar.bz2')"><button style="width:150px;height: 150px;border:none;background-image:url(https://main.qcloudimg.com/raw/e80b8f4462e2904b31dcdcaabe71c484.png);background-size: cover;">
</button></a></td>
</tr>
</table>


## 크로스 플랫폼 Demo
<table>
<tr>
<td>
<input type="button" value="영상 통화" class="inbuttom" onclick="window.open('https://web.sdk.qcloud.com/trtc/webrtc/demo/latest/official-demo/index.html')" /><br><br>
<input type="button" value="ILVB" class="inbuttom" onclick="window.open('https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html')" />
</td>
<td>
<a onclick="window.open('https://www.pgyer.com/KP03')" value="Flutter_ios_버전">
	<button style="width:150px;height: 83px;border:none;background-image:url(https://main.qcloudimg.com/raw/6d4d839ef8050cd3839b86f98bd7c35f.png);background-size: cover;">
</button>
</a>
<br>
<a onclick="window.open('https://comm.qq.com/im_demo_download/trtc_flutter_demo.apk')" value="Flutter_android_버전"> 
	<button style="width:150px;height: 83px;border:none;background-image:url(https://main.qcloudimg.com/raw/f53741b9ad7567c475841e68cc65dbc3.png);background-size: cover;">
</button>
</a></td>
<td>
<input type="button" value="Windows 버전" class="inbuttom"  onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education/TRTC_Education_Demo%20Setup%201.1.0.exe')" /><br><br>
<input type="button" value="MacOS 버전" class="inbuttom" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education/TRTC_Education_Demo-1.1.0.dmg')" /></td>
</tr>
</table>





## 영상 통화 시나리오
일대일 또는 그룹 영상 통화로 720P, 1080P 고화질을 지원합니다. 단일 방은 최대 300명 동시 접속, 최대 50명 동시 카메라 활성화를 지원합니다. 주요 응용 시나리오에는 일대일 영상 통화, 300명 화상 회의, 온라인 진료, 화상 채팅, 화상 고객서비스, 화상 면접 심사, 영상 녹음 및 녹화, 마피아 게임 등이 있습니다.
<dx-tabs>
::: iOS&Android

<table>
<tr>
   <th>액티브 콜</th>
   <th>콜 수신</th>
 </tr>
<tr>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/group-call.gif"/></td>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/group-recv.gif"/></td>
</tr>
</table>
:::
::: Flutter\s(iOS/Android)
![](https://imgcache.qq.com/operation/dianshi/other/8d81a52d-ffd3-4bbd-bd09-1a1648569b2d.453825bf12c01b9fe937ca8d7291f3c44b48cced.gif)
:::
::: Windows
![](https://imgcache.qq.com/operation/dianshi/other/win.836bd473a766ea962d0b40117888e99aad5db6c8.gif)
:::
::: macOS
![](https://imgcache.qq.com/operation/dianshi/other/macOS.cd7d6d7e8a7fcc388ec27e41c6952b8615ce9d34.gif)
:::
::: 데스크톱 브라우저
![](https://imgcache.qq.com/operation/dianshi/other/058ffcf5-60f0-430c-96c7-e1760b93e444.fdd0f2c10a8242dadbf99108a48a59124124b437.gif)

<table>
<tr><th>액티브 콜</th><th>콜 수신</th> </tr>
<tr>
<td><img src="https://webim-1252463788.cos.ap-shanghai.myqcloud.com/trtc-calling-doc-assets/videocall.gif"/></td>
<td><img src="https://webim-1252463788.cos.ap-shanghai.myqcloud.com/trtc-calling-doc-assets/videoaccept.gif"/></td>
</tr>
</table>

:::
</dx-tabs>

## 음성 통화 시나리오
일대일 또는 그룹 음성 통화로 48kHz 및 듀얼 사운드 채널을 지원합니다. 단일 방은 최대 300명 동시 접속, 최대 50명 동시 마이크 활성화를 지원합니다. 주요 응용 시나리오에는 일대일 음성 통화, 그룹 음성 통화, 음성 채팅, 음성 회의, 음성 고객서비스, 마피아 게임 등이 있습니다.
<dx-tabs>
::: iOS&Android

<table>
<tr>
   <th>액티브 콜</th>
   <th>콜 수신</th>
 </tr>
<tr>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/call.gif"/></td>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/recv.gif"/></td>
</tr>
</table>

## 비디오 ILVB 시나리오
비디오 ILVB 시나리오는 호스트와 시청자의 비디오 마이크 연결 인터랙션을 지원합니다. 호스트의 크로스 룸(라이브 룸 사이) PK를 지원하며, 원활한 마이크 On/Off 지원으로 대기 시간 없이 전환되며 호스트 딜레이 시간은 300ms 미만입니다. 단일 방의 마이크 연결 인원 수는 무제한이며, 최대 50명 동시 마이크 연결을 지원합니다. 저딜레이 라이브 방송 모드에서 시청자 10만 명의 동시 재생을 지원하며, 재생 딜레이 시간은 1000ms 미만입니다. CDN 릴레이 라이브 방송 모드에서는 시청자 인원 수의 제한이 없습니다. 주요 응용 시나리오에는 비디오 저딜레이 라이브 방송, 10만 명 인터랙션 수업, 비디오 라이브 방송 PK, 비디오 소개팅 방, 인터랙션 수업, 원격 트레이닝, 대형 회의 등이 있습니다.
<dx-tabs>
::: iOS&Android
<table>
<tr>
<td><img width="260" height="561" src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/beauty.gif"/></td>
<td><img width="260" height="561" src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/join.gif"/></td>
<td><img width="260" height="561" src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/msg.gif"/></td>
<td><img width="260" height="561" src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/pk.gif"/></td>
</tr>
</table>
:::
::: 데스크톱 브라우저
![](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/doc-assets/demo-official-website.gif)
:::
</dx-tabs>

## 음성 ILVB 시나리오
음성 ILVB 시나리오는 호스트와 시청자의 비디오 마이크 연결 인터랙션을 지원합니다. 호스트의 크로스 룸(라이브 룸 사이) PK를 지원하며, 원활한 마이크 On/Off 지원으로 대기 시간 없이 전환되며 호스트 딜레이 시간은 300ms 미만입니다. 단일 방의 마이크 연결 인원 수는 무제한이며, 최대 50명 동시 마이크 연결을 지원합니다. 저딜레이 라이브 방송 모드에서 시청자 10만 명의 동시 재생을 지원하며, 재생 딜레이 시간은 1000ms 미만입니다. CDN 릴레이 라이브 방송 모드에서는 시청자 인원 수의 제한이 없습니다. 주요 응용 시나리오에는 음성 저딜레이 라이브 방송, 음성 라이브 방송 마이크 연결, 음성 라이브 방송 PK, 음성 채팅방, 음성 소개팅 방, 노래방, FM 방송국 등이 있습니다.
<table>
     <tr>
         <th>호스트 마이크 위치 작업</th>  
         <th>시청자 마이크 위치 작업</th>  
     </tr>
<tr>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/voiceroom_pick_seat.gif"/></td>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/voiceroom_enter_seat.gif"/></td>
</tr>
</table>


## 화상 회의 시나리오
화상 회의 시나리오는 1080p 고화질 및 48kHz 고음질을 지원합니다. 멀티미디어 딜레이 시간은 300ms 미만으로 끊김 없는 고화질 회의가 가능합니다. 화면 및 파일 공유를 지원하여 회의의 효율을 높이며, IM 결합으로 텍스트나 이미지 등 다양한 형식으로 토론을 지원하여 원활한 회의를 구현합니다. 주요 응용 시나리오에는 옴니미디어 고객서비스, 온라인 회의, 정부와 기업의 라이브 방송 등이 있습니다.
<table>
     <tr>
         <th>회의 입장</th>  
         <th>화면 공유</th>  
     </tr>
<tr>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/enterroom.gif"/></td>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/enterroom.gif"/></td>
</tr>
</table>

## 인터랙션 시나리오
인터랙션 수업 시나리오는 선생님과 학생의 인터랙션 마이크 연결을 지원하며, 최대 50명이 동시에 마이크를 연결할 수 있습니다. 원활한 마이크 On/Off 지원으로 대기 시간 없이 전환되며 소통 시 딜레이 시간은 300ms 미만입니다. 저딜레이 라이브 방송 모드에서 10만 명의 학생이 동시에 시청할 수 있으며, 이때 딜레이 시간은 1000ms 미만입니다. CDN 릴레이 라이브 방송에서는 시청자 인원 수의 제한이 없습니다. 화면 공유, 인터랙션 화이트보드, 녹화 방송 등 다양한 기능을 수업에 응용하여 보다 다양한 온라인 수업을 실현할 수 있습니다. 주요 비즈니스 시나리오로 대규모 인원 수업, 소수 인원 수업, 극소수 인원 수업, AI 수업, 학생 모집 수업, 내부 트레이닝 라이브 방송 수업, 일대일 온라인 교육 등이 있습니다.
<table>
     <tr>
         <th>선생님(Electron)</th>  
         <th>학생(Electron)</th>  
     </tr>
<tr>
<td><img src="https://imgcache.qq.com/operation/dianshi/other/Electron_teacher.76058b065f0b01ccc5d6bfd058c6b655e69a149c.gif"/></td>
<td><img src="https://imgcache.qq.com/operation/dianshi/other/Electron_stu.9e3f55291b657d94878963ad86471b331190f47c.gif"/></td>
</tr>
</table>
