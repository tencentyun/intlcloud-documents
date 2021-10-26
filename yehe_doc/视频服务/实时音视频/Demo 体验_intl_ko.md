<style>
.markdown-text-box table th,.markdown-text-box table td{text-align: center;}
.inbuttom{height: 30px;width: 150px;min-width: 24px;padding: 0 20px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;vertical-align: middle;white-space: nowrap;}
</style>


## Native Demo
<table>
<tr>
<th>iOS&Android</th><th>Windows</th><th >Mac OS</th>
</tr>
<tr>
<td><img style="width:150px;" src="https://main.qcloudimg.com/raw/d9de23724ad57cab508cfb43f500897c.png" data-nonescope="true" ></td>
<td><a onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Win_Demo.exe')"><button style="width:150px;height: 150px;border:none;background-image:url(https://main.qcloudimg.com/raw/9c0b20a049f02e07c53ceb8396946d5c.png);background-size: cover;">
</button></a></td>
<td><a onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Mac_Demo.tar.bz2')"><button style="width:150px;height: 150px;border:none;background-image:url(https://main.qcloudimg.com/raw/9c0b20a049f02e07c53ceb8396946d5c.png);background-size: cover;">
</button></a></td>
</tr>
</table>


## 크로스 플랫폼 Demo
<table>
<tr>
<th>Web</th><th>Flutter </th><th>Electron</th>
</tr>
<tr>
</div></a></td>
<td>
<input type="button" value="웹측 코드 예" class="inbuttom" onclick="window.open('https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html')" />
</td>
<td>
<img style="width:150px" src="https://main.qcloudimg.com/raw/844e3de73cf2537e8a58e2263de5900e.png" data-nonescope="true">
</td>
<td>
<input type="button" value="Windows 버전" style="height: 30px;width: 150px;min-width: 24px;padding: 0 20px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;vertical-align: middle;white-space: nowrap;"  onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/api-example/TRTC-Electron-API-Examples-windows.zip')" /><br><br>
<input type="button" value="MacOS 버전" style="height: 30px;width: 150px;min-width: 24px;padding: 0 20px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;vertical-align: middle;white-space: nowrap;" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/api-example/TRTC-Electron-API-Examples-mac.zip')" /></td>
</tr>
</table>






## 영상 통화 시나리오
1:1 또는 그룹 영상 통화로 720P, 1080P 고화질을 지원합니다. 단일 방에 최대 300명 동시 접속, 최대 50명 카메라 동시 활성화를 지원합니다. 주요 응용 시나리오에는 1:1 영상 통화, 300명 화상 회의, 온라인 진료, 화상 채팅, 화상 고객서비스, 화상 면접 심사, 듀얼 녹화, 온라인 보상 청구, 화상 마피아 게임 등이 있습니다.
<dx-tabs>
::: iOS&Android
<table>
<tr>
   <th>발신자</th>
   <th>수신자</th>
 </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/ef83db73d0a8c487e72986dd1f92e361.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/f57ed3a55112233b05260f5dc37342ca.jpeg"/></td>
</tr>
</table>
:::

</dx-tabs>

## 음성 통화 시나리오
1:1 또는 그룹 음성 통화로 48kHz 및 듀얼 사운드 채널을 지원합니다. 단일 방은 최대 300명 동시 접속, 최대 50명 마이크 동시 활성화를 지원합니다. 주요 응용 시나리오에는 1:1 음성 통화, 그룹 음성 통화, 음성 채팅, 음성 회의, 음성 고객서비스, 마피아 게임 등이 있습니다.
<dx-tabs>
::: iOS&Android
<table>
<tr>
   <th>발신자</th>
   <th>수신자</th>
 </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/7b03f80d5ad33bd33b6fb551e392b4d3.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/60581f007dda722e06af6333b13afbd4.jpeg"/></td>
</tr>
</table>
:::

</dx-tabs>

## 인터랙티브 라이브 비디오 스트리밍 시나리오
인터랙티브 라이브 비디오 스트리밍 시나리오는 호스트와 시청자의 비디오 마이크 연결 인터랙션을 지원합니다. 호스트의 크로스 룸(크로스 라이브 룸) PK를 지원하며, 원활한 마이크 On/Off 지원으로 대기 시간 없이 전환됩니다. 호스트 딜레이 시간은 300ms 미만입니다. 단일 방의 마이크 연결은 인원 제한이 없으며, 최대 50명의 마이크 동시 연결을 지원합니다. 저지연 라이브 방송 모드에서 10만 명의 시청자 동시 재생을 지원하며, 재생 딜레이 시간은 1000ms 미만입니다. CDN 릴레이 라이브 방송 모드는 시청자 인원 제한이 없습니다. 주요 응용 시나리오에는 저지연 라이브 방송, 10만 명 인터랙션 수업, 라이브 방송 PK, 영상 소개팅, 인터랙션 수업, 원격 트레이닝, 대형 회의 등이 있습니다.
<dx-tabs>
::: iOS&Android
<table>
<tr>
<td><img width="260" height="561" src="https://main.qcloudimg.com/raw/317b3eb7ebf971ef7291dec2bacfa18a.jpeg"/></td>
<td><img width="260" height="561" src="https://main.qcloudimg.com/raw/162112aa8768d0db63e1850c2495a370.jpeg"/></td>
<td><img width="260" height="561" src="https://main.qcloudimg.com/raw/dab9fe1e5c93deb5ee02155b27bdf639.jpeg"/></td>
<td><img width="260" height="561" src="https://main.qcloudimg.com/raw/3182620f791a594d555ecab0cd170e1f.jpeg"/></td>
</tr>
</table>
:::
::: Web

:::
</dx-tabs>

## 인터랙티브 라이브 오디오 스트리밍 시나리오
인터랙티브 라이브 오디오 스트리밍은 호스트와 시청자의 오디오 마이크 연결 인터랙션을 지원합니다. 호스트의 크로스 룸(크로스 라이브 룸) PK를 지원하며, 원활한 마이크 On/Off 지원으로 대기 시간 없이 전환됩니다. 호스트 딜레이 시간은 300ms 미만입니다. 단일 방의 마이크 연결은 인원 제한이 없으며, 최대 50명의 마이크 동시 연결을 지원합니다. 저지연 라이브 방송 모드에서 10만 명의 시청자 동시 재생을 지원하며, 재생 딜레이 시간은 1000ms 미만입니다. CDN 릴레이 라이브 방송 모드는 시청자 인원 제한이 없습니다. 주요 응용 시나리오에는 저지연 오디오 라이브 방송, 라이브 방송 마이크 연결, 음성 라이브 PK, 음성 채팅방, 음성 소개팅, 노래방, FM 방송국 등이 있습니다.
<table>
     <tr>
         <th>호스트 마이크 자리 화면</th>  
         <th>시청자 마이크 자리 화면</th>  
     </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/dd836080683a49418bc548bfb9f59857.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/7b73bfdd915a0ba281c52b9ac0518b80.jpeg"/></td>
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
<td><img src="https://main.qcloudimg.com/raw/a1fc2d23946377cb9466d8b645c14d24.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/5c613b7c7ee890b7e3feb7a3270a9a89.jpeg"/></td>
</tr>
</table>

## 인터랙션 시나리오
인터랙션 수업 시나리오는 선생님과 학생의 인터랙션 마이크 연결을 지원하며, 최대 50명이 동시에 마이크를 연결할 수 있습니다. 원활한 마이크 On/Off 지원으로 대기 시간 없이 전환되며, 딜레이 시간은 300ms 미만입니다. 저지연 라이브 방송 모드에서 10만 명의 학생이 동시에 시청할 수 있으며, 이때 딜레이 시간은 1000ms 미만입니다. CDN 릴레이 라이브 방송 모드는 시청자 인원 제한이 없습니다. 화면 공유, 인터랙션 화이트보드, 녹화 재생 등 다양한 기능을 수업에 응용하여 보다 다양한 온라인 수업을 진행할 수 있습니다. 주요 비즈니스 시나리오에는 대규모 수업, 소규모 수업, 슈퍼 소그룹 수업(대규모 강의/그룹 수업 복합 수업), AI 수업, 시범 강의, 사내 교육, 1:1 온라인 교육 등이 있습니다.

| <img src="https://main.qcloudimg.com/raw/76cb1831b3f4b5340243a6b7406d8d73.png" alt="wecom-temp-799c836bbc6c6c3cd9fed14d03465f5d" style="zoom:50%;" /> | <img src="https://main.qcloudimg.com/raw/ca1e4f364230e18b78c7789cf8db08ae.png" alt="wecom-temp-d05e8b456350695101a745553926b07e" style="zoom:28%;" /> |



## 온라인 노래방(KTV 시나리오)
KTV 시나리오는 호스트와 시청자가 노래할 수 있도록 마이크 연결을 지원합니다. 원활한 마이크 On/Off 지원으로 대기 시간 없이 전환되며 호스트 딜레이 시간은 300ms 미만입니다; 단일 방의 마이크 연결 인원 수는 무제한이며, 최대 50명이 동시에 마이크를 연결할 수 있습니다. 저지연 라이브 방송 모드에서 10만 명의 학생이 동시에 시청할 수 있으며, 이때 딜레이 시간은 1000ms 미만입니다. CDN 릴레이 라이브 방송 모드는 시청자 인원 제한이 없습니다. 주요 응용 시나리오에는 저지연 오디오 라이브 방송, 라이브 방송 마이크 연결, 음성 라이브 PK, 음성 채팅방, 음성 소개팅, 노래방, FM 방송국 등이 있습니다.
<table>
     <tr>
         <th>방 주인 노래 신청 화면</th>  
         <th>시청자 노래 신청 화면</th>  
     </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/dcb4f550d478b35212f4b7ef5c332fcf.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/90dff32d6b506237ce3725083b47421a.jpeg"/></td>
</tr>
</table>
