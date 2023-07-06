
<dx-alert infotype="explain" title="">
- 이미지 업데이트 히스토리는 배포 시간 순으로 정리되어 있습니다.
- 이미지는 리전의 그레이 스케일에 따라 배포됩니다. -  CVM 인스턴스를 생성할 때 이미지가 업데이트 히스토리의 최신 버전이 아닌 경우 이미지가 아직 해당 리전에 릴리스되지 않았을 수 있습니다.
- 콘솔에서 업데이트 히스토리의 이미지를 찾을 수 없는 경우, 이미지가 완전히 오픈되지 않았을 수 있습니다. 이 경우 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)을 통해 자세한 정보를 얻을 수 있습니다.
</dx-alert>

## 이미지 업데이트 히스토리

<table>
<thead>
<tr>
<th width="60%"><strong>업데이트된 기능</strong></th>
<th><strong>업데이트 날짜</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>
<ul class="params">
<li>firewalld\sssd\rngd 서비스 비활성화</li>
<li>microcode_ctl/nss-softokn/avahi 소프트웨어 패키지 제거</li>
<li>keymap 설정</li>
<li>timezone 설정</li>
<li>kdump 시작 설정은 cloudinit.target에 의존합니다.</li>
<li>repo에 mirrors.tencentyun.com을 첫 번째 URL로 구성</li>
<li>/etc/rc.d/rc.local 파일 권한을 755로 변경</li>
<li>/var/lib/ 아래의 일부 디렉터리 권한 오류 수정</li>
</ul>
</td>
<td>2022-09-16</td>
</tr>
<tr>
<td>
<ul class="params">
<li>커널 버전이 5.4.119-19.0010으로 업데이트됨</li>
<li>기타 사용자 모드 소프트웨어가 업데이트됨</li>
<li>이미지 타임스탬프가 업데이트됨</li>
</ul>
</td>
<td>2022-07-27</td>
</tr>
<tr>
<td>
<ul class="params">
<li>퍼블릭 클라우드에 OpenCloudOS 8.5 출시됨</li>
</ul>
</td>
<td>2022-03-04</td>
</tr>
</tbody></table>                                                 
