HLS 세그먼트의 크기와 수를 조정하여 HLS 재생 지연 시간을 제어할 수 있습니다. 지연 시간을 너무 낮게 설정하면 재생이 끊길 수 있습니다.

## 전제 조건
- CSS 서비스가 활성화되어 있고 [CSS 콘솔](https://console.cloud.tencent.com/live/livestat)에 로그인되어 있어야 합니다.
- [푸시 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가되어 있어야 합니다.


## 지연 시간 설정
1. 왼쪽 사이드바에서 [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)를 선택하고 HLS 지연 구성이 필요한 타깃 **푸시 도메인**을 클릭하거나 오른쪽의 **관리**를 클릭하여 도메인 관리 페이지로 이동합니다.
2. **고급 구성** 탭을 선택합니다.
3. 필요에 맞는 지연 시간을 선택합니다. GOP는 HLS 세그먼트의 크기에 영향을 줍니다. 푸시에 대한 GOP를 1s - 2s로 설정하는 것이 좋습니다.
4. GOP가 2s로 설정된 경우 지연 시간은 다음과 같습니다:
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
<td>20s - 25s</td>
<td>10s - 15s</td>
<td>6s - 8s</td>
</tr>
</tbody></table>

<img src="https://qcloudimg.tencent-cloud.cn/raw/3032e36b30c1a966f5db814f19635612.png">
