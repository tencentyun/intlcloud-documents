필요에 맞는 지연 시간을 설정합니다. 지연 시간을 너무 낮게 설정하면 재생이 끊길 수 있습니다.

## 전제 조건
- CSS 서비스가 활성화되어 있고 [CSS 콘솔](https://console.cloud.tencent.com/live/livestat)에 로그인되어 있어야 합니다.
- [재생 도메인 이름](https://intl.cloud.tencent.com/document/product/267/35970)을 추가했습니다.


## 지연 시간 설정
1. 왼쪽 사이드바에서 [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)를 선택하고 RTMP 및 FLV를 구성하려는 **재생 도메인**을 클릭합니다. 또는 오른쪽의 **관리**를 클릭하여 세부정보 페이지로 이동합니다.
2. **고급 구성** 탭을 선택합니다.
3. 필요에 맞는 지연 시간을 선택합니다. 푸시에 대한 GOP를 1s - 2s로 설정하는 것이 좋습니다. GOP가 높을수록 지연 시간이 길어집니다.
4. GOP가 2s로 설정된 경우 지연 시간은 다음과 같습니다.
<table>
<thead>
<tr>
<th>지연 시간 설정</th>
<th>높음</th>
<th>중간</th>
<th>낮음</th>
</tr>
</thead>
<tbody><tr>
<td>예상 지연 시간</td>
<td>7s - 9s</td>
<td>5s - 7s</td>
<td>4s -5s</td>
</tr>
</tbody></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/49744a600f2e1101a9261a0205b5e651.png">

